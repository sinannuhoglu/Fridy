# Fridy - Smart Food Assistant App

Fridy is an Android application that helps users identify the ingredients in their fridge using computer vision techniques and generates meal recipes based on those ingredients. It uses a custom-trained YOLOv8 object detection model to process images and detect food items, which are then passed through a prompt to generate rich, structured recipes using AI-powered language models. It also creates visual illustrations of meals and supports text-to-speech for reading the recipes aloud.

Built with modern Android technologies including Jetpack Compose, MVVM architecture, Hilt, Retrofit and TensorFlow Lite.

---

## Screenshots

| Home Screen        | Detection Screen      | Fridge Screen         | Detail Screen        | Recipe Screen        |
|--------------------|------------------------|------------------------|------------------------|------------------------|
| <img width="1194" height="2532" alt="Image" src="https://github.com/user-attachments/assets/79995a6d-b4b0-4c26-8f40-ce9fa1a51d63" /> | <img width="1194" height="2532" alt="Image" src="https://github.com/user-attachments/assets/8702db23-bc9c-4ef9-af00-ea804b3b487c" /> | <img width="1194" height="2532" alt="Image" src="https://github.com/user-attachments/assets/8ec19c4b-c0cc-4f7d-9dab-36189bc117fa" /> | <img width="1194" height="2532" alt="Image" src="https://github.com/user-attachments/assets/abba6de6-f33e-4077-87a3-9f4b27b246f9" /> | <img width="1194" height="2532" alt="Image" src="https://github.com/user-attachments/assets/ede01104-f415-4e22-a869-bd19e2dc6902" /> |

---

## Project Structure

```
com.sinannuhoglu.fridy/
├── camera/
│   ├── CameraScreen.kt             # Object detection screen. Uses YOLOv8 to detect items in an image.
│   ├── CameraViewModel.kt          # Manages detection logic and state.
│   └── YoloV8Classifier.kt         # Runs YOLOv8 TensorFlow model and performs classification.
│
├── data.remote/
│   ├── AIService.kt                # Defines API interface for recipe and image generation.
│   └── RetrofitClient.kt           # Retrofit setup (Timeouts, Base URL, etc.).
│
├── detail/
│   └── DetailScreen.kt             # Collects meal type and note to generate recipe request.
│
├── di/
│   └── YoloModule.kt               # Hilt module for injecting YoloV8Classifier.
│
├── fridge/
│   ├── FridgeScreen.kt             # Displays and selects detected items.
│   └── FridgeViewModel.kt          # Groups and manages selected fridge items.
│
├── home/
│   ├── HomeScreen.kt               # Entry screen for image selection or camera.
│   └── HomeViewModel.kt            # Handles image temp file, loading state and navigation.
│
├── model/                          # Data models including DetectionResult, FridgeItem, RecipeUiState.
│   
│
├── navigation/
│   └── BottomNavGraph.kt           # Sets up screen navigation.
│
├── recipes/
│   ├── RecipeResultScreen.kt       # Displays recipe results, image and TTS button.
│   ├── RecipesViewModel.kt         # Handles recipe/image fetching, error and state management.
│   └── TextToSpeechManager.kt      # Manages TTS initialization and playback.
│
├── shared/
│   └── SharedViewModel.kt          # Shared data like selected image URI and items across screens.
│
├── ui/
│   ├── components/                 # Reusable UI components (buttons, cards, etc.).
│   └── theme/                      # Theme and color settings.
│
├── util/
│   ├── Constants.kt               # API keys and constants.
│   ├── ParseRecipeContent.kt      # Converts recipe text into RecipeUiState.
│   └── RecipeUtils.kt             # Prompt builders and helpers for AI input.
│
├── FridyApplication.kt            # Application entry point with Hilt support.
└── MainActivity.kt                # Hosts Scaffold, NavController and global theme.
```

---
## Features

| Feature                    | Description |
|---------------------------|-------------|
| Image-based object detection | Detects food items from gallery or camera images using YOLOv8 and TFLite. |
| Item grouping and selection | Groups similar items and allows users to choose which ones to use. |
| Meal type and notes input   | Users can specify meal types (breakfast, lunch, dinner) and add extra notes. |
| Recipe generation using AI  | Uses AI to create creative and structured recipes based on selected items. |
| Image generation using AI   | Generates a realistic food image based on the recipe. |
| Text-to-Speech (TTS)        | Reads the recipe aloud in Turkish using Android's TTS engine. |
| Jetpack Compose UI          | Fully built with Compose and modern UI components. |

---

## Tech Stack

| Technology         | Purpose |
|--------------------|---------|
| Jetpack Compose    | Declarative UI toolkit for Android |
| Hilt               | Dependency injection |
| Retrofit & Gson    | Networking and JSON serialization |
| Kotlin Coroutines  | Asynchronous tasks |
| TensorFlow Lite    | Running YOLOv8 model on-device |
| Custom-trained YOLOv8 | Used for image-based ingredient detection |
| AI API (Chat & Image) | Generates recipe content and visuals |
| TextToSpeech API   | For reading recipes aloud |
| Coil               | For image loading |
| Lottie             | Animations |

---

## Screen Flow

| Screen              | Description |
|---------------------|-------------|
| **HomeScreen**      | Lets user select image from gallery or take a new photo |
| **CameraScreen**    | Detects objects from image using YOLOv8 and displays detection results |
| **FridgeScreen**    | Displays detected items, allows selection and grouping |
| **DetailScreen**  | Collects meal type and additional note for recipe generation |
| **RecipeResultScreen** | Displays AI-generated recipe and image with option to listen via TTS |

---

## Model Information

This project leverages a **custom-trained YOLOv8 model** specifically tailored for detecting food items within a refrigerator environment. Designed with mobile deployment in mind, the model has been converted to TensorFlow Lite (TFLite) format to ensure efficient, real-time performance on edge devices.

The training process was carried out using a meticulously annotated dataset and enriched with a variety of visual conditions—such as different lighting setups, camera angles and image qualities—to improve the model’s generalization to real-world scenarios.

Thanks to these optimizations, the model delivers fast and accurate predictions on mobile platforms, maintaining high reliability across diverse use cases.

### Performance

- Object Detection Accuracy: Nearly 100%  
- Classification Accuracy: Above 97%  
- Consistent and robust performance across various food categories and environmental conditions.

### Model Predictions

<table>
  <tr>
    <td><img width="495" height="319" alt="Image" src="https://github.com/user-attachments/assets/68f8e7ec-4c88-4fec-b7d0-08f873b45366" /></td>
    <td><img width="495" height="319" alt="Image" src="https://github.com/user-attachments/assets/3f553f9c-2e3d-423c-b078-a6e18098f5d6" /></td>
  </tr>
  <tr>
    <td><img width="495" height="319" alt="Image" src="https://github.com/user-attachments/assets/29b3cd5e-d82a-4c36-acc5-e4a54fc89e03" /></td>
    <td><img width="495" height="319" alt="Image" src="https://github.com/user-attachments/assets/011bc6ea-21c4-4c3f-bef1-59167c297d66" /></td>
  </tr>
</table>
