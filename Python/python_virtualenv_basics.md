# python_virtualenv_basics 

Reference: 
1. [Venv_FreeCodeCamp](https://www.freecodecamp.org/news/how-to-setup-virtual-environments-in-python/)
2. [geeksforgeeks](https://www.geeksforgeeks.org/creating-python-virtual-environment-windows-linux/)


If pip is not in your system
```bash
sudo apt-get install python-pip
```

Then install virtualenv
```bash
pip install virtualenv
```

Now check your installation
```bash
virtualenv --version
```

Create a virtual environment now,
```bash
virtualenv virtualenv_name
```

After this command, a folder named **virtualenv_name** will be created. You can name anything to it. If you want to create a virtualenv for specific python version, type
```bash
virtualenv -p /usr/bin/python3 virtualenv_name
```
or
```bash
virtualenv -p /usr/bin/python2.7 virtualenv_name
```

Now at last we just need to activate it, using command
```bash
source virtualenv_name/bin/activate
```

Now you are in a Python virtual environment
You can deactivate using
```bash
deactivate
```

## How to Install Libraries in a Virtual Environment

To install new libraries, you can easily just pip install the libraries. The virtual environment will make use of its own pip, so you don't need to use pip3.

After installing your required libraries, you can view all installed libraries by using pip list, or you can generate a text file listing all your project dependencies by running the code below:

```bash
pip freeze > requirements.txt
```

You can name this requirements.txt file whatever you want.

## Requirements File
Instead of having to install each dependency one by one, they could just run the code below to install all your dependencies within their own copy of the project:

```bash
pip install -r requirements.txt
```


### Python venv

```bash
python3 -m venv /path/to/new/virtual/environment
```
