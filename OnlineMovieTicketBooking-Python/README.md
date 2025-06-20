# 🎬 Movie Booking Web Application

A full-stack web application to manage and book movie tickets with ease. Built using **Flask**, **MySQL**, and **jQuery**.



## 🚀 Features

✅ **User Login**  
🎟️ **Book tickets** by selecting date, movie, time, and seats  
🧑‍💼 **Manager Panel**:
- Add new movies
- Create shows
- View booked tickets
- Modify seat pricing



## 🛠️ Tech Stack

| Layer      | Technology             |
|------------|------------------------|
| Frontend   | HTML, CSS, JavaScript, jQuery |
| Backend    | Python (Flask)         |
| Database   | MySQL                  |



## 📁 Project Structure

```

movie-booking-app/
├── static/
│   └── js/
│       └── script.js            # All frontend JavaScript logic
├── templates/
│   ├── login.html               # Login form
│   ├── dashboard.html           # After login view
│   └── ...                      # Other templates
├── app.py                       # Flask application
├── schema.sql                   # Database schema
└── README.md                    # Project documentation

```



## ⚙️ Prerequisites

- Python 3.x (⚠️ Recommended)
- MySQL Server
- pip (Python package manager)



## 🔧 Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/movie-booking-app.git
cd movie-booking-app
```

# 2. Create MySQL Database

```sql
CREATE DATABASE dbtheatre;
```

Then import the schema:

```bash
mysql -u root -p dbtheatre < dbtheatre.sql
```

### 3. Update DB Credentials in `app.py`

```python
db = mysql.connector.connect(
    host="localhost",
    user="root",
    password="your_mysql_password",   # 🔒 Set your password here
    database="dbtheatre"
)
```

✅ **Make sure to change your MySQL DB password in `app.py` before running the project!**


# 📦 Install Python Dependencies

```bash
pip install flask mysql-connector-python
```



# ▶️ Run the Application

```bash
python app.py
```

🔗 Open your browser and visit:
👉 `http://localhost:5000`



# 🔐 Login Credentials

# 👨‍💼 Manager Login

* **Username**: `manager`
* **Password**: `Password@123`

# 💼 Cashier Login

* **Username**: `cashier`
* **Password**: `cashier123`


# 🤝 Contributing

Contributions are welcome!
Feel free to fork this repository, make changes, and create a pull request.


