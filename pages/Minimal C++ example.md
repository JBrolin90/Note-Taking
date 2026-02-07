-
- main.cpp
	- ```c++
	  #include <gtkmm.h>
	  
	  class MyWindow : public Gtk::Window
	  {
	  public:
	      MyWindow()
	      {
	          set_title("GTKmm Styled");
	          set_default_size(300, 150);
	  
	          m_box.set_orientation(Gtk::Orientation::VERTICAL);
	          m_box.set_margin(20);
	          m_box.set_spacing(10);
	          set_child(m_box);
	  
	          m_entry.set_placeholder_text("Type here...");
	          // Add a CSS class for specific styling if needed
	          m_entry.add_css_class("my-entry"); 
	          m_box.append(m_entry);
	  
	          m_button.set_label("Submit");
	          m_button.add_css_class("my-button");
	          m_box.append(m_button);
	  
	          m_button.signal_clicked().connect([this]() {
	              m_button.set_label("You typed: " + m_entry.get_text());
	          });
	      }
	  
	  protected:
	      Gtk::Box m_box;
	      Gtk::Entry m_entry;
	      Gtk::Button m_button;
	  };
	  
	  int main(int argc, char* argv[])
	  {
	      auto app = Gtk::Application::create("org.example.gtkmm");
	  
	      // 1. Connect to the 'startup' signal to load CSS globally
	      app->signal_startup().connect([]() {
	          auto css_provider = Gtk::CssProvider::create();
	          
	          // 2. Define standard CSS (similar to Web)
	          // We target the widgets directly or via classes
	          css_provider->load_from_data(R"(
	              window {
	                  background-color: #f0f0f0;
	              }
	              .my-entry {
	                  border: 2px solid #ccc;
	                  border-radius: 4px;
	                  padding: 5px;
	                  color: #333;
	              }
	              .my-button {
	                  background-color: #0078d7;
	                  color: white;
	                  font-weight: bold;
	                  border-radius: 4px;
	              }
	              .my-button:hover {
	                  background-color: #005a9e;
	              }
	          )");
	  
	          // 3. Apply to the default display
	          Gtk::StyleContext::add_provider_for_display(
	              Gdk::Display::get_default(),
	              css_provider,
	              GTK_STYLE_PROVIDER_PRIORITY_APPLICATION
	          );
	      });
	  
	      return app->make_window_and_run<MyWindow>(argc, argv);
	  }
	  ```
- meson.build
  collapsed:: true
	- ```meson
	  project('gtkmm_styled', 'cpp',
	    default_options : ['cpp_std=c++17']) # gtkmm-4.0 requires C++17
	  
	  # Find the gtkmm-4.0 dependency
	  gtkmm_dep = dependency('gtkmm-4.0')
	  
	  # Define the executable
	  executable('styled_app',
	    'main.cpp',
	    dependencies : gtkmm_dep
	  )
	  
	  ```
	- To build and run from terminal
		- ```bash
		  $ meson setup builddir
		  $ cd builddir
		  $ meson compile
		  
		  $ ./styled_app
		  ```