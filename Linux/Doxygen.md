## Doxygen Installation and Configuration Notes

### Installation Command (Linux/Debian)

Bash

```
sudo apt install doxygen
sudo apt install doxygen-gui
```
### Core Commands

| **Action**                       | **Command**                               | **Notes**                                                                                 |
| -------------------------------- | ----------------------------------------- | ----------------------------------------------------------------------------------------- |
| **Generate Default Config File** | `doxygen -g doxygen.txt`                  | Creates the main configuration file with all default settings.                            |
| **Generate Documentation**       | `doxygen doxygen.txt`                     | Executes the documentation generation based on the settings in the specified config file. |
| **View Documentation**           | Open `[OUTPUT_DIRECTORY]/html/index.html` | This is the file you open in a web browser (e.g., Chrome, Firefox).                       |
| **GUI**                          | `doxywizard doxygen.txt`                  | Graphical Interface for configuration.                                                    |

### Essential Configuration Settings

The following are the key variables to change in the `doxygen.txt` file (find the variable and change the value after the `=` sign).

|**Doxygen Variable**|**Setting Used**|**Description**|
|---|---|---|
|**PROJECT_NAME**|`Mike's Doxygen Demonstration`|Sets the title of the generated documentation.|
|**OUTPUT_DIRECTORY**|`doxygen_docs`|Specifies the parent folder for the generated output (HTML, LaTeX, etc.).|
|**INPUT**|`source/`|Specifies the path to your source code directory.|
|**RECURSIVE**|`YES`|Tells Doxygen to look for source files in subdirectories of the `INPUT` path.|
|**GENERATE_LATEX**|`NO`|Disables LaTeX/PDF generation, resulting in faster runs and only HTML output.|

### Enhancing Documentation Features

These optional settings improve the usability and look of the generated documentation.

|**Doxygen Variable**|**Setting Used**|**Feature Description**|
|---|---|---|
|**GENERATE_TREEVIEW**|`YES`|Adds an interactive sidebar (tree view) for easier navigation between classes, files, and namespaces.|
|**SOURCE_BROWSER**|`YES`|Enables linking from the documentation to the original source code lines.|
|**INLINE_SOURCES**|`YES`|Displays the source code block directly inside the function's documentation page.|

### Source Code Documentation Style

For Doxygen to pick up comments and include them in the output, use a special comment style immediately before the class, struct, function, or variable.

|**Style**|**Example**|**Notes**|
|---|---|---|
|**Triple Slash**|`///`|Common style used in the video for C/C++ and D.|
|**Javadoc/Block**|`/** ... */`|Another popular style for multi-line comments.|

**Example of Documenting a Function:**

C++

```
/**
 * @brief Calculates the rotation matrix.
 *
 * @param angle The rotation angle in radians.
 * @return A 4x4 matrix representing the rotation.
 */
Matrix4 calculate_rotation(float angle) 
{ 
    // ... function implementation
}
```

### Adding Custom Pages

1. Create a Markdown-like file (e.g., `main.docs`).
    
2. Use the `\mainpage` command in the file to define the content for your main landing page.
    
3. Ensure the file is in a directory specified by the **INPUT** variable.
    

**Content for `main.docs`:**

Markdown

```
/*! \mainpage Mike's Project Documentation

# Welcome to Mike's Doxygen Demonstration

This is the main page for the project documentation. You can use Markdown 
syntax here to write tutorials, build instructions, or a project overview.

- Check out the **Namespaces** tab for the code structure.
- Look at the **Classes** tab for all available types.

*/
```