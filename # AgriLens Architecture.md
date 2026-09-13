# AgriLens Architecture

This document describes the software architecture of AgriLens v2 and the responsibilities of each component.

---

# Design Philosophy

AgriLens follows a modular architecture that separates:

- User Interface
- Business Logic
- Data Models
- Application Services

The primary objective is to keep the UI lightweight while isolating prediction logic and data management into reusable services.

---

# High-Level Architecture

```
                   User

                     │

                     ▼

              Home Screen UI

                     │

                     ▼

          Image Selection Service

                     │

                     ▼

             TensorFlow Lite Model

                     │

                     ▼

          Prediction + Confidence

                     │

          ┌──────────┴──────────┐

          ▼                     ▼

 Knowledge Base          Class Mapping

          ▼                     ▼

       Disease Info      Class Name

          └──────────┬──────────┘

                     ▼

             PredictionResult

                     ▼

                 Result Card
```

---

# Application Flow

1. User selects an image.
2. The image is resized and preprocessed.
3. TensorFlow Lite performs inference.
4. Confidence scores are computed.
5. Predicted class index is converted into a class name.
6. Disease information is retrieved from the knowledge base.
7. Results are displayed to the user.

---

# Project Structure

```
lib/

├── core/
│   ├── constants/
│   ├── theme/
│   └── utils/
│
├── models/
│
├── services/
│
├── screens/
│   ├── splash/
│   ├── home/
│   └── about/
│
└── widgets/
    ├── common/
    ├── home/
    └── about/
```

---

# Core Components

## HomeScreen

Responsible for:

- image selection
- prediction requests
- loading state
- displaying results

HomeScreen owns the application state.

---

## TFLiteService

Responsibilities:

- load TensorFlow Lite model
- image preprocessing
- model inference
- confidence calculation
- prediction generation

Returns a PredictionResult object.

---

## ClassService

Loads:

```
class_names.json
```

Maps model output indices to readable class names.

---

## KnowledgeService

Loads:

```
knowledge_base.json
```

Provides:

- disease description
- symptoms
- causes
- prevention
- management recommendations

---

## PredictionResult

Acts as the application's central data model.

Contains:

- predicted class
- confidence
- disease metadata
- advisory information

---

# State Management

AgriLens intentionally uses simple local state management.

Application state is owned by HomeScreen and passed to child widgets as immutable data.

No external state management framework (Provider, Riverpod, Bloc, etc.) is currently required due to the application's modest complexity.

---

# Asset Organization

```
assets/

├── model/
│
├── data/
│
├── fonts/
│
├── images/
│
└── icon/
```

---

# Design Principles

- Separation of concerns
- Reusable services
- Minimal UI logic
- Offline-first architecture
- Immutable data flow
- Modular code organization

---

# Advantages

This architecture provides:

- easier maintenance
- improved readability
- reusable business logic
- simplified testing
- scalability for future features

Future additions such as Grad-CAM visualization, history tracking, multilingual support, and cloud synchronization can be integrated with minimal architectural changes.