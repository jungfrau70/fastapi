# FastApi

export WORKDIR='/root/fastapi'
cd $WORKDIR

#########################################################################################
# 1. Setup IDE
#########################################################################################

apt-get install python3.8
virtualenv -p python3.8 venv
source venv/bin/activate

(venv) python --version
(venv) pip install --upgrade pip
(venv) pip install fastapi uvicorn


#########################################################################################
# 2. Coding Sample Code
#########################################################################################

cat <<EOF | tee main.py
from typing import Optional
from fastapi import FastAPI

app = FastAPI()


@app.get('/')
def dead_root():
    return { "Hello": "World" }

@app.get('/item/{item-id}')
def read_item(item_id: int, q: Optional[str] = None):
    return {'item_id': item_id, "q": q}
EOF


#########################################################################################
# 2. Run Sample Code
#########################################################################################

uvicorn main:app --reload

export PYTHONPATH=~/fastapi && python app/main.py

#########################################################################################
# 2. Run Sample Code
#########################################################################################

git reset --hard [commit-id]
git reflog