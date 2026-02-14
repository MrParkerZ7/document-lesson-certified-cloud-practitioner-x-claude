# 🤖 AWS AI and Machine Learning Services

## File Structure

```
lesson-15-aws-ai-ml-and-analytics-services/
└── 01-ai-ml-services/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

AWS provides a comprehensive suite of artificial intelligence (AI) and machine learning (ML) services that enable developers to add intelligent capabilities to applications without requiring deep ML expertise. These services range from pre-trained AI services for common use cases to platforms for building custom ML models.

## AI/ML Services Hierarchy

```
+------------------------------------------------------------------+
|                    AWS AI/ML SERVICES STACK                       |
+------------------------------------------------------------------+
|                                                                   |
|   ┌─────────────────────────────────────────────────────────────┐ |
|   │  AI SERVICES (Pre-trained, API-based - No ML expertise)     │ |
|   │  Rekognition | Comprehend | Polly | Lex | Translate | etc.  │ |
|   └─────────────────────────────────────────────────────────────┘ |
|                              ▲                                    |
|   ┌─────────────────────────────────────────────────────────────┐ |
|   │  ML PLATFORMS (Build Custom Models - Some ML expertise)     │ |
|   │  Amazon SageMaker | Amazon Personalize | Amazon Forecast    │ |
|   └─────────────────────────────────────────────────────────────┘ |
|                              ▲                                    |
|   ┌─────────────────────────────────────────────────────────────┐ |
|   │  ML FRAMEWORKS & INFRASTRUCTURE (Deep ML expertise)         │ |
|   │  TensorFlow | PyTorch | EC2 | GPU Instances                 │ |
|   └─────────────────────────────────────────────────────────────┘ |
|                                                                   |
+------------------------------------------------------------------+
```

## Amazon SageMaker

Amazon SageMaker is a fully managed platform for building, training, and deploying machine learning models at scale.

```
+------------------------------------------------------------------+
|                      AMAZON SAGEMAKER                             |
+------------------------------------------------------------------+
|                                                                   |
|   BUILD              TRAIN               DEPLOY                   |
|   ┌──────────┐      ┌──────────┐        ┌──────────┐              |
|   │ Notebooks│ ──▶  │ Training │  ──▶   │ Endpoints│              |
|   │ Studio   │      │ Jobs     │        │ Inference│              |
|   └──────────┘      └──────────┘        └──────────┘              |
|                                                                   |
|   Features:                                                       |
|   • Built-in algorithms  • Auto-scaling   • A/B testing           |
|   • Jupyter notebooks    • Spot training  • Model monitoring      |
|   • Ground Truth (labeling)              • MLOps pipelines        |
|                                                                   |
+------------------------------------------------------------------+
```

| Component | Description |
|-----------|-------------|
| SageMaker Studio | Integrated IDE for ML development |
| SageMaker Notebooks | Managed Jupyter notebooks |
| Ground Truth | Data labeling service |
| Autopilot | Automated model creation (AutoML) |
| Model Training | Distributed training at scale |
| Model Deployment | Real-time and batch inference |

## Amazon Rekognition

Amazon Rekognition provides image and video analysis using deep learning.

| Feature | Description | Use Cases |
|---------|-------------|-----------|
| Object Detection | Identifies objects in images/video | Inventory management, content categorization |
| Facial Analysis | Detects faces, emotions, attributes | User verification, sentiment analysis |
| Face Comparison | Compares faces for similarity | Identity verification |
| Text in Image | Extracts text from images | License plate recognition, sign reading |
| Celebrity Recognition | Identifies celebrities | Media and entertainment |
| Content Moderation | Detects inappropriate content | User-generated content filtering |
| Custom Labels | Train custom image classifiers | Industry-specific detection |

```
+------------------------------------------------------------------+
|                    REKOGNITION CAPABILITIES                       |
+------------------------------------------------------------------+
|                                                                   |
|   IMAGE INPUT                              ANALYSIS OUTPUT        |
|   ┌──────────┐                            ┌──────────────────┐    |
|   │  📷      │  ───▶  [Rekognition] ───▶  │ • Objects: car   │    |
|   │  Image   │                            │ • Faces: 2       │    |
|   │  or      │                            │ • Text: "STOP"   │    |
|   │  Video   │                            │ • Emotions: happy│    |
|   └──────────┘                            │ • Moderation: OK │    |
|                                            └──────────────────┘    |
|                                                                   |
+------------------------------------------------------------------+
```

## Amazon Comprehend

Amazon Comprehend is a natural language processing (NLP) service for extracting insights from text.

| Feature | Description |
|---------|-------------|
| Sentiment Analysis | Determines if text is positive, negative, neutral, or mixed |
| Entity Recognition | Identifies people, places, organizations, dates |
| Key Phrase Extraction | Extracts key phrases and topics |
| Language Detection | Identifies the language of the text |
| Syntax Analysis | Parses text for parts of speech |
| Custom Classification | Train custom document classifiers |
| PII Detection | Identifies personally identifiable information |

```
+------------------------------------------------------------------+
|                    COMPREHEND NLP ANALYSIS                        |
+------------------------------------------------------------------+
|                                                                   |
|   INPUT: "I love AWS services! The London office is amazing."     |
|                                                                   |
|   ┌─────────────────────────────────────────────────────────────┐ |
|   │                      COMPREHEND                              │ |
|   └─────────────────────────────────────────────────────────────┘ |
|                              │                                    |
|   ┌──────────────────────────┼──────────────────────────────────┐ |
|   │                          ▼                                   │ |
|   │  Sentiment: POSITIVE (0.95)                                  │ |
|   │  Entities: "AWS" (Organization), "London" (Location)         │ |
|   │  Key Phrases: "AWS services", "London office"                │ |
|   │  Language: English (en)                                      │ |
|   └─────────────────────────────────────────────────────────────┘ |
|                                                                   |
+------------------------------------------------------------------+
```

## Amazon Polly

Amazon Polly converts text into lifelike speech using deep learning.

| Feature | Description |
|---------|-------------|
| Neural TTS | High-quality neural text-to-speech voices |
| Standard TTS | Traditional text-to-speech voices |
| Languages | 60+ voices in 30+ languages |
| SSML Support | Speech Synthesis Markup Language for control |
| Speech Marks | Timing information for lip-sync |
| Lexicons | Custom pronunciation dictionaries |

| Voice Type | Description | Use Case |
|------------|-------------|----------|
| Neural | Most natural, human-like | Customer-facing applications |
| Standard | Traditional TTS, more voices | High-volume, cost-sensitive |
| Long-form | Optimized for articles/books | Audiobooks, articles |
| Newscaster | News anchor style | News applications |

## Amazon Lex

Amazon Lex builds conversational interfaces (chatbots) using voice and text.

```
+------------------------------------------------------------------+
|                       AMAZON LEX                                  |
+------------------------------------------------------------------+
|                                                                   |
|   USER INPUT                        BOT RESPONSE                  |
|   ┌──────────┐                     ┌──────────────┐               |
|   │ "I want  │                     │ "What type   │               |
|   │ to book  │  ──▶  [LEX]  ──▶    │ of flower?   │               |
|   │ flowers" │       Bot           │ Roses, tulips│               |
|   └──────────┘                     │ or lilies?"  │               |
|                                    └──────────────┘               |
|   COMPONENTS:                                                     |
|   • Intents - What user wants to accomplish                       |
|   • Utterances - Ways users express intents                       |
|   • Slots - Data to fulfill the intent                            |
|   • Fulfillment - Lambda function to process request              |
|                                                                   |
+------------------------------------------------------------------+
```

| Component | Description |
|-----------|-------------|
| Intent | User's goal (BookHotel, OrderFlowers) |
| Utterance | Sample phrases users might say |
| Slot | Required data to fulfill intent |
| Fulfillment | Lambda function or return data |

> **Note**: Amazon Lex is the same technology that powers Amazon Alexa.

## Amazon Translate

Amazon Translate provides neural machine translation for real-time language translation.

| Feature | Description |
|---------|-------------|
| Languages | 75+ languages supported |
| Real-time | Low-latency translation |
| Batch | Process large volumes of text |
| Custom Terminology | Define specific translations |
| Formality | Control formal vs informal tone |
| Profanity Masking | Filter inappropriate content |

## Amazon Transcribe

Amazon Transcribe converts speech to text using automatic speech recognition (ASR).

| Feature | Description |
|---------|-------------|
| Real-time | Live audio transcription |
| Batch | Process audio/video files |
| Custom Vocabulary | Industry-specific terms |
| Speaker Identification | Identify different speakers |
| Channel Identification | Separate audio channels |
| Medical Transcribe | HIPAA-eligible medical transcription |
| Call Analytics | Analyze customer service calls |

```
+------------------------------------------------------------------+
|                    TRANSCRIBE WORKFLOW                            |
+------------------------------------------------------------------+
|                                                                   |
|   AUDIO INPUT           TRANSCRIBE           TEXT OUTPUT          |
|   ┌──────────┐         ┌──────────┐         ┌──────────────────┐  |
|   │  🎤      │         │          │         │ Speaker 1: Hello │  |
|   │  Audio   │  ──▶    │   ASR    │  ──▶    │ Speaker 2: Hi    │  |
|   │  File    │         │  Engine  │         │ [00:05] Meeting  │  |
|   └──────────┘         └──────────┘         │ started...       │  |
|                                             └──────────────────┘  |
|                                                                   |
+------------------------------------------------------------------+
```

## Amazon Textract

Amazon Textract extracts text, forms, and tables from scanned documents.

| Feature | Description |
|---------|-------------|
| Text Detection | Extract printed and handwritten text |
| Form Extraction | Key-value pairs from forms |
| Table Extraction | Structured table data |
| Query-based | Answer specific questions about documents |
| Analyze ID | Extract data from identity documents |
| Analyze Expense | Process invoices and receipts |

```
+------------------------------------------------------------------+
|                    TEXTRACT DOCUMENT ANALYSIS                     |
+------------------------------------------------------------------+
|                                                                   |
|   DOCUMENT INPUT                    EXTRACTED DATA                |
|   ┌──────────────┐                 ┌──────────────────────────┐   |
|   │ ┌──────────┐ │                 │ Raw Text:                │   |
|   │ │ Name: Bob│ │                 │   "Name: Bob"            │   |
|   │ │ Age: 30  │ │  ──▶            │                          │   |
|   │ │ ┌─────┐  │ │  Textract       │ Forms (Key-Value):       │   |
|   │ │ │Table│  │ │                 │   Name → Bob             │   |
|   │ │ └─────┘  │ │                 │   Age → 30               │   |
|   │ └──────────┘ │                 │                          │   |
|   └──────────────┘                 │ Tables: [[...], [...]]   │   |
|                                    └──────────────────────────┘   |
|                                                                   |
+------------------------------------------------------------------+
```

## Amazon Kendra

Amazon Kendra is an intelligent enterprise search service powered by machine learning.

| Feature | Description |
|---------|-------------|
| Natural Language | Query using natural language questions |
| Document Ranking | ML-powered relevance ranking |
| Data Sources | S3, SharePoint, Salesforce, databases |
| FAQs | Automatic FAQ detection and highlighting |
| Incremental Learning | Learns from user feedback |
| Security | Respects document-level permissions |

```
+------------------------------------------------------------------+
|                     AMAZON KENDRA                                 |
+------------------------------------------------------------------+
|                                                                   |
|   DATA SOURCES                    SEARCH                          |
|   ┌──────────┐                                                    |
|   │    S3    │───┐                                                |
|   └──────────┘   │              ┌─────────────────┐               |
|   ┌──────────┐   │              │ Q: "What is the │               |
|   │SharePoint│───┼──▶ KENDRA ◀──│ vacation policy?"│              |
|   └──────────┘   │              └─────────────────┘               |
|   ┌──────────┐   │                      │                         |
|   │ Database │───┘                      ▼                         |
|   └──────────┘              ┌─────────────────────┐               |
|                             │ A: "Employees get   │               |
|                             │ 15 days PTO..."     │               |
|                             └─────────────────────┘               |
|                                                                   |
+------------------------------------------------------------------+
```

## Amazon Personalize

Amazon Personalize creates real-time personalized recommendations.

| Feature | Description |
|---------|-------------|
| Recommendations | Product, content, search recommendations |
| User Segmentation | Group users by preferences |
| Recipes | Pre-built algorithms for common use cases |
| Real-time | Update recommendations as users interact |
| A/B Testing | Compare recommendation strategies |

| Use Case | Example |
|----------|---------|
| E-commerce | "Customers who bought this also bought..." |
| Media | "Because you watched..." |
| Marketing | Personalized email campaigns |
| Search | Personalized search results |

## Amazon Forecast

Amazon Forecast creates accurate time-series forecasts using machine learning.

| Feature | Description |
|---------|-------------|
| AutoML | Automatically selects best algorithm |
| Accuracy | 50% more accurate than traditional methods |
| Related Data | Incorporate external factors (weather, events) |
| What-if Analysis | Scenario planning |
| Cold Start | Forecast for new items without history |

| Use Case | Example |
|----------|---------|
| Retail | Demand forecasting for inventory |
| Finance | Revenue and cash flow prediction |
| Supply Chain | Resource planning |
| Energy | Power demand forecasting |

## AI/ML Services Quick Reference

| Service | Primary Function | Input | Output |
|---------|-----------------|-------|--------|
| SageMaker | Build/train/deploy ML models | Data | Trained models |
| Rekognition | Image and video analysis | Images/Videos | Labels, faces, text |
| Comprehend | Natural language processing | Text | Sentiment, entities |
| Polly | Text-to-speech | Text | Audio |
| Lex | Conversational bots | Voice/Text | Bot responses |
| Translate | Language translation | Text | Translated text |
| Transcribe | Speech-to-text | Audio | Text |
| Textract | Document extraction | Documents | Structured data |
| Kendra | Enterprise search | Query | Search results |
| Personalize | Recommendations | User data | Recommendations |
| Forecast | Time-series prediction | Historical data | Forecasts |

## AI/ML Services by Use Case

```
+------------------------------------------------------------------+
|                 AI/ML SERVICES BY USE CASE                        |
+------------------------------------------------------------------+
|                                                                   |
|   VISION/IMAGE          TEXT/LANGUAGE         VOICE/SPEECH        |
|   ┌──────────────┐     ┌──────────────┐      ┌──────────────┐     |
|   │ Rekognition  │     │ Comprehend   │      │ Polly        │     |
|   │ • Images     │     │ • Sentiment  │      │ • Text→Speech│     |
|   │ • Videos     │     │ • Entities   │      │              │     |
|   │ • Faces      │     │ • NLP        │      │ Transcribe   │     |
|   │              │     │              │      │ • Speech→Text│     |
|   │ Textract     │     │ Translate    │      │              │     |
|   │ • Documents  │     │ • Languages  │      │ Lex          │     |
|   │ • Forms      │     │              │      │ • Chatbots   │     |
|   └──────────────┘     └──────────────┘      └──────────────┘     |
|                                                                   |
|   PERSONALIZATION       FORECASTING          SEARCH               |
|   ┌──────────────┐     ┌──────────────┐      ┌──────────────┐     |
|   │ Personalize  │     │ Forecast     │      │ Kendra       │     |
|   │ • Products   │     │ • Demand     │      │ • Enterprise │     |
|   │ • Content    │     │ • Inventory  │      │ • Documents  │     |
|   │ • Campaigns  │     │ • Planning   │      │ • NL queries │     |
|   └──────────────┘     └──────────────┘      └──────────────┘     |
|                                                                   |
+------------------------------------------------------------------+
```

## 🎯 Exam Tips

- **SageMaker** = fully managed ML platform for building, training, and deploying custom models
- **Rekognition** = image and video analysis (faces, objects, content moderation)
- **Comprehend** = NLP for text analysis (sentiment, entities, key phrases)
- **Polly** = text-to-speech (remember: "Polly wants a cracker" - it talks)
- **Lex** = chatbots and conversational interfaces (same tech as Alexa)
- **Translate** = neural machine translation between languages
- **Transcribe** = speech-to-text (audio to written text)
- **Textract** = extract text, forms, and tables from documents
- **Kendra** = intelligent enterprise search service
- **Personalize** = real-time personalized recommendations
- **Forecast** = time-series forecasting for demand planning
- Most AI services are **fully managed** - no ML expertise required
- **SageMaker** requires more ML knowledge than pre-trained AI services
- These services are all **pay-per-use** with no upfront costs

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Machine Learning (ML) | Systems that learn from data to make predictions |
| Natural Language Processing (NLP) | AI that understands human language |
| Computer Vision | AI that analyzes images and videos |
| Text-to-Speech (TTS) | Converting written text to audio |
| Speech-to-Text (STT) | Converting audio to written text |
| Sentiment Analysis | Determining emotional tone of text |
| Entity Recognition | Identifying named entities (people, places, organizations) |
| OCR | Optical Character Recognition - extracting text from images |
| Neural Network | ML architecture modeled after the brain |
| Inference | Using a trained model to make predictions |

## 💡 Key Takeaways

1. AWS AI services provide pre-trained models accessible via APIs - no ML expertise required
2. Amazon SageMaker is the fully managed platform for building custom ML models
3. Rekognition analyzes images and videos for objects, faces, and content moderation
4. Comprehend provides natural language processing for text analysis
5. Polly converts text to speech; Transcribe converts speech to text
6. Lex builds conversational chatbots using the same technology as Alexa
7. Textract extracts structured data from scanned documents
8. Kendra provides intelligent enterprise search with natural language queries
9. Personalize creates real-time recommendations for users
10. Forecast predicts future values based on historical time-series data
11. All AI/ML services are pay-per-use with no upfront commitments

---

*Next: [02 - Analytics Services](../02-analytics-services/readme.md)*
