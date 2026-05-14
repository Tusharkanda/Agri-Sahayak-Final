# Agri-Sahayak: Bridging the Digital Divide with a Voice-First AI Companion

Agri-Sahayak is a hyper-local, multi-modal AI assistant designed to bridge the critical information gap for Indian farmers, empowering them with accessible, proactive, and trustworthy advice.

## 🚀 Key Features in Agri-Sahayak

- **Multi-Modal Access**: A modern React web dashboard for smartphone users and a fully-featured IVR Voice Call system (via Twilio) for any farmer with a basic mobile phone.
- **Hyper-Local Intelligence**: Delivers state-specific advice using a Retrieval-Augmented Generation (RAG) model on curated knowledge bases.
- **Multilingual Support**: Fully functional in both English and Hindi, including the voice assistant.
- **Proactive SMS Alerts**: Automatically sends farmers personalized SMS warnings about severe weather or pest outbreaks in their district.
- **Visual Diagnosis**: Allows farmers to upload a photo of a diseased crop to get an instant AI-powered diagnosis.
- **Interactive Dashboard**: With widgets for Weather, Market Prices, and a Crop Activity Calendar.
- **Holistic Knowledge**: Covers both Crop Management and Livestock & Dairy.

## 🛠️ Technology Stack

- **Frontend**: React, Chakra UI, Tailwind CSS
- **Backend**: Python, FastAPI
- **AI & Data**: LangChain, FAISS, Google Generative AI (LLM & Vision)
- **Platforms & APIs**: Twilio (Voice & SMS), OpenWeatherMap, data.gov.in
- **Database**: SQLite

## ⚙️ Local Setup and Installation

### Prerequisites

- Git
- Python 3.9+
- Node.js and npm

### 1. Clone the Repository

```bash
git clone <your-repository-url>
cd <repository-name>
```

### 2. Backend Setup

```bash
# Create and activate a virtual environment
python -m venv venv

# On Windows
venv\Scripts\activate

# On macOS/Linux
source venv/bin/activate

# Install Python dependencies
pip install -r requirements.txt
```

### 3. Frontend Setup

```bash
# Navigate to the frontend directory
cd frontend/agri-sahayak-project

# Install npm dependencies
npm install
```

### 4. Environment Variables

Create a file named `.env` in the project's root directory and add the following keys. You will get these from the respective service dashboards.

```env
GOOGLE_API_KEY="your_google_ai_api_key"
TWILIO_ACCOUNT_SID="your_twilio_account_sid"
TWILIO_AUTH_TOKEN="your_twilio_auth_token"
TWILIO_PHONE_NUMBER="your_twilio_phone_number"
OPENWEATHER_API_KEY="your_openweathermap_api_key"
DATA_GOV_API_KEY="your_data_gov_api_key"
```

### 5. Data Ingestion (You can skip this step as we have already made faiss_indexes per state and saved them in backend/faiss_indexes and then pushed them to github)

**Note**: We have already created and included pre-built FAISS indexes in the `backend/faiss_indexes/` directory for all 4 states (Karnataka, Maharashtra, Punjab, and others). These indexes are ready to use out of the box, so you can skip this step unless you want to create your own custom knowledge base.

**Optional - Only if you want to create custom indexes:**

1. Create an `agri_knowledge_base/` directory in the project root
2. Place your curated PDF documents into state-specific subfolders within the `agri_knowledge_base/` directory:
   ```
   agri_knowledge_base/
   ├── karnataka/
   │   ├── crop_guide_karnataka.pdf
   │   └── livestock_karnataka.pdf
   ├── maharashtra/
   │   ├── farming_practices_mh.pdf
   │   └── weather_guide_mh.pdf
   └── punjab/
       ├── wheat_cultivation_pb.pdf
       └── dairy_management_pb.pdf
   ```
3. Run the ingestion script from the root directory to build the knowledge bases:
   ```bash
   python ingest_agri_data.py
   ```

### 6. Running the Application

**Start the Backend Server** (from the root directory):
```bash
uvicorn backend.main:app --reload
```

**Start the Frontend Server** (from the frontend/agri-sahayak-project directory):
```bash
npm start
```

The application will be available at `http://localhost:3000`.

## 📱 Features Overview

### Web Dashboard
- **User Authentication**: Secure login/signup with profile management
- **Multi-language Support**: Seamless switching between English and Hindi
- **Voice Recognition**: Built-in speech-to-text for hands-free interaction
- **Image Analysis**: Upload crop photos for AI-powered disease diagnosis
- **Market Price Comparison**: Real-time price data from multiple mandis
- **Weather Integration**: Location-based weather forecasts and alerts

### Voice System (IVR)
- **Twilio Integration**: Call-based interaction for farmers without smartphones
- **Hindi Voice Support**: Natural language processing in Hindi
- **SMS Notifications**: Automated alerts for weather and market updates

### AI Capabilities
- **RAG-based Responses**: Context-aware answers using state-specific agricultural data
- **Crop Disease Detection**: Computer vision for plant health assessment
- **Market Intelligence**: Price comparison across nearby mandis
- **Weather Alerts**: Proactive notifications for severe weather conditions

## 🗂️ Project Structure

```
agri-sahayak/
├── backend/
│   ├── faiss_indexes/          # State-specific FAISS vector stores
│   ├── database.py             # SQLite database operations
│   ├── main.py                 # FastAPI application entry point
│   ├── routes.py               # API endpoints and business logic
│   └── voice.py                # Twilio voice/SMS integration
├── frontend/
│   └── agri-sahayak-project/   # React application
│       ├── public/
│       ├── src/
│       └── package.json
├── agri_knowledge_base/        # PDF documents organized by state
├── ingest_agri_data.py         # Script to build FAISS indexes
├── requirements.txt            # Python dependencies
└── README.md
```

## 🔧 API Endpoints

### Authentication
- `POST /create_profile` - User registration
- `POST /login` - User authentication
- `POST /logout` - User logout

### Conversations
- `POST /conversations/start` - Start new conversation
- `POST /ask` - Ask questions to AI assistant
- `POST /analyze_image` - Upload and analyze crop images

### Voice & SMS
- `POST /voice/incoming` - Handle incoming voice calls
- `POST /voice/sms` - Send SMS notifications

### Health Checks
- `GET /health/index/{user_id}` - Check FAISS index status

## 🌐 Deployment

The application is designed to be deployed on cloud platforms with the following considerations:

1. **Backend**: Deploy FastAPI app using services like Railway, Heroku, or AWS
2. **Frontend**: Deploy React app using Netlify, Vercel, or similar
3. **Environment Variables**: Configure all API keys in production environment
4. **FAISS Indexes**: Ensure knowledge base files are properly uploaded and indexed

## 🔮 Future Work

Our vision is to evolve Agri-Sahayak from a trusted advisor into a predictive co-pilot and a full-stack agricultural ecosystem, integrating the entire supply chain from seed to sale.

**Planned Features:**
- **IoT Integration**: Connect with farm sensors for real-time monitoring
- **Marketplace Integration**: Direct connection to buyers and sellers
- **Financial Services**: Integration with agricultural loans and insurance
- **Predictive Analytics**: AI-powered crop yield and disease predictions
- **Community Features**: Farmer-to-farmer knowledge sharing platform

## 👥 Team

- **Sachin Choudhary**
- **Priyanshu Maniyar**
- **Tushar Kanda**

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Google Generative AI for powering our language models
- Twilio for voice and SMS capabilities
- Government of India's data.gov.in for market price data
- The farming community for their invaluable feedback and support

---

**Built with ❤️ for Indian Farmers**
