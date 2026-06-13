# AI-Based Online Exam Proctoring System

## Overview

The **AI-Based Online Exam Proctoring System** is a cutting-edge proctoring solution that ensures the integrity of online examinations. It employs advanced artificial intelligence techniques, including face detection, object detection, gaze tracking, real-time browser activity monitoring, and audio analysis, to monitor and prevent fraudulent activities during exams. This system helps maintain fairness and credibility in remote examinations by providing automated invigilation and detailed reports.

## Features
- **Face Detection**: Identifies and verifies the student's face to ensure the registered candidate is taking the exam.
- **Object Detection**: Detects unauthorized objects such as smartphones, books, or other cheating materials.
- **Gaze Detection**: Monitors the candidate's eye movements to detect suspicious behavior, such as looking away from the screen frequently.
- **Real-Time Browser Activity Monitoring**: Tracks tab switches and alerts when the candidate navigates away from the exam interface.
- **Audio Analysis**: Captures and analyzes external sounds through an external microphone to detect conversations or background noises.
- **Comprehensive Reports**: Generates detailed reports on suspicious activities and rule violations for invigilators to review.
- **User Authentication**: Face matching and email/password authentication required only during student registration and login.
- **Intuitive User Interface**: A well-designed homepage with a modern layout, login and register buttons, and important notices.
- **No Offline Mode Support**: The system explicitly notifies users that offline mode is not supported to prevent exam manipulation.

## Tech Stack
- **Backend**: Django 5.1.5 (Python-based web framework)
- **Database**: PostgreSQL (for efficient data storage and retrieval)
- **Frontend**: HTML, CSS, JavaScript (with UI/UX inspired by provided images)
- **AI Models**: OpenCV, MediaPipe (for face and object detection), custom ML models
- **Authentication**: Django authentication system with face-matching capabilities
- **Deployment**: Hosted on a cloud platform with scalability in mind

### 📽️ Demo Video

Watch the demo here: [https://youtu.be/O8kfFmwkfOU](https://youtu.be/O8kfFmwkfOU)

## Installation & Setup

### Prerequisites
- Python 3.8 or higher
- PostgreSQL database
- Webcam and microphone access (for AI monitoring)
- YOLO model weights file (yolo11s.pt)

### Environment Setup

1. **Clone the Repository**
   ```bash
   git clone https://github.com/HelpRam/An-Inbrowser-Proctoring-System.git
   cd futurproctor
   ```

2. **Create and Activate Virtual Environment**
   ```bash
   python -m venv venv
   # On Windows:
   venv\Scripts\activate
   # On Linux/Mac:
   source venv/bin/activate
   ```

3. **Install Dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Environment Configuration**
   Create a `.env` file in the project root:
   ```bash
   cp env.example .env
   ```

   Edit the `.env` file with your configuration:
   ```env
   # Django Configuration
   SECRET_KEY=your-super-secret-key-here-make-it-long-and-random
   DEBUG=False
   ALLOWED_HOSTS=localhost,127.0.0.1,yourdomain.com

   # Database Configuration
   DB_NAME=exam_proctor_db
   DB_USER=your_db_user
   DB_PASSWORD=your_db_password
   DB_HOST=localhost
   DB_PORT=5432

   # Optional: YOLO Model Path
   YOLO_MODEL_PATH=yolo11s.pt
   ```

5. **Database Setup**
   - Ensure PostgreSQL is running
   - Create a database named `exam_proctor_db`
   - Update database credentials in `.env` file

6. **Run Migrations**
   ```bash
   python manage.py migrate
   ```

7. **Create Superuser (Admin)**
   ```bash
   python manage.py createsuperuser
   ```

8. **Start the Development Server**
   ```bash
   python manage.py runserver
   ```
   The application will be accessible at `http://127.0.0.1:8000/`.

## Production Deployment

### Security Considerations
- Set `DEBUG=False` in production
- Use a strong `SECRET_KEY`
- Configure `ALLOWED_HOSTS` properly
- Use HTTPS in production
- Set up proper logging
- Use environment variables for sensitive data
- Regularly update dependencies

### Environment Variables
```env
# Production Settings
DEBUG=False
SECRET_KEY=your-production-secret-key
ALLOWED_HOSTS=yourdomain.com,www.yourdomain.com

# Database (use production database)
DB_NAME=prod_exam_db
DB_USER=prod_user
DB_PASSWORD=secure_password
DB_HOST=your-db-host
DB_PORT=5432

# Optional settings
AUDIO_THRESHOLD=1500
YOLO_MODEL_PATH=/path/to/production/model.pt
```

### Using Docker (Recommended for Production)
```dockerfile
# Dockerfile example
FROM python:3.11-slim

WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .
RUN python manage.py collectstatic --noinput

CMD ["gunicorn", "futurproctor.wsgi:application", "--bind", "0.0.0.0:8000"]
```

## Usage

### For Students
1. **Registration**: Create an account with face recognition
2. **Login**: Authenticate using email/password and face verification
3. **Take Exam**: Follow on-screen instructions during the exam
4. **Real-time Monitoring**: AI systems monitor behavior throughout

### For Administrators
1. **Access Admin Panel**: Login to `/admin/` with superuser credentials
2. **View Reports**: Monitor cheating events and student performance
3. **Generate Reports**: Export detailed proctoring reports

## API Endpoints

- `GET /` - Home page
- `GET /registration/` - Student registration
- `POST /login/` - Student login with face verification
- `GET /dashboard/` - Student dashboard
- `GET /exam/` - Start exam session
- `POST /submit_exam/` - Submit completed exam
- `GET /admin_dashboard/` - Admin dashboard (staff only)

## Troubleshooting

### Common Issues

1. **Camera/Microphone Access**
   - Ensure browser permissions are granted
   - Check hardware connections

2. **Model Loading Errors**
   - Verify YOLO model file exists
   - Check file permissions

3. **Database Connection**
   - Verify PostgreSQL is running
   - Check database credentials in `.env`

4. **Audio Detection Issues**
   - Adjust `AUDIO_THRESHOLD` in environment variables
   - Test microphone input levels

### Logs
Check application logs in `futurproctor/logs/futurproctor.log` for detailed error information.

## Development

### Running Tests
```bash
python manage.py test
```

### Code Quality
- Run linting: `flake8 .`
- Format code: `black .`
- Type checking: `mypy .`

## Future Enhancements
- **Live Human Proctoring Integration**
- **Voice Command Detection for Additional Security**
- **Mobile App for Enhanced Accessibility**
- **Multi-Exam Support with Custom Rules Configuration**
- **Real-time Video Streaming to Admin Dashboard**

## Security Notes
- Face recognition data is stored securely
- All communications should use HTTPS in production
- Regular security audits recommended
- Monitor for potential bypass attempts

## Contributors
- **Ramdular Yadav** (Lead Developer)

## License
This project is licensed under the MIT License.

## Contact
For any inquiries or contributions, feel free to reach out to:
- **Email**: rammey115@gmail.com
- **Phone**: 9819936338

