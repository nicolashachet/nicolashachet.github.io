---
id: 455
title: 'CakePHP 2 : composant d&rsquo;upload de fichiers images'
date: '2012-01-05T14:29:02+01:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=455'
permalink: /blog/developpement-php/cakephp-2-composant-dupload-de-fichiers-images/
dsq_thread_id:
    - '1285641211'
image: /wp-content/uploads/2012/01/upload-512x198.png
categories:
    - 'PHP'
tags:
    - CakePHP
    - PHP
---


[![](/wp-content/uploads/2012/01/upload-150x150.png "upload")](/wp-content/uploads/2012/01/upload.png)Pour ce premier article de 2012, je vous propose un code qui peut s’avérer très pratique pour la gestion de vos uploads de fichiers images. Ce composant **CakePHP 2.0** prend forme en tant que Behaviour (helpeur de modèle). Le code est basé sur la **version 1.0.1 du MeioUploadBehavior**. Vous trouverez toutes les infos utiles sur le site [MeioUpload Behavior](https://www.meiocodigo.com/projects/meioupload/).

## Liens utiles

[Site de l’auteur](https://www.meiocodigo.com/projects/meioupload/)  
[Sujet sur le forum Cakephp france](https://forum.cakephp-fr.org/viewtopic.php?id=130)  
[MeioUpload sur Github](https://github.com/jrbasso/MeioUpload)  
[Branches de développement MeioUpload sur Github](https://github.com/jrbasso/MeioUpload/branches)

A noter que le composant est toujours en développement : vous trouverez probablement une version plus à jour sur le github du MeioUpload. Vous trouverez de la **documentation** sur les liens précédents.

## Utilisation

**Fichier model**  
{% highlight php linenos %}  
var $actsAs = array(  
 ‘MeioUpload’ => array(  
 ‘picture’ => array(  
 ‘dir’ => ‘img{DS}{model}{DS}{field}’,  
 ‘create_directory’ => true,  
 ‘allowed_mime’ => array(‘image/jpeg’, ‘image/pjpeg’, ‘image/png’),  
 ‘allowed_ext’ => array(‘.jpg’, ‘.jpeg’, ‘.png’),  
 ‘thumbsizes’ => array(  
 ‘normal’ => array(‘width’=>200, ‘height’=>200),  
 ),  
 ‘default’ => ‘default.jpg’,  
 )  
 )  
);  
{% endhighlight %}

## Code source

Il s’agit de la version MeioUpload 1.0.1 mise à jour pour CakePHP 2.

{% highlight php linenos %}  
<?php  
/*\*  
 \* MeioUpload Behavior  
 \* This behavior is based on Tane Piper’s improved uplaod behavior (https://digitalspaghetti.tooum.net/switchboard/blog/2497:Upload_Behavior_for_CakePHP_12)  
 \* @author Vinicius Mendes (vbmendes@gmail.com)  
 \* @link https://www.meiocodigo.com  
 \* @filesource https://www.meiocodigo.com/meioupload  
 \* @version 1.0.1  
 \* @lastmodified 2008-10-04  
 \*  
 \* Usage:  
 \* 1) Download this behaviour and place it in your models/behaviours/upload.php  
 \* 2) If you require thumbnails for image generation, download Nate’s phpThumb Component (https://bakery.cakephp.org/articles/view/phpthumb-component)  
 \* 3) Insert the following SQL into your database. This is a basic model you can expand on:  
 \* CREATE TABLE `images` (  
 \* `id` int(8) unsigned NOT NULL auto_increment,  
 \* `filename` varchar() default NULL,  
 \* `dir` varchar(255) default NULL,  
 \* `mimetype` varchar(255) NULL,  
 \* `filesize` int(11) unsigned default NULL,  
 \* `created` datetime default NULL,  
 \* `modified` datetime default NULL,  
 \* PRIMARY KEY (`id`) ) ENGINE=MyISAM DEFAULT CHARSET=utf8;  
 \* 4) In your model that you want to have the upload behavior work, place the below code. This example is for an Image model:  
 \*  
 \* var $actsAs = array(‘Upload’ => array(  
 \* ‘filename’ => array(  
 \* ‘dir’ => ‘files/images’,  
 \* ‘create_directory’ => false,  
 \* ‘allowed_mime’ => array(‘image/jpeg’, ‘image/pjpeg’, ‘image/gif’, ‘image/png’),  
 \* ‘allowed_ext’ => array(‘.jpg’, ‘.jpeg’, ‘.png’, ‘.gif’),  
 \* ‘thumbsizes’ => array(  
 \* ‘small’ => array(‘width’=>100, ‘height’=>100),  
 \* ‘medium’ => array(‘width’=>220, ‘height’=>220),  
 \* ‘large’ => array(‘width’=>800, ‘height’=>600)  
 \* )  
 \* )  
 \* )  
 \* );  
 \* The above code will save the uploaded file’s name in the ‘filename’ field in database,  
 \* it will not overwrite existing files, instead it will create a new filename based on the original  
 \* plus a counter.  
 \* Allowed Mimetypes and extentions should be pretty explanitory.  
 \* For thumbnails, when the file is uploaded, it will create 3 thumbnail sizes and prepend the name  
 \* to the thumbfiles (i.e. image_001.jpg will produced thumb.small.image_001.jpg, thumb.medium.image_001.jpg, etc)  
 \*  
 \* 5) Create your upload view, make sure it’s a multipart/form-data form, and the filename field is of type $form->file  
 \* 6) Make sure your directory is at least CHMOD 775, also check your php.ini MAX_FILE_SIZE is enough to support the filesizes you are uploading  
 \*  
 \* Version Details  
 \*  
 \* 1.0.1  
 \* + Fixed a bug in the create folder method  
 \* + Now you can use the $validate var of the model to apply the changes to default validation rules;  
 \* + Changed the my_array_merge function, now it’s part of the behavior, name arrayMerge;  
 \* + Allow use of {DS}, {model} and {field} constants in directory name and fields names;  
 \* + Fixed a bug with the replacement of the default names.  
 \*  
 \* 1.0  
 \* + Initial release.  
 \*/

App :: uses(‘Folder’, ‘Utility’);

class MeioUploadBehavior extends ModelBehavior {  
 /*\*  
 \* The default options for the behavior  
 \*/  
 var $default_options = array(  
 ‘dir’ =>",  
 ‘allowed_mime’ => array(),  
 ‘allowed_ext’ => array(),  
 ‘create_directory’ => true,  
 ‘max_size’ => 2097152,  
 ‘thumbsizes’ => array(),  
 ‘default’ => false,  
 ‘fields’ => array(  
 ‘dir’ => ‘dir’,  
 ‘filesize’ => ‘filesize’,  
 ‘mimetype’ => ‘mimetype’  
 ),  
 ‘validations’ => array(  
 ‘FieldName’ => array(  
 ‘rule’ => array(‘uploadCheckFieldName’),  
 ‘check’ => true,  
 ‘message’ => ‘Nom du fichier incompatible avec les paramètres du comportement Meio.’  
 ),  
 ‘Dir’ => array(  
 ‘rule’ => array(‘uploadCheckDir’),  
 ‘check’ => true,  
 ‘message’ => ‘Répertoire de téléchargement introuvable ou inaccessible en écriture.’  
 ),  
 ‘Empty’ => array(  
 ‘rule’ => array(‘uploadCheckEmpty’),  
 ‘check’ => true,  
 ‘on’ => ‘create’,  
 ‘message’ => ‘Fichier introuvable.’  
 ),  
 ‘UploadError’ => array(  
 ‘rule’ => array(‘uploadCheckUploadError’),  
 ‘check’ => true,  
 ‘message’ => ‘Erreur lors du téléchargement du fichier.’  
 ),  
 ‘MaxSize’ => array(  
 ‘rule’ => array(‘uploadCheckMaxSize’),  
 ‘check’ => true,  
 ‘message’ => ‘Fichier trop volumineux.’  
 ),  
 ‘InvalidMime’ => array(  
 ‘rule’ => array(‘uploadCheckInvalidMime’),  
 ‘check’ => true,  
 ‘message’ => ‘Type de contenu invalide.’  
 ),  
 ‘InvalidExt’ => array(  
 ‘rule’ => array(‘uploadCheckInvalidExt’),  
 ‘check’ => true,  
 ‘message’ => ‘Extension du fichier invalide.’  
 )  
 )  
 );

 var $default_validations = array(  
 ‘FieldName’ => array(  
 ‘rule’ => array(‘uploadCheckFieldName’),  
 ‘check’ => true,  
 ‘message’ => ‘Nom du fichier incompatible avec les paramètres du comportement Meio.’  
 ),  
 ‘Dir’ => array(  
 ‘rule’ => array(‘uploadCheckDir’),  
 ‘check’ => true,  
 ‘message’ => ‘Répertoire de téléchargement introuvable ou inaccessible en écriture.’  
 ),  
 ‘Empty’ => array(  
 ‘rule’ => array(‘uploadCheckEmpty’),  
 ‘check’ => true,  
 ‘on’ => ‘create’,  
 ‘message’ => ‘Fichier introuvable.’  
 ),  
 ‘UploadError’ => array(  
 ‘rule’ => array(‘uploadCheckUploadError’),  
 ‘check’ => true,  
 ‘message’ => ‘Erreur lors du téléchargement du fichier.’  
 ),  
 ‘MaxSize’ => array(  
 ‘rule’ => array(‘uploadCheckMaxSize’),  
 ‘check’ => true,  
 ‘message’ => ‘Fichier trop volumineux.’  
 ),  
 ‘InvalidMime’ => array(  
 ‘rule’ => array(‘uploadCheckInvalidMime’),  
 ‘check’ => true,  
 ‘message’ => ‘Type de contenu invalide.’  
 ),  
 ‘InvalidExt’ => array(  
 ‘rule’ => array(‘uploadCheckInvalidExt’),  
 ‘check’ => true,  
 ‘message’ => ‘Extension du fichier invalide.’  
 )  
 );

 /*\*  
 \* The message for move error.  
 \*/  
 var $moveErrorMsg = ‘Erreur lors du déplacement du fichier temporaire.’;

 /*\*  
 \* The array that saves the $options for the behavior  
 \*/  
 var $__fields = array();

 /*\*  
 \* Patterns of reserved words  
 \*/  
 var $patterns = array(  
 "thumb",  
 "default"  
 );

 /*\*  
 \* Words to replace the patterns of reserved words  
 \*/  
 var $replacements = array(  
 "t_umb",  
 "d_fault"  
 );

 /*\*  
 \* Array of files to be removed on the afterSave callback  
 \*/  
 var $__filesToRemove = array();

 /*\*  
 \* Setup the behavior. It stores a reference to the model, merges the default options with the options for each field, and setup the validation rules.  
 \*  
 \* @author Vinicius Mendes  
 \* @return null  
 \* @param $model Object  
 \* @param $config Array[optional]  
 \*/  
 function setup(&amp;$model, $config=array()) {

 $this->Folder = &amp;new Folder;  
 $this->__model = $model;  
 $this->__fields = array();  
 foreach($config as $field => $options) {

 // Check if given field exists  
 if(!$model->hasField($field)) {  
 trigger_error(‘MeioUploadBehavior Error: The field "’.$field.’" doesn\\’t exists in the model "’.$model->name.’".’, E_USER_WARNING);  
 }

 // Merge given options with defaults  
 $options = $this->arrayMerge($this->default_options, $options);  
 // Including the default name to the replacements  
 if($options[‘default’]){  
 if(!preg_match(‘/^.+\\..+$/’,$options[‘default’])){  
 trigger_error(‘MeioUploadBehavior Error: The default option must be the filename with extension.’, E_USER_ERROR);  
 }  
 $this->_includeDefaultReplacement($options[‘default’]);  
 }  
 // Verifies if the thumbsizes names is alphanumeric  
 foreach($options[‘thumbsizes’] as $name => $size){  
 if(!preg_match(‘/^[0-9a-zA-Z]+$/’,$name)){  
 trigger_error(‘MeioUploadBehavior Error: The thumbsizes names must be alphanumeric.’, E_USER_ERROR);  
 }  
 }  
 // Process the max_size if it is not numeric  
 $options[‘max_size’] = $this->sizeToBytes($options[‘max_size’]);  
 $this->__fields[$field] = $options;

 // Generate temporary directory if none provided  
 if(empty($options[‘dir’])) {  
 $this->__fields[$field][‘dir’] = ‘uploads’ . DS . $model->name;  
 // Else replace the tokens of the dir.  
 } else {  
 $this->__fields[$field][‘dir’] = $this->replaceTokens($options[‘dir’],$field);  
 }

 // Replace tokens in the fields names.  
 foreach($this->__fields[$field][‘fields’] as $fieldToken => $fieldName){  
 $this->__fields[$field][‘fields’][$fieldToken] = $this->replaceTokens($fieldName,$field);  
 }

 // Check that the given directory does not have a DS on the end  
 if($options[‘dir’][strlen($options[‘dir’])-1] == DS) {  
 $options[‘dir’] = substr($options[‘dir’],0,strlen($options[‘dir’])-2);  
 }  
 }  
 }

 /*\*  
 \* Merges two arrays recursively  
 \*  
 \* @author Vinicius Mendes  
 \* @return Array  
 \* @param $arr Array  
 \* @param $ins Array  
 \*/  
 function arrayMerge($arr, $ins) {  
 if (is_array($arr)) {  
 if (is_array($ins)) {  
 foreach ($ins as $k=>$v) {  
 if (isset($arr[$k])&amp;&amp;is_array($v)&amp;&amp;is_array($arr[$k])) {  
 $arr[$k] = $this->arrayMerge($arr[$k],$v);  
 }  
 else $arr[$k] = $v;  
 }  
 }  
 } elseif (!is_array($arr)&amp;&amp;(strlen($arr)==0||$arr==0)) {  
 $arr=$ins;  
 }  
 return($arr);  
 }

 /*\*  
 \* Replaces some tokens. {model} to the underscore version of the model name, {field} to the field name, {DS}. / or \\ to DS constant value.  
 \*  
 \* @author Vinicius Mendes  
 \* @return String  
 \* @param $string String  
 \* @param $fieldName String  
 \*/  
 function replaceTokens($string,$fieldName){  
 return str_replace(array(‘{model}’, ‘{field}’, ‘{DS}’,’/’,’\\\\’),array(Inflector::underscore($this->__model->name),$fieldName,DS,DS,DS),$string);  
 }

 /*\*  
 \* Convert a size value to bytes. For example: 2 MB to 2097152.  
 \*  
 \* @author Vinicius Mendes  
 \* @return int  
 \* @param $size String  
 \*/  
 function sizeToBytes($size){  
 if(is_numeric($size)) return $size;  
 if(!preg_match(‘/^[1-9][0-9]\* (kb|mb|gb|tb)$/i’, $size)){  
 trigger_error(‘MeioUploadBehavior Error: The max_size option format is invalid.’, E_USER_ERROR);  
 return 0;  
 }  
 list($size, $unit) = explode(‘ ‘,$size);  
 if(strtolower($unit) == ‘kb’) return $size\*1024;  
 if(strtolower($unit) == ‘mb’) return $size\*1048576;  
 if(strtolower($unit) == ‘gb’) return $size\*1073741824;  
 if(strtolower($unit) == ‘tb’) return $size\*1099511627776;  
 trigger_error(‘MeioUploadBehavior Error: The max_size unit is invalid.’, E_USER_ERROR);  
 return 0;  
 }

 /*\*  
 \* Sets the validation for each field, based on the options.  
 \*  
 \* @author Vinicius Mendes  
 \* @return null  
 \* @param $fieldName String  
 \* @param $options Array  
 \*/  
 function setupValidation($fieldName, $options){  
 $options = $this->__fields[$fieldName];

 if(isset($this->__model->validate[$fieldName])){  
 if(isset($this->__model->validate[$fieldName][‘rule’])){  
 $this->__model->validate[$fieldName] = array(  
 ‘oldValidation’ => $this->__model->validates[$fieldName]  
 );  
 }  
 } else {  
 $this->__model->validate[$fieldName] = array();  
 }  
 $this->__model->validate[$fieldName] = $this->arrayMerge($this->default_validations,$this->__model->validate[$fieldName]);  
 $this->__model->validate[$fieldName] = $this->arrayMerge($options[‘validations’],$this->__model->validate[$fieldName]);  
 }

 /*\*  
 \* Checks if the field was declared in the MeioUpload Behavior setup  
 \*  
 \* @author Vinicius Mendes  
 \* @return boolean  
 \* @param $model Object  
 \* @param $data Array  
 \*/  
 function uploadCheckFieldName(&amp;$model, $data,$other){  
 foreach($data as $fieldName => $field){  
 if(!$this->__model->validate[$fieldName][‘FieldName’][‘check’]) return true;  
 if(isset($this->__fields[$fieldName])){  
 return true;  
 } else {  
 $this->log(‘UploadBehavior Error: The field "’.$fieldName.’" wasn\\’t declared as part of the UploadBehavior in model "’.$model->name.’".’);  
 return false;  
 }  
 }  
 return true;  
 }

 /*\*  
 \* Checks if the folder exists or can be created or writable.  
 \*  
 \* @author Vinicius Mendes  
 \* @return boolean  
 \* @param $model Object  
 \* @param $data Array  
 \*/  
 function uploadCheckDir(&amp;$model, $data){  
 foreach($data as $fieldName => $field){  
 if(!$this->__model->validate[$fieldName][‘Dir’][‘check’]) return true;  
 $options = $this->__fields[$fieldName];  
 if(empty($field[‘remove’]) || empty($field[‘name’])){  
 // Check if directory exists and create it if required  
 if(!is_dir($options[‘dir’])) {  
 if($options[‘create_directory’]){  
 if(!$this->Folder->create($options[‘dir’])) {  
 trigger_error(‘UploadBehavior Error: The directory ‘.$options[‘dir’].’ does not exist and cannot be created.’, E_USER_WARNING);  
 return false;  
 }  
 } else {  
 trigger_error(‘UploadBehavior Error: The directory’.$options[‘dir’].’ does not exist.’, E_USER_WARNING);  
 return false;  
 }  
 }

 // Check if directory is writable  
 if(!is_writable($options[‘dir’])) {  
 trigger_error(‘UploadBehavior Error: The directory ‘.$options[‘dir’].’ isn\\’t writable.’, E_USER_WARNING);  
 return false;  
 }  
 }  
 }  
 return true;  
 }

 /*\*  
 \* Checks if the filename is not empty.  
 \*  
 \* @author Vinicius Mendes  
 \* @return boolean  
 \* @param $model Object  
 \* @param $data Array  
 \*/  
 function uploadCheckEmpty(&amp;$model, $data){  
 foreach($data as $fieldName => $field){  
 if(!$this->__model->validate[$fieldName][‘Empty’][‘check’]) return true;  
 if(empty($field[‘remove’])){  
 if(!is_array($field) || empty($field[‘name’])){  
 return false;  
 }  
 }  
 }  
 return true;  
 }

 /*\*  
 \* Checks if ocurred erros in the upload.  
 \*  
 \* @author Vinicius Mendes  
 \* @return boolean  
 \* @param $model Object  
 \* @param $data Array  
 \*/  
 function uploadCheckUploadError(&amp;$model, $data){  
 foreach($data as $fieldName => $field){  
 if(!$this->__model->validate[$fieldName][‘UploadError’][‘check’]) return true;  
 if(!empty($field[‘name’]) &amp;&amp; $field[‘error’] > 0){  
 return false;  
 }  
 }  
 return true;  
 }

 /*\*  
 \* Checks if the file isn’t bigger then the max file size option.  
 \*  
 \* @author Vinicius Mendes  
 \* @return boolean  
 \* @param $model Object  
 \* @param $data Array  
 \*/  
 function uploadCheckMaxSize(&amp;$model, $data){  
 foreach($data as $fieldName => $field){  
 if(!$this->__model->validate[$fieldName][‘MaxSize’][‘check’]) return true;  
 $options = $this->__fields[$fieldName];  
 if(!empty($field[‘name’]) &amp;&amp; $field[‘size’] > $options[‘max_size’]) {  
 return false;  
 }  
 }  
 return true;  
 }

 /*\*  
 \* Checks if the file is of an allowed mime-type.  
 \*  
 \* @author Vinicius Mendes  
 \* @return boolean  
 \* @param $model Object  
 \* @param $data Array  
 \*/  
 function uploadCheckInvalidMime(&amp;$model, $data){  
 foreach($data as $fieldName => $field){  
 if(!$this->__model->validate[$fieldName][‘InvalidMime’][‘check’]) return true;  
 $options = $this->__fields[$fieldName];  
 if(!empty($field[‘name’]) &amp;&amp; count($options[‘allowed_mime’]) > 0 &amp;&amp; !in_array($field[‘type’], $options[‘allowed_mime’])) {  
 return false;  
 }  
 }  
 return true;  
 }

 /*\*  
 \* Checks if the file has an allowed extension.  
 \*  
 \* @author Vinicius Mendes  
 \* @return boolean  
 \* @param $model Object  
 \* @param $data Array  
 \*/  
 function uploadCheckInvalidExt(&amp;$model, $data){  
 foreach($data as $fieldName => $field){  
 if(!$this->__model->validate[$fieldName][‘InvalidExt’][‘check’]) return true;  
 $options = $this->__fields[$fieldName];  
 if(!empty($field[‘name’])){  
 if(count($options[‘allowed_ext’]) > 0) {  
 $matches = 0;  
 foreach($options[‘allowed_ext’] as $extension) {  
 if(substr($field[‘name’],-strlen($extension)) == $extension) {  
 $matches++;  
 }  
 }

 if($matches == 0) {  
 return false;  
 }  
 }  
 }  
 }  
 return true;  
 }

 /*\*  
 \* Set a file to be removed in afterSave callback  
 \*  
 \* @author Vinicius Mendes  
 \* @return null  
 \* @param $fieldName String  
 \*/  
 function setFileToRemove($fieldName){  
 $filename = $this->__model->field($fieldName);  
 if(!empty($filename) &amp;&amp; $filename != $this->__fields[$fieldName][‘default’]){  
 $this->__filesToRemove[] = array(  
 ‘dir’ => $this->__fields[$fieldName][‘dir’],  
 ‘name’ => $filename  
 );  
 }  
 }

 /*\*  
 \* Include a pattern of reserved word based on a filename, and it’s replacement.  
 \*  
 \* @author Vinicius Mendes  
 \* @return null  
 \* @param $default String  
 \*/  
 function _includeDefaultReplacement($default){  
 $replacements = $this->replacements;  
 list($newPattern, $ext) = $this->splitFilenameAndExt($default);  
 if(!in_array($newPattern, $this->patterns)){  
 $this->patterns[] = $newPattern;  
 $newReplacement = $newPattern;  
 if(isset($newReplacement[1])){  
 if($newReplacement[1] != ‘_’){  
 $newReplacement[1] = ‘_’;  
 } else {  
 $newReplacement[1] = ‘a’;  
 }  
 } elseif($newReplacement != ‘_’) {  
 $newReplacement = ‘_’;  
 } else {  
 $newReplacement = ‘a’;  
 }  
 $this->replacements[] = $newReplacement;  
 }  
 }

 /*\*  
 \* Removes the bad characters from the $filename and replace reserved words. It updates the $model->data.  
 \*  
 \* @author Vinicius Mendes  
 \* @return null  
 \* @param $fieldName String  
 \*/  
 function fixName($fieldName){  
 // updates the filename removing the keywords thumb and default name for the field.  
 list($filename, $ext) = $this->splitFilenameAndExt($this->__model->data[$this->__model->name][$fieldName][‘name’]);  
 $filename = str_replace($this->patterns,$this->replacements,$filename);  
 $filename = Inflector::slug($filename);  
 $i = 0;  
 $newFilename = $filename;  
 while(file_exists($this->__fields[$fieldName][‘dir’].DS.$newFilename.’.’.$ext)){  
 $newFilename = $filename.$i;  
 $i++;  
 }  
 $this->__model->data[$this->__model->name][$fieldName][‘name’] = $newFilename.’.’.$ext;  
 }

 /*\*  
 \* Splits a filename in two parts: the name and the extension. Returns an array with it respectively.  
 \*  
 \* @author Vinicius Mendes  
 \* @return Array  
 \* @param $filename String  
 \*/  
 function splitFilenameAndExt($filename){  
 $parts = explode(‘.’,$filename);  
 $ext = $parts[count($parts)-1];  
 unset($parts[count($parts)-1]);  
 $filename = implode(‘.’,$parts);  
 return array($filename,$ext);  
 }

 /*\*  
 \* Sets the validation rules for each field.  
 \*  
 \* @return true  
 \* @param $model Object  
 \*/  
 function beforeValidate(&amp;$model) {  
 foreach($this->__fields as $fieldName=>$options){  
 $this->setupValidation($fieldName, $options);  
 }  
 return true;  
 }

 /*\*  
 \* Uploads the files before saving the record.  
 \*  
 \* @author Vinicius Mendes  
 \* @param $model Object  
 \*/  
 function beforeSave(&amp;$model) {  
 foreach($this->__fields as $fieldName=>$options){  
 // if the file is marked to be deleted, use the default or set the field to null  
 if(!empty($model->data[$model->name][$fieldName][‘remove’])){  
 if($options[‘default’]){  
 $model->data[$model->name][$fieldName] = $options[‘default’];  
 } else {  
 $model->data[$model->name][$fieldName] = null;  
 }  
 //if the record is already saved in the database, set the existing file to be removed after the save is sucessfull  
 if(!empty($model->data[$model->name][$model->primaryKey])){  
 $this->setFileToRemove($fieldName);  
 }  
 continue;  
 }

 // If no file has been upload, then unset the field to avoid overwriting existant file  
 if(!isset($model->data[$model->name][$fieldName]) || !is_array($model->data[$model->name][$fieldName]) || empty($model->data[$model->name][$fieldName][‘name’])){  
 if(!empty($model->data[$model->name][$model->primaryKey]) || !$options[‘default’]){  
 unset($model->data[$model->name][$fieldName]);  
 } else {  
 $model->data[$model->name][$fieldName] = $options[‘default’];  
 }  
 continue;  
 }  
 //if the record is already saved in the database, set the existing file to be removed after the save is sucessfull  
 if(!empty($model->data[$model->name][$model->primaryKey])){  
 $this->setFileToRemove($fieldName);  
 }

 // Fix the filename, removing bad characters and avoiding from overwriting existing ones  
 $this->_includeDefaultReplacement($options[‘default’]);  
 $this->fixName($fieldName);  
 $saveAs = $options[‘dir’].DS.$model->data[$model->name][$fieldName][‘name’];

 // Attempt to move uploaded file  
 if(!move_uploaded_file($model->data[$model->name][$fieldName][‘tmp_name’], $saveAs)){  
 $model->validationErrors[$field] = $moveErrorMsg;  
 return false;  
 }

 // It the file is an image, try to make the thumbnails  
 if (count($options[‘allowed_ext’]) > 0 &amp;&amp; in_array($model->data[$model->name][$fieldName][‘type’], array(‘image/jpeg’, ‘image/pjpeg’, ‘image/png’))) {  
 foreach ($options[‘thumbsizes’] as $key => $value) {  
 // If a ‘normal’ thumbnail is set, then it will overwrite the original file  
 if($key == ‘normal’){  
 $thumbSaveAs = $saveAs;  
 // Otherwise, set the thumb filename to thumb.$key.$filename.$ext  
 } else {  
 $thumbSaveAs = $options[‘dir’].DS.’thumb.’.$key.’.’.$model->data[$model->name][$fieldName][‘name’];  
 }  
 $this->createthumb($saveAs, $thumbSaveAs, $value[‘width’], $value[‘height’]);  
 }  
 }

 // Update model data  
 $model->data[$model->name][$options[‘fields’][‘dir’]] = $options[‘dir’];  
 $model->data[$model->name][$options[‘fields’][‘mimetype’]] = $model->data[$model->name][$fieldName][‘type’];  
 $model->data[$model->name][$options[‘fields’][‘filesize’]] = $model->data[$model->name][$fieldName][‘size’];  
 $model->data[$model->name][$fieldName] = $model->data[$model->name][$fieldName][‘name’];  
 }  
 return true;  
 }

 /*\*  
 \* Deletes the files marked to be deleted in the save method. A file can be marked to be deleted if it is overwriten by another or if the user mark it to be deleted.  
 \*  
 \* @author Vinicius Mendes  
 \* @param $model Object  
 \*/  
 function afterSave(&amp;$model) {  
 foreach($this->__filesToRemove as $file){  
 if($file[‘name’])  
 $this->_deleteFiles($file[‘name’], $file[‘dir’]);  
 }  
 // Reset the filesToRemove array  
 $this->__filesToRemove = array();  
 }

 /*\*  
 \* Deletes all files associated with the record beforing delete it.  
 \*  
 \* @author Vinicius Mendes  
 \* @param $model Object  
 \*/  
 function beforeDelete(&amp;$model) {  
 $model->read(null, $model->id);  
 if(isset($model->data)) {  
 foreach($this->__fields as $field=>$options) {  
 $file = $model->data[$model->name][$field];  
 if($file &amp;&amp; $file != $options[‘default’])  
 $this->_deleteFiles($file, $options[‘dir’]);  
 }  
 }  
 return true;  
 }

 /*\*  
 \* Delete the $filename inside the $dir and the thumbnails.  
 \* Returns true if the file is deleted and false otherwise.  
 \*  
 \* @author Vinicius Mendes  
 \* @return boolean  
 \* @param $filename Object  
 \* @param $dir Object  
 \*/  
 function _deleteFiles($filename, $dir){  
 $saveAs = $dir . DS . $filename;  
 if(is_file($saveAs) &amp;&amp; !unlink($saveAs))  
 {  
 return false;  
 }  
 $folder = &amp;new Folder($dir);  
 $files = $folder->find(‘thumb\\.[a-zA-Z0-9]+\\.’.$filename);  
 foreach($files as $f) unlink($dir.DS.$f);  
 return true;  
 }

 // Function to create thumbnail image  
 // This requires Nate Constant’s thumbnail generator for PHPThumb  
 // https://bakery.cakephp.org/articles/view/phpthumb-component  
 // Thi function is original from digital spaghetti’s version  
 /*function createthumb($name, $filename, $new_w, $new_h)  
 {  
 App::import(‘Component’, ‘Thumb’);  
 $system = explode(".", $name);

 if (preg_match("/jpg|jpeg/", $system[1]))  
 {  
 $src_img = imagecreatefromjpeg($name);  
 }

 if (preg_match("/png/", $system[1]))  
 {  
 $src_img = imagecreatefrompng($name);  
 }

 $old_x = imagesx($src_img);  
 $old_y = imagesy($src_img);

 if ($old_x >= $old_y)  
 {  
 $thumb_w = $new_w;  
 $ratio = $old_y / $old_x;  
 $thumb_h = $ratio \* $new_w;  
 } else if ($old_x < $old_y) {  
 $thumb_h = $new_h;  
 $ratio = $old_x / $old_y;  
 $thumb_w = $ratio \* $new_h;  
 }

 $dst_img = imagecreatetruecolor($thumb_w, $thumb_h);  
 imagecopyresampled($dst_img, $src_img, 0, 0, 0, 0, $thumb_w, $thumb_h, $old_x, $old_y);

 if (preg_match("/png/", $system[1]))  
 {  
 imagepng($dst_img, $filename);  
 } else {  
 imagejpeg($dst_img, $filename);  
 }

 imagedestroy($dst_img);  
 imagedestroy($src_img);  
 }\*/

 /*\*  
 \* Création d’un aperçu d’image  
 \*  
 \* @param $name String Nom du fichier sur le serveur  
 \* @param $filename String Nom final du fichier  
 \* @param $new_w Int Largeur en px  
 \* @param $new_h Int Hauteur en px  
 \* @param $zc Bool "Zoom crop" (si vrai, découpe le plus grand carré possible au centre de l’image)  
 \*/  
 function createthumb($name, $filename, $new_w, $new_h, $zc)  
 {  
 App :: import(‘Vendor’, ‘phpThumb’, array(‘file’ => ‘phpThumb’ . DS . ‘phpthumb.class.php’));

 $phpThumb = new phpThumb();  
 $phpThumb->setSourceFilename($name);  
 $phpThumb->setParameter(‘w’, $new_w);  
 $phpThumb->setParameter(‘h’, $new_h);  
 $phpThumb->setParameter(‘zc’, $zc);

 $phpThumb->generateThumbnail();  
 $phpThumb->RenderToFile($filename);  
 }

}  
{% endhighlight %}
