<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Machine Downtime Prediction API</title>
</head>
<body>
    <h1>Machine Downtime Prediction API</h1>

    <h2>Overview</h2>
    <p>The Machine Downtime Prediction API provides a service for predicting potential machine downtimes based on various features such as temperature, leakage, and electricity usage. This system uses a machine learning model to forecast whether a machine will experience downtime on the following day, empowering businesses to perform preventive maintenance and optimize their operations.</p>

    <p>This system is designed for ease of use and efficiency, providing RESTful API endpoints to upload data, train models, and predict downtime with real-time inputs. The predictions help businesses take proactive measures to avoid unexpected downtimes and improve the overall maintenance process.</p>

    <h2>Features</h2>
    <ul>
        <li><strong>Upload Dataset:</strong> Users can upload a CSV file containing the historical machine data.</li>
        <li><strong>Train the Model:</strong> Allows training the machine learning model based on the uploaded dataset.</li>
        <li><strong>Predict Downtime:</strong> Users can send feature data (temperature, leakage, electricity) for predicting whether the machine will experience downtime.</li>
        <li><strong>Real-time Prediction:</strong> Instant predictions for new data sent via API calls.</li>
        <li><strong>Confidence Score:</strong> Each prediction comes with a confidence score indicating the likelihood of the downtime.</li>
        <li><strong>Easy Deployment:</strong> Built using FastAPI, making it easy to deploy the service for real-time use.</li>
    </ul>

    <h2>Technologies Used</h2>
    <ul>
        <li>Python (FastAPI, scikit-learn, pandas)</li>
        <li>Machine Learning for downtime prediction model</li>
        <li>FastAPI for creating the API service</li>
        <li>Uvicorn for serving the FastAPI application</li>
        <li>Streamlit (for optional dashboard interface, if desired)</li>
    </ul>

    <h2>Project Structure</h2>
    <pre>
Machine Downtime Prediction API
├── app/
│   ├── main.py                 - FastAPI app for prediction and training
│   ├── model.pkl               - Trained machine learning model for prediction
│   ├── requirements.txt        - Python dependencies for the project
├── data/
│   └── cleaned_machine_failure_data.csv   - Sample cleaned dataset for training and testing
├── notebooks/                   
|   └── data_exploration  - Jupyter notebook for model training and exploration
├── README.md                   - Project documentation (this file)
└── .gitignore                  - Git ignore file for unnecessary files
</pre>

    <h2>Installation</h2>
    <p>Clone the repository:</p>
    <pre><code>git clone https://github.com/your-repo-url.git
cd Machine-Downtime-Prediction-API
</code></pre>
    <p>Install the dependencies:</p>
    <pre><code>pip install -r app/requirements.txt</code></pre>

    <h2>Usage</h2>
    <p>To start the FastAPI server, use the following command:</p>
    <pre><code>uvicorn app.main:app --reload</code></pre>
    <p>This will start the FastAPI server, and you can access the API at <a href="http://127.0.0.1:8000">http://127.0.0.1:8000</a>.</p>

    <h2>API Endpoints</h2>

    <h3>1. Upload Dataset</h3>
    <p><strong>URL:</strong> /upload</p>
    <p><strong>Method:</strong> POST</p>
    <p><strong>Description:</strong> Upload a CSV file containing the machine data (columns like temperature, leakage, electricity, etc.).</p>
    <pre>curl -X POST -F "file=@your_dataset.csv" http://127.0.0.1:8000/upload</pre>

    <h3>2. Train the Model</h3>
    <p><strong>URL:</strong> /train</p>
    <p><strong>Method:</strong> POST</p>
    <p><strong>Description:</strong> Train the model with the uploaded dataset. Ensure the dataset is uploaded before training the model.</p>
    <pre>curl -X POST http://127.0.0.1:8000/train</pre>

    <h3>3. Make a Prediction</h3>
    <p><strong>URL:</strong> /predict</p>
    <p><strong>Method:</strong> POST</p>
    <p><strong>Description:</strong> Send a JSON object with features to predict machine downtime.</p>
    <pre>curl -X POST "http://127.0.0.1:8000/predict" -H "Content-Type: application/json" -d "{\"Min_Temp\": 12.5, \"Max_Temp\": 32.1, \"Leakage\": 1.5, \"Electricity\": 8.5}"</pre>

    <h2>Example Responses</h2>

    <h3>For /predict endpoint:</h3>
    <p>If the prediction is "No" downtime with 100% confidence, you will receive the following response:</p>
    <pre>
    {
      "Downtime": "No",
      "Confidence": 1.0
    }
    </pre>

    <p>If the prediction is "Yes" downtime with a different confidence score:</p>
    <pre>
    {
      "Downtime": "Yes",
      "Confidence": 0.87
    }
    </pre>

    <h2>Troubleshooting</h2>

    <h3>Error: "JSON decode error"</h3>
    <p>Ensure the request body is valid JSON format. For example:</p>
    <pre>
    {
      "Min_Temp": 12.5,
      "Max_Temp": 32.1,
      "Leakage": 1.5,
      "Electricity": 8.5
    }
    </pre>

    <h3>Error: "Model not trained"</h3>
    <p>Ensure that you have uploaded the dataset and trained the model before making predictions.</p>

    <h2>License</h2>
    <p>This project is licensed under the MIT License - see the <a href="LICENSE">LICENSE</a> file for details.</p>
</body>
</html>
