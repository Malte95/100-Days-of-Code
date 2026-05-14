Today I started my first App for the aviation-software-projects repository on my github.

**The Goal:**

Transition my Python unit converter from a text-based command-line interface into a modern desktop application with a graphical user interface (GUI). 
The app must allow users to input values and select aviation-specific conversions (Knots, Feet, Gallons) using modern visual elements.

**My Approach:**

1.Environment Setup & Installation:

I chose CustomTkinter over the standard Tkinter library to achieve a sleek, modern UI design that natively supports system dark mode. 
I configured my local environment and installed the library via the package manager.

2.GUI Initialization:

I structured the base application by setting the appearance mode to system-default and choosing a unified color theme. 
I initialized the main application window, defined a clean geometry (400x300 pixels), and set up the global event loop to keep the application active.

3.Widget Layout & Ordering:

I implemented and arranged essential visual widgets (CTkLabel and CTkEntry) to capture user inputs. 
I fixed a critical logical order bug by ensuring that all interface components are loaded before running the infinite main event loop.

4.Scalable Selection UI:

Instead of creating individual buttons for each conversion, I integrated a CTkOptionMenu (dropdown dropdown) alongside a single action button. 
This approach ensures the software architecture remains clean, scalable, and easy to expand with more aviation units in the future.
