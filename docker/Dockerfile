from python:3.7-alpine

RUN apk add --no-cache git postgresql-dev gcc libc-dev
RUN apk add --no-cache gcc g++ make libffi-dev python3-dev build-base

RUN pip install gunicorn
RUN pip install psycopg2
RUN pip install ipdb
RUN pip install ipython

WORKDIR /app

RUN git clone https://github.com/marcascal2/decide-1 .
RUN pip install -r requirements.txt

WORKDIR /app/decide

# local settings.py
ADD docker-settings.py /app/decide/local_settings.py

RUN ./manage.py collectstatic

#CMD ["gunicorn", "-w 5", "decide.wsgi", "--timeout=500", "-b 0.0.0.0:5000"]

# Base image 
FROM python:3 
#copy the requirements txt file with all our dependencies
COPY requirements.txt ./ 
#install the dependencies
RUN pip install --no-cache-dir -r requirements.txt  
#copy the app in the image
COPY holamundo.py ./  
#define a default command to execute
CMD [ "python", "./holamundo.py" ]