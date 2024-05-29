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

## main.py
```python
from PyQt6.QtWidgets import QApplication, QMainWindow, QTextEdit, QLineEdit, QPushButton
import sys
from backend import Chatbot
import threading

class ChatbotWindow(QMainWindow):
    def __init__(self):
        super().__init__()
        self.chatbot = Chatbot()
        self.setMinimumSize(700, 500)

        self.chat_area = QTextEdit(self)
        self.chat_area.setGeometry(10, 10, 480, 320)
        self.chat_area.setReadOnly(True)

        self.input_field = QLineEdit(self)
        self.input_field.setGeometry(10, 340, 480, 40)
        self.input_field.returnPressed.connect(self.send_message)

        self.button = QPushButton("Send", self)
        self.button.setGeometry(500, 340, 100, 40)
        self.button.clicked.connect(self.send_message)

        self.show()

    def send_message(self):
        user_input = self.input_field.text().strip()
        self.chat_area.append(f"<p style='color:#333333'>Me: {user_input}</p>")
        self.input_field.clear()
        thread = threading.Thread(target=self.get_bot_response, args=(user_input, ))
        thread.start()

    def get_bot_response(self, user_input):
        response = self.chatbot.get_response(user_input)
        self.chat_area.append(f"<p style='color:#333333; background-color: #E9E9E9'>Bot: {response}</p>")

app = QApplication(sys.argv)
main_window = ChatbotWindow()
sys.exit(app.exec())
```

## backend.py
```python
import openai

class Chatbot:
    def __init__(self):
        openai.api_key = "YOUR_API_KEY"

    def get_response(self, user_input):
        response = openai.Completion.create(
            engine="text-davinci-003",
            prompt=user_input,
            max_tokens=3000,
            temperature=0.5
        ).choices[0].text
        return response

if __name__ == "__main__":
    chatbot = Chatbot()
    response = chatbot.get_response("Write a joke about birds.")
    print(response)
```

## Contributing
Feel free to fork the repository and submit pull requests. For major changes, please open an issue first to discuss what you would like to change.

## License
This project is licensed under the MIT License.
