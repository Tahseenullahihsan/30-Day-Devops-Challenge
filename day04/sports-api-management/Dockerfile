FROM python:3.9-slim

# Set the working directory inside the container
WORKDIR /app

# Copy the requirements file into the container
COPY requirements.txt requirements.txt

# Install dependencies
RUN pip install -r requirements.txt

# Copy all files from the current directory into the container
COPY . .

# Expose the port your app runs on
EXPOSE 8000

# Command to run the application
CMD ["python", "flask_app.py"]