# 🍷 Sistema de Controle de Temperatura para Vinharia com Arduino

## 📝 Descrição

Este projeto tem como objetivo desenvolver um sistema automatizado de controle de temperatura para armazenamento de vinhos, utilizando a plataforma Arduino. A proposta consiste em monitorar continuamente a temperatura do ambiente de uma vinharia e garantir que ela permaneça dentro da faixa ideal para conservação dos vinhos.

O sistema realiza a leitura de sensores de temperatura e, com base nos valores obtidos, pode acionar dispositivos como ventiladores ou sistemas de resfriamento/aquecimento, assegurando condições adequadas para preservar as características e a qualidade do vinho.

Esse tipo de controle é fundamental, pois variações de temperatura podem comprometer o sabor, o aroma e a durabilidade da bebida. Dessa forma, o projeto demonstra, de forma prática, a aplicação da automação e da eletrônica no controle ambiental, sendo uma solução acessível e eficiente para pequenas adegas ou fins educacionais.

---

## ⚙️ Funcionalidades

- Monitoramento da temperatura em tempo real por meio de sensor
- Controle automático da temperatura do ambiente
- Acionamento de sistema de resfriamento (ex: ventilador) quando a temperatura ultrapassa o limite ideal
- Desligamento automático do sistema quando a temperatura retorna ao nível adequado
- Alerta sonoro por meio de buzzer quando a temperatura está acima do valor recomendado
- Indicação do estado do sistema (ligado/desligado) por meio de LED
- Leitura contínua dos dados para manter a estabilidade térmica

---

## 🧰 Componentes Utilizados

- Arduino Uno
- Sensor de temperatura (ex: LM35 ou DHT11)
- Display LCD 16x2
- Buzzer (alarme sonoro)
- LEDs (indicadores de estado)
- Resistores
- Protoboard
- Jumpers (fios de conexão)
- Potenciômetro (para ajuste do contraste do display LCD)

---

## 💻 Funcionamento

O sistema de controle de temperatura funciona por meio da leitura contínua dos dados captados por um sensor de temperatura instalado no ambiente da vinharia. Essas informações são enviadas ao Arduino, que realiza o processamento dos valores em tempo real.

Com base na temperatura medida, o sistema compara os valores com uma faixa considerada ideal para a conservação do vinho. Caso a temperatura ultrapasse o limite estabelecido, o Arduino aciona automaticamente um sistema de resfriamento, como um ventilador, com o objetivo de reduzir a temperatura do ambiente.

Simultaneamente, um buzzer é ativado para emitir um alerta sonoro, indicando que a temperatura está acima do recomendado. Além disso, LEDs são utilizados para sinalizar visualmente o estado do sistema, facilitando a identificação das condições de funcionamento.

O display LCD exibe, em tempo real, os valores de temperatura monitorados, permitindo ao usuário acompanhar continuamente as condições do ambiente.

Quando a temperatura retorna aos níveis ideais, o sistema desativa automaticamente o resfriamento e o alerta sonoro, mantendo o ambiente estável. Dessa forma, o projeto garante um controle eficiente e automatizado, contribuindo para a preservação da qualidade do vinho.

# esquema do circuito 
