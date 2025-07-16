# RAG-Based-Career-Counseling-System-for-Indian-Students
This repository contains a Python application that provides an AI-powered career counseling service for Indian students after 12th grade. Using Twilio for voice communication and OpenAI's Realtime API for conversational AI, it guides students in choosing educational and career paths in Science, Arts, and Commerce streams.
Features
Interactive Voice Interface: Handles incoming calls via Twilio, allowing students to discuss career options in real-time.
AI-Powered Guidance: Uses OpenAI's GPT-4o Realtime API to provide personalized advice based on a knowledge base of courses, entrance exams, and career paths.
Stream-Specific Recommendations: Offers tailored suggestions for Science (e.g., B.Tech, MBBS), Arts (e.g., B.A., BJMC), and Commerce (e.g., B.Com, CA) streams.
WebSocket Integration: Manages real-time audio streams between Twilio and OpenAI for seamless voice interactions.
FastAPI Backend: Serves the application with endpoints for incoming calls and WebSocket connections.
Requirements
Python 3.10+
Libraries: fastapi, websockets, twilio, python-dotenv, uvicorn
Environment Variables:
OPENAI_API_KEY: Your OpenAI API key for accessing the Realtime API.
PORT: Server port (default: 5050).
Twilio Account: For handling incoming calls and media streams.
Ngrok or similar: For exposing the local server to the internet for Twilio WebSocket connections.
Installation
Clone the repository:
git clone https://github.com/<your-username>/ai-career-counselor.git
cd ai-career-counselor
Install dependencies:
pip install -r requirements.txt
Create a .env file in the root directory and add your OpenAI API key:
OPENAI_API_KEY=your_openai_api_key_here
PORT=5050
Run the application:
python app.py
Expose the local server using Ngrok (required for Twilio WebSocket):ngrok http 5050
Configure Twilio to route incoming calls to https://<ngrok-url>/incoming-call.
Usage
Start a Call: Dial the Twilio phone number configured for your account. The AI will greet the caller and prompt them to share their stream (Science, Arts, Commerce) and interests.
Interact: Speak naturally to discuss career goals. The AI uses a predefined knowledge base to suggest courses, entrance exams, institutes, and career paths.
Example Interaction:
User: "I’m from the Science stream and interested in engineering."
AI: "Great choice! For PCM, you can pursue B.Tech in Computer Science or AI. Entrance exams like JEE Main or BITSAT are key. Top institutes include IITs and NITs, with starting salaries of ₹6–20 LPA."
Code Structure
app.py: Main application file with FastAPI endpoints and WebSocket logic for handling Twilio and OpenAI communication.
Key Components:
/incoming-call: Handles incoming Twilio calls and returns TwiML to connect to a WebSocket stream.
/media-stream: WebSocket endpoint for real-time audio exchange between Twilio and OpenAI.
initialize_session: Configures the OpenAI Realtime API session with system prompts and audio settings.
receive_from_twilio & send_to_twilio: Manage audio data flow and handle interruptions (e.g., when the user starts speaking).
Notes
Twilio Setup: Ensure your Twilio account is configured with a phone number and webhook pointing to /incoming-call.
OpenAI API: The application uses the gpt-4o-realtime-preview-2024-10-01 model. Ensure your API key has access to this model.
Ngrok: Required for testing locally, as Twilio needs a public URL for WebSocket connections.
Audio Format: Uses g711_ulaw for input/output audio, compatible with Twilio’s media streams.
Error Handling: The application logs events like errors, speech detection, and response completion for debugging.
Troubleshooting
Missing API Key: Ensure OPENAI_API_KEY is set in the .env file.
WebSocket Errors: Verify that Ngrok is running and the WebSocket URL (wss://<ngrok-url>/media-stream) is correctly configured in Twilio.
Audio Issues: Check that the audio format (g711_ulaw) matches Twilio’s requirements.
Dependencies: Run pip install -r requirements.txt to ensure all libraries are installed.
License
This project is licensed under the MIT License. See the LICENSE file for details.
Acknowledgments
Twilio for voice communication APIs.
OpenAI for the Realtime API enabling conversational AI.
FastAPI for the web server framework.
