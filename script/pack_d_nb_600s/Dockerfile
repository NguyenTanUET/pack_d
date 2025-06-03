# --- STEP 1: Chọn base image
FROM python:3.10-slim

# --- STEP 2: Thiết lập working directory bên trong container
WORKDIR /app

# --- STEP 3: Copy requirements và cài dependencies
# (đường dẫn tính từ build context = thư mục "pack_d/")
COPY script/pack_d_nb_600s/requirements.txt .

RUN pip install --upgrade pip \
 && pip install --no-cache-dir -r requirements.txt \
 && pip install --no-cache-dir google-cloud-storage

# --- STEP 4: Copy source code và data vào container
COPY script/pack_d_nb_600s/rcpsp_pack_d_nb_600s.py .
COPY data ./data
COPY result ./result

# --- STEP 5: Bật chế độ in log ngay ra stdout
ENV PYTHONUNBUFFERED=1

# Khi container khởi, nó sẽ tự chạy script chính
CMD ["bash", "-lc", "\
    echo '>>> Container started, running RCPSP batch...'; \
    python rcpsp_pack_d_nb_600s.py; \
    echo '>>> rcpsp_pack_d_nb_600s.py done'; \
    echo '>>> All scripts done, exiting.' \
"]
