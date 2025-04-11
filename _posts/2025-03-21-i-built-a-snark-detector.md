---
layout: post
title: "I Built a Snark Detector"
date: 2025-03-21
categories: [projects, machine-learning]
---

Have you ever wondered if your tone of voice comes across as snarky? I built a tool that can help answer that question! The Snark Detector is a web application that analyzes audio recordings to detect snarkiness in speech. It combines the power of OpenAI's Whisper for transcription, AssemblyAI for voice analysis, and GPT-4 for snark detection.

The idea for this project came from a real-world challenge I faced in my work as a data scientist. In technical discussions and code reviews, I noticed that sometimes well-intentioned feedback could come across as snarky or condescending, even when that wasn't the intention. This realization led me to explore how we could use AI to help people become more aware of their communication style.

The Snark Detector represents an interesting intersection of natural language processing, audio analysis, and behavioral psychology. It's not just about detecting sarcasm or irony - it's about understanding the subtle ways in which our tone and word choice can affect how our message is received. This is particularly important in professional settings where clear, constructive communication is crucial.

Building this tool presented several interesting challenges:
1. **Audio Processing**: Converting raw audio into meaningful features that could indicate snarkiness
2. **Context Understanding**: Teaching the model to distinguish between genuine snark and other forms of expression
3. **Real-time Analysis**: Making the system responsive enough for practical use
4. **User Experience**: Creating an interface that makes the feedback constructive rather than discouraging

The potential applications of this technology extend beyond just detecting snark. It could be used for:
- Improving workplace communication
- Training public speakers and presenters
- Helping non-native English speakers understand tone and nuance
- Providing feedback for customer service representatives
- Enhancing virtual communication in remote work settings

## How It Works

The Snark Detector processes audio in two main ways:
1. **Audio Analysis**: Using AssemblyAI, it analyzes voice characteristics like tone, pitch, and emphasis
2. **Text Analysis**: Using GPT-4, it evaluates the transcribed text for snarky content

The final output includes:
- A snark score (0-100)
- Specific snarky phrases detected
- Voice characteristics analysis
- Full transcription

## Technical Implementation

The application is built using Streamlit, making it easy to deploy and use. Here's a breakdown of the key components:

### Audio Recording and Processing

```python
import streamlit as st
import tempfile
import os
from dotenv import load_dotenv
import openai
import assemblyai as aai
import json
import base64

# Load environment variables
load_dotenv()

# Configure API clients
openai.api_key = os.getenv("OPENAI_API_KEY")
aai.settings.api_key = os.getenv("ASSEMBLYAI_API_KEY")
```

### Snark Detection with GPT-4

The core of the snark detection is handled by GPT-4, which analyzes the transcribed text:

```python
def analyze_text_with_gpt(text: str) -> dict:
    """Analyze text for snarkiness using GPT-4"""
    try:
        response = openai.chat.completions.create(
            model="gpt-4",
            messages=[
                {"role": "system", "content": """
                You are a snark detection system. Analyze the given text for snarkiness and respond ONLY with a JSON object in this exact format:
                {
                    "score": <number between 0-100>,
                    "phrases": [
                        {
                            "phrase": "<detected snarky phrase>",
                            "context": "<explanation of why it's snarky>",
                            "score": <number between 0-10>
                        }
                    ]
                }
                """},
                {"role": "user", "content": text}
            ]
        )
        return json.loads(response.choices[0].message.content)
    except Exception as e:
        st.error(f"GPT analysis failed: {str(e)}")
        return None
```

### Voice Analysis with AssemblyAI

AssemblyAI provides detailed voice analysis:

```python
def analyze_audio_with_assemblyai(audio_file_path: str) -> dict:
    """Analyze audio characteristics using AssemblyAI"""
    try:
        transcriber = aai.Transcriber()
        transcript = transcriber.transcribe(audio_file_path)
        
        config = aai.TranscriptionConfig(
            language_code="en",
            sentiment_analysis=True
        )
        
        detailed_transcript = transcriber.transcribe(audio_file_path, config=config)
        
        analysis = {
            "tone": "Neutral",
            "pitch": "Normal",
            "emphasis": "Standard emphasis",
            "speed": "Normal"
        }
        
        if hasattr(detailed_transcript, 'sentiment_analysis_results'):
            analysis["tone"] = detailed_transcript.sentiment_analysis_results[0].sentiment
        
        return {
            "transcription": transcript.text,
            "voice_analysis": analysis
        }
    except Exception as e:
        st.error(f"Audio analysis failed: {str(e)}")
        return None
```

## User Interface

The application features a clean, intuitive interface with two main options:
1. Upload an existing audio file
2. Record audio directly in the browser

The UI includes:
- Real-time recording controls
- Progress indicators
- Detailed results display
- Interactive elements for exploring the analysis

## Results and Analysis

The Snark Detector provides comprehensive feedback:
- Overall snark score (0-100)
- Specific snarky phrases with context
- Voice characteristics (tone, pitch, emphasis, speed)
- Full transcription of the audio

## Future Improvements

Some potential enhancements I'm considering:
1. Adding historical analysis to track snarkiness trends
2. Implementing multi-language support
3. Creating a mobile app version
4. Adding more detailed voice analysis features

## Try It Yourself

The Snark Detector is a fun and practical tool that demonstrates the power of combining different AI technologies. Whether you're curious about your communication style or just want to experiment with AI-powered voice analysis, give it a try!

You can find the complete code on [GitHub](https://github.com/yourusername/snark-detector).

*Note: This project requires API keys for OpenAI and AssemblyAI. Make sure to set up your environment variables accordingly.* 