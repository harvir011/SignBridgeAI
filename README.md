<div align="center">

<img src="assets/signbridge-banner.png" alt="SignBridge AI — Breaking Communication Barriers with Real-Time Gesture Recognition" width="100%">

SignBridge AI 🤟

Breaking communication barriers with real-time gesture recognition


Turn hand gestures into text and speech — right in your browser.
<p>
  <img src="https://img.shields.io/badge/Computer%20Vision-MediaPipe-0B9E8A?style=for-the-badge&logo=googlechrome&logoColor=white" alt="MediaPipe">
  <img src="https://img.shields.io/badge/AI%2FML-TensorFlow.js-FF8F00?style=for-the-badge&logo=tensorflow&logoColor=white" alt="TensorFlow.js">
  <img src="https://img.shields.io/badge/Frontend-Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white" alt="Vite">
  <img src="https://img.shields.io/badge/Accessibility-First-16A34A?style=for-the-badge&logo=accessibility&logoColor=white" alt="Accessibility">
</p>

<p>
  <a href="#-features">Features</a> ·
  <a href="#-how-it-works">How it works</a> ·
  <a href="#-get-started">Get started</a> ·
  <a href="#-custom-model-training">Model training</a> ·
  <a href="#-limitations-and-responsible-use">Limitations</a>
</p>

</div>

🌟 About the project
SignBridge AI is a browser-based hand-gesture recognition prototype built to explore how computer vision and machine learning can support more accessible communication. It uses MediaPipe to track hand landmarks, recognizes a small set of static hand poses, maps them to demo text labels, and can speak the resulting message using the browser's Web Speech API.
The app also includes an AI Training Lab for collecting labeled landmark samples and exporting them for experimentation with a custom classifier.

Project scope: SignBridge AI is a limited-vocabulary static-pose prototype—not a complete sign-language translator. Its demo labels are illustrative and are not validated translations of ASL, Indian Sign Language, or any other sign language.

✨ Features
<table>
  <tr>
    <td width="50%">
      <h3>🖐️ Real-time hand tracking</h3>
      Detects and visualizes the 21 hand landmarks through MediaPipe.
    </td>
    <td width="50%">
      <h3>🧠 Gesture recognition</h3>
      Recognizes seven built-in static poses, with support for an optional custom TensorFlow.js model.
    </td>
  </tr>
  <tr>
    <td>
      <h3>💬 Gesture-to-text</h3>
      Maps recognized poses to demo labels and lets users edit the message.
    </td>
    <td>
      <h3>🔊 Text-to-speech</h3>
      Speaks the message using the browser's Web Speech API.
    </td>
  </tr>
  <tr>
    <td>
      <h3>🧪 AI Training Lab</h3>
      Collects labeled landmark samples in the browser for model experiments.
    </td>
    <td>
      <h3>📦 Data export</h3>
      Exports collected samples as CSV/JSON for analysis and training.
    </td>
  </tr>
  <tr>
    <td>
      <h3>📈 Performance dashboard</h3>
      Shows tracking and inference timing, plus FPS information.
    </td>
    <td>
      <h3>🔐 Local-first processing</h3>
      Camera frames are processed in the browser by default and are not uploaded to a server by the app.
    </td>
  </tr>
</table>

🖐️ Built-in demo gestures


Static pose	Example output

Open Palm	HELLO
Closed Fist	STOP
Pointing Up	HELP
Thumb Up	YES
Thumb Down	NO
Victory (V)	PEACE
I Love You	I LOVE YOU


These are prototype mappings, not universal meanings. Sign languages vary by community and language, and many signs rely on motion, facial expression, body posture, and context.



## System Architecture

SignBridge AI follows a **local-first, browser-based Edge AI architecture** that transforms webcam hand gestures into text and speech. It combines real-time hand tracking, landmark-based feature extraction, gesture classification, and an interactive communication interface.

### Architecture Overview

```mermaid
flowchart TB
    A(["📷 Webcam Input"]) --> B["Video Frame Capture"]
    B --> C["MediaPipe Tasks Vision<br/>Hand & Gesture Recognition"]

    C --> D["21 Hand Landmarks<br/>3D Coordinates"]
    C --> E["Pretrained Gesture Recognition<br/>7 Supported Static Poses"]

    D --> F["Landmark Normalization<br/>63 Numerical Features"]
    F --> G["Optional Custom Classifier<br/>TensorFlow.js MLP"]

    E --> H["Gesture Prediction"]
    G --> H

    H --> I["Confidence Threshold<br/>& Stability Filtering"]
    I --> J["Gesture-to-Label Mapping"]
    J --> K["Editable Text Output"]
    K --> L["Web Speech API<br/>Text-to-Speech"]

    F -.-> M[("Local Sample Storage")]
    M -.-> N["JSON / CSV Export"]
    N -.-> O["Python Training Pipeline"]
    O -.-> P["Evaluation Reports<br/>& Trained Model"]
    P -.-> G

    style A fill:#172554,stroke:#60A5FA,color:#FFFFFF
    style C fill:#312E81,stroke:#A5B4FC,color:#FFFFFF
    style G fill:#064E3B,stroke:#34D399,color:#FFFFFF
    style I fill:#78350F,stroke:#FBBF24,color:#FFFFFF
    style K fill:#164E63,stroke:#67E8F9,color:#FFFFFF
    style L fill:#164E63,stroke:#67E8F9,color:#FFFFFF
```

### Processing Pipeline

| Stage | Component | Responsibility |
|---|---|---|
| 01 | Webcam API | Captures live video after user permission. |
| 02 | MediaPipe Tasks Vision | Detects hand landmarks and recognizes supported gestures. |
| 03 | Feature Engineering | Converts 21 three-dimensional landmarks into 63 normalized numerical features for custom classification. |
| 04 | Gesture Classification | Uses the pretrained gesture recognizer and, when configured, an optional custom TensorFlow.js model. |
| 05 | Prediction Filtering | Applies confidence thresholds and stability checks to reduce unreliable or repeated predictions. |
| 06 | Text Generation | Maps recognized gestures to labels and builds an editable message. |
| 07 | Speech Synthesis | Uses the browser's Web Speech API to speak the generated text. |

### Custom Model Training Pipeline

SignBridge AI also includes a data collection and model training workflow:

1. **Collect:** Capture labeled hand-landmark samples through the browser-based Training Lab.
2. **Export:** Save collected samples locally and export them as JSON or CSV.
3. **Train:** Use the Python training script to train a custom static-pose classifier.
4. **Evaluate:** Generate classification metrics and a confusion matrix using held-out samples.
5. **Convert:** Convert the trained Keras model to TensorFlow.js format.
6. **Integrate:** Load the converted model into the browser for custom gesture inference.

### Edge AI & Privacy

- **Local inference:** Video frames are processed in the browser rather than uploaded to a project backend.
- **Local data handling:** Collected training samples are stored in browser local storage until exported or cleared.
- **Browser-native output:** Text-to-speech uses the browser's speech synthesis API.
- **Model flexibility:** The application supports pretrained static gestures and an optional custom-trained classifier.

### Important Scope

SignBridge AI is a limited-vocabulary gesture recognition prototype, not a complete sign-language translation system. Its demonstration labels are not validated translations of ASL or Indian Sign Language. Recognition performance depends on the training data, lighting, camera conditions, and signer variation.



## Landmark preprocessing

For custom-model training, each landmark's coordinates are shifted relative to the wrist (landmark 0). The shifted coordinates are scaled by the maximum Euclidean distance from the wrist, producing 63 normalized values. Training and browser inference must use the same preprocessing.

🧰 Tech stack

<p>
  <img src="https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white" alt="HTML5">
  <img src="https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white" alt="CSS3">
  <img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black" alt="JavaScript">
  <img src="https://img.shields.io/badge/Vite-646CFF?style=flat-square&logo=vite&logoColor=white" alt="Vite">
  <img src="https://img.shields.io/badge/MediaPipe-0097A7?style=flat-square&logo=google&logoColor=white" alt="MediaPipe">
  <img src="https://img.shields.io/badge/TensorFlow.js-FF6F00?style=flat-square&logo=tensorflow&logoColor=white" alt="TensorFlow.js">
  <img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python">
</p>

## Technology	Role


i) HTML, CSS, JavaScript	Web interface and application logic

ii) Vite	Development server and production build

iii) MediaPipe Tasks Vision	Hand landmark tracking and built-in gesture recognition

iv)  TensorFlow.js	Optional custom browser-side classifier

v) Web Speech API	Speech synthesis in supported browsers

vi) Python, TensorFlow/Keras	Custom static-pose model training and evaluation


🚀 Get started

Prerequisites:

- Node.js 18 or newer
- npm
- A webcam
- A modern browser with camera and speech-synthesis support
  
1. Clone the repository

Replace YOUR-USERNAME with your GitHub username:
git clone https://github.com/harvir011/SignBridgeAI.git
cd SignBridge

2. Install dependencies

```npm install```

3. Start the development server

```npm run dev```

Open the localhost URL printed by Vite (typically http://localhost:5173) and allow camera access.

4. Create a production build

```npm run build```

To preview the production build locally:
```npm run preview```


Important: **Open the app using localhost or HTTPS rather than opening index.html directly with a file:// URL. The app copies MediaPipe WASM assets from its installed package during the predev and prebuild scripts. Hosted MediaPipe model assets may require an internet connection.**


🧪 Custom model training

The repository includes a Python training pipeline for experimenting with a custom static-pose classifier.
1. Launch the app and open AI Training Lab.
2. Collect diverse, correctly labeled examples for each intended pose.
3. Export the samples as JSON.
4. Save the exported file as datasets/landmarks.json.
5. Create a Python environment and install the training requirements.


`Windows PowerShell`

`python -m venv .venv`

`.\.venv\Scripts\Activate.ps1`

`pip install -r training/requirements.txt`

`python training/train_classifier.py --data datasets/landmarks.json`

`macOS / Linux`

`python3 -m venv .venv`

`source .venv/bin/activate`

`pip install -r training/requirements.txt`

`python training/train_classifier.py --data datasets/landmarks.json`


**The script writes a trained Keras model, metadata, training history, classification report, and confusion matrix to training/output/. For TensorFlow.js conversion and loading instructions, see [`training/README.md`](training/README.md).**

Training recommendations

- Capture examples across multiple sessions, hand positions, and lighting conditions.
- Keep labels consistent with the sign vocabulary you intend to study.
- Prefer participant- or session-level evaluation splits to reduce data leakage.
- Treat small-dataset results as preliminary; do not present them as general sign-language accuracy.


📁 Project structure

SignBridge/

├── index.html

├── public/

│   ├── mediapipe/

│   └── models/

├── src/

│   ├── main.js

│   └── style.css

├── scripts/

│   └── copy-mediapipe.js

├── training/

│   ├── README.md

│   ├── requirements.txt

│   └── train_classifier.py

├── datasets/

│   └── README.md

├── docs/

│   ├── system-architecture.md

│   ├── prompt-documentation.md

│   └── evaluation.md

├── package.json

├── package-lock.json

└── README.md


Training output and collected landmark data may be generated locally and may not exist in a fresh clone.


🔒 Privacy


- Camera frames are processed in the browser by default; the app does not upload camera frames to a server.
- Training samples can remain in browser local storage until exported or cleared.
- Review exported datasets before sharing them, and obtain consent before publishing identifiable or personal samples.

  
⚠️ Limitations and responsible use


- The current baseline supports a limited set of static hand poses; it does not translate complete sign-language conversations.
- Sign languages have distinct vocabulary and grammar; signs may depend on movement, facial expression, body posture, and context.
- Confidence scores are not a guarantee that a prediction is correct or that an unknown gesture will be rejected.
- Results can vary with lighting, camera quality, background, hand orientation, and signer.
- Do not use this prototype as a substitute for a qualified interpreter in medical, legal, emergency, or other critical situations.


🛣️ Future improvements


- Temporal recognition for motion-based signs
- A larger, carefully validated sign vocabulary
- More evaluation across participants and recording conditions
- Multilingual text and speech options
- Improved mobile accessibility and responsive layouts
- Reproducible benchmarks and documented evaluation results

  
🤝 Contributing


Issues, suggestions, and pull requests are welcome. For substantial changes, open an issue first to discuss the proposed improvement. Please avoid committing private or identifiable training samples without informed consent.


📄 License


No license is specified in this repository yet.
 Add a LICENSE file before describing the project as open source, and choose a license that matches how you want others to use and distribute your work.
 
<div align="center">


Built with AI, computer vision, and a goal of more inclusive communication.

*SignBridge AI · More access. More inclusion. A brighter future.*
</div>


> [!NOTE]
> Camera access is required for gesture recognition.

> [!WARNING]
> Gesture recognition may be less reliable in poor lighting.

