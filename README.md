# CHATGPT GUI Chatbot Using PyQt6

A simple GUI-based chatbot application built with PyQt6, leveraging OpenAI's GPT-3 for generating responses.

## Features
- Interactive chat interface with input field and send button.
- Multithreaded response handling to keep the UI responsive.
- Uses OpenAI's GPT-3 to generate responses.

## Installation

1. Clone the repository:
   ```sh
   git clone https://github.com/convenience-tinashe-chibatamoto/CHATGPT-GUI-Chatbot-Using-PyQt6.git
   cd CHATGPT-GUI-Chatbot-Using-PyQt6
   ```

2. Install the required dependencies:
   ```sh
   pip install -r requirements.txt
   ```

3. Set your OpenAI API key in `backend.py`:
   ```python
   openai.api_key = "YOUR_API_KEY"
   ```

## Usage

Run the application:
```sh
main.py
```

## File Overview

- **main.py**: Contains the GUI implementation using PyQt6. Handles user interactions and displays chat messages.
- **backend.py**: Contains the `Chatbot` class that communicates with the OpenAI API to get responses.

## Contributing
Feel free to fork the repository and submit pull requests. For major changes, please open an issue first to discuss what you would like to change.

## License
This project is licensed under the MIT License.
