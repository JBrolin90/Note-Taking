type:: Permanent
state:: Develop
tags:: #[[Software Development]] #GTKmm #GTK #make

- [The Meson Build System main web site](https://mesonbuild.com/)
- Meson asserts itself as being a simple to use, i.e., user friendly as well as an all encompassing build system that includes support for source generation, unit tests and more.
- A simple no frill make file
  collapsed:: true
	- meson.build for C
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
	- meson.build for C++
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
- typical launch.json for VSCode
  collapsed:: true
	- launch.json
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