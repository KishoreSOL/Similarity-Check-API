# Similarity Detection API

## Overview

The Similarity Detection API is a Flask-based RESTful service that allows users to register, authenticate, and use tokens to calculate the similarity between two pieces of text. The API leverages MongoDB for data storage and Spacy's NLP capabilities to perform text similarity calculations.

## Features

- **User Registration**: Allows users to create an account.
- **Authentication**: Verifies user credentials before processing requests.
- **Token Management**: Users are assigned tokens that are deducted upon each similarity calculation. Tokens can be refilled by an admin.
- **Text Similarity Detection**: Calculates and returns the similarity score between two texts.

## Requirements

- Python 3.x
- Flask
- Flask-RESTful
- PyMongo
- Bcrypt
- Spacy and English language model (`en_core_web_sm`)

## Installation

1. Clone the repository:

   ```bash
   git clone git@github.com:KishoreSOL/Similarity-Check-API.git
   cd similarity-detection-api
   ```

2. Create a virtual environment and activate it:

   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```

3. Install the dependencies:

   ```bash
   pip install -r requirements.txt
   ```

4. Install Spacy's English language model:

   ```bash
   python -m spacy download en_core_web_sm
   ```

5. Ensure MongoDB is running and accessible.

## Configuration

- **MongoDB**: The app connects to a MongoDB instance running on `mongodb://db:27017`. Make sure MongoDB is running on this URL or adjust the connection string in the app code if necessary.

## Usage

1. Start the Flask app:

   ```bash
   python app.py
   ```

2. The API will be available at `http://0.0.0.0:5000`.

## API Endpoints

### Register

- **Endpoint**: `/register`
- **Method**: POST
- **Description**: Registers a new user.
- **Request Body**:
  ```json
  {
    "username": "your_username",
    "password": "your_password"
  }
  ```
- **Response**:
  ```json
  {
    "status": 200,
    "msg": "You successfully signed up for the API"
  }
  ```
  or
  ```json
  {
    "status": 301,
    "msg": "Invalid Username"
  }
  ```

### Detect

- **Endpoint**: `/detect`
- **Method**: POST
- **Description**: Calculates the similarity between two texts.
- **Request Body**:
  ```json
  {
    "username": "your_username",
    "password": "your_password",
    "text1": "Text to compare 1",
    "text2": "Text to compare 2"
  }
  ```
- **Response**:
  ```json
  {
    "status": 200,
    "ratio": similarity_score,
    "msg": "Similarity score calculated successfully"
  }
  ```
  or error messages based on validation failures.

### Refill

- **Endpoint**: `/refill`
- **Method**: POST
- **Description**: Refill tokens for a user. Only accessible with an admin password.
- **Request Body**:
  ```json
  {
    "username": "your_username",
    "admin_pw": "admin_password",
    "refill": refill_amount
  }
  ```
- **Response**:
  ```json
  {
    "status": 200,
    "msg": "Refilled successfully"
  }
  ```
  or error messages based on validation failures.

## Token Management

- Users start with 6 tokens.
- Each `/detect` request consumes 1 token.
- Tokens can be refilled using the `/refill` endpoint with the correct admin password.

## Development

### Running Tests

For development purposes, ensure that your MongoDB instance is correctly set up and running.

1. You can start the application in debug mode to facilitate development and troubleshooting:

   ```bash
   FLASK_ENV=development flask run
   ```

### Deployment

- Adjust the `host` and `port` parameters in `app.run` for your deployment environment.
- Ensure your MongoDB instance is secured and accessible to your application.

## Security Notes

- The default admin password is hardcoded as `"abc123"`. In a production environment, replace this with a more secure mechanism for managing admin access.
- Ensure MongoDB is configured with appropriate authentication and network access controls.

## Troubleshooting

- **MongoDB Connection**: Ensure MongoDB is running and accessible at the specified URL.
- **Dependencies**: Make sure all Python dependencies are installed, including Spacy's language model.

## Future Enhancements

- Add user authentication tokens to replace password usage in requests.
- Implement better token management and monitoring.
- Enhance security for admin operations and sensitive endpoints.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contact

For any issues or queries, please contact [kishoreyuva147@gmail.com].

---

This README provides an overview and detailed instructions for running and using the Similarity Detection API. Adjust the contact information and license details as needed for your project.