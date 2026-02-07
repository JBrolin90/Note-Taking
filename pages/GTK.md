Type:: Permanent
state:: Develop
Tags:: #GUI #[[Mastering UI Frameworks]]
links:: [The GTK Project](https://www.gtk.org/) [GTK C Tutorial](https://github.com/ToshioCP/Gtk4-tutorial/tree/main) [Widget gallery](https://docs.gtk.org/gtk4/visual_index.html)

- The Bare minimum you need to wrap your head around
	- The smallest possible GTK program
	- ```C
	  app_activate (GApplication *app, gpointer *app_object) 
	  {
	  
	     //This static method would call: app_object->OnInit()
	     GtkWindow *win;
	  
	     win = (GtkWindow*) gtk_application_window_new(GTK_APPLICATION (app));
	     gtk_window_set_title(win, "Hello World");
	     gtk_window_present(win);
	  }
	   
	  int main (int argc, char **argv) 
	  {
	     GtkApplication *app;
	     int stat;
	   
	     app = gtk_application_new ("com.github.ToshioCP.lb1", G_APPLICATION_DEFAULT_FLAGS);
	  
	     g_signal_connect (app, "activate", G_CALLBACK (app_activate), NULL/*Here we could send an object reference*/);
	     
	     stat = g_application_run (G_APPLICATION (app), argc, argv);
	     
	     g_object_unref (app);
	     return stat;
	  } 
	  ```
- The build system
	- I have used #meson for this C program, here is the build file
	- ```meson
	  project('pr1', 'c',
	    version: '1.0',
	    default_options: ['warning_level=3', 'c_std=c23'])
	  
	  gtk4_dep = dependency('gtk4')
	  
	  executable('pr1',
	    'pr1.c',
	    dependencies: gtk4_dep,
	    install: false)
	  ```