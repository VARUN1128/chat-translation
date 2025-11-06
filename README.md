Lingo/README.md
# Lingo Chat App

A real-time chatting webapp built with Next.js (frontend) and Node.js with Socket.IO (backend).

## Features

- **Real-time Messaging**: Instant message delivery using Socket.IO
- **User Authentication**: Simple username-based login (no passwords or database)
- **Online Users**: See who's currently online in real-time
- **One-to-One Chat**: Private conversations between users
- **Typing Indicators**: See when someone is typing
- **Real-time Translation**: AI-powered translation using Sarvam-Translate model
- **Multi-language Support**: Support for 22+ Indian languages
- **Virtual Keyboard**: On-screen keyboard for regional language input
- **Modern UI**: Clean, WhatsApp-like interface built with TailwindCSS
- **Responsive Design**: Works on desktop and mobile devices

## Tech Stack

### Frontend
- **Next.js 14** - React framework
- **TailwindCSS** - Utility-first CSS framework
- **Socket.IO Client** - Real-time communication

### Backend
- **Node.js** - JavaScript runtime
- **Express.js** - Web framework
- **Socket.IO** - Real-time bidirectional communication
- **Supabase** - PostgreSQL database with real-time features
- **CORS** - Cross-origin resource sharing

### Translation & AI
- **Sarvam-Translate** - AI-powered translation model for Indian languages
- **Python 3** - Translation service backend
- **Transformers** - Hugging Face transformers library
- **PyTorch** - Deep learning framework

## Project Structure

```
lingo/
├── server.js              # Backend server (Node.js + Express + Socket.IO + Supabase)
├── package.json           # Dependencies and scripts
├── .env                   # Environment variables (Supabase credentials)
├── next.config.js         # Next.js configuration
├── tailwind.config.js     # TailwindCSS configuration
├── postcss.config.js      # PostCSS configuration
├── requirements.txt       # Python dependencies for translation service
├── sarvam_translate.py    # Python script for Sarvam-Translate model
├── translationService.js  # Node.js translation service wrapper
├── test_final_translation.js # Translation testing script
├── components/
│   └── VirtualKeyboard.js # Virtual keyboard component for regional languages
├── styles/
│   ├── globals.css        # Global styles and TailwindCSS imports
│   └── virtual-keyboard.css # Virtual keyboard specific styles
├── pages/
│   ├── _app.js           # Main app component with routing logic
│   ├── _document.js      # HTML document structure
│   ├── index.js          # Login page
│   ├── users.js          # Online users list page
│   └── chat/
│       └── [id].js       # Individual chat page
├── DATABASE.md           # Database schema documentation
├── AGENTS.md             # AI agents documentation
├── SARVAM_TRANSLATE_SETUP.md # Translation setup guide
└── README.md              # This file
```

## Getting Started

### Prerequisites

- Node.js (v16 or higher)
- npm or yarn
- Python 3.8 or higher (for translation service)
- Supabase account and project

### Installation

1. **Clone the repository**  
   ```bash
   git clone <repository-url>
   cd lingo
   ```

2. **Create and Activate a Virtual Environment**  
   Create a virtual environment for the Python translation service:
   ```bash
   python -m venv venv
   ```
   Activate the virtual environment:
   - On Linux/macOS:
     ```bash
     source venv/bin/activate
     ```
   - On Windows:
     ```bash
     venv\Scripts\activate
     ```

3. **Install Python Dependencies**  
   With the virtual environment activated, install the required Python packages:
   ```bash
   pip install -r requirements.txt
   ```

4. **Test the Translation Handler**  
   Test the Sarvam-Translate handler using the following command:
   ```bash
   python sarvam_translate.py --text "സുഗ്  ആൻ " --target-language "hi-IN" --source-language "ml-IN"
   ```
   Replace the sample text and language codes as needed.

5. **Install Node.js Dependencies**  
   In a separate terminal (or after testing Python), install the Node.js packages:
   ```bash
   npm install
   ```

6. **Set up Supabase**  
   - Create a new project at [supabase.com](https://supabase.com)
   - Copy your project URL and service role key
   - Create a `.env` file with your credentials:
     ```bash
     NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
     SUPABASE_SERVICE_ROLE_KEY=your_service_role_key
     PORT=5000
     ```

7. **Set up the Database**  
   - Go to your Supabase dashboard → SQL Editor
   - Run the SQL commands from `DATABASE.md` to create the required tables

8. **Configure Translation Service (Optional)**  
   - By default, the app uses mock translations.
   - To enable the real Sarvam-Translate model, set `usePythonScript = true` in `translationService.js`
   - Refer to `SARVAM_TRANSLATE_SETUP.md` for detailed setup instructions

9. **Start the Development Servers**  
   In the project root, run:
   ```bash
   npm run dev
   ```
   This command will start both:
   - Backend server on `http://localhost:5000`
   - Frontend (Next.js) on `http://localhost:3000`

### Alternative: Run Servers Separately

- **Backend only**:  
  ```bash
  npm run server
  ```
- **Frontend only**:  
  ```bash
  npm run client
  ```

## Usage

1. **Open your browser** and navigate to `http://localhost:3000`.

2. **Login**: Enter a username (minimum 3 characters) and click "Start Chatting".

3. **View Online Users**: You'll be redirected to the users page showing all online users.

4. **Start Chatting**: Click on any user to start a private conversation.

5. **Use Translation**: Select source and target languages to enable real-time translation.

6. **Virtual Keyboard**: Use the on-screen keyboard for typing in regional languages.

7. **Test Multi-User**: Open the app in multiple browser tabs with different usernames to test real-time messaging.

## API Endpoints

### Backend Server (`http://localhost:5000`)

- `GET /health` - Server health check
- WebSocket connection for real-time communication

### Socket.IO Events

#### Client to Server
- `user_login` - User login with username
- `private_message` - Send private message
- `typing_start` - Start typing indicator
- `typing_stop` - Stop typing indicator
- `translate_message` - Request message translation
- `set_language_preference` - Set user's language preference

#### Server to Client
- `login_success` - Login successful
- `login_error` - Login failed
- `users_list_update` - Updated list of online users
- `user_joined` - New user joined
- `user_left` - User left
- `private_message` - Receive private message
- `message_sent` - Message sent confirmation
- `typing_start` - User started typing
- `typing_stop` - User stopped typing
- `translation_result` - Translation response
- `supported_languages` - List of supported languages

## Features in Detail

### Real-time Communication
- Messages are delivered instantly using Socket.IO.
- Message persistence with Supabase PostgreSQL database.
- Typing indicators show when someone is composing a message.
- Chat history is automatically saved and retrieved.

### Translation Features
- AI-powered translation using the Sarvam-Translate model.
- Support for 22+ Indian languages including Hindi, Tamil, Malayalam, Bengali, etc.
- Real-time translation of messages during chat.
- Fallback to mock translation when the AI model is not available.
- Language preference settings per user.

### User Management
- Usernames must be unique across all connected users.
- Automatic disconnection handling when users close tabs.
- Real-time updates when users join/leave.

### UI/UX Features
- Clean, modern interface inspired by WhatsApp Web.
- Responsive design for mobile and desktop.
- Smooth animations and transitions.
- Loading states and error handling.#
