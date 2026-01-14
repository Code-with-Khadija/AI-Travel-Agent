# 🧳 AI Travel Agent - Voice Powered Trip Planner

An intelligent, voice-enabled travel planning assistant built with N8N that automates the entire trip booking workflow—from conversation to personalized itinerary delivery via email.

## 📋 Overview

This project demonstrates an end-to-end AI travel agent that:
- Conducts natural voice conversations with users via Retell AI
- Extracts travel requirements (destination, dates, budget, preferences)
- Searches for flights and hotels in real-time
- Generates personalized HTML email itineraries using AI
- Automatically sends complete travel plans to users

## 🎯 Features

- **Voice Interaction**: Natural conversation flow powered by Retell AI integration
- **Intelligent Data Extraction**: Converts conversational inputs into structured travel data
- **Airport Code Resolution**: Automatically converts city names to airport codes
- **Date Validation**: Ensures travel dates are in the future
- **Real-Time Search**: 
  - Flight options via Google Flights (SerpAPI)
  - Hotel listings via Google Hotels (SerpAPI)
- **AI-Powered Email Generation**: Creates professional, personalized HTML email itineraries
- **Automated Delivery**: Sends complete travel plans directly to user's email

## 🏗️ Architecture

```
User Voice Input (Retell AI)
    ↓
Webhook Trigger
    ↓
Data Extraction & Validation
    ↓
Airport Codes & Date Conversion (OpenAI)
    ↓
Parallel API Calls
    ├── Hotels Search (SerpAPI)
    └── Flights Search (SerpAPI)
    ↓
Email Generation (AI Agent)
    ↓
Gmail Delivery
```

## 🛠️ Technologies Used

- **N8N**: Workflow automation platform
- **Retell AI**: Voice conversation interface
- **OpenAI GPT-4**: 
  - Airport code conversion
  - Date validation
  - Email content generation
- **SerpAPI**: 
  - Google Flights data
  - Google Hotels data
- **Gmail API**: Email delivery

## 📦 Prerequisites

- N8N instance (self-hosted or cloud)
- OpenAI API key
- SerpAPI account and API key
- Gmail account with OAuth2 configured
- Retell AI account (for voice interface)

## 🚀 Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/Code-wit-Khadija/AI-Travel-Agent.git
   cd travel-agent-n8n
   ```

2. **Import the workflow**
   - Open your N8N instance
   - Go to Workflows → Import from File
   - Select `AI-Travel-Agent-workflow.json`

3. **Configure credentials**
   
   Create the following credentials in N8N:

   - **OpenAI API**
     - Name: `OpenAI API`
     - API Key: Your OpenAI key

   - **SerpAPI**
     - Name: `SerpAPI account`
     - API Key: Your SerpAPI key

   - **Gmail OAuth2**
     - Name: `Gmail account`
     - Follow N8N's Gmail OAuth2 setup guide

4. **Set up the webhook**
   - Activate the workflow
   - Note the webhook URL generated
   - Configure this URL in your Retell AI agent settings

## ⚙️ Configuration

### Environment Variables

Create a `.env` file (not committed to git):

```env
OPENAI_API_KEY=your_openai_key
SERPAPI_KEY=your_serpapi_key
WEBHOOK_URL=your_webhook_url
```

### Workflow Customization

Key areas you might want to customize:

1. **Airport Codes Node**: Modify the prompt if you need different date formats
2. **Email Agent Node**: Customize the email template style/structure
3. **Search Parameters**: Adjust flight/hotel search criteria in HTTP Request nodes

## 📝 Usage

### Via Voice (Retell AI)

1. User calls the Retell AI number
2. AI agent asks for:
   - Origin city
   - Destination city
   - Departure date
   - Return date
   - Number of travelers
   - Budget
   - Special preferences/activities
   - Email address
3. System processes and sends itinerary

### Manual Testing

You can trigger the workflow manually by sending a POST request to the webhook:

```bash
curl -X POST https://your-n8n-instance/webhook/your-webhook-id \
  -H "Content-Type: application/json" \
  -d '{
    "args": {
      "origin": "New York",
      "destination": "Paris",
      "departure_date": "2025-06-01",
      "return_date": "2025-06-07",
      "travelers": "2",
      "budget": "3000 USD",
      "preferences": "Visit Eiffel Tower",
      "email": "user@example.com"
    }
  }'
```

## 🔧 Workflow Nodes Explained

| Node | Purpose |
|------|---------|
| **Webhook** | Receives data from Retell AI |
| **Respond to Webhook** | Sends immediate acknowledgment |
| **Edit Fields** | Extracts and structures travel data |
| **Airport codes and dates** | Converts cities to airport codes, validates dates |
| **Hotels** | Searches for hotel options |
| **Flights** | Searches for flight options |
| **Email Agent** | Generates personalized HTML email |
| **Send a message** | Delivers email via Gmail |

## 🎨 Email Template

The AI generates a professional HTML email including:
- Trip summary header
- All flight options with:
  - Airline names
  - Departure times
  - Duration
  - Prices
- Hotel recommendations with:
  - Property names and images
  - Rates per night
  - Nearby attractions
  - Amenities
- Personalized activity suggestions
- Professional sign-off

## 🔒 Security Notes

- Never commit credentials to the repository
- Use N8N's credential management system
- Enable webhook authentication in production
- Regularly rotate API keys
- Review email content before sending in production

## 🐛 Troubleshooting

**Webhook not receiving data:**
- Check webhook URL configuration in Retell AI
- Verify webhook is active in N8N

**API errors:**
- Confirm all credentials are properly configured
- Check API key quotas and limits

**Email not sending:**
- Verify Gmail OAuth2 permissions
- Check spam folder
- Review N8N execution logs

## 📈 Future Enhancements

- [ ] Add multi-currency support
- [ ] Include car rental options
- [ ] Add weather forecasts for destination
- [ ] Support for multi-city trips
- [ ] Integration with calendar apps
- [ ] User preference memory/profiles
- [ ] Real-time pricing updates
- [ ] Booking confirmation integration

## 🤝 Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👏 Acknowledgments

- Built with [N8N](https://n8n.io/)
- Voice powered by [Retell AI](https://retellai.com/)
- AI capabilities from [OpenAI](https://openai.com/)
- Search data from [SerpAPI](https://serpapi.com/)

## 📧 Contact

Your Name - [@yourtwitter](https://twitter.com/yourtwitter)

Project Link: [https://github.com/yourusername/travel-agent-n8n](https://github.com/yourusername/travel-agent-n8n)

---

⭐ If you find this project helpful, please consider giving it a star!
