# Import base image OS you can get this from google python official
FROM python:3.9-slim
    
# Working directory where your code will get store in container
WORKDIR /app
    
#Copy source code to conatiner's working directoy
    
COPY app.py .
# here . means /app directory from container which current directory u can also do src/* app/
    
# Now given command for insatlling libraries and compling commands && needs atleast one argument after insatll
RUN pip install --upgrade pip
    
#Expose ports . Deafult pythong is runnign on port 8000
EXPOSE 80
    
# here Command to serve application
    CMD ["python","app.py"]
