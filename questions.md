1. Ниже представлен код, опишите какие уязвимости содержатся в нем и как их можно эксплуатировать. Дайте рекомендации по их исправлению.

```html
<body>
    <input type="text" id="userInput" placeholder="Write a message:">
    <button id="submitButton">Отправить</button>
    <div id="displayArea"></div>

    <script>
        document.addEventListener('DOMContentLoaded', function () {document.getElementById('submitButton').addEventListener('click', validateAndDisplay);
        });
        function validateAndDisplay() {
            var userInput = document.getElementById('userInput').value;
            var displayArea = document.getElementById('displayArea');
	    displayArea.innerHTML = "Ur input: " + userInput;
        }
    </script>
</body>
```
***

2. Ниже представлена конфигурация CSP для домена secure-shop.shop. Опишите недостатки ее конфигурации и способы улучшения.
```
Content-Security-Policy: default-src 'self' https://trusted-plugins.com; script-src 'self' 'unsafe-inline' https://cdn.example.com; style-src 'self' 'unsafe-inline'; img-src *; connect-src 'self' https://api.example.com;
```

***

3. Ниже представлен python код, содержащий уязвимости серверной стороны. Необходимо описать данную уязвимость, способы ее эксплуатации и предложить способы решения и устранения данной уязвимости.
```python
from flask import Flask, request, render_template_string
app = Flask(__name__)

def create_greeting(name):
    template = f"<p>Hello, {name}! You are welcome.</p>"
    return template

@app.route('/')
def index():
    name = request.args.get('name', 'anon')
    greeting_template = create_greeting(name)
    return render_template_string(greeting_template)

if __name__ == "__main__":
    app.run(debug=True)
```
***
4. Вы анализируете следующий фрагмент кода веб-приложения, разработанного на Node.js, который отвечает за аутентификацию пользователей:
```js
app.post('/', function (request, response) {
    const userLogin = request.body.username.replace('"', '');
    const userPassword = crypto.createHash('sha1').update(request.body.password).digest('hex');

    if ( userLogin.length > 0 && userPassword.length > 0 ) {
        db.execute(`SELECT * FROM users WHERE (username="${userLogin}") AND (password = "${userPassword}")`)
        .then(([resultRows, fieldAttributes]) => {
            if ( resultRows.length > 0 ) {
                response.send("Logged in!");
                logger.info(`User ${userLogin} logged in successfully.`);
            }
        })
        .catch((error) => {   
            logger.error('Error executing query:', error);
        });
    }
})
```
1. **Найти и описать уязвимости** в представленном коде. 
2. **Предложить способы устранения** обнаруженных уязвимостей с учетом лучших практик безопасной разработки.