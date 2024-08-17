# Virtual Environment


```bash
mkdir my_project
```

Within the project directory, create the virtual environment as follows:
```bash
python3 -m venv myproject/venv
```

Activate the virtual environment
```bash
source myproject/venv/bin/activate
```

to deactivate the virtual environment, run:
```bash
deactivate
```

to delete a virtual environment, just delete the directory for the environment
```bash
rm -rf my_project/venv
```

### Exporting packages
Run the following command inside your virtual environment
```bash
pip freeze > requirements.txt
```

### Importing packages
Run the following command inside your virtual environment. You will need to have a requirements.txt file inside the virtual environment
```
pip install -r requirements.txt
```
