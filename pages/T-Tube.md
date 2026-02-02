- Creating a T-tube (or T-junction) in FreeCAD is a classic exercise in Part Design. The most robust way to do this is by using two additive cylinders and then hollow them out using either the **Thickness** tool or a subtraction.
	- ### 1. Create the main body
		- **Create a New Sketch:** Select the $XY$-Plane and draw a circle centered at the origin. This will be the outer diameter of your main pipe.
		- **Pad it:** Use the **Pad** tool to extrude the circle to your desired length (e.g., $100\text{ mm}$). Set the "Type" to **Symmetric to plane** so the center of the pipe stays at the origin.
	- ### 2. Create the Branch Pipe
		- **Create a Second Sketch:** Select a plane perpendicular to the first (like the $XZ$-Plane).
		- **Draw the Branch:** Draw another circle. Position it so its center is on the axis of the first pipe.
		- **Pad the Branch:** Use the **Pad** tool again. Set the length to reach outward from the center.
		  
		  > **Tip:** If the branch needs to start from the surface of the main pipe, you may need to use an "Offset" or simply pad it from the center and let it merge with the first cylinder. FreeCAD handles this overlap perfectly within a single "Body."
	- ### 3. Hollowing the Tube (The "Shell" Method)
	  The easiest way to make it look like a pipe rather than a solid T-junction is the **Thickness** tool:
		- Select the **three circular end-faces** of the T-junction (the two ends of the main pipe and the one end of the branch). Hold `Ctrl` while clicking to select multiple faces.
		- Click the **Thickness** tool.
		- Set the thickness to a negative value (e.g., $-2\text{ mm}$) to create the wall thickness inward. FreeCAD will automatically "hollow out" the intersection where the pipes meet.
	- ### 4. [Free Cad example](../assets/HanmgerT_1769877153163_0.FCStd)