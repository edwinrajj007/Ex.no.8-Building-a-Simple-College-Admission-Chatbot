
# EX.NO.8 – BUILDING A SIMPLE COLLEGE ADMISSION CHATBOT

## AIM

To design, implement, and test a simple rule-based chatbot in Python that answers frequently asked questions related to college admissions, such as courses offered, eligibility criteria, fees, application process, required documents, important dates, hostel facilities, and contact details.

---

# INTRODUCTION

A chatbot is a software application that simulates a conversation with a human user, typically through text or voice. Chatbots are widely used in websites, customer support systems, educational platforms, banking applications, and other services to provide quick responses to frequently asked questions.

A **rule-based chatbot** is one of the simplest types of conversational systems. It works by comparing the user's input against a predefined collection of keywords, phrases, or patterns. When a matching pattern is identified, the chatbot selects and returns a suitable pre-written response.

Unlike modern AI chatbots that may use machine learning and large language models, a rule-based chatbot does not require a large training dataset or complex model. This makes it an excellent beginner-friendly project for understanding the basic concepts behind conversational systems.

In this experiment, a **College Admission Chatbot** is developed using Python. The chatbot acts as a virtual help-desk assistant that can answer common questions from prospective students.

The chatbot can provide information about:

* Courses offered
* Eligibility criteria
* Admission fees
* Application procedure
* Required documents
* Important admission dates
* Hostel facilities
* Contact information
* Greetings and goodbyes

The project demonstrates the basic workflow of a conversational system:

**User Input → Pattern Matching → Intent Identification → Response Selection → Chatbot Output**

---

# OBJECTIVES

The major objectives of this experiment are:

1. To understand the basic concept of a rule-based chatbot.
2. To implement a chatbot using Python.
3. To create a knowledge base containing admission-related information.
4. To identify user intentions using keywords and patterns.
5. To use regular expressions for pattern matching.
6. To generate appropriate responses based on identified intents.
7. To implement an interactive conversation loop.
8. To test the chatbot using sample queries.
9. To understand the limitations of rule-based conversational systems.

---

# REQUIREMENTS

## Software Requirements

* Python 3.x
* Python IDLE / VS Code / Jupyter Notebook / any Python IDE
* Operating system such as Windows, Linux, or macOS

## Python Libraries

### 1. re

The `re` module is Python's regular expression library. It is used to search for keywords and patterns in the user's input.

### 2. random

The `random` module is used to randomly select one response when an intent contains multiple possible responses.

This makes repeated conversations less repetitive.

---

# PAGE 1 – BASIC CONCEPT OF THE CHATBOT

## WORKING PRINCIPLE

The chatbot follows a simple rule-based architecture.

### Step 1: User Input

The user enters a question such as:

"Which courses are available?"

### Step 2: Preprocessing

The input is converted into lowercase so that matching is not affected by capitalization.

For example:

"Which COURSES are available?"

becomes:

"which courses are available?"

### Step 3: Pattern Matching

The chatbot compares the user's input against predefined patterns such as:

* course
* courses
* programs
* branches
* degree

### Step 4: Intent Identification

If a matching pattern is found, the chatbot identifies the corresponding intent.

For example:

**Input:** "Which courses are available?"

**Intent:** `courses`

### Step 5: Response Generation

The chatbot selects an appropriate response from the response list associated with the `courses` intent.

### Step 6: Display Output

The response is displayed to the user.

---

# PAGE 2 – PROCEDURE

# PROCEDURE

## STEP 1: IMPORT REQUIRED LIBRARIES

The first step is to import the required Python libraries.

The chatbot uses two libraries:

### `re`

Python's regular expression module is used to search for keyword patterns inside the user's message.

### `random`

The `random` module is used to randomly select one response when multiple responses are available for the same intent.

### Code

```python
import re
import random
```

The use of these libraries keeps the chatbot simple while providing the required functionality.

---

# STEP 2: DESIGN THE KNOWLEDGE BASE

The knowledge base contains the information required by the chatbot.

It is stored using a Python dictionary.

Each intent contains two major components:

1. **Patterns** – words or phrases that may appear in the user's question.
2. **Responses** – possible answers associated with that intent.

For example:

```python
"courses": {
    "patterns": ["course", "courses", "program", "branch"],
    "responses": [
        "We offer undergraduate and postgraduate courses."
    ]
}
```

When the user asks about courses, the chatbot searches for matching patterns.

## KNOWLEDGE BASE INTENTS

The chatbot can contain the following major intents:

| Intent      | Example Keywords                     | Purpose                        |
| ----------- | ------------------------------------ | ------------------------------ |
| Greeting    | hello, hi, hey                       | Welcome the user               |
| Courses     | course, courses, programs            | Provide course information     |
| Eligibility | eligibility, eligible, qualification | Explain admission requirements |
| Fees        | fees, fee, tuition, cost             | Provide fee information        |
| Application | apply, application, admission        | Explain application procedure  |
| Documents   | documents, certificates, papers      | List required documents        |
| Dates       | date, deadline, last date            | Provide important dates        |
| Hostel      | hostel, accommodation                | Provide hostel information     |
| Contact     | contact, phone, email                | Provide contact details        |
| Goodbye     | bye, exit, quit                      | End the conversation           |

The dictionary-based structure makes the chatbot easy to modify and expand.

---

# PAGE 3 – KNOWLEDGE BASE AND INTENTS

## KNOWLEDGE BASE SUMMARY

A simplified knowledge base can be organized as follows:

### Greeting Intent

**Patterns:**

* hi
* hello
* hey
* good morning

**Responses:**

* "Hello! How can I help you with college admissions?"
* "Welcome! What admission information do you need?"

---

### Courses Intent

**Patterns:**

* course
* courses
* programs
* branches

**Responses:**

* "Our college offers several undergraduate and postgraduate programs."
* "Please contact the admission office for the current list of available courses."

---

### Eligibility Intent

**Patterns:**

* eligibility
* eligible
* qualification
* requirements

**Responses:**

* "Eligibility requirements depend on the course and admission category."
* "Please check the admission requirements for your selected program."

---

### Fees Intent

**Patterns:**

* fee
* fees
* tuition
* cost

**Responses:**

* "Fee structure varies according to the selected course."
* "Please contact the admission office for the latest fee details."

---

### Application Intent

**Patterns:**

* apply
* application
* admission
* register

**Responses:**

* "Applications can be submitted through the college admission process."
* "Please follow the official admission procedure to apply."

---

### Documents Intent

**Patterns:**

* documents
* certificates
* papers
* required documents

**Responses:**

* "Common documents include academic certificates, identification documents, photographs, and other required certificates."

---

### Dates Intent

**Patterns:**

* date
* deadline
* last date
* admission date

**Responses:**

* "Please check the official admission notice for the latest important dates."

---

### Hostel Intent

**Patterns:**

* hostel
* accommodation
* residence

**Responses:**

* "Hostel facilities may be available for eligible students. Please contact the college for current availability and details."

---

### Contact Intent

**Patterns:**

* contact
* phone
* email
* admission office

**Responses:**

* "Please contact the college admission office for further assistance."

---

### Goodbye Intent

**Patterns:**

* bye
* goodbye
* exit
* quit

**Responses:**

* "Thank you for contacting us. Goodbye!"
* "Goodbye! Have a great day."

---

# PAGE 4 – INTENT MATCHING

# STEP 3: FUNCTION TO MATCH USER INPUT TO AN INTENT

The `match_intent()` function is responsible for identifying the topic of the user's question.

The function performs the following operations:

1. Receives the user's message.
2. Converts the message to lowercase.
3. Iterates through all intents in the knowledge base.
4. Searches for matching patterns using `re.search()`.
5. Returns the matching intent.
6. Returns `None` if no pattern is found.

### Code

```python
def match_intent(user_input):
    user_input = user_input.lower()

    for intent, data in knowledge_base.items():
        for pattern in data["patterns"]:
            if re.search(pattern, user_input):
                return intent

    return None
```

## Explanation

### `user_input.lower()`

Converts the input to lowercase.

For example:

```text
"WHAT COURSES DO YOU OFFER?"
```

becomes:

```text
"what courses do you offer?"
```

This allows the chatbot to match words regardless of capitalization.

### `knowledge_base.items()`

This accesses every intent and its associated data.

### `re.search()`

The regular expression function searches the user's message for the specified pattern.

If the pattern is found, the corresponding intent is returned.

### `return None`

If none of the predefined patterns match the user's message, the function returns `None`.

This allows the chatbot to use a fallback response.

---

# STEP 4: DEFINE THE CHATBOT RESPONSE FUNCTION

The `get_response()` function generates the chatbot's final response.

It performs two main operations:

1. Identifies the user's intent.
2. Selects a response for that intent.

### Code

```python
def get_response(user_input):
    intent = match_intent(user_input)

    if intent:
        return random.choice(knowledge_base[intent]["responses"])

    return "Sorry, I didn't understand your question. Please try again."
```

## Explanation

The function first calls:

```python
match_intent(user_input)
```

to determine what the user is asking.

If an intent is found, `random.choice()` selects one response from the corresponding response list.

If no intent is found, the chatbot displays a fallback message.

### Example

**User:**

"How much are the fees?"

**Identified intent:**

`fees`

**Chatbot:**

"Fee structure varies according to the selected course."

---

# PAGE 5 – INTERACTIVE CHATBOT

# STEP 5: BUILD THE INTERACTIVE CONVERSATION LOOP

The chatbot needs a mechanism to continuously receive messages from the user.

Python's `input()` function is used for this purpose.

### Code

```python
def chat():
    print("College Admission Chatbot")
    print("Type 'bye', 'exit', or 'quit' to end the conversation.")

    while True:
        user_input = input("You: ")

        response = get_response(user_input)
        print("Bot:", response)

        if match_intent(user_input) == "goodbye":
            break
```

## Working

The chatbot first displays a welcome message.

The `while True` loop continuously accepts user input.

For every message:

**User Input → get_response() → Chatbot Response**

The conversation continues until the user enters a message that matches the `goodbye` intent.

For example:

```text
You: Hello
Bot: Hello! How can I help you with college admissions?

You: What courses do you offer?
Bot: Our college offers several undergraduate and postgraduate programs.

You: Bye
Bot: Thank you for contacting us. Goodbye!
```

The `break` statement terminates the loop.

---

# PAGE 6 – TESTING THE CHATBOT

# STEP 6: TEST THE CHATBOT WITH SAMPLE QUERIES

Testing is an important part of software development.

A list of realistic questions can be used to check whether the chatbot correctly identifies every intent.

### Example

```python
sample_queries = [
    "Hello",
    "What courses are offered?",
    "What is the eligibility?",
    "How much are the fees?",
    "How can I apply?",
    "What documents are required?",
    "When is the admission deadline?",
    "Do you have hostel facilities?",
    "How can I contact the admission office?",
    "Bye"
]

for query in sample_queries:
    print("You:", query)
    print("Bot:", get_response(query))
    print()
```

This method makes it possible to test the chatbot automatically without manually entering every question.

---

# TEST CASES

| Test Case | User Query                  | Expected Intent |
| --------- | --------------------------- | --------------- |
| 1         | Hello                       | Greeting        |
| 2         | What courses are available? | Courses         |
| 3         | Am I eligible?              | Eligibility     |
| 4         | What are the fees?          | Fees            |
| 5         | How do I apply?             | Application     |
| 6         | What documents do I need?   | Documents       |
| 7         | What is the last date?      | Dates           |
| 8         | Is hostel available?        | Hostel          |
| 9         | How can I contact you?      | Contact         |
| 10        | Bye                         | Goodbye         |

The test results help verify that the predefined patterns correctly represent the intended categories.

---

# STEP 7: RUN THE CHATBOT

The complete Python script is executed after creating the knowledge base, intent-matching function, response function, and interactive chat loop.

The sample queries can be executed first to verify each intent.

After testing, the `chat()` function can be executed to start a real-time conversation.

### Example

```python
chat()
```

The chatbot then waits for user input.

---

# PAGE 7 – OUTPUT AND ANALYSIS

# OUTPUT

## SAMPLE CONVERSATION OUTPUT – PART 1

The chatbot correctly identifies common admission-related questions.

### Sample Interaction

```text
College Admission Chatbot
Type 'bye', 'exit', or 'quit' to end the conversation.

You: Hello
Bot: Hello! How can I help you with college admissions?

You: What courses are offered?
Bot: Our college offers several undergraduate and postgraduate programs.

You: What is the eligibility?
Bot: Eligibility requirements depend on the course and admission category.

You: What are the fees?
Bot: Fee structure varies according to the selected course.

You: How can I apply?
Bot: Please follow the official admission procedure to apply.
```

The output demonstrates that the chatbot can identify different intents based on keywords contained in the user's questions.

---

## SAMPLE CONVERSATION OUTPUT – PART 2

The remaining admission-related questions can also be tested.

```text
You: What documents are required?
Bot: Common documents include academic certificates and identification documents.

You: When is the last date?
Bot: Please check the official admission notice for the latest important dates.

You: Is hostel available?
Bot: Hostel facilities may be available for eligible students.

You: How can I contact the admission office?
Bot: Please contact the college admission office for further assistance.

You: Bye
Bot: Thank you for contacting us. Goodbye!
```

When the user enters "Bye", the chatbot identifies the `goodbye` intent and terminates the conversation.

---

# RESULT ANALYSIS

The chatbot successfully performs the basic tasks for which it was designed.

### Observations

1. The chatbot recognizes predefined keywords.
2. It identifies the user's intent.
3. It provides an appropriate predefined response.
4. Multiple responses can be randomly selected.
5. The chatbot can handle a continuous conversation.
6. A fallback response is provided for unknown questions.
7. The chatbot can be easily extended by adding new intents.

---

# PAGE 8 – ADVANTAGES, LIMITATIONS AND CONCLUSION

# ADVANTAGES

## 1. Simple Implementation

The chatbot can be implemented using basic Python concepts.

## 2. Easy to Understand

The rule-based approach is suitable for beginners learning chatbot development.

## 3. Low Computational Requirement

No large machine-learning model or training dataset is required.

## 4. Fast Response

Since the chatbot searches predefined patterns, responses can be generated quickly.

## 5. Easy to Modify

New admission-related topics can be added by modifying the knowledge base.

## 6. Predictable Responses

Because responses are predefined, the developer has control over what the chatbot says.

---

# LIMITATIONS

Although the chatbot works for predefined questions, it has several limitations.

### 1. Limited Understanding

The chatbot does not truly understand language in the same way as advanced AI systems.

### 2. Keyword Dependence

If the user uses a word or phrase that is not included in the knowledge base, the chatbot may fail to identify the correct intent.

### 3. No Learning

The basic chatbot does not automatically learn from previous conversations.

### 4. Limited Context

The chatbot may not remember previous questions and may have difficulty handling follow-up questions.

### 5. Fixed Responses

The responses are predefined rather than dynamically generated.

### 6. Ambiguous Questions

A question containing multiple topics may be incorrectly classified if several keywords are present.

---

# FUTURE ENHANCEMENTS

The basic chatbot can be improved in several ways.

### Natural Language Processing

NLP techniques can be introduced to improve language understanding.

### Machine Learning

Machine-learning-based intent classification can allow the chatbot to recognize more variations of user questions.

### Database Integration

A database can be connected to store:

* Course information
* Fee structures
* Admission dates
* Seat availability
* Hostel information

### Web Interface

The chatbot can be integrated into a college website.

### Voice Interaction

Speech recognition and text-to-speech technologies can be added to enable voice-based interaction.

### Advanced AI

Modern AI models can be integrated to provide more flexible and context-aware conversations.

---

# CONCLUSION

Thus, a simple rule-based **College Admission Chatbot** was successfully designed, implemented, and tested using Python.

The chatbot uses a keyword- and pattern-based knowledge base to identify the intent behind a user's question and provide an appropriate predefined response. It can answer common admission-related queries covering courses, eligibility, fees, application procedures, required documents, important dates, hostel facilities, and contact information.

The experiment demonstrates the fundamental building blocks of a conversational system:

**Knowledge Base → Intent Matching → Response Generation → Interactive Conversation**

The use of Python's `re` module enables pattern matching, while the `random` module allows different responses to be selected for the same intent. The interactive loop allows users to communicate with the chatbot in real time.

Although a rule-based chatbot has limitations in understanding complex language and maintaining conversation context, it provides a strong foundation for learning chatbot development. More advanced systems can extend this basic architecture using Natural Language Processing, machine learning, databases, web interfaces, and modern AI models.


