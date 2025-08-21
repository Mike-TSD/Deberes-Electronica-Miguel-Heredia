# Deberes-Electronica-Miguel-Heredia
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Actividades de Electrónica – Miguel Heredia</title>
  <style>
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background-color: #f5f5f5;
      margin: 0;
      padding: 0;
      color: #222;
    }
    header {
      background-color: #00796b;
      color: white;
      padding: 20px;
      text-align: center;
    }
    nav {
      display: flex;
      justify-content: center;
      background-color: #4db6ac;
    }
    nav button {
      background: none;
      border: none;
      padding: 15px 25px;
      cursor: pointer;
      font-weight: bold;
      font-size: 16px;
      color: #004d40;
      transition: background 0.3s;
    }
    nav button:hover {
      background: #b2dfdb;
    }
    nav button.active {
      border-bottom: 3px solid #004d40;
    }
    section {
      display: none;
      max-width: 900px;
      margin: 20px auto;
      padding: 20px;
      background-color: white;
      border-radius: 10px;
      box-shadow: 0 3px 8px rgba(0,0,0,0.1);
      opacity: 0;
      transform: translateY(20px);
      transition: opacity 0.5s ease, transform 0.5s ease;
    }
    section.active {
      display: block;
      opacity: 1;
      transform: translateY(0);
    }
    h1, h2, h3 {
      color: #004d40;
    }
    pre {
      background-color: #e0f2f1;
      padding: 10px;
      border-radius: 8px;
      overflow-x: auto;
    }
    footer {
      background-color: #00796b;
      color: white;
      text-align: center;
      padding: 10px;
      margin-top: 30px;
    }
  </style>
</head>
<body>
  <header>
    <h1>Proyecto Práctico de Electrónica – Miguel Heredia</h1>
    <p>Aplicación de conceptos de Arduino y circuitos básicos</p>
  </header>

  <nav>
    <button class="tab-btn active" data-tab="intro">Introducción</button>
    <button class="tab-btn" data-tab="act1">Actividad 1</button>
    <button class="tab-btn" data-tab="act2">Actividad 2</button>
    <button class="tab-btn" data-tab="act3">Actividad 3</button>
    <button class="tab-btn" data-tab="act4">Actividad 4</button>
    <button class="tab-btn" data-tab="act5">Actividad 5</button>
  </nav>

  <section id="intro" class="active">
    <h2>Bienvenida</h2>
    <p>En esta página se presentan las actividades prácticas de la asignatura de Electrónica. 
    Cada actividad permite aplicar conceptos de programación con Arduino y el manejo de componentes básicos de circuitos.</p>
  </section>

  <section id="act1">
    <h3>Actividad 1: Patrón de LEDs</h3>
    <p><strong>Objetivo:</strong> Aprender a controlar múltiples LEDs usando bucles <code>for</code> y <code>while</code>.</p>
    <pre><code>
// Código Arduino: Secuencia de LEDs
for (int pin = 2; pin <= 8; pin++) {
  digitalWrite(pin, HIGH);
  delay(200);
  digitalWrite(pin, LOW);
}

int i = 2;
while (i <= 8) {
  digitalWrite(i, HIGH);
  delay(200);
  digitalWrite(i, LOW);
  i++;
}
    </code></pre>
  </section>

  <section id="act2">
    <h3>Actividad 2: Sensor Ultrasónico con LED y Alarma</h3>
    <p><strong>Objetivo:</strong> Medir distancia con HC-SR04 y activar LED o buzzer según la medición.</p>
    <pre><code>
const int trigPin = 9;
const int echoPin = 10;
const int ledPin = 3;
const int buzzerPin = 4;
long duration;
int distance;

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(ledPin, OUTPUT);
  pinMode(buzzerPin, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2;

  if (distance > 100) {
    digitalWrite(ledPin, HIGH);
    digitalWrite(buzzerPin, LOW);
  } else {
    digitalWrite(ledPin, LOW);
    digitalWrite(buzzerPin, HIGH);
  }
}
    </code></pre>
  </section>

  <section id="act3">
    <h3>Actividad 3: Pantalla LCD</h3>
    <p><strong>Objetivo:</strong> Mostrar mensajes en una pantalla LCD 16x2 usando comunicación I2C.</p>
    <pre><code>
#include &lt;Wire.h&gt;
#include &lt;LiquidCrystal_I2C.h&gt;
LiquidCrystal_I2C lcd(0x27, 16, 2);

void setup() {
  lcd.init();
  lcd.backlight();
  lcd.setCursor(0,0);
  lcd.print("Hola Mundo!");
  lcd.setCursor(0,1);
  lcd.print("Miguel Heredia");
}

void loop() {}
    </code></pre>
  </section>

  <section id="act4">
    <h3>Actividad 4: Distancia en LCD</h3>
    <p><strong>Objetivo:</strong> Mostrar la distancia medida en tiempo real en la pantalla LCD.</p>
    <pre><code>
#include &lt;Wire.h&gt;
#include &lt;LiquidCrystal_I2C.h&gt;
LiquidCrystal_I2C lcd(0x27, 16, 2);
const int trigPin = 9;
const int echoPin = 10;
long duration;
int distance;

void setup() {
  lcd.init();
  lcd.backlight();
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
}

void loop() {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2;

  lcd.clear();
  lcd.setCursor(0,0);
  lcd.print("Distancia:");
  lcd.setCursor(0,1);
  lcd.print(distance);
  lcd.print(" cm");
  delay(500);
}
    </code></pre>
  </section>

  <section id="act5">
    <h3>Actividad 5: Simulación de Login</h3>
    <p><strong>Objetivo:</strong> Verificar usuario y contraseña en el monitor serie de Arduino.</p>
    <pre><code>
String user;
String pass;

void setup() {
  Serial.begin(9600);
  Serial.println("Ingrese usuario:");
}

void loop() {
  if (Serial.available() > 0) {
    user = Serial.readStringUntil('\n');
    Serial.println("Ingrese clave:");
    while (Serial.available() == 0) {}
    pass = Serial.readStringUntil('\n');

    if (user == "miguel" && pass == "1234") {
      Serial.println("Acceso permitido!");
    } else {
      Serial.println("Usuario o clave incorrecta");
    }
  }
}
    </code></pre>
  </section>

  <footer>
    <p>Proyecto Académico – Miguel Heredia &copy; 2025</p>
  </footer>

  <script>
    const buttons = document.querySelectorAll(".tab-btn");
    const sections = document.querySelectorAll("section");

    buttons.forEach(btn => {
      btn.addEventListener("click", () => {
        buttons.forEach(b => b.classList.remove("active"));
        sections.forEach(s => s.classList.remove("active"));

        btn.classList.add("active");
        document.getElementById(btn.dataset.tab).classList.add("active");
      });
    });
  </script>
</body>
</html>
