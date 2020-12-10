Python environment folder.

## Download Python
https://www.python.org/downloads/release/python-379/

`find local instalation`
in new folder cmd 
### Create a new virtual environment
```
"C:\Program Files\Python37\python.exe" -m venv venv
```

## Activate the virtual environment:
```
C:\> .\venv\Scripts\activate
```
-------------------------------------------

## Rasa installation 
```
pip install rasa
```

for testing just run `rasa`

then you can create new project by
```
rasa init
```

then you can train your bot etc 
```
rasa train 
rasa run actions
```
