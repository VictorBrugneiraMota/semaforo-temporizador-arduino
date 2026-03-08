# Semáforo Interativo com Travessia de Pedestres (Arduino)

## Descrição

Este projeto implementa um sistema de **semáforo interativo com solicitação de travessia para pedestres** utilizando Arduino.

O sistema simula o funcionamento de um cruzamento urbano onde pedestres podem solicitar a travessia pressionando um botão. Quando o botão é acionado, o sistema realiza a transição segura do semáforo de veículos, ativa a sinalização de pedestres e inicia uma **contagem regressiva em um display de 7 segmentos**.

Durante os últimos segundos da travessia, o sistema emite **alertas visuais e sonoros**, simulando o comportamento encontrado em semáforos reais.

---

## Componentes Utilizados

- Arduino Uno (ou compatível)
- 3 LEDs para semáforo de veículos
- 2 LEDs para sinalização de pedestres
- 1 display de 7 segmentos
- 1 botão (push button)
- 1 buzzer
- resistores
- protoboard
- jumpers

---

## Mapeamento de Pinos

### Semáforo de Veículos

| Função | Pino |
|------|------|
| Vermelho | 11 |
| Amarelo | 12 |
| Verde | 13 |

### Sinalização de Pedestres

| Função | Pino |
|------|------|
| Vermelho | 9 |
| Verde | 10 |

### Entrada e Som

| Dispositivo | Pino |
|------|------|
| Botão de travessia | 2 |
| Buzzer | 8 |

### Display de 7 Segmentos

| Segmento | Pino |
|------|------|
| A | 7 |
| B | 6 |
| C | 5 |
| D | 4 |
| E | 3 |
| F | A1 |
| G | A0 |

---

## Funcionamento do Sistema

### Estado Inicial

Ao iniciar o sistema:

- o **semáforo de veículos permanece verde**
- o **semáforo de pedestres permanece vermelho**

Nesse estado, veículos podem circular normalmente e pedestres devem aguardar.

---

### Solicitação de Travessia

Quando o botão de pedestre é pressionado, o Arduino verifica se já se passaram **5 segundos desde a última mudança de estado**. Isso evita múltiplas ativações consecutivas do sistema.

Se a condição for satisfeita, o sistema inicia a sequência de mudança do semáforo.

---

### Sequência do Semáforo

A sequência ocorre da seguinte forma:

1. O **verde dos veículos é desligado**
2. O **amarelo é ligado por 2 segundos**
3. O **amarelo é desligado**
4. O **vermelho dos veículos é ligado**

Essa transição simula o comportamento típico de semáforos reais.

---

### Travessia de Pedestres

Após a parada dos veículos:

- o **vermelho dos pedestres é desligado**
- o **verde dos pedestres é ligado**
- o **buzzer é ativado**

Simultaneamente, inicia-se uma **contagem regressiva de 5 até 0 segundos** no display de 7 segmentos.

---

### Alerta de Término de Travessia

Durante os **últimos dois segundos da contagem**:

- o LED verde de pedestres **pisca**
- o buzzer **emite sinais sonoros intermitentes**

Esse comportamento indica que o tempo de travessia está chegando ao fim.

---

### Retorno ao Estado Inicial

Após o término da contagem:

- o verde de pedestres é desligado
- o vermelho de pedestres é ligado
- o vermelho dos veículos é desligado
- o verde dos veículos é ligado novamente

O sistema retorna ao estado inicial de operação.

---

## Estrutura do Código

### `setup()`

Responsável por:

- configurar todos os pinos como **entrada ou saída**
- definir o **estado inicial do semáforo**
- inicializar os pinos do display de 7 segmentos

---

### `loop()`

Executado continuamente pelo Arduino.

Nesta função o sistema:

- lê o estado do botão
- verifica se o tempo mínimo entre mudanças foi respeitado
- chama a função responsável pela troca do semáforo

---

### `changeLights()`

Controla toda a sequência do sistema:

- transição do semáforo de veículos
- ativação do semáforo de pedestres
- ativação do buzzer
- chamada da função de contagem regressiva

---

### `contagemRegressiva()`

Executa a contagem regressiva exibida no display.

Também controla o comportamento de alerta durante os últimos segundos, fazendo o LED verde de pedestres piscar e o buzzer emitir sinais intermitentes.

---

### `mostrarNumero()`

Responsável por ativar os segmentos corretos do display para representar o número desejado.

Cada número é representado por uma combinação específica de segmentos.

---

### `desligarDisplay()`

Desliga todos os segmentos do display antes da exibição do próximo número.

---

## Objetivo do Projeto

Este projeto tem como objetivo demonstrar conceitos fundamentais de sistemas embarcados, incluindo:

- leitura de entradas digitais
- controle de saídas digitais
- interação entre hardware e software
- lógica de controle baseada em estados
- utilização de displays de 7 segmentos
- geração de sinais sonoros com buzzer

---

## Possíveis Melhorias

Algumas melhorias que podem ser implementadas no projeto:

- implementação de **debounce do botão**
- substituição de `delay()` por controle de tempo usando `millis()`
- utilização de **display de dois dígitos**
- uso de **interrupções para leitura do botão**
- adição de **modo noturno**
- expansão para múltiplas faixas de pedestres

---

Projeto desenvolvido para fins educacionais utilizando Arduino.
