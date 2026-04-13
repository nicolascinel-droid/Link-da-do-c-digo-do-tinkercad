#  Sistema de Controle de Temperatura para Vinharia com Arduino

# Descrição

Este projeto tem como objetivo desenvolver um sistema automatizado de controle de temperatura para armazenamento de vinhos, utilizando a plataforma Arduino. A proposta consiste em monitorar continuamente a temperatura do ambiente de uma vinharia e garantir que ela permaneça dentro da faixa ideal para conservação dos vinhos.

O sistema realiza a leitura de sensores de temperatura e, com base nos valores obtidos, pode acionar dispositivos como ventiladores ou sistemas de resfriamento/aquecimento, assegurando condições adequadas para preservar as características e a qualidade do vinho.

Esse tipo de controle é fundamental, pois variações de temperatura podem comprometer o sabor, o aroma e a durabilidade da bebida. Dessa forma, o projeto demonstra, de forma prática, a aplicação da automação e da eletrônica no controle ambiental, sendo uma solução acessível e eficiente para pequenas adegas ou fins educacionais.

# Funcionalidades

- Monitoramento da temperatura em tempo real por meio de sensor
- Controle automático da temperatura do ambiente
- Acionamento de sistema de resfriamento (ex: ventilador) quando a temperatura ultrapassa o limite ideal
- Desligamento automático do sistema quando a temperatura retorna ao nível adequado
- Alerta sonoro por meio de buzzer quando a temperatura está acima do valor recomendado
- Indicação do estado do sistema (ligado/desligado) por meio de LED
- Leitura contínua dos dados para manter a estabilidade térmica

# Componentes Utilizados

- Arduino Uno
- Sensor de temperatura (ex: LM35 ou DHT11)
- Display LCD 16x2
- Buzzer (alarme sonoro)
- LEDs (indicadores de estado)
- Resistores
- Protoboard
- Jumpers (fios de conexão)
- Potenciômetro (para ajuste do contraste do display LCD)

# Funcionamento

O sistema de controle de temperatura funciona por meio da leitura contínua dos dados captados por um sensor de temperatura instalado no ambiente da vinharia. Essas informações são enviadas ao Arduino, que realiza o processamento dos valores em tempo real.

Com base na temperatura medida, o sistema compara os valores com uma faixa considerada ideal para a conservação do vinho. Caso a temperatura ultrapasse o limite estabelecido, o Arduino aciona automaticamente um sistema de resfriamento, como um ventilador, com o objetivo de reduzir a temperatura do ambiente.

Simultaneamente, um buzzer é ativado para emitir um alerta sonoro, indicando que a temperatura está acima do recomendado. Além disso, LEDs são utilizados para sinalizar visualmente o estado do sistema, facilitando a identificação das condições de funcionamento.

O display LCD exibe, em tempo real, os valores de temperatura monitorados, permitindo ao usuário acompanhar continuamente as condições do ambiente.

Quando a temperatura retorna aos níveis ideais, o sistema desativa automaticamente o resfriamento e o alerta sonoro, mantendo o ambiente estável. Dessa forma, o projeto garante um controle eficiente e automatizado, contribuindo para a preservação da qualidade do vinho.

# esquema do circuito 

Acesse a simulação do circuito no link ao lado:https://www.tinkercad.com/things/fqWEfd4NYwY/editel

 # Código do Projeto
#include <LiquidCrystal.h>

LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

int ldrPin = A0;
int ledVerde = 8;
int ledAmarelo = 9;
int ledVermelho = 7;
int buzzer = 6;

int valorLDR = 0;
int porcentagem = 0;

// 🍷 níveis da garrafa
byte g0[8] = {B00100,B00100,B01110,B10001,B10001,B10001,B10001,B01110};
byte g1[8] = {B00100,B00100,B01110,B10001,B10001,B11111,B11111,B01110};
byte g2[8] = {B00100,B00100,B01110,B10001,B11111,B11111,B11111,B01110};
byte g3[8] = {B00100,B00100,B01110,B11111,B11111,B11111,B11111,B01110};

void setup() {
  pinMode(ledVerde, OUTPUT);
  pinMode(ledAmarelo, OUTPUT);
  pinMode(ledVermelho, OUTPUT);
  pinMode(buzzer, OUTPUT);

  lcd.begin(16, 2);

  lcd.createChar(0, g0);
  lcd.createChar(1, g1);
  lcd.createChar(2, g2);
  lcd.createChar(3, g3);

  // 👇 MENSAGEM INICIAL
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Vinheria Agnello");

  lcd.setCursor(0, 1);
  lcd.print("Bem-vindo");

  delay(3000);
  lcd.clear();
}

void loop() {

  // 🔧 FILTRO SIMPLES
  int soma = 0;
  for(int i=0; i<5; i++){
    soma += analogRead(ldrPin);
    delay(5);
  }
  valorLDR = soma / 5;

  porcentagem = map(valorLDR, 0, 1023, 0, 100);

  // RESET LEDs
  digitalWrite(ledVerde, LOW);
  digitalWrite(ledAmarelo, LOW);
  digitalWrite(ledVermelho, LOW);

  String status = "";

  // 🟢 0–30
  if (porcentagem <= 30) {
    digitalWrite(ledAmarelo, HIGH);
    digitalWrite(ledVerde, LOW);
    digitalWrite(ledVermelho, HIGH);
    status = "OK";
  }

  // 🟡 31–70
  else if (porcentagem <= 70) {
    digitalWrite(ledAmarelo, LOW);
    digitalWrite(ledVerde, HIGH);
    digitalWrite(ledVermelho, HIGH);
    status = "ALERTA";
  }

  // 🔴 71–100
  else {
    digitalWrite(ledAmarelo, HIGH);
    digitalWrite(ledVerde, HIGH);
    digitalWrite(ledVermelho, LOW);
    status = "PERIGO";
  }

  // 🔊 BUZZER
  if (porcentagem > 30) {
    digitalWrite(buzzer, HIGH);
  } else {
    digitalWrite(buzzer, LOW);
  }

  // 🍷 nível da garrafa
  int nivel = 0;
  if (porcentagem <= 25) nivel = 0;
  else if (porcentagem <= 50) nivel = 1;
  else if (porcentagem <= 75) nivel = 2;
  else nivel = 3;

  // LCD
  lcd.setCursor(0, 0);
  lcd.print("Luz: ");
  lcd.print(porcentagem);
  lcd.print("%   ");

  lcd.setCursor(0, 1);
  lcd.print(status);
  lcd.print("     ");

  lcd.setCursor(14, 0);
  lcd.write(byte(nivel));

  delay(2000);
}

# Como Executar

1. Monte o circuito conforme a simulação disponibilizada no link do projeto
2. Abra o código na IDE do Arduino
3. Conecte o Arduino Uno ao computador via cabo USB
4. Selecione a porta e a placa correta na IDE
5. Realize o upload do código para o Arduino
6. Após a execução, acompanhe a temperatura exibida no display LCD
7. Observe o acionamento automático do sistema (LED, buzzer e ventilação) conforme a variação da temperatura

# Estrutura do Projeto

- /codigo → contém o código fonte do Arduino
- /imagens → (opcional) imagens do circuito
- README.md → documentação do projeto

# Autores

Nomes: Nícolas Cinel, Luis Fernando, Kelvin Lucas,Guilherme Caiano e Leonardo Formigari
Curso: Edge Computing e Computer Systems
Professor: Fabio Cabrini 


# Observações

Projeto desenvolvido para fins acadêmicos.

