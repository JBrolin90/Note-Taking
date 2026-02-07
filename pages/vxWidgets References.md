type:: Permanent
state:: Develop
tags:: #GUI #[[Mastering UI Frameworks]]
links:: [GitHub](https://github.com/wxWidgets/wxWidgets) [Main web site](https://www.wxwidgets.org/) [Offical Documentation](https://docs.wxwidgets.org/) [C++ GUI Tutorial]({{video https://www.youtube.com/playlist?list=PLFk1_lkqT8MbVOcwEppCPfjGOGhLvcf9G}})

- For Linux, vxWidgets is, like #GTKmm, a wrapper on top of GTK, while on Windows, I assume it is based on the Win32 things, as it claims native look and feel.
	- For this reason, it should be safe to assume that the look and feel would resemble GTKmm and normal Windows look and feel when on Windows.
- The Bare minimum that you need to wrap your head around
	- The smallest possible wxWidget program
		- ```C++
		  #include <wx/app.h>
		  #include <wx/frame.h>
		  
		  class MyApp : public wxApp {
		  	public: virtual bool OnInit()     {
		          wxFrame *frame = new wxFrame(NULL, wxID_ANY, "Hello World");
		          bool frameOpenedSuccefully = frame->Show(true);
		          return frameOpenedSuccefully;
		      }
		  };
		  
		  wxIMPLEMENT_APP(MyApp);
		  ```
		- This program effectively does 4 things
			- `wxIMPLEMENT_APP(MyApp)`
			  logseq.order-list-type:: number
				- This is part of the wxWidget's magic. It creates the main function and instantiates the a MyApp object. It then, somehow, calls the MyApp.OnInit() method. If OnInit returns **true**, it starts the message loop and the application is up and running. If OnInit returns false, the application terminates.
			- `wxFrame *frame = new wxFrame(NULL, wxID_ANY, "Hello World");`
			  logseq.order-list-type:: number
			  collapsed:: true
				- Creates a new independent desktop window (frame in wxWidget lingo)
				  collapsed:: true
					- The first argument, the parent, is null which makes it an independentt desktop window.
					- The second argument is the window's unique ID. passing wxID_ANY (-1) asks the framework to assign a unique ID.
				- Note that wxFrame will destroy, first its children and then itself and finally delete itself from the heap when it receives an exit signal. For that reason, one should not allocate any frame on the stack.
			- `bool frameOpenedSuccefully = frame->Show(true);`
			  logseq.order-list-type:: number
				- This line, effectively, tries to show the window. If successful, it returns true, otherwise it returns false.
			- `return frameOpenedSuccefully;`
			  logseq.order-list-type:: number
				- The success of the OnInit method is determined by the boolean frameOpenedSuccefully. It allows the caller to take proper action
		- Check the #GTK minimum program to see how the wxImplement_APP works.
		  logseq.order-list-type:: number
	- The build system
		- wxWidgets refers to #CMAKE but I am using #Meson here.
			- meson.build
			- ```meson
			  project('wx_hello', 'cpp',
			    version : '0.1',
			    default_options : ['warning_level=3', 'cpp_std=c++17']
			  )
			  
			  sources = [
			    'hello.cpp'
			  ]
			  
			  # 1. Look for wxWidgets. 
			  # 'modules' specifies which components of the library you need.
			  # For a basic app, 'core' and 'base' are the essentials.
			  wx_dep = dependency('wxwidgets', version : '>=3.0.0', modules : ['core', 'base'])
			  
			  # 2. Define the executable
			  executable('hello_world',
			    sources,
			    dependencies : wx_dep,
			    # This flag ensures Windows doesn't open a console window in the background
			    win_subsystem : 'windows', 
			    install : true
			  )
			  ```
			- When reading on meson's web page, I understood that wxWidgets does not support pkg-config but aperantly it does. Therefore it is simple.
			- I did not need to create a tasks.json but Ctrl-Shift-B build works on VSCode as long as #meson is installed.
			- For debugging, I have this launch.json
			- ```json
			  {
			      "version": "0.2.0",
			      "configurations": [
			          {
			              "name": "Debug hello_world",
			              "type": "cppdbg",
			              "request": "launch",
			              "program": "${workspaceFolder}/builddir/hello_world",
			              "args": [],
			              "stopAtEntry": false,
			              "cwd": "${workspaceFolder}",
			              "environment": [],
			              "externalConsole": false,
			              "MIMode": "gdb",
			              "setupCommands": [
			                  {
			                      "description": "Enable pretty-printing for gdb",
			                      "text": "-enable-pretty-printing",
			                      "ignoreFailures": true
			                  }
			              ],
			              "preLaunchTask": "Meson: Build hello_world:executable"
			          }
			      ]
			  }
			  ```