
# FarmWise - Grow Smarter, Not Harder

**FarmWise** is a production-ready PWA (Progressive Web App) designed for farmers in India. It serves as a comprehensive "Super App" that combines hyper-local data with advanced crop analysis and real-time interaction capabilities.

## 🚀 Key Features

### 1. 🔴 FarmWise Live
A real-time, conversational experience.
*   **"Eyes on the Field"**: Streams live video from the farmer's camera. Farmers can point at crops and ask, "Is this leaf yellowing due to lack of water or pests?"
*   **Voice-First**: Hands-free interaction. Farmers speak naturally in their local language, and the app responds with a professional Indian accent.
*   **Pinch-to-Zoom & Camera Flip**: Optimized for field usage on mobile devices.

### 2. 🩺 Crop Doctor
*   **Instant Diagnosis**: Upload a high-res photo for deep analysis.
*   **Structured Reports**: Returns confidence scores, local disease names (e.g., in Marathi/Hindi), and chemical vs. organic treatment plans.

### 3. 🧠 Smart Advisor
*   **Deep Analysis Mode**: Reasons through complex scenarios (e.g., "It rained 2 hours after I sprayed pesticide, should I spray again?").
*   **Store Locator**: Finds real physical agri-input stores nearby.

### 4. 📊 Market & Weather Pulse
*   **Mandi Rates**: Real-time market prices for crops based on location.
*   **Hyper-local Weather**: 3-day forecasts with specific agricultural alerts (e.g., "Heatwave alert: irrigate immediately").

## 🛠️ Tech Stack & Architecture

*   **Frontend**: React 18, TypeScript, Tailwind CSS

## ⚡ Technical Implementation Highlights

### 🎥 Real-Time Video Streaming (FarmWise Live)
We implemented a custom WebSocket-based streaming architecture:
1.  **Video Capture**: We use an invisible HTML5 Canvas to capture frames from the device camera.
2.  **Compression**: Frames are downscaled to 320px width and compressed to JPEG (0.6 quality) to ensure performance on 4G rural networks.
3.  **Synchronization**: Images are sent alongside audio chunks.
4.  **Audio**: We implemented custom 16kHz raw PCM encoding/decoding.

### 🧩 Structured Data
For the Crop Doctor, we utilize structured data enforcement. This ensures that the output is always a clean JSON object containing `diseaseName`, `confidence`, and `treatment` arrays, preventing UI breakages.

### 🗣️ Linguistics & Persona
We enforce a specific persona:
*   **Voice**: Male, Authoritative yet friendly.
*   **Language Locking**: The app is strictly instructed to speak *only* in the user's selected language (e.g., Marathi), or if English is selected, to use a "Natural Indian Accent".

## 🔑 Setup & Installation

1.  **Clone the repository**.
2.  **Install dependencies**:
    ```bash
    npm install
    ```
3.  **Configure Environment**:
    *   Create a `.env` file in the root.
    *   Add your API key:
        ```env
        API_KEY=your_api_key_here
        ```
4.  **Run the app**:
    ```bash
    npm run dev
    ```
    *Note: To test the Camera/Microphone on mobile, you must serve the app over HTTPS or use `localhost`.*

## 📱 Demo Flow

**0:00 - 0:45: The "FarmWise Live" Experience**
*   *Action*: Open the app, click the pulsing "Live" microphone.
*   *Visual*: The camera opens (UI looks like a video call).
*   *User*: Points phone at a plant. Zooms in. "Hey, look at these spots. Is this dangerous?"
*   *Response (Voice)*: "I see small dark spots with yellow halos. That looks like Early Blight. Since you are in Pune and humidity is high, you should apply a copper-based fungicide immediately."

**0:45 - 1:30: Deep Diagnosis**
*   *Action*: Switch to "Camera" tab. Take a high-res photo.
*   *Visual*: "Analyzing..." animation.
*   *Result*: A structured card appears showing "Early Blight (लवकर करपा)" with 95% confidence and a step-by-step cure.

**1:30 - 2:15: Market & Commerce**
*   *Action*: Go to "Mandi". Show prices for "Onion" in "Nashik".
*   *Action*: Switch role to "Consumer". Add "Fresh Mangoes" to cart and Checkout.

**2:15 - 3:00: Multilingual Capability**
*   *Action*: Open Menu -> Change Language to **Marathi** or **Punjabi**.
*   *Result*: The entire UI instantly switches language context.

## ☁️ Deployment

*   **Vercel/Netlify**: Connect repo, set `API_KEY` in environment variables.
*   **Docker**:
    ```dockerfile
    FROM node:18-alpine
    WORKDIR /app
    COPY . .
    RUN npm install && npm run build
    CMD ["npx", "serve", "-s", "dist"]
    ```