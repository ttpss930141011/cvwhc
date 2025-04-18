# Use Python 3.9 slim image as base
FROM python:3.9-slim

# Set working directory
WORKDIR /app

# Copy requirements first to leverage Docker cache
COPY requirements.txt .

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application
COPY . .

# Copy model files
COPY robust_scaler.pkl .
COPY model_freq_map.pkl .
COPY logistic_model.pkl .
COPY model_metrics.json .

# Expose the port the app runs on
EXPOSE 8080

# Set environment variables
ENV FLASK_APP=app.py
ENV FLASK_ENV=production

# Command to run the application using gunicorn for production
CMD ["gunicorn", "--bind", "0.0.0.0:8080", "app:app"] 