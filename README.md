Rail Plot

Rail Plot is a full-stack web application designed to manage, visualize, and analyze railway-related data. It leverages a modern cloud-native architecture using AWS services, a Python backend, and a React frontend.

📌 Tech Stack
Frontend
React.js (SPA)
Hosted on AWS S3 (Static Hosting)
Backend
Python (Flask / FastAPI — adjust based on your actual framework)
Hosted on AWS EC2
Database
PostgreSQL
Cloud & DevOps
AWS EC2 (Backend hosting)
AWS S3 (Frontend hosting)
AWS IAM (Access management)
Nginx (Reverse proxy - optional but recommended)

🏗️ Architecture Overview
User (Browser)
   ↓
React App (AWS S3)
   ↓ API Calls
Backend API (AWS EC2 - Python)
   ↓
PostgreSQL Database
⚙️ Features
📊 Railway data visualization
🗺️ Plotting rail routes / analytics
🔐 Secure API handling
⚡ Scalable cloud deployment
📡 RESTful API integration
📁 Project Structure

rail-plot/
│
├── backend/
│   ├── app/
│   ├── routes/
│   ├── models/
│   ├── config/
│   ├── main.py
│   └── requirements.txt
│
├── frontend/
│   ├── public/
│   ├── src/
│   ├── package.json
│   └── build/
│
├── database/
│   └── schema.sql
│
└── README.md

🔧 Backend Setup (AWS EC2)
1. Launch EC2 Instance
Choose Ubuntu (recommended)
Open ports:
22 (SSH)
80 (HTTP)
443 (HTTPS)
5000 or your app port
2. Connect to EC2
ssh -i your-key.pem ubuntu@your-ec2-ip
3. Install Dependencies
sudo apt update
sudo apt install python3-pip python3-venv nginx -y
4. Setup Project
git clone https://github.com/yourusername/rail-plot.git
cd rail-plot/backend

python3 -m venv venv
source venv/bin/activate

pip install -r requirements.txt
5. Environment Variables

Create .env file:

DB_HOST=your-db-host
DB_NAME=railplot
DB_USER=postgres
DB_PASSWORD=yourpassword
6. Run Backend
python main.py

Or with production server:

pip install gunicorn
gunicorn -w 4 -b 0.0.0.0:5000 main:app
🌐 Nginx Configuration (Optional but Recommended)
sudo nano /etc/nginx/sites-available/railplot
server {
    listen 80;
    server_name your-domain.com;

    location / {
        proxy_pass http://127.0.0.1:5000;
    }
}
sudo ln -s /etc/nginx/sites-available/railplot /etc/nginx/sites-enabled
sudo systemctl restart nginx
🗄️ Database Setup (PostgreSQL)
Install PostgreSQL
sudo apt install postgresql postgresql-contrib
Create Database
CREATE DATABASE railplot;

CREATE USER railuser WITH PASSWORD 'password';

ALTER ROLE railuser SET client_encoding TO 'utf8';
ALTER ROLE railuser SET default_transaction_isolation TO 'read committed';
ALTER ROLE railuser SET timezone TO 'UTC';

GRANT ALL PRIVILEGES ON DATABASE railplot TO railuser;
Run Schema
psql -U railuser -d railplot -f database/schema.sql
🎨 Frontend Setup (React)
1. Install Dependencies
cd frontend
npm install
2. Environment Config

Create .env:

REACT_APP_API_URL=http://your-ec2-ip

3. Build Project
npm run build
☁️ Deploy Frontend to AWS S3
1. Create S3 Bucket
Enable Static Website Hosting
Set permissions to public
2. Upload Build Files
aws s3 sync build/ s3://your-bucket-name
3. Enable Hosting
Index document: index.html

🔐 CORS Configuration

In backend (Flask example):
from flask_cors import CORS
CORS(app)

🚀 API Example
GET Rail Data
GET /api/rails
POST New Plot
POST /api/plot

🧪 Testing
Backend
pytest
Frontend
npm test

📦 Deployment Workflow
Push code to GitHub
Pull latest code on EC2
Restart backend server
Rebuild frontend
Sync to S3

🔒 Security Best Practices
Use HTTPS (AWS Certificate Manager)
Store secrets in environment variables
Restrict DB access (security groups)
Use IAM roles instead of keys

📈 Future Improvements
Dockerize the application
CI/CD with GitHub Actions
Add caching (Redis)
Use AWS RDS instead of local PostgreSQL
Implement authentication (JWT)

👨‍💻 Author
Pragya Kumari

Your Name
GitHub: https://github.com/yourusername
