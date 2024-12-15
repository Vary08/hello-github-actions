water_monitoring_app/
    app.py
    templates/
        index.html
    static/
        style.css
 from flask import Flask, render_template, request, redirect, url_for

app = Flask(__name__)

# Список для хранения данных о качестве воды
water_data = []

@app.route('/')
def index():
    return render_template('index.html', water_data=water_data)

@app.route('/submit', methods=['POST'])
def submit():
    # Получаем данные из формы
    data = request.form['data']
    water_data.append(data)  # Добавляем данные в список
    return redirect(url_for('index'))

if __name__ == '__main__':
    app.run(debug=True)
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="{{ url_for('static', filename='style.css') }}">
    <title>Мониторинг качества воды</title>
</head>
<body>
    <h1>Мониторинг качества сточных вод</h1>

    <form action="/submit" method="post">
        <label for="data">Введите данные о качестве воды:</label>
        <input type="text" id="data" name="data" required>
        <button type="submit">Отправить</button>
    </form>

    <h2>Данные о качестве воды:</h2>
    <ul>
        {% for record in water_data %}
            <li>{{ record }}</li>
        {% endfor %}
    </ul>
</body>
</html>
body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    margin: 0;
    padding: 20px;
}

h1 {
    color: #333;
}

form {
    margin: 20px 0;
}

input[type="text"] {
    padding: 10px;
    width: 300px;
    margin-right: 10px;
}

button {
    padding: 10px;
}

ul {
    list-style: none;
    padding: 0;
}

li {
    background-color: #fff;
    margin: 5px 0;
    padding: 10px;
    border: 1px solid #ddd;
}




