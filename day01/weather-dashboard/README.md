Weather Data Collection System 🌤️
Day 1 Project of the 30-Days DevOps Challenge

This project is a Weather Data Collection System that integrates with the OpenWeather API to fetch real-time weather data for multiple cities and stores the data in an AWS S3 bucket.

It demonstrates core DevOps principles, such as:

Cloud integration (AWS S3)
External API consumption
Error handling
Infrastructure as Code (IaC) principles
Environment variable management
Features ✨
Fetch real-time weather data (temperature, humidity, weather conditions).
Automatically uploads the data to an AWS S3 bucket for storage.
Supports multiple cities.
Adds timestamps to all data for historical tracking.
Architecture
Programming Language: Python 3.x
Cloud Provider: AWS (S3)
External API: OpenWeather API
Key Dependencies:
boto3: AWS SDK for Python
requests: For API requests
python-dotenv: For managing environment variables
Setup Instructions 🛠️
1. Clone the Repository
bash
Copy code
git clone https://github.com/your-username/weather-data-collector.git  
cd weather-data-collector  
2. Install Dependencies
Ensure Python 3.x is installed. Then:

bash
Copy code
pip install -r requirements.txt  
3. Configure the Environment Variables
Create a .env file in the root directory with the following content:

plaintext
Copy code
OPENWEATHER_API_KEY=your_openweather_api_key  
AWS_BUCKET_NAME=your_aws_s3_bucket_name  
4. Configure AWS CLI
Ensure you have configured AWS CLI with proper credentials:

bash
Copy code
aws configure  
5. Run the Application
Run the main Python script to fetch and store weather data:

bash
Copy code
python src/weather_dashboard.py  
Example Output
Sample Console Log:

plaintext
Copy code
Fetching weather data for New York...  
Data fetched successfully!  
Uploading data to S3...  
Data uploaded successfully to bucket: weather-data-bucket  
What I Learned 🎓
AWS S3 bucket creation and management
Environment variable management for secure API keys
Python best practices for API integration
Git workflow for project development
Error handling in distributed systems
Future Enhancements 🚀
Add weather forecasting.
Implement data visualization (charts, graphs).
Support additional cities via a dynamic input.
Automate testing and validation pipelines.
Set up a full CI/CD pipeline.
License
This project is licensed under the MIT License.
