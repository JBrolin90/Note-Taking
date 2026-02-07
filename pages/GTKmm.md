Type:: Reference
state:: Develop
Tags:: #GUI, #[[Mastering UI Frameworks]], #C++

- [Programming with gtkmm 4](https://gnome.pages.gitlab.gnome.org/gtkmm-documentation/) Is the official GNOME documentation for GTKmm
- [GTKmm Reference Manual](https://gnome.pages.gitlab.gnome.org/gtkmm/index.html)
- The Bare minimum that you need to wrap your head around
	- The smallest possible GTKmm program
	  collapsed:: true
		- The following complete program creates a GTkmm application, creates a Window and starts the application. The window is empty but functioning.  ref: [Gnome simple example](https://gnome.pages.gitlab.gnome.org/gtkmm-documentation/chapter-basics.html#sec-basics-simple-example)
		- Note that there are two Gtkmm atomic includes, one for the application and one for the window
		- main.cpp
		- ```C++
		  #include <gtkmm/application.h>
		  #include <gtkmm/window.h>
		  int main(int argc, char* argv[])
		  {
		      auto app = Gtk::Application::create("org.example.gtkmm");
		    	auto result = app->make_and_run<Gtk::Window>(argc, argv);
		  	return result;
		  }
		  ```
		- As you can see, it is rather straight forward to get GTKmm up and running.
		- Note that in order to populate the Window, you should create a Custom Window class, inheriting from Gtk::Window. See below
	- Creating a custom window
	  collapsed:: true
		- The simplest way you can create a functioning custom window is to derive it from Gtk::Window and a simple example can be seen from this snippet:
		- ```C++
		  class MyWindow : public Gtk::Window
		  {
		  public:
		      MyWindow()
		      {
		          set_title("My Window");
		          set_default_size(300, 150);
		      }
		  };
		  
		  ```
		- Populating the window
			- How can I add a Textbox to my page?
	- The build system
		- Gnome recommends the #Meson build system.
		- A minimal make file, meson.build, could look like this
		- ```meson
		  project('gtkmm_simple', 'cpp',
		    default_options : ['cpp_std=c++26']) # gtkmm-4.0 requires C++17
		  
		  # Find the gtkmm-4.0 dependency
		  gtkmm_dep = dependency('gtkmm-4.0')
		  
		  # Define the executable
		  executable('simple_app',
		    'main.cpp',
		    dependencies : gtkmm_dep
		  )
		  ```
		- You setup the build by the following command:
		- ```bash
		  meson setup builddir
		  ```
		- "builddir", in the command above, is the name of the build directory.
-
-
-