# Portfolio-task6
Build a Portfolio Website with Flask
from flask import Flask, render_template_string

app = Flask(__name__)

# HTML templates inside Python
base_html = """
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>{{ title }}</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 0; background: #f4f4f4; }
        header { background: #333; padding: 10px; text-align: center; }
        header a { color: white; margin: 0 15px; text-decoration: none; }
        header a:hover { text-decoration: underline; }
        main { background: white; padding: 20px; max-width: 800px; margin: auto; }
        footer { background: #333; color: white; text-align: center; padding: 10px; }
        img { border-radius: 50%; }
    </style>
</head>
<body>
    <header>
        <nav>
            <a href="/">Home</a>
            <a href="/about">About</a>
            <a href="/projects">Projects</a>
            <a href="/contact">Contact</a>
        </nav>
    </header>

    <main>
        {% block content %}{% endblock %}
    </main>

    <footer>
        <p>© 2025 My Portfolio</p>
    </footer>
</body>
</html>
"""

home_html = """
{% extends "base" %}
{% block content %}
<h1>Welcome to My Portfolio</h1>
<img src="https://via.placeholder.com/150" alt="Profile">
<p>Hi, I’m Shailoo — a software developer passionate about creating things from scratch!</p>
{% endblock %}
"""

about_html = """
{% extends "base" %}
{% block content %}
<h1>About Me</h1>
<p>I am a Python and Flask developer. I enjoy solving problems and building projects.</p>
{% endblock %}
"""

projects_html = """
{% extends "base" %}
{% block content %}
<h1>My Projects</h1>
<ul>
    <li>Portfolio Website in Flask</li>
    <li>Data Analysis Dashboard</li>
    <li>API Development with Flask</li>
</ul>
{% endblock %}
"""

contact_html = """
{% extends "base" %}
{% block content %}
<h1>Contact Me</h1>
<p>Email: example@email.com</p>
<p>LinkedIn: <a href="#">My Profile</a></p>
{% endblock %}
"""

# Register templates
templates = {
    "base": base_html,
    "index": home_html,
    "about": about_html,
    "projects": projects_html,
    "contact": contact_html
}

@app.route("/")
def home():
    return render_template_string(templates["index"], title="Home", **templates)

@app.route("/about")
def about():
    return render_template_string(templates["about"], title="About", **templates)

@app.route("/projects")
def projects():
    return render_template_string(templates["projects"], title="Projects", **templates)

@app.route("/contact")
def contact():
    return render_template_string(templates["contact"], title="Contact", **templates)

if __name__ == "__main__":
    app.run(debug=True)
