

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
