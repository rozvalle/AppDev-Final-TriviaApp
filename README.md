# Trivia App
[![Ask DeepWiki](https://devin.ai/assets/askdeepwiki.png)](https://deepwiki.com/rozvalle/AppDev-Final-TriviaApp)

## Overview

This repository contains the source code for an Android Trivia App. It's a mobile application where users can test their knowledge across various categories. The app features user authentication, fetches questions from a public API, tracks scores, and maintains a public leaderboard.

This project is built using Kotlin and integrates with Firebase for backend services and the Open Trivia Database for questions.

## Features

*   **User Authentication**: Secure user registration and login system powered by Firebase Authentication.
*   **Category Selection**: Users can choose from a wide range of trivia categories, including General Knowledge, Film, Video Games, Science, and more.
*   **Trivia Gameplay**: A 20-question quiz with multiple-choice answers for the selected category.
*   **Scoring System**: Tracks the user's score based on correct answers.
*   **Live Leaderboard**: Displays the top 10 high scores from all players, fetched in real-time from Firebase Firestore.
*   **API Integration**: Fetches trivia questions dynamically from the Open Trivia Database (OpenTDB).

## Technologies Used

*   **Language**: Kotlin
*   **Backend**:
    *   **Firebase Authentication**: For managing user accounts (email/password).
    *   **Firebase Firestore**: To store user data and leaderboard scores.
*   **Networking**:
    *   **Retrofit**: A type-safe HTTP client for Android and Java to connect to the OpenTDB API.
    *   **Gson**: For parsing JSON data from the API response into Kotlin data classes.
*   **UI**:
    *   Android XML for layouts.
    *   `RecyclerView` to efficiently display the leaderboard list.
*   **Build Tool**: Gradle

## Project Structure

The application is organized into several key components:

*   **Activities**:
    *   `LoginActivity`: The entry point for the app. Handles user sign-in and redirects to the registration screen.
    *   `RegisterActivity`: Allows new users to create an account. Usernames are stored in Firestore.
    *   `MainActivity`: The main hub after logging in. Users can select a trivia category, navigate to the leaderboard, or log out.
    *   `TriviaActivity`: Manages the quiz session. It fetches questions, displays them, validates answers, updates the score, and saves the final score to the Firestore leaderboard.
    *   `LeaderboardActivity`: Fetches and displays the top 10 scores from the `leaderboard` collection in Firestore.

*   **API and Network**:
    *   `data/api/TriviaApi.kt`: A Retrofit interface defining the GET request to the OpenTDB API (`https://opentdb.com/`).
    *   `data/network/RetrofitInstance.kt`: A singleton object that provides a configured instance of Retrofit.
    *   `data/model/`: Contains Kotlin data classes (`TriviaResponse`, `LeaderboardEntry`) for mapping JSON responses.

*   **Adapter**:
    *   `adapter/LeaderboardAdapter.kt`: A `RecyclerView.Adapter` to bind leaderboard data to the view items in `LeaderboardActivity`.

## Setup and Installation

To run this project on your local machine, follow these steps:

1.  **Clone the Repository**
    ```bash
    git clone https://github.com/rozvalle/AppDev-Final-TriviaApp.git
    ```

2.  **Open in Android Studio**
    *   Launch Android Studio.
    *   Select "Open an existing Project" and navigate to the cloned repository directory.

3.  **Sync Gradle**
    *   Android Studio will automatically sync the project's Gradle files. This may take a few moments.

4.  **Run the Application**
    *   Connect an Android device or start an Android Virtual Device (AVD).
    *   Click the "Run" button in Android Studio to build and install the app.

The project includes the `google-services.json` file, so it should connect to the pre-configured Firebase project out of the box. If you wish to use your own Firebase project, you will need to:
1.  Create a new project on the [Firebase Console](https://console.firebase.google.com/).
2.  Add an Android app to your Firebase project.
3.  Download the generated `google-services.json` file and replace the existing one in the `app/` directory.
4.  Enable Email/Password authentication in the Firebase Authentication section.
5.  Set up Firestore database rules to allow reads/writes to the `users` and `leaderboard` collections.
