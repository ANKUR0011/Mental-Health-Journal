# README.md

## Mental Health Journal with Sentiment Analysis

A comprehensive web application for tracking daily mood and mental well-being through journal entries with automatic sentiment analysis, mood visualization, and personalized recommendations.

![Django](https://img.shields.io/dge/Dge/Python-3.11






## 🎯 Features

- **User Authentication**: Secure registration/login with token-based authentication
- **Journal Management**: Create, read, update, and delete daily journal entries
- **Automated Sentiment Analysis**: Real-time mood detection using VADER and TextBlob
- **Mood Analytics**: Visual trends, statistics, and pattern recognition
- **Personalized Recommendations**: AI-driven suggestions based on mood patterns
- **Background Processing**: Asynchronous tasks for heavy computations
- **Data Export**: Export journal data in JSON/CSV formats
- **Privacy Controls**: Secure, private entries with user-defined privacy levels

## 🛠️ Tech Stack

- **Backend**: Django 5.0.8, Django REST Framework
- **Database**: SQLite (development), MySQL (production)
- **Task Queue**: Celery with Redis broker
- **NLP**: VADER Sentiment, TextBlob, Transformers
- **Authentication**: Token-based authentication
- **API**: RESTful API with comprehensive endpoints
- **Deployment**: Docker, Docker Compose

## 📋 Prerequisites

Before running this project, ensure you have:

- Python 3.8+ installed
- Redis server running
- MySQL (for production) or SQLite (for development)
- Git (optional but recommended)

### Installation Steps

1. **Clone the repository**
```bash
git clone <repository-url>
cd mh_journal_django
```

2. **Create virtual environment**
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Install dependencies**
```bash
pip install -r requirements.txt
```

4. **Environment setup**
```bash
cp .env.example .env
# Edit .env file with your configuration
```

5. **Database migration**
```bash
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser
```

6. **Start services**
```bash
# Terminal 1: Start Redis
redis-server

# Terminal 2: Start Celery worker
celery -A mh_journal worker --loglevel=info

# Terminal 3: Start Celery beat (optional - for scheduled tasks)
celery -A mh_journal beat --loglevel=info

# Terminal 4: Start Django server
python manage.py runserver
```

## 🚀 Quick Start with Docker

```bash
# Clone and navigate to project
git clone <repository-url>
cd mh_journal_django

# Create environment file
cp .env.example .env

# Start all services
docker-compose up --build

# Run migrations (in separate terminal)
docker-compose exec web python manage.py migrate
docker-compose exec web python manage.py createsuperuser
```

Visit `http://localhost:8000/api/` to access the API.

## 📚 API Documentation

### Authentication Endpoints
- `POST /api/auth/register/` - User registration
- `POST /api/auth/login/` - User login
- `POST /api/auth/logout/` - User logout
- `GET /api/auth/profile/` - Get user profile

### Journal Endpoints
- `GET /api/journal/entries/` - List journal entries
- `POST /api/journal/entries/` - Create new entry
- `GET /api/journal/entries/{id}/` - Get specific entry
- `PUT /api/journal/entries/{id}/` - Update entry
- `DELETE /api/journal/entries/{id}/` - Delete entry
- `POST /api/journal/entries/{id}/reanalyze_sentiment/` - Re-analyze sentiment

### Analytics Endpoints
- `GET /api/analytics/mood-trends/` - Get mood trends
- `GET /api/analytics/statistics/` - Comprehensive mood statistics
- `GET /api/analytics/recommendations/` - Get personalized recommendations
- `GET /api/analytics/pattern/` - User mood patterns
- `POST /api/analytics/export/` - Export user data

## 🏗️ Project Structure

```
mh_journal_django/
├── mh_journal/           # Django project settings
│   ├── settings.py       # Main configuration
│   ├── urls.py          # URL routing
│   └── celery.py        # Celery configuration
├── users/               # User management app
│   ├── models.py        # User models
│   ├── serializers.py   # API serializers
│   └── views.py         # API views
├── journal/             # Journal management app
│   ├── models.py        # Journal and sentiment models
│   ├── serializers.py   # Journal serializers
│   └── views.py         # Journal API views
├── analytics/           # Analytics and recommendations
│   ├── models.py        # Analytics models
│   ├── tasks.py         # Celery background tasks
│   └── views.py         # Analytics API views
├── nlp_service/         # NLP processing
│   └── sentiment.py     # Sentiment analysis logic
├── requirements.txt     # Python dependencies
└── docker-compose.yml   # Docker services
```

## 🔧 Configuration

### Environment Variables

Create a `.env` file with the following variables:

```env
DEBUG=True
SECRET_KEY=your-secret-key-here
DATABASE_NAME=mh_journal
DATABASE_USER=your-db-user
DATABASE_PASSWORD=your-db-password
DATABASE_HOST=localhost
DATABASE_PORT=3306
REDIS_URL=redis://localhost:6379/0
CELERY_BROKER_URL=redis://localhost:6379/0
CELERY_RESULT_BACKEND=redis://localhost:6379/0
```

## 🔒 Security & Privacy

- All journal entries are private by default
- Token-based authentication for API access
- Data encryption at rest (configurable)
- Privacy controls for users
- No data selling or sharing policy
- GDPR compliance considerations built-in

## ⚠️ Important Disclaimer

This application provides non-clinical mood analysis for self-awareness and personal tracking only. **It is not a substitute for professional mental health care.** If you are experiencing a mental health crisis, please contact your local emergency services or a mental health crisis hotline immediately.

## 🧪 Testing

```bash
# Run all tests
python manage.py test

# Run specific app tests
python manage.py test users
python manage.py test journal
python manage.py test analytics

# Run with coverage
coverage run --source='.' manage.py test
coverage report
```

## 🚀 Deployment

### Production Setup

1. Set `DEBUG=False` in environment variables
2. Configure production database (MySQL recommended)
3. Set up proper Redis instance
4. Configure static file serving
5. Use production WSGI server (Gunicorn)
6. Set up reverse proxy (Nginx)
7. Configure SSL certificates
8. Set up monitoring and logging

### Docker Production

```bash
# Build and run in production mode
docker-compose -f docker-compose.prod.yml up --build
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-feature`)
3. Commit your changes (`git commit -am 'Add new feature'`)
4. Push to the branch (`git push origin feature/new-feature`)
5. Create a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

- Create an issue on GitHub for bugs or feature requests
- Check existing documentation and issues before creating new ones
- For security issues, please email security@yourproject.com

## 🙏 Acknowledgments

- [Django](https://djangoproject.com/) - Web framework
- [Django REST Framework](https://www.django-rest-framework.org/) - API framework
- [VADER Sentiment](https://github.com/cjhutto/vaderSentiment) - Sentiment analysis
- [Celery](https://celeryproject.org/) - Distributed task queue
- [Redis](https://redis.io/) - In-memory data store

## 📈 Roadmap

- [ ] React/Vue.js frontend
- [ ] Mobile app (React Native/Flutter)
- [ ] Advanced ML models for sentiment analysis
- [ ] Social features (anonymous mood sharing)
- [ ] Integration with wearables
- [ ] Multi-language support
- [ ] Advanced data visualization
- [ ] Therapist dashboard (optional feature)

***

**Made with ❤️ for mental health awareness and self-care**

