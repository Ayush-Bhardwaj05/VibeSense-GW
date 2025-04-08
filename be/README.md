# Speech Emotion Recognition API

This project is a Speech Emotion Recognition system that uses machine learning models to detect emotions from audio and video inputs. It also provides a modern web application interface for users to interact with the system. The backend is built with FastAPI, and the frontend is developed using Next.js.

---

## Table of Contents

1. [Overview](#overview)
2. [Features](#features)
3. [Architecture](#architecture)
4. [Backend Setup](#backend-setup)
5. [Frontend Setup](#frontend-setup)
6. [API Documentation](#api-documentation)
7. [Components](#components)
8. [Usage](#usage)
9. [License](#license)

---

## Overview

The Speech Emotion Recognition API is designed to process audio and video inputs to detect emotions such as happiness, sadness, anger, and neutrality. It supports multiple endpoints for different use cases, including Indian accent-specific emotion detection, video-based emotion detection, and generative AI-based conversational analysis.

---

## Features

- **Emotion Detection**: Detect emotions from audio and video inputs.
- **Indian Accent Support**: Specialized model for Indian accents.
- **Generative AI Integration**: Analyze conversations and provide human-like responses.
- **Heatmap Visualization**: Generate emotion heatmaps based on user activity.
- **User Authentication**: Secure signup and login functionality.
- **Modern Web Interface**: Built with Next.js for a seamless user experience.

---

## Architecture

### Backend
- **Framework**: FastAPI
- **Database**: MongoDB (via Motor)
- **Machine Learning Models**: TensorFlow/Keras
- **Audio Processing**: Librosa, Pydub
- **Authentication**: JWT-based authentication

### Frontend
- **Framework**: Next.js
- **Styling**: Tailwind CSS
- **State Management**: React hooks and context API

---

## Backend Setup

### Prerequisites
- Python 3.9+
- MongoDB instance
- Virtual environment (optional but recommended)

### Installation

1. Clone the repository:
    ```sh
    git clone https://github.com/yourusername/emotion-detection-backend.git
    cd emotion-detection-backend
    ```

2. Create a virtual environment and activate it:
    ```sh
    python -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    ```

3. Install dependencies:
    ```sh
    pip install -r requirements.txt
    ```

4. Configure environment variables:
    - Create a `.env` file in the `backend/` directory.
    - Add the following variables:
      ```env
      DATABASE_URL=mongodb+srv://<username>:<password>@cluster0.mongodb.net/
      SECRET_KEY=your_secret_key
      ```

5. Run the application:
    ```sh
    uvicorn main:app --reload
    ```

6. Access the API at `http://127.0.0.1:8000`.

---

## Frontend Setup

### Prerequisites
- Node.js 16+
- npm or yarn

### Installation

1. Navigate to the frontend directory:
    ```sh
    cd fe
    ```

2. Install dependencies:
    ```sh
    npm install
    ```

3. Configure environment variables:
    - Create a `.env.local` file in the `fe/` directory.
    - Add the following variables:
      ```env
      NEXT_PUBLIC_API_BASE_URL=http://127.0.0.1:8000
      ```

4. Run the development server:
    ```sh
    npm run dev
    ```

5. Open your browser and navigate to `http://localhost:3000`.

---

## API Documentation

### Base URL

`http://127.0.0.1:8000`

### Endpoints

#### 1. `/convo/process-text`

**Method:** POST

**Description:** Processes a text input and returns a generative AI response.

**Request Body:**
```json
{
  "text": "Your input text here"
}
```

**Response:**
```json
{
  "response": "Generative AI response text"
}
```

#### 2. `/convo/process-audio`

**Method:** POST

**Description:** Uploads an audio file, processes it with generative AI, and returns the response.

**Form Data:**
- `file`: The audio file to be uploaded.
- `responses`: A string of previous responses separated by `|`.

**Response:**
```json
{
  "message": "File uploaded and processed",
  "file_path": "unique_filename.extension",
  "response": "Generative AI response text"
}
```

#### 3. `/convo/get-audio/{filename}`

**Method:** GET

**Description:** Retrieves the audio file by filename.

**Path Parameter:**
- `filename`: The name of the audio file to retrieve.

**Response:**
- Returns the audio file if found.
- If not found:
```json
{
  "error": "File not found"
}
```

#### 4. `/auth/signup`

**Method:** POST

**Description:** Registers a new user.

**Request Body:**
```json
{
  "username": "user123",
  "email": "user@example.com",
  "password": "password123"
}
```

**Response:**
```json
{
  "message": "User registered successfully"
}
```

#### 5. `/auth/login`

**Method:** POST

**Description:** Logs in a user and returns an access token.

**Request Body:**
```json
{
  "username": "user123",
  "password": "password123"
}
```

**Response:**
```json
{
  "access_token": "jwt_token",
  "token_type": "bearer"
}
```

#### 6. `/protected`

**Method:** GET

**Description:** A protected route that requires a valid token.

**Response:**
```json
{
  "message": "Welcome, {username}! This is a protected route."
}
```

#### 7. `/predict-indian`

**Method:** POST

**Description:** Uploads an audio file, processes it to predict emotion for Indian accent, and returns the emotion.

**Form Data:**
- `file`: The audio file to be uploaded.

**Response:**
```json
{
  "emotion": "predicted_emotion"
}
```

#### 8. `/predict-emotion/`

**Method:** POST

**Description:** Uploads a WAV audio file, processes it to predict emotion, and returns the emotion.

**Form Data:**
- `file`: The WAV audio file to be uploaded.

**Response:**
```json
{
  "emotion": "predicted_emotion"
}
```

---

## Components

### Backend
- FastAPI application for API endpoints.
- MongoDB database for storing user data and logs.
- TensorFlow/Keras models for emotion detection.

### Frontend
- Next.js application for user interaction.
- Tailwind CSS for styling.
- React hooks for state management.

---

## Usage

### Running the Application

#### Backend
```bash
uvicorn main:app --reload
```

#### Frontend
```bash
npm run dev
```

---

## License

This project is licensed under the MIT License.