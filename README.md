## Python Script Docker Deployment

1. Install Docker <br>
First, you need to install Docker on your machine. You can download Docker Desktop from the official Docker website.

2. Create a Python Script <be>
Create a Python script that you want to run. For example, save the following script as script.py:

Python code
```
print("Hello from inside a Docker container!")
```

3. Create a Dockerfile <be>
A Dockerfile specifies how to build your Docker image. Here's a simple Dockerfile for running a Python script:

Dockerfile code
```
# Use an official Python runtime as a parent image
FROM python:3.8-slim

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Run script.py when the container launches
CMD ["python", "script.py"]
```

This Dockerfile starts from a slim version of the official Python 3.8 image, sets the working directory to /app inside the container, copies the local directory's contents to /app, and specifies that the container should run python script.py when it starts.

4. Build the Docker Image <be>
Navigate to the directory containing your Dockerfile and run the following command to build your Docker image:

bash code
```
docker build -t python-script .
```

This command builds an image from the Dockerfile in the current directory and tags it as python-script.

5. Run the Docker Container
After the image is built, you can run it with the following command:

bash code
```
docker run python-script
```

This command runs your Python script inside a new container based on the python-script image.

6. Managing Data and Dependencies
If your script requires external libraries or needs to access data files, you should modify your Dockerfile to install these dependencies and to copy these files into the image. For example, if you need the requests library:

Add this line to your Dockerfile to install packages from requirements.txt:

Dockerfile code
```
RUN pip install -r requirements.txt
```

And create a requirements.txt file in the same directory as your Dockerfile that includes:

Copy code
```
requests
```

7. Clean Up <be>
After running the containers, you might want to clean up to free up space:

bash code <be>
**Remove containers that have finished running**
```
docker container prune
```

**Remove images that are not in use**
```
docker image prune
```
