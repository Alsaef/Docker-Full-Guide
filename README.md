# 📦 Docker Full Guide (Linux)

এই ডকুমেন্টে Docker-এর সব দরকারি কমান্ড, ব্যাখ্যা, উদাহরণ সহ একদম পরিষ্কার করে দেওয়া হয়েছে।

---

# 🚀 1. Folder এ যাও

```bash
cd your_project_folder
```

👉 এখানে **your_project_folder** মানে তোমার প্রজেক্টের ফোল্ডারের নাম।
উদাহরণ:

```bash
cd frontend
```

---

# 🧱 2. Docker Compose দিয়ে প্রজেক্ট রান

```bash
sudo docker-compose up --build -d
```

#### ব্যাখ্যা:

* `--build` → নতুন করে image বানাবে।
* `-d` → ব্যাকগ্রাউন্ডে container চালাবে।

---

# 📌 3. Running Containers দেখো

```bash
sudo docker ps
```

👉 এটি শুধু **চলমান (running)** containers দেখায়।

---

# ⛔ 4. Container বন্ধ করা

```bash
sudo docker stop <container_name>
```

উদাহরণ:

```bash
sudo docker stop frontend-frontend-1
```

👉 এখানে `frontend-frontend-1` হলো container-এর নাম।
এটা Compose স্বয়ংক্রিয়ভাবে তৈরি করে।

---

# 🔄 5. Container আবার চালু (attached mode)

```bash
sudo docker start -ai <container_id>
```

👉 `-a` = attach, মানে লগ দেখাবে।
👉 `-i` = interactive।

---

# 🔍 6. সব Containers দেখো (running + stopped)

```bash
sudo docker ps -a
```

👉 এখানে running, stopped, exited—সব দেখাবে।

---

# 🗑️ 7. Container Delete

```bash
sudo docker rm <container_name>
```

উদাহরণ:

```bash
sudo docker rm frontend-frontend-1
```

---

# 🗑️ 8. Image Delete

```bash
sudo docker rmi <image_name>
```

উদাহরণ:

```bash
sudo docker rmi frontend-frontend
```

---

# 🛑 9. Docker Compose দিয়ে সব বন্ধ

```bash
sudo docker-compose down
```

👉 সব container + network বন্ধ করবে।

---

# 🧹 10. Full Cleanup

```bash
sudo docker system prune -a
```

👉 **সতর্কতা:** এতে unused container, image, cache সব মুছে যাবে।

---

# 🏗️ 11. A to Z — কিভাবে Docker Image & Container তৈরি হয়

## ✔️ Step 1: Dockerfile তৈরি

```Dockerfile
FROM node:18
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
```

👉 এই Dockerfile Node.js অ্যাপ রান করার নিয়ম শেখায়।

---

## ✔️ Step 2: Image Build

```bash
sudo docker build -t myapp-image .
```

👉 এখানে **myapp-image** এর মতো নাম না দিয়ে নিজের প্রজেক্টের নাম দেওয়া উচিত।

উদাহরণ:

```bash
sudo docker build -t frontend-image .
```

---

## ✔️ Step 3: Container Run

```bash
sudo docker run -d -p 3000:3000 --name frontend-container frontend-image
```

ব্যাখ্যা:

* `-d` → detached mode
* `-p 3000:3000` → Host port : Container port
* `--name frontend-container` → container নাম
* `frontend-image` → image নাম

---

## ✔️ Step 4: Container Log দেখো

```bash
sudo docker logs frontend-container
```

---

## ✔️ Step 5: Container এর ভিতরে ঢুকো

```bash
sudo docker exec -it frontend-container bash
```

---

## ✔️ Step 6: Container বন্ধ করা

```bash
sudo docker stop frontend-container
```

---

## ✔️ Step 7: Container delete

```bash
sudo docker rm frontend-container
```

---

## ✔️ Step 8: Image delete

```bash
sudo docker rmi frontend-image
```

---

# ⚠️ "myapp" কেন লেখা হয়? (স্পেশাল ব্যাখ্যা)

Docker বা tutorial-এ অনেক সময় `myapp`, `myapp-container`, `myapp-image` এই নামগুলো দেখা যায়।

👉 এগুলো **example name**.
👉 তুমি নিজের প্রজেক্টের প্রকৃত নাম বসাবে।

### সঠিক উদাহরণ:

যদি প্রজেক্টের নাম `frontend` হয়—

* Image নাম → `frontend-image`
* Container নাম → `frontend-container`

```bash
sudo docker build -t frontend-image .
sudo docker run -d -p 3000:3000 --name frontend-container frontend-image
```

---

# 📘 Summary Table

| কাজ                  | কমান্ড                   |
| -------------------- | ------------------------ |
| চলমান কন্টেইনার দেখো | `docker ps`              |
| সব কন্টেইনার দেখো    | `docker ps -a`           |
| কন্টেইনার বন্ধ       | `docker stop <name>`     |
| কন্টেইনার চালাও      | `docker start <name>`    |
| কন্টেইনার ডিলিট      | `docker rm <name>`       |
| ইমেজ লিস্ট           | `docker images`          |
| ইমেজ ডিলিট           | `docker rmi <image>`     |
| Compose run          | `docker-compose up -d`   |
| Compose stop         | `docker-compose down`    |
| Full cleanup         | `docker system prune -a` |

---

# 📂 Docker `ps` Command Explained

`docker ps` = currently running container list.

## Basic

```bash
docker ps
```

## Show All

```bash
docker ps -a
```

## Only IDs

```bash
docker ps -q
```

## With size info

```bash
docker ps -s
```

### Example Output

```
CONTAINER ID   IMAGE            STATUS         PORTS         NAMES
91ab23d91ac1   frontend-image   Up 5 minutes   3000->3000    frontend-container
```

---

## Author
**Md Al Saef Ratul**

