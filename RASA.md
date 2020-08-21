

To see if the conda installation of Python is in your PATH variable:

On macOS and Linux, open the terminal and run echo $PATH.
On Windows, open an Anaconda Prompt and run echo %PATH%.
To see which Python installation is currently set as the default:

On macOS and Linux, open the terminal and run which python.
On Windows, open an Anaconda Prompt and run where python.
To see which packages are installed in your current conda environment and their version numbers, in your terminal window or an Anaconda Prompt, run conda list.

# Create new conda environment 
```java
conda update conda
```
```python
conda create --name installingrasa python==3.7.6
```
```xml
conda install ujson
```
```java
conda install tensorflow
```
```python
pip install rasa
```
```
rasa init
```
-------------
```
rasa train
```
```
rasa run actions
```
https://www.accelevents.com/e/JulyRasaCertificationWorkshop/portal/stage/17058
https://www.accelevents.com/e/JulyRasaCertificationWorkshop/portal/stage/17059


# Create Python Environment VM
donload python
```
https://www.python.org/downloads/release/python-379/
```
run the command to set any folder to be as vertual environment for python by running the below commands inside any folder
```
"C:\Program Files\Python37\python.exe" -m venv venv
```
everytime you need to activate the venv by:
```
bin\Scripts\activate.bat
```
Install Rasa:
```
pip install rasa
```
create rasa project:
```
rasa init
```
