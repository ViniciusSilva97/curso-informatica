# Aula 3 — Memória RAM: O laboratório de trabalho do processador

## Pergunta da investigação

```text
Por que um computador extremamente rápido se torna lento quando falta memória RAM?
```

## Dossiê da Investigação

### Caso nº 002

Um escritório possui dois computadores praticamente idênticos.

#### Computador A

- Ryzen 7
- 32 GB RAM
- SSD NVMe

#### Computador B

- Ryzen 7
- 8 GB RAM
- SSD NVMe

Os dois possuem exatamente o mesmo processador, mesmo SSD,
mesmo sistema operacional, mesmo monitor, mesmo software.Entretanto, quando várias planilhas, o navegador, o sistema ERP e uma videoconferência são executados ao mesmo tempo, apenas um deles continua trabalhando normalmente.  

**Por quê?**

Hoje vamos investigar.

## Objetivos da Aula

Ao final desta aula você será capaz de:

- compreender a verdadeira função da memória RAM;
- entender por que ela influencia tanto a experiência do usuário;
- interpretar especificações técnicas;
- identificar gargalos relacionados à memória;
- utilizar ferramentas para investigar seu funcionamento.

## O erro mais comum

Pergunte para alguém:  
O que é memória RAM?
Provavelmente ouvirá:  
**"É uma memória temporária."**
A resposta está correta. Mas ela não explica praticamente nada.  
A verdadeira pergunta é:  
Por que o computador precisa de uma memória temporária?  

## O verdadeiro problema
Imagine um chef preparando um jantar, todos os ingredientes estão guardados em uma despensa.
Cada vez que precisa de sal, ele caminha até a despensa.  
Depois volta, agora precisa da panela.  
Volta novamente, depois pega uma faca.  
Depois volta outra vez. O jantar ficará pronto?  
Sim. Rapidamente? Nem um pouco.  
Agora imagine outra situação.  
O cozinheiro coloca todos os ingredientes sobre a bancada, tudo está ao alcance das mãos. O trabalho flui naturalmente.  
A memória RAM é essa bancada, o SSD é a despensa.

## O que realmente acontece?
O processador trabalha em velocidades extremamente altas.
O SSD, embora muito rápido, ainda é lento quando comparado à CPU.  

Se o processador precisasse buscar cada informação diretamente no SSD, passaria grande parte do tempo esperando.  

A RAM existe justamente para reduzir esse tempo de espera. Ela mantém disponíveis os dados e programas que estão sendo utilizados naquele momento.

## Como funciona?

Imagine nosso computador.

SSD

↓

Memória RAM

↓

Processador

↓

Resultado

Quando você abre um programa, ele não é executado diretamente do SSD. O sistema operacional copia as informações necessárias para a memória RAM.  
Somente depois o processador começa a trabalhar.

## Um conceito importante
A memória RAM é chamada de memória volátil. Isso significa que seu conteúdo depende de energia elétrica.
Quando o computador é desligado, todas as informações armazenadas nela desaparecem.  
Esse comportamento é uma característica do seu projeto e não um defeito.

## Investigação

Vamos observar o computador.  
Abrimos um navegador.
Depois uma planilha.  
Depois um editor de texto.  
Depois uma videoconferência.  

O que está acontecendo?  

Todos esses programas estão ocupando espaço na memória RAM ao mesmo tempo.  

Quando a capacidade disponível diminui, o sistema operacional passa a utilizar parte do SSD como memória auxiliar (memória virtual ou arquivo de paginação). Essa solução permite continuar trabalhando, mas é muito mais lenta do que acessar a RAM diretamente.  

## Dentro da Caixa

Vamos analisar uma ficha técnica.

**Kingston Fury Beast**

- Capacidade........16 GB

- Tecnologia........DDR5

- Velocidade........6000 MT/s

- Latência..........CL30

- Formato...........DIMM

- Tensão............1,35 V

Agora vamos investigar.

### Capacidade

É a quantidade total de dados que podem permanecer disponíveis para o processador.
Mais capacidade significa maior espaço de trabalho.
Não significa automaticamente maior velocidade.

### Tecnologia

DDR4 e DDR5 utilizam arquiteturas diferentes.
Uma placa-mãe suporta apenas a tecnologia para a qual foi projetada.

### Velocidade

Expressa em MT/s.

Representa a quantidade de transferências realizadas por segundo. Valores maiores podem aumentar o desempenho em determinadas aplicações.  

### Latência

Representa o tempo necessário para iniciar um acesso.
Imagine duas bibliotecas.
Uma possui livros muito rápidos para serem encontrados.
Outra demora um pouco mais.
Essa diferença é semelhante ao conceito de latência.

### Formato

#### DIMM.

Desktop.

#### SO-DIMM.

Notebook.

## Laboratório

Hoje conheceremos ferramentas utilizadas por profissionais.

### CPU-Z

Permite verificar:

- capacidade instalada;
- frequência real;
- tipo de memória;
- quantidade de canais;
- fabricante dos módulos.

### HWiNFO

Mostra:

- utilização da RAM;
- consumo por aplicação;
- frequência;
- temperatura (quando suportado);
- diversos sensores da plataforma.

### Gerenciador de Tarefas (Windows)

**Ferramenta nativa.**

Permite observar:

- uso de memória em tempo real;
- quantidade disponível;
- memória comprometida;
- utilização por processos.

É um excelente ponto de partida para diagnósticos simples.

## O que um investigador observaria?

Imagine que um usuário diga:

```text
"Meu computador ficou lento."
```

Antes de recomendar mais memória, um investigador responderia com perguntas:

- A RAM realmente está sendo totalmente utilizada?
- Quantos programas estão abertos?
- Existe paginação excessiva para o SSD?
- Algum programa apresenta vazamento de memória (memory leak)?
- A lentidão ocorre sempre ou apenas em determinadas tarefas?

Perceba que a conclusão depende das evidências.

## Estudo de Caso

Durante um atendimento foram observados os seguintes dados:

- CPU: 28%
- SSD: 6%
- GPU: 9%
- Memória RAM: 98%

O computador apresenta lentidão apenas quando muitas aplicações permanecem abertas.

**Pergunta:**
Qual hipótese inicial parece mais consistente?  
Como ela poderia ser confirmada antes de recomendar um upgrade?  

## Curiosidade Técnica  
Sistemas operacionais modernos utilizam técnicas como cache de arquivos, compressão de memória e gerenciamento inteligente de páginas para aproveitar melhor a RAM disponível. Além disso, um programa pode apresentar vazamento de memória (memory leak), situação em que reserva memória e deixa de liberá-la corretamente. Esse tipo de problema pode causar lentidão mesmo em computadores com grande quantidade de RAM e é um excelente exemplo de como nem todo problema aparentemente relacionado ao hardware tem origem no hardware. 