# PySpace
GLSL Fractal Ray Marcher in Python

## Initial Setup

### Windows and VS Code

#### Set up VS Code
1. Open this project directory in VS Code.
1. Install the Python extension for VS Code.
1. Download Python for Windows: https://www.python.org/downloads/, typically use the Download Python 3.7.1 button that appears first on the page.
1. Make sure you check the box to add Python to the PATH.
1. When installation is done, there will be a button to ensure your PATH doesn't have a max character limit (260 I think), click this.
1. Check that Python is in PATH; use `Win+R` and type `cmd`, then type `path`. You should see Python in there.
1. Restart VS code to ensure Python settings and PATH is not cached.
1. Update PIP: 
    ```
    PS> python -m pip install --upgrade pip
    ``` 
    to avoid `"You are using pip version X, however version Y is available"`.
1. Select a Python interpreter: From within VS Code, select a Python 3 interpreter by opening the **Command Palette (`Ctrl+Shift+P`)**, start typing the **Python: Select Interpreter** command to search, then select the command. 
    
    You can also use the **Select Python Environment** option on the Status Bar if available (it may already show a selected interpreter, too). If you don't see **Python: Select Interpreter** in the command Pallette, reload VS Code.

#### Install virtual environment
***You don't have to do this unless you want to constrain all pip installs to
single environments***. By default, installing Python modules does so globally
on your system, so you can technically skip this section and install all the
modules globally.
1. Install virtual env: 
    ```
    PS> pip install virtualenv
    ```
1. And pip install virtual env wrapper:
    ```
    PS> pip install virtualenvwrapper-win
    ```
1. Change the environment variable in Windows (Same place the PATH is changed),
    and add `WORKON_HOME` for the key, and browse or add the directory you want the virtual environments to be stored. (I set mine up to be `E:/virtualenv`)
1. Create environment for this project:
    ```
    PS> mkvirtualenv pyspace
    ```
1. Run the script: `python .\ray_marcher_demo.py` (See "Running" section below).

### Installing required modules
The easiest way is to use the install script, although all this does is install the required modules for this one after the other.

1. Install the **PowerShell** extension for VS Code.
1. Install **Shader languages support for VS Code**
1. Open `install.ps1` in VS Code (if you like)
1. In the terminal, run:
    ```
    PS> ./install.ps1
    ```
1. Or, just do it yourself:
    ```
    PS> pip install pygame numpy pyopengl
    ```

## Running

Run the script! There are multiple ways to run this script:
1. In the PowerShell terminal, run:
    ```
    PS> ./Run
    ```
    Or:
    ```
    PS> python .\ray_marcher_demo.py
    ```
1. Right click inside the document, and select **Run Python File in Terminal**
1. Select one or more lines, then press `Shift+Enter` or right-click and select **Run Selection/Line in Python Terminal**. This command is convenient for testing just a part of a file.
1. Use the **Python: Start REPL** command to open a REPL terminal for the currently selected Python interpreter. In the REPL, you can then enter and run lines of code one at a time.

You should see something similar:
```
pygame 1.9.4
Hello from the pygame community. https://www.pygame.org/contribute.html
```

## Changing environments

Open `ray_marcher_demo.py` and find the following section:
```py
	#======================================================
	#               Change the fractal here
	#======================================================
	obj_render = tree_planet()
	#======================================================
```

This is where you can change which fractal scene is rendered.

These can be:
- `infinite_spheres`
- `butterweed_hills`
- `mandelbox`
- `mausoleum`
- `menger`
- `tree_planet`
- `sierpinski_tetrahedron`
- `snow_stadium`
- `test_fractal`

## Recording Video
When you're ready to record a video, press `[R]` to start recording,
and then move around.  

The camera's path and live `0` through `5` parameters are recorded to a file.
Press `[R]` when finished.

Now you can exit the program and turn up the camera parameters for better
rendering. For example; **window size**, **anti-aliasing**, **motion blur**,
and **depth of field** are great options.

When you're ready to play back and render, press `[P]` and the recorded
movements are played back. Images are saved to a `./playback` folder.
You can import the image sequence to editing software to convert it to a video.

You can press `[S]` anytime for a screenshot.

## Real-time Tuning
When building your own fractals, you can substitute numbers with string
placeholders which can be tuned real-time with key bindings.

In this example program:
| Index |   Increase   |   Decrease   |
|-------|--------------|--------------|
| `[0]` | `[Insert]`   | `[Delete]`   |
| `[1]` | `[Home]`     | `[End]`      |
| `[2]` | `[PageUp]`   | `[PageDown]` |
| `[3]` | `[NumPad7]`  | `[NumPad4]`  |
| `[4]` | `[NumPad8]`  | `[NumPad5]`  |
| `[5]` | `[NumPad9]`  | `[NumPad6]`  |

- Hold down `[left-shift]` to decrease rate 10x
- Hold down `[right-shift]` to increase rate 10x 

Set initial values of '0' through '6' for each key: 
```
keyvars = [1.5, 1.5, 2.0, 1.0, 1.0, 1.0]
```

Eg. setting the `x` of the sphere to a string of `'0'` lets it be edited real-time with `[Insert]` and `[Delete]`:
```py
def infinite_spheres():
    obj = Object()
    obj.add(FoldRepeatX(2.0))
    obj.add(FoldRepeatY(2.0))
    obj.add(FoldRepeatZ(2.0))
    obj.add(Sphere(0.5, ('0', 1.0, 1.0), color=(0.9, 0.9, 0.5)))
    return obj
```

## Demo Videos
Overview: https://youtu.be/svLzmFuSBhk

Examples: https://youtu.be/N8WWodGk9-g

ODS Demo: https://youtu.be/yJyp7zEGKaU
