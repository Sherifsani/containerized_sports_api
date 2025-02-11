# NFL Schedule API

This project showcases the development of a containerized API management system for querying sports data. It utilizes Amazon ECS (Fargate) to run containers, Amazon API Gateway to expose REST endpoints, and an external Sports API for real-time data retrieval. The implementation highlights advanced cloud computing concepts, including API management, container orchestration, and secure AWS integrations.


---



## Features

- Fetches NFL game schedules from Google search results via SerpAPI.
- Scalable and serverless architecture 
- Returns formatted JSON with game details including teams, venue, date, and time.
- Deployed on AWS using **ECS Fargate**, **ALB**, and **API Gateway**.
- Uses **Amazon Elastic Container Registry (ECR)** for secure container storage.
- **CloudWatch Logs** for real-time monitoring and logging.


---


## Architecture
![architecture diagram](https://github.com/Sherifsani/containerized_sports_api/blob/main/diagram.png)



## Technologies Used

- **Flask** – Lightweight web framework
- **SerpAPI** – Google search results API
- **Docker** – Containerization
- **AWS ECS (Fargate)** – Serverless container deployment
- **Amazon ECR** – Private container registry
- **API Gateway** – Exposes API securely
- **Amazon ALB** – Load balancing for ECS service
- **CloudWatch Logs** – Logging and monitoring



---


## Prerequisites

Ensure you have the following installed:

- Python 3.x
- Docker
- AWS account
- An active SerpAPI account (API Key required)



---



## Installation

1. Clone this repository:
   ```sh
   git clone https://github.com/Sherifsani/containerized_sports_api.git
   cd containerized_sports_api
   ```
2. Install dependencies:
   ```sh
   pip install -r requirements.txt
   ```
3. Set up environment variables:
   ```sh
   export SERP_API_KEY=your_serp_api_key
   ```
4. Run the Flask app locally:
   ```sh
   python app.py
   ```


---




## Dockerization

1. Build the Docker image:
   ```sh
   docker build -t nfl-schedule-api .
   ```
2. Run the container:
   ```sh
   docker run -p 8080:8080 -e SERP_API_KEY=your_serp_api_key nfl-schedule-api
   ```

## Deployment on AWS


### Deploying to ECS

1. Authenticate Docker with AWS:
   ```sh
   aws ecr get-login-password --region your-region | docker login --username AWS --password-stdin your-account-id.dkr.ecr.your-region.amazonaws.com
   ```
2. Tag and push the image:
   ```sh
   docker tag nfl-schedule-api your-account-id.dkr.ecr.your-region.amazonaws.com/nfl-schedule-api
   docker push your-account-id.dkr.ecr.your-region.amazonaws.com/nfl-schedule-api
   ```
3. Update ECS task definition and redeploy the service:
   ```sh
   aws ecs update-service --cluster your-cluster-name --service your-service-name --force-new-deployment
   ```

## API Usage

### Endpoint:

```
GET /sports
```

### Sample Response:

```json
{
  "message": "NFL schedule fetched successfully.",
  "games": [
    {
      "away_team": "Dallas Cowboys",
      "home_team": "San Francisco 49ers",
      "venue": "Levi's Stadium",
      "date": "2024-10-10",
      "time": "8:20 PM ET"
    }
  ]
}
```

## Monitoring & Logging

- **CloudWatch** is used for log aggregation.
- **AWS X-Ray** (optional) for request tracing.

## Future Improvements

- Add caching with Redis or DynamoDB.
- Implement authentication via API Gateway.
- Enhance error handling and retry logic.

## License

This project is licensed under the MIT License.

