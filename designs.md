# **Designs** 🎨  

Explore OpenJar's 3D CAD models, repositories, and resources for makers, designers, and developers.

![Jar CAD Models image](https://d2t1xqejof9utc.cloudfront.net/screenshots/pics/f4bd3216fb07e0610818bb71d688dfc8/large.png "cad models image")

---

## **Quick Links** 🔗  
- [**GrabCAD Publication**](https://grabcad.com/library/openjar-1) – Download CAD models.  
- [**OpenJar on GitHub**](https://github.com/dmalawey/OpenJar) – Access the repository.  
- [**Docsify-This.net**](https://docsify-this.net/#/) – Template for building a page like this.  
- [**Webpage Short Link**](https://qr.page/g/2VtU8nxHXhN) – Direct link to this page, routed through a dynamic QR code generator.

---

## **Cap Design** 🧢  

This **Cap Design** is optimized for bottles and incorporates essential features for robust usability.  

![Cap Design](https://d2t1xqejof9utc.cloudfront.net/screenshots/pics/1148c8c902ae0bd4ff8536bd32c8df54/original.jpg "Cap Design Image" ':class=image-50 center')  

> **Key Features of the Bottle Cap:**  
> - Threads for secure attachment.  
> - Sealing for airtight or watertight performance.  
> - Textured grip for easy handling.  
> - A revolved body for a sleek, ergonomic design.  

> Unlike the Mason Jar cap, this bottle cap is tailored for bottle-specific applications, incorporating **design intent** for various use cases.  

Access the model here: [**Model on GrabCAD**](https://grabcad.com/library/cap-43)  

---



-------------------------------------------------------------------------------------------------------------------------------------------------



---

##KAASI-LID
##WIP

--- 

-------------------------------------------------------------------------------------------------------------------------------------------------

## MakerLuis
 The Power of Python and Fusion 360 for 3D Printing

**Date:** *June 12, 2020*  
**Author:** *MakerLuis*

 Introduction

3D printing has revolutionized the way we prototype and manufacture parts. However, getting from a concept to a final 3D model ready for printing can be time-consuming. That’s where the combination of **Python** scripting and **Autodesk Fusion 360** comes in, making the workflow more efficient and customized for your needs.

In this guide, we’ll explore how to harness Python’s power to automate and streamline Fusion 360’s parametric modeling environment, ultimately optimizing 3D printing projects.

 Why Python and Fusion 360?

- **Parametric Modeling:** Fusion 360 is well-known for its parametric modeling capabilities, where every geometric entity can be defined by parameters (dimensions, relationships, constraints).
- **Scripting & Automation:** Python offers straightforward scripting capabilities. By tapping into Fusion 360’s Application Programming Interface (API), you can automate repetitive tasks, batch-process multiple files, and modify models on the fly.
- **Accelerated Iteration:** With code-driven parameter adjustments, you can rapidly iterate through designs, changing dimensions or features with minimal manual effort.
- **Customization:** Rather than relying solely on Fusion 360’s built-in tools, Python scripting allows you to tailor the software’s behavior to your project’s unique requirements.

 Key Benefits

1. **Time Savings:**  
   Automate the generation and modification of complex geometries, significantly cutting down manual modeling time.

2. **Consistency & Repeatability:**  
   Ensure that all modifications follow a set of consistent rules, reducing human error.

3. **Scalability:**  
   Quickly apply the same modifications or generation logic to multiple projects, parts, or assemblies.

4. **Enhanced Creativity:**  
   Free yourself from repetitive tasks to focus on new design concepts and innovations.

 Getting Started With the Fusion 360 API

 Requirements

- **Fusion 360 Installation:**  
  Make sure you have Fusion 360 installed and updated.
  
- **Python Environment:**  
  Python is embedded in Fusion 360’s scripting environment. No external installation needed for basic scripting.
  
- **Developer Panel:**  
  Access the “Scripts and Add-Ins” panel in Fusion 360 to create, run, and manage your Python scripts.

Basic Steps

1. **Open the Script Manager:**  
   Go to **Tools > Add-Ins > Scripts and Add-Ins**.
   
2. **Create a New Script:**  
   Click **+** to create a new Python script. This provides a template to start coding.
   
3. **Edit Your Script:**  
   Use the built-in editor or an external code editor to write and refine your Python script.
   
4. **Run and Test:**  
   Execute your script to modify the Fusion 360 model. Observe results, adjust parameters, and iterate as needed.

 Example: Parametric Cube Generation

Below is a simple Python code snippet that demonstrates how to create a cube with a user-defined side length:

```python
import adsk.core, adsk.fusion, adsk.cam

def run(context):
    app = adsk.core.Application.get()
    ui  = app.userInterface
    design = app.activeProduct

    # Prompt user for cube size
    side_length = 10  # in millimeters, for example
    
    rootComp = design.rootComponent
    sketches = rootComp.sketches
    xyPlane = rootComp.xYConstructionPlane
    sketch = sketches.add(xyPlane)

    # Draw a square
    lines = sketch.sketchCurves.sketchLines
    square = [
        lines.addByTwoPoints(adsk.core.Point3D.create(0, 0, 0),
                             adsk.core.Point3D.create(side_length, 0, 0)),
        lines.addByTwoPoints(adsk.core.Point3D.create(side_length, 0, 0),
                             adsk.core.Point3D.create(side_length, side_length, 0)),
        lines.addByTwoPoints(adsk.core.Point3D.create(side_length, side_length, 0),
                             adsk.core.Point3D.create(0, side_length, 0)),
        lines.addByTwoPoints(adsk.core.Point3D.create(0, side_length, 0),
                             adsk.core.Point3D.create(0, 0, 0))
    ]

    # Extrude the square to form a cube
    prof = sketch.profiles.item(0)
    extrudes = rootComp.features.extrudeFeatures
    extInput = extrudes.createInput(prof, adsk.fusion.FeatureOperations.NewBodyFeatureOperation)
    distance = adsk.core.ValueInput.createByReal(side_length)
    extInput.setDistanceExtent(False, distance)
    extrudes.add(extInput)
    
    ui.messageBox('Cube created with side length: {} mm'.format(side_length))
```

 How It Works

- **Sketch Generation:** We create a simple square sketch on the XY plane.
- **Extrusion:** Using the `extrudeFeatures` API, the square is extruded to form a cube.
- **Parametric Control:** By adjusting `side_length`, you can instantly regenerate cubes of different sizes.

 Tips for More Advanced Projects

- **Leverage Parameters:**  
  Store frequently changed values (e.g., thickness, radius, hole diameter) as variables. This allows quick global edits.
  
- **Integrate with External Data:**  
  Pull data from spreadsheets or other external sources to systematically generate variations of a model.
  
- **Combine with Other Tools:**  
  Integrate your Python script with version control (Git) or project management tools to streamline collaboration.

Exporting Your Models

After automating the creation of a 3D model, you can:

- **Export as STL:**  
  Ideal for 3D printing. Easily convert your Fusion 360 file to STL directly or via the API.
  
- **Adjust Print Parameters:**  
  Once the geometry is finalized, move it to your slicer of choice and set layer heights, infill, supports, etc.

 Conclusion

Python scripting in Fusion 360 enables a flexible and efficient workflow for 3D printing. By automating repetitive modeling tasks, you can focus on innovation, ensure consistent quality, and quickly iterate through design variations. Whether you’re making a single part or a family of products, code-driven customization is a powerful tool in your digital fabrication toolbox.

---

*For more tutorials and tips, visit [MakerLuis.com](https://www.makerluis.com/).*


-------------------------------------------------------------------------------------------------------------------------------------------------