# Worker Hiring & Job Search System

A robust full-stack application designed to connect employers with potential employees and streamline the job search process through real-time data integration. This project was developed as part of the **Nighthawk Coding Society**.

## 🚀 Key Features

* **Worker Management:** Employers can register new workers with specific metadata, including programming languages, preferred locations, and internship status.
* **Relevancy Search:** Implements a backend algorithm to find the "Most Relevant Worker" based on skills and location matches.
* **LinkedIn Job Integration:** A personalized job search tool that leverages the **LinkedIn Jobs Search API** via RapidAPI to fetch real-time full-time and internship opportunities.
* **User Authentication:** A secure registration system that stores user data and session state via `localStorage` for personalized experiences.

## 🛠️ Technical Stack

* **Frontend:** HTML5, CSS3, JavaScript (ES6+), and jQuery for asynchronous API calls.
* **Backend:** **Spring Boot (Java)** providing a RESTful API for worker and user management.
* **Infrastructure:** Deployed using **AWS Cloud Infrastructure** to ensure scalability and reliability.
* **External APIs:** LinkedIn Jobs Search API (via RapidAPI).

## 📊 System Architecture



The application follows a standard Client-Server architecture:
1.  **Client Tier:** Handled by a responsive HTML/JS frontend that captures user input and displays job/worker data.
2.  **Logic Tier:** A Spring Boot (Java) REST API that processes business logic, such as filtering "most relevant" workers.
3.  **Data Tier:** Persists user and worker information (integrated with AWS for deployment).

## 🔌 API Endpoints

| Endpoint | Method | Description |
| :--- | :--- | :--- |
| `/api/worker/add` | `POST` | Registers a new worker to the system database. |
| `/api/worker/findMostRelevant` | `POST` | Returns the top 'k' workers matching specific search criteria. |
| `/api/worker/allWorkers` | `GET` | Retrieves a comprehensive list of all registered workers. |
| `/api/v1/users/register` | `POST` | Handles new user registration and authentication logic. |

## 💡 Innovation: AI-Driven Prototyping

During the development of this system, I utilized **Generative AI (Gemini/ChatGPT)** to:
* **Accelerate Implementation:** Rapidly drafted complex fetch logic for seamless API integrations.
* **Optimization:** Debugged and resolved CORS (Cross-Origin Resource Sharing) issues between the local frontend and the AWS-hosted Spring Boot backend.
* **UI/UX Design:** Refined the interface for the job search form and result containers to ensure a clean, user-friendly experience.

## 🏁 Getting Started

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/yourusername/worker-hiring-system.git](https://github.com/yourusername/worker-hiring-system.git)
    ```
2.  **Start the Backend:** Ensure your Spring Boot server is running on `http://localhost:8020`.
3.  **Configure API Keys:** Replace the `X-RapidAPI-Key` in the job search script with your personal key from RapidAPI.
4.  **Open Frontend:** Launch `PersonalizedSkills.html` or `FindEmployees.html` in your browser.
