---
id: 1390
title: 'Bug lors du lancement Eclipse 4.3 : Unable to &#8230;'
date: '2013-01-17T11:16:52+01:00'
author: 'Nicolas Hachet'
layout: post
guid: 'https://blog.nicolashachet.com/?p=1390'
permalink: /blog/developpement-php/bug-lors-du-lancement-eclipse-4-3-unable-to/
dsq_thread_id:
    - '1285642279'
image: /wp-content/uploads/2013/01/eclipse_bugs-295x300.png
categories:
    - 'Eclipse'
tags:
    - 'Eclipse IDE'
    - IDE
---

Si votre **Eclipse 4.3 (Juno) a planté** et qu’il ne veut plus redémarrer, voici l’astuce permettant de "réparer" votre workspace. Elle permet de démarrer un Eclipse dont le workspace serait corrompu à cause d’un plantage ou d’un freeze de Java.  
Au démarrage, Eclipse devrait vous raconter ce genre de salade, sans plus d’infos sur le problème :  
Unable to bla bla bla…

Le fichier de log D:\\Workspace\\.metadata\\**.log** contient l’erreur suivante :

!ENTRY <strong>org.eclipse.osgi</strong> 4 0 2012-10-31 10:40:52.799  
!MESSAGE Application error  
!STACK 1  
org.eclipse.swt.SWTException: Failed to execute runnable (java.lang.NullPointerException)  
at org.eclipse.swt.SWT.error(SWT.java:4361)  
at org.eclipse.swt.SWT.error(SWT.java:4276)  
at org.eclipse.swt.widgets.Synchronizer.runAsyncMessages(Synchronizer.java:138)  
at org.eclipse.swt.widgets.Display.runAsyncMessages(Display.java:4144)  
at org.eclipse.swt.widgets.Display.readAndDispatch(Display.java:3761)  
at org.eclipse.swt.widgets.Display.release(Display.java:3814)  
at org.eclipse.swt.graphics.Device.dispose(Device.java:295)  
at org.eclipse.ui.internal.ide.application.IDEApplication.start(IDEApplication.java:140)  
at org.eclipse.equinox.internal.app.EclipseAppHandle.run(EclipseAppHandle.java:196)  
at org.eclipse.core.runtime.internal.adaptor.EclipseAppLauncher.runApplication(EclipseAppLauncher.java:110)  
at org.eclipse.core.runtime.internal.adaptor.EclipseAppLauncher.start(EclipseAppLauncher.java:79)  
at org.eclipse.core.runtime.adaptor.EclipseStarter.run(EclipseStarter.java:353)  
at org.eclipse.core.runtime.adaptor.EclipseStarter.run(EclipseStarter.java:180)  
at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)  
at sun.reflect.NativeMethodAccessorImpl.invoke(Unknown Source)  
at sun.reflect.DelegatingMethodAccessorImpl.invoke(Unknown Source)  
at java.lang.reflect.Method.invoke(Unknown Source)  
at org.eclipse.equinox.launcher.Main.invokeFramework(Main.java:629)  
at org.eclipse.equinox.launcher.Main.basicRun(Main.java:584)  
at org.eclipse.equinox.launcher.Main.run(Main.java:1438)  
at org.eclipse.equinox.launcher.Main.main(Main.java:1414)  
Caused by: java.lang.NullPointerException  
at org.eclipse.ui.internal.Workbench.createWorkbenchWindow(Workbench.java:1235)  
at org.eclipse.ui.internal.Workbench.getActiveWorkbenchWindow(Workbench.java:1228)  
at com.dubture.pdt.formatter.Starter$1.run(Starter.java:63)  
at org.eclipse.swt.widgets.RunnableLock.run(RunnableLock.java:35)  
at org.eclipse.swt.widgets.Synchronizer.runAsyncMessages(Synchronizer.java:135)  
… 18 more  


La solution est de supprimer le contenu du répertoire suivant dans votre wordspace (ici D:\\Workspace) :  
D:\\Workspace\\**.metadata\\.plugins\\org.eclipse.e4.workbench**

Vous devriez y trouver un fichier **workbench.xmi** : supprimez-le et relancez Eclipse. 🙂

## Des problèmes de lenteurs sur Eclipse 4 (Juno) ?

Vous avez des [problèmes de lenteurs sur Eclipse Juno ? Un patch existe, voyez cet article.](https://www.nicolashachet.com/blog/2013/02/18/ide/eclipse/ameliorer-les-performances-declipse-4-x-juno/ "Améliorer les performances d’Eclipse 4.x (Juno)")
