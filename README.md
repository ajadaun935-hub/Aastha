# Aastha
Website for my school 
school-website/
│── app.py:from flask import Flask, render_template_string, request

app = Flask(__name__)

# Main HTML template
template = """
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Range Hills Public School</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 0; padding: 0; background: #f8f9fa; }
        header { background: #2c3e50; color: white; padding: 15px; display: flex; align-items: center; justify-content: center; }
        header img { height: 60px; margin-right: 15px; }
        nav { background: #34495e; padding: 10px; text-align: center; }
        nav a { color: white; margin: 0 15px; text-decoration: none; font-weight: bold; }
        nav a:hover { text-decoration: underline; }
        section { padding: 20px; min-height: 65vh; }
        footer { background: #2c3e50; color: white; text-align: center; padding: 10px; }
        .gallery { display: flex; flex-wrap: wrap; justify-content: center; }
        .gallery img { width: 250px; height: 180px; object-fit: cover; margin: 10px; border-radius: 10px;
                       box-shadow: 0 2px 6px rgba(0,0,0,0.3); transition: transform 0.2s; }
        .gallery img:hover { transform: scale(1.05); }
        form input, form textarea, form select { display: block; margin: 10px 0; padding: 10px; width: 100%; max-width: 400px; }
        form button { background: #2c3e50; color: white; padding: 10px 20px; border: none; cursor: pointer; border-radius: 5px; }
        form button:hover { background: #1a252f; }
    </style>
</head>
<body>
    <header>
        <img src="/static/logo.png" alt="School Logo">
        <h1>Range Hills Public School</h1>
    </header>
    <nav>
        <a href="/">Home</a>
        <a href="/about">About</a>
        <a href="/gallery">Gallery</a>
        <a href="/admissions">Admissions</a>
        <a href="/contact">Contact</a>
    </nav>
    <section>
        {{ content | safe }}
    </section>
    <footer>
        <p>&copy; 2025 Range Hills Public School. All rights reserved.</p>
    </footer>
</body>
</html>
"""

@app.route("/")
def home():
    return render_template_string(template, content="""
        <h2>Welcome to Range Hills Public School</h2>
        <p>We nurture young minds with knowledge, creativity, and values.</p>
        <img src="/static/school-building.jpg" alt="School Building"
             style="width:100%;max-width:700px;border-radius:10px;
                    box-shadow:0 2px 8px rgba(0,0,0,0.3);margin-top:15px;">
    """)

@app.route("/about")
def about():
    return render_template_string(template, content="""
        <h2>About Us</h2>
        <p>Range Hills Public School was founded with a vision to provide holistic education.</p>
        <h3>Our Vision</h3>
        <p>To create responsible global citizens with wisdom, values, and leadership skills.</p>
        <h3>Facilities</h3>
        <ul>
            <li>Smart Classrooms</li>
            <li>Science & Computer Labs</li>
            <li>Library & Sports Facilities</li>
            <li>Extracurricular Activities</li>
        </ul>
        <hr>
        <h3>Principal's Message</h3>
        <div style="display:flex;align-items:center;gap:20px;flex-wrap:wrap;">
            <img src="/static/principal.jpg" alt="Principal Photo"
                 style="width:200px;height:250px;object-fit:cover;
                        border-radius:10px;box-shadow:0 2px 8px rgba(0,0,0,0.3);">
            <div>
                <p><strong>Dr. A. B. Sharma</strong><br>
                Principal, Range Hills Public School</p>
                <p>“At Range Hills Public School, our mission is to nurture every child’s 
                potential with care, discipline, and innovative teaching methods. 
                We believe in creating leaders who are compassionate, knowledgeable, 
                and ready for the future.”</p>
            </div>
        </div>
    """)

@app.route("/gallery")
def gallery():
    return render_template_string(template, content="""
        <h2>School Gallery</h2>
        <div class="gallery">
            <img src="/static/school-building.jpg" alt="School Building">
            <img src="/static/students-3d-glasses.jpg" alt="Students Activity">
            <img src="/static/school-assembly.jpg" alt="School Assembly">
            <img src="/static/classroom.jpg" alt="Classroom">
            <img src="/static/sports.jpg" alt="Sports Activity">
        </div>
    """)

@app.route("/admissions", methods=["GET", "POST"])
def admissions():
    if request.method == "POST":
        name = request.form.get("name")
        grade = request.form.get("grade")
        email = request.form.get("email")
        message = request.form.get("message")
        return render_template_string(template, content=f"""
            <h2>Admission Form Submitted</h2>
            <p>Thank you, <strong>{name}</strong>. We have received your application for Grade {grade}.</p>
            <p>We will contact you at <strong>{email}</strong>.</p>
            <p>Your Message: {message}</p>
        """)
    return render_template_string(template, content="""
        <h2>Admission Form</h2>
        <form method="POST">
            <input type="text" name="name" placeholder="Student's Full Name" required>
            <select name="grade" required>
                <option value="">Select Grade</option>
                <option value="Nursery">Nursery</option>
                <option value="1">Class 1</option>
                <option value="5">Class 5</option>
                <option value="10">Class 10</option>
                <option value="12">Class 12</option>
            </select>
            <input type="email" name="email" placeholder="Parent's Email" required>
            <textarea name="message" placeholder="Additional Details"></textarea>
            <button type="submit">Submit</button>
        </form>
    """)

@app.route("/contact")
def contact():
    return render_template_string(template, content="""
        <h2>Contact Us</h2>
        <p>Email: info@rangehillspublicschool.com</p>
        <p>Phone: +91-9456667266</p>
        <p>Address: Range Hills Public School, G.T. Road, Aligarh</p>
        <iframe src="https://maps.google.com/maps?q=range%20hills%20school%20aligarh&t=&z=13&ie=UTF8&iwloc=&output=embed" 
                width="100%" height="300" style="border:0;"></iframe>
    """)

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
│── requirements.txt:
flask
gunicorn
│── static/
    │![1000163415](https://github.com/user-attachments/assets/fcfb3190-07da-44ab-996a-800d65537318)
── logo.png![1000163425](https://github.com/user-attachments/assets/c1158cd0-6885-4b66-95b6-772afc1f37a5)

    ![1000163419](https://github.com/user-attachments/assets/d5590719-ea81-4205-b2cf-c44f3ccf420d)
![1000163418](https://github.com/user-attachments/assets/755445d4-0320-4201-9f55-40870936094a)
│── school-building.jpg
    ![1000163423](https://github.com/user-attachments/assets/a1d850b5-07f1-45da-ad16-ad3ffa5de57c)
│── principal.jpg
    ![1000163416](https://github.com/user-attachments/assets/8d29d7de-dfad-4910-9d20-e6d4ba7c2240)
│── students-3d-glasses.jpg
    ![1000163420](https://github.com/user-attachments/assets/0913f25d-4be5-409c-9579-e3333fe1e9db)
![1000163419](https://github.com/user-attachments/assets/ab1a7f39-218a-446b-8304-6adef8dc6719)
│── school-assembly.jpg
![1000163419](https://github.com/user-attachments/assets/8db03c3b-098e-4b6b-a148-0a2b3d7d86a8)
│── classroom.jpg
    ![1000163421](https://github.com/user-attachments/assets/5a3f6e1c-4556-4f16-8c80-beed3dcfc61c)
│── sports.jpg
