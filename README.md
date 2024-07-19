# 45import sqlite3
from datetime import datetime

# Connect to SQLite database (or create it if it doesn't exist)
conn = sqlite3.connect('ball_hits.db')
cursor = conn.cursor()

# Create a table to store ball hit records
cursor.execute('''
CREATE TABLE IF NOT EXISTS hits (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    hit_time TEXT NOT NULL
)
''')
conn.commit()

# Function to add a new ball hit record
def add_hit():
    hit_time = datetime.now().strftime('%Y-%m-%d %H:%M:%S')
    cursor.execute('INSERT INTO hits (hit_time) VALUES (?)', (hit_time,))
    conn.commit()
    print(f"Hit recorded at {hit_time}")

# Function to retrieve all ball hit records
def get_hits():
    cursor.execute('SELECT * FROM hits')
    hits = cursor.fetchall()
   
