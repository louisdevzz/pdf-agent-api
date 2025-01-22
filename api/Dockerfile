# Sử dụng base image Python
FROM python:3.9-slim

# Thiết lập thư mục làm việc
WORKDIR /app

# Copy file requirements vào container
COPY requirements.txt .

# Cài đặt các thư viện Python
RUN pip install --no-cache-dir -r requirements.txt

# Copy mã nguồn vào container
COPY . .

# Expose port cho API
EXPOSE 8000

# Khởi chạy API
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]