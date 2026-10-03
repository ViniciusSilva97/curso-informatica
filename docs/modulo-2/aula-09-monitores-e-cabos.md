# Módulo 2 — Investigação Computacional I
## Anatomia do Hardware

# Aula 9 — Monitores e Cabos: Quando o Defeito da Imagem Está Fora do Computador?

> **Pergunta da investigação**
>
> Se a GPU está produzindo a imagem corretamente, por que ainda podem surgir piscadas, perda de sinal, cores estranhas, resolução incorreta ou falhas apenas em altas taxas de atualização?

---

# 📁 Dossiê da Investigação

## Caso nº 008 — Funciona em 60 Hz, mas falha em 165 Hz

Um usuário possui:

- GPU moderna;
- monitor de 2560 × 1440;
- suporte anunciado para 165 Hz;
- conexão DisplayPort.

Em 60 Hz, tudo funciona normalmente.

Ao selecionar 165 Hz:

- surgem pontos brilhantes;
- a tela pisca;
- ocasionalmente aparece “Sem sinal”;
- alguns jogos fazem o monitor apagar por alguns segundos.

O usuário reduz para 144 Hz.

Os sintomas diminuem.

Em 120 Hz, desaparecem completamente.

A primeira conclusão foi:

> “A placa de vídeo não está aguentando 165 Hz.”

Mas será?

A GPU continua renderizando normalmente.

Uma captura de tela realizada durante as piscadas não contém os defeitos visíveis no monitor.

Depois de substituir o cabo DisplayPort, 165 Hz passa a funcionar perfeitamente.

O que aconteceu?

Nesta aula investigaremos a parte do computador que normalmente recebe pouca atenção:

> **o caminho existente entre a imagem pronta e nossos olhos.**

---

# Objetivos da aula

Ao final desta aula, você deverá ser capaz de:

- compreender como a imagem sai da GPU e chega ao painel;
- diferenciar resolução, taxa de atualização e FPS;
- compreender largura de banda de vídeo;
- entender o papel de HDMI e DisplayPort;
- reconhecer limitações de cabos, portas e adaptadores;
- compreender EDID e negociação de capacidades;
- diferenciar RGB de YCbCr e compreender *chroma subsampling*;
- interpretar profundidade de cor e HDR;
- compreender sincronização adaptativa;
- diferenciar taxa de atualização de tempo de resposta;
- investigar piscadas, perda de sinal e pontos brilhantes;
- distinguir defeitos da GPU, cabo e monitor;
- compreender pixels mortos, vazamento de luz, retenção e burn-in;
- construir uma investigação não invasiva do sistema de vídeo.

---

# A imagem não termina na GPU

Na aula anterior, vimos o processamento gráfico.

Mas a renderização é apenas parte da história.

Depois que o quadro está pronto, ainda existe uma cadeia de transmissão:

```text
Aplicação
   ↓
Driver
   ↓
GPU
   ↓
Framebuffer
   ↓
Controlador de exibição
   ↓
HDMI / DisplayPort
   ↓
Cabo
   ↓
Entrada do monitor
   ↓
Controlador interno
   ↓
Painel
   ↓
Imagem percebida pelo usuário
```

Portanto, quando alguma coisa aparece errada na tela, não podemos começar dizendo:

> “É a placa de vídeo.”

Primeiro precisamos determinar:

> **Em qual ponto dessa cadeia a informação foi alterada ou interrompida?**

---

# A diferença entre renderizar e exibir

Imagine um jogo rodando a 120 FPS.

A GPU está produzindo aproximadamente 120 quadros por segundo.

Mas isso não significa necessariamente que o monitor esteja exibindo 120 atualizações por segundo.

Esses são conceitos diferentes.

## FPS

**Frames Per Second**

Representa quantos quadros a aplicação e o computador estão produzindo por segundo.

## Hz

**Hertz**

Representa quantas vezes por segundo o monitor pode atualizar sua imagem.

Exemplo:

```text
GPU renderizando: 200 FPS
Monitor:           60 Hz
```

Outro cenário:

```text
GPU renderizando: 45 FPS
Monitor:          144 Hz
```

Portanto:

> **FPS e Hz estão relacionados, mas não são a mesma coisa.**

---

# O que significa 60 Hz?

Um monitor de 60 Hz realiza aproximadamente 60 ciclos de atualização por segundo.

```text
1 segundo ÷ 60 ≈ 16,67 ms
```

Em 120 Hz:

```text
1 segundo ÷ 120 ≈ 8,33 ms
```

Em 144 Hz:

```text
≈ 6,94 ms
```

Em 240 Hz:

```text
≈ 4,17 ms
```

Quanto maior a taxa de atualização, menor o intervalo entre atualizações do painel.

Isso pode produzir percepção de:

- maior fluidez;
- movimentos mais suaves;
- menor atraso visual;
- melhor rastreamento de objetos em movimento.

Mas taxa de atualização não determina sozinha toda a resposta do monitor.

---

# Taxa de atualização não é tempo de resposta

Um monitor pode ser anunciado como:

> 165 Hz e 1 ms.

São especificações diferentes.

## Taxa de atualização

Indica quantas vezes o painel pode atualizar a imagem.

## Tempo de resposta

Refere-se ao tempo necessário para os pixels mudarem de um estado para outro.

Fabricantes podem apresentar números baseados em:

- GtG — Gray to Gray;
- MPRT — Moving Picture Response Time;
- cenários específicos de overdrive.

Assim:

> **“1 ms” não significa obrigatoriamente que todas as transições do painel ocorrem em exatamente 1 milissegundo.**

---

# Ghosting

Quando os pixels não conseguem realizar determinadas transições suficientemente rápido, objetos em movimento podem deixar uma espécie de rastro.

Esse fenômeno é conhecido como **ghosting**.

Possíveis influências:

- tecnologia do painel;
- tempo de resposta;
- configuração de overdrive;
- taxa de atualização;
- temperatura;
- transição específica de cor.

Ghosting não significa que a GPU esteja defeituosa.

---

# Overdrive

Muitos monitores possuem opções como:

- Normal;
- Fast;
- Faster;
- Extreme;
- Response Time;
- Overdrive.

Overdrive excessivo pode gerar **overshoot**, resultando em *inverse ghosting*.

```text
Overdrive baixo
→ transições lentas
→ mais ghosting

Overdrive adequado
→ melhor equilíbrio

Overdrive excessivo
→ overshoot
→ inverse ghosting
```

A opção “mais rápida” nem sempre produz a melhor imagem.

---

# Resolução

A resolução indica a quantidade de pixels utilizados na imagem.

Exemplos:

```text
1920 × 1080
2560 × 1440
3840 × 2160
```

Em 1920 × 1080:

```text
1920 × 1080 = 2.073.600 pixels
```

Em 3840 × 2160:

```text
3840 × 2160 = 8.294.400 pixels
```

Uma imagem 4K possui aproximadamente quatro vezes a quantidade de pixels de 1080p.

---

# Aqui nasce um conceito fundamental: largura de banda

Considere:

### Configuração A

```text
1920 × 1080
60 Hz
```

### Configuração B

```text
3840 × 2160
144 Hz
```

A segunda precisa transportar muito mais informação.

Também precisamos considerar:

- profundidade de cor;
- formato de cor;
- HDR;
- sincronização;
- informações auxiliares;
- overhead do protocolo.

> **Não basta o cabo conseguir transmitir imagem. Ele precisa suportar a quantidade de dados exigida pelo modo escolhido.**

---

# Por que um cabo funciona em 60 Hz e falha em 144 Hz?

Porque o sinal pode estar operando próximo ou acima da capacidade confiável daquele conjunto.

Isso envolve:

- padrão da porta;
- implementação da GPU;
- monitor;
- cabo;
- comprimento;
- qualidade do cabo;
- conectores;
- adaptadores;
- interferência;
- resolução;
- taxa de atualização;
- profundidade de cor.

Um cabo marginal pode funcionar perfeitamente em 1440p 60 Hz e apresentar erros em 1440p 165 Hz.

---

# O comportamento de um sinal digital

Existe um mito importante:

> “Digital funciona ou não funciona. Não existe perda de qualidade.”

Quando a integridade do sinal começa a ficar marginal, podem ocorrer:

- pontos brilhantes;
- piscadas;
- perda temporária de sinal;
- tela preta;
- renegociação da conexão;
- redução de recursos;
- instabilidade.

Não costuma ocorrer uma degradação progressiva semelhante ao ruído típico de sinais analógicos antigos. Em vez disso, aparecem erros digitais.

---

# O famoso “cabo HDMI que melhora a imagem”

Se dois cabos compatíveis transmitem corretamente o mesmo sinal digital nas mesmas condições, o cabo mais caro não cria:

- cores melhores;
- mais nitidez;
- pixels mais bonitos;
- detalhes inexistentes.

A diferença pode estar em:

- qualidade física;
- durabilidade;
- certificação;
- blindagem;
- capacidade de transmissão;
- comprimento;
- construção;
- tolerância em frequências maiores.

> O cabo pode determinar **se determinado modo funciona de maneira confiável**, mas não deveria modificar artisticamente os pixels de uma transmissão digital correta.

---

# HDMI

HDMI significa **High-Definition Multimedia Interface**.

Ele pode transportar:

- vídeo;
- áudio;
- dados auxiliares;
- informações de controle.

Duas portas HDMI visualmente iguais podem possuir capacidades diferentes.

---

# DisplayPort

DisplayPort é bastante utilizado para:

- altas taxas de atualização;
- monitores de alta resolução;
- sincronização adaptativa;
- configurações com múltiplos monitores.

Uma porta DisplayPort não garante automaticamente suporte a todas as combinações possíveis de resolução, Hz, HDR e profundidade de cor.

---

# HDMI versus DisplayPort: qual tem melhor imagem?

Se ambos transmitem:

- mesma resolução;
- mesma taxa de atualização;
- mesma profundidade de cor;
- mesmo formato de cor;
- mesmo intervalo dinâmico;

e a transmissão está correta, a qualidade essencial dos pixels não melhora simplesmente porque o protocolo mudou.

A pergunta mais útil é:

> **Qual interface suporta corretamente os recursos de que preciso?**

---

# O problema dos adaptadores

```text
GPU
DisplayPort
   ↓
Adaptador
   ↓
HDMI
   ↓
Monitor
```

Adaptadores podem ser:

- passivos;
- ativos;
- unidirecionais;
- limitados em resolução;
- limitados em frequência;
- incompatíveis com HDR;
- incompatíveis com determinados recursos.

Um adaptador que funciona em 1080p 60 Hz pode falhar em 4K 120 Hz.

O encaixe físico não prova capacidade de transmissão.

---

# EDID — quando o monitor diz ao computador quem ele é

O monitor disponibiliza informações conhecidas como **EDID — Extended Display Identification Data**.

Esses dados podem incluir:

- fabricante;
- modelo;
- resolução nativa;
- modos suportados;
- frequências;
- características de cor;
- recursos do equipamento.

Problemas nessa negociação podem produzir:

- resolução incorreta;
- monitor identificado genericamente;
- frequência ausente;
- HDR indisponível;
- modo esperado não listado.

---

# Hot Plug Detection

HDMI e DisplayPort possuem mecanismos para identificar conexão e desconexão.

Problemas nessa comunicação podem causar:

- monitor desaparecendo;
- janelas sendo reposicionadas;
- tela piscando;
- renegociação da conexão.

Novamente, nem toda tela preta é defeito na GPU.

---

# RGB e YCbCr

Computadores geralmente representam cores utilizando vermelho, verde e azul.

Vídeo também pode utilizar representações baseadas em luminância e crominância, como:

- YCbCr 4:4:4;
- YCbCr 4:2:2;
- YCbCr 4:2:0.

## 4:4:4

Preserva resolução completa de crominância.

É especialmente desejável para:

- textos;
- área de trabalho;
- interfaces;
- produtividade.

## 4:2:2 e 4:2:0

Reduzem parte da informação cromática.

Em filmes, isso pode ser pouco perceptível. Em texto pequeno de computador, diferenças podem ficar visíveis.

---

# Por que um computador pode alterar para 4:2:2?

Uma configuração como:

```text
4K
120 Hz
HDR
10 bits
```

exige bastante largura de banda.

Em determinadas configurações, reduzir a informação cromática pode diminuir a quantidade de dados transmitidos.

Por isso, avaliar apenas “4K” é insuficiente.

Precisamos perguntar:

> 4K em qual taxa de atualização, profundidade de cor e formato?

---

# Profundidade de cor

Em 8 bits por canal:

```text
2⁸ = 256 níveis
```

Com três canais RGB:

```text
256 × 256 × 256
≈ 16,7 milhões de combinações
```

Em 10 bits:

```text
2¹⁰ = 1024 níveis por canal
```

Isso permite gradientes mais finos e pode ajudar a reduzir **banding**, dependendo de toda a cadeia.

---

# Banding

Banding acontece quando um gradiente apresenta faixas perceptíveis em vez de uma transição suave.

Pode estar relacionado a:

- profundidade de cor;
- conteúdo;
- compressão;
- processamento;
- configuração do monitor;
- pipeline gráfico.

Não devemos concluir imediatamente que o painel está danificado.

---

# HDR

HDR significa **High Dynamic Range**.

O resultado depende de:

- brilho;
- contraste;
- capacidade do painel;
- controle da iluminação;
- profundidade de cor;
- gamut;
- processamento;
- conteúdo;
- sistema operacional;
- aplicativo.

HDR não é apenas “aumentar o brilho”.

---

# LCD não produz luz sozinho

Em monitores LCD, os pixels modulam luz fornecida por um sistema de iluminação traseira.

```text
Backlight
   ↓
Camadas ópticas
   ↓
LCD
   ↓
Filtros de cor
   ↓
Imagem
```

Isso ajuda a explicar:

- vazamento de luz;
- brilho desigual;
- contraste limitado;
- blooming em determinados sistemas.

---

# IPS, VA e TN

## IPS

Pode oferecer:

- bons ângulos de visão;
- boa reprodução de cores;
- boa consistência.

## VA

Frequentemente oferece:

- contraste estático elevado;
- pretos mais profundos que muitos IPS.

Alguns modelos podem apresentar transições escuras mais lentas.

## TN

Historicamente conhecido por:

- respostas rápidas;
- baixo custo.

Pode apresentar limitações em ângulos de visão e reprodução de cores.

Não existe uma tecnologia universalmente superior para todos os usos.

---

# OLED

Em OLED, os pixels produzem sua própria luz.

Vantagens potenciais:

- excelente contraste;
- resposta muito rápida;
- preto profundo;
- ausência de backlight convencional.

Particularidades:

- retenção temporária;
- risco de desgaste diferencial;
- burn-in;
- mecanismos de proteção;
- comportamento de brilho.

---

# Retenção de imagem e burn-in

## Retenção temporária

Uma imagem pode permanecer perceptível por algum tempo e depois desaparecer.

## Burn-in

Representa desgaste diferencial persistente.

Monitores OLED modernos podem empregar mecanismos como:

- deslocamento de pixels;
- redução de brilho em elementos;
- ciclos de compensação;
- proteção de logotipos;
- atualização do painel.

---

# Pixel morto

Um pixel ou subpixel pode:

- permanecer apagado;
- permanecer aceso;
- ficar preso em determinada cor.

Um teste com fundos sólidos em vermelho, verde, azul, branco e preto pode ajudar.

Se o ponto permanece na mesma posição física e não aparece em capturas de tela, a suspeita sobre o painel aumenta.

Não pressione a região defeituosa.

---

# Vazamento de luz e IPS Glow

*Backlight bleed* pode aparecer principalmente nas bordas de painéis com iluminação traseira.

O chamado **IPS glow** pode produzir aparência luminosa em determinadas regiões e varia bastante com:

- posição do observador;
- distância;
- ângulo.

Eles não são exatamente o mesmo fenômeno.

Fotografias em ambiente escuro podem exagerar bastante ambos.

---

# Uniformidade, calibração e perfil

Mesmo um monitor funcional pode não ter brilho e cor perfeitamente uniformes.

Em fluxos profissionais podem ser utilizados:

- colorímetros;
- espectrofotômetros;
- perfis ICC;
- softwares especializados.

## Calibração

Ajusta o comportamento do dispositivo em direção a determinado objetivo.

## Perfil

Descreve características do dispositivo para sistemas com gerenciamento de cor.

Ajustar “no olho” não equivale a uma calibração instrumental.

---

# Monitor “amarelado” não significa defeito automaticamente

Podem estar ativados:

- modo de leitura;
- filtro de luz azul;
- luz noturna;
- temperatura quente;
- perfil ICC;
- HDR;
- configuração personalizada.

---

# VRR — taxa de atualização variável

Tecnologias de taxa de atualização variável permitem que o monitor ajuste dinamicamente seu ritmo dentro de determinada faixa.

Exemplos incluem:

- Adaptive-Sync;
- FreeSync;
- G-SYNC.

O objetivo é melhorar a apresentação quando a taxa de quadros varia.

---

# Tearing

Sem sincronização adequada, partes de quadros diferentes podem aparecer simultaneamente.

```text
Parte superior → quadro A
Parte inferior → quadro B
```

Esse fenômeno é chamado de **screen tearing**.

Ele não é artefato de VRAM.

---

# V-Sync e flickering com VRR

V-Sync procura alinhar a apresentação dos quadros ao ciclo do monitor.

VRR procura ajustar dinamicamente a taxa do monitor.

Algumas configurações podem apresentar flickering relacionado a:

- variações abruptas de FPS;
- faixa de operação;
- comportamento do painel;
- compensação em baixas taxas;
- driver;
- firmware.

Um teste controlado é comparar o comportamento com VRR ligado e desligado, alterando apenas essa variável.

---

# DSC — Display Stream Compression

Em algumas combinações modernas de alta resolução, taxa de atualização e profundidade de cor, pode ser utilizada **DSC**.

Seu uso depende de:

- GPU;
- monitor;
- protocolo;
- implementação.

Não devemos assumir suporte apenas pela presença de HDMI ou DisplayPort.

---

# O monitor também possui firmware

Monitores modernos podem possuir:

- processador interno;
- firmware;
- scaler;
- controladores;
- USB;
- hubs;
- KVM;
- recursos de rede em alguns modelos.

Consequentemente, também podem existir:

- bugs;
- atualizações;
- incompatibilidades;
- falhas de suspensão;
- problemas de negociação.

---

# Scaler e overscan

Quando a resolução enviada não corresponde à resolução física do painel, o monitor pode precisar redimensionar a imagem.

Em televisores, também pode existir **overscan**, cortando ligeiramente as bordas.

Isso pode produzir:

- barra de tarefas cortada;
- texto fora da tela;
- perda das bordas.

Não é necessariamente defeito da GPU.

---

# O monitor apaga por dois segundos e volta

Possíveis hipóteses:

- renegociação do sinal;
- cabo marginal;
- HDR ativando;
- troca de frequência;
- driver reiniciando;
- VRR;
- monitor mudando de modo;
- porta;
- adaptador;
- GPU;
- alimentação do monitor.

A sequência temporal é uma evidência importante.

---

# O teste da captura de tela

Faça:

1. captura do sistema;
2. fotografia externa do monitor.

### Captura contém o defeito

Investigue:

- aplicativo;
- driver;
- GPU;
- VRAM;
- composição.

### Captura normal, fotografia mostra o defeito

A suspeita aumenta sobre:

- saída;
- porta;
- cabo;
- monitor;
- painel.

Não é prova absoluta, mas é uma técnica investigativa poderosa.

---

# Outro teste excelente: menu interno do monitor

Abra o menu OSD quando o defeito estiver acontecendo.

Se o OSD permanece perfeito enquanto a imagem recebida apresenta falhas, a falha pode estar no sinal ou em outra etapa anterior.

Se o defeito também afeta o próprio OSD, a suspeita sobre o monitor aumenta.

---

# Teste sem computador

Se a falha continua aparecendo no logotipo, OSD ou tela “Sem sinal” do próprio monitor:

> A GPU não está sequer participando.

Isso transforma radicalmente a investigação.

---

# Monitor piscando: teste de alimentação

O monitor também possui alimentação própria.

Falhas podem causar:

- desligamento;
- brilho instável;
- demora para ligar;
- reinicializações;
- piscadas;
- ruídos.

Verifique:

- tomada;
- cabo de força;
- adaptador;
- conector;
- tensão adequada;
- fonte original.

Não abra fontes internas sem qualificação.

---

# Cuidado com USB-C

USB-C descreve o conector físico.

Ele não garante sozinho:

- vídeo;
- carregamento;
- determinada potência;
- determinada velocidade;
- Thunderbolt;
- DisplayPort Alternate Mode.

> **USB-C é formato físico, não uma garantia universal de funcionalidades.**

---

# Dock stations

Em notebooks, uma cadeia pode ser:

```text
Notebook
  ↓
USB-C / Thunderbolt
  ↓
Dock
  ↓
Controlador interno
  ↓
DisplayPort ou HDMI
  ↓
Cabo
  ↓
Monitor
```

Se a tela apresenta problemas, investigue também:

- firmware da dock;
- driver;
- capacidade da porta;
- quantidade de monitores;
- resolução;
- largura de banda compartilhada;
- alimentação.

---

# 🔬 Laboratório — investigação de uma cadeia de vídeo

## Etapa 1 — Documentar o sistema

Registre:

```text
GPU:
Monitor:
Resolução nativa:
Taxa máxima:
Conexão:
Porta utilizada:
Cabo:
Adaptadores:
Driver:
HDR:
VRR:
Profundidade de cor:
Formato de cor:
```

## Etapa 2 — Estabelecer uma configuração básica

Utilize temporariamente uma configuração conservadora:

- resolução nativa;
- 60 Hz;
- HDR desligado;
- VRR desligado;
- sem adaptadores desnecessários.

Observe a estabilidade.

## Etapa 3 — Aumentar uma variável

Por exemplo:

```text
60 Hz → 120 Hz
120 Hz → 144 Hz
144 Hz → 165 Hz
```

Teste cada etapa.

## Etapa 4 — Testar o cabo

Substitua por outro cabo conhecido e adequado.

Não altere outras variáveis.

## Etapa 5 — Testar portas

Experimente outra porta compatível, mantendo os demais parâmetros sempre que possível.

## Etapa 6 — Registrar o defeito

Faça:

- fotografia;
- vídeo;
- captura de tela;
- anotação do horário.

Determine se:

- aparece na captura;
- aparece no OSD;
- aparece sem computador;
- acompanha o cabo;
- acompanha a porta;
- acompanha o monitor.

## Etapa 7 — Construir a matriz

| Teste | Resultado |
|---|---|
| 1440p 60 Hz | Normal |
| 1440p 120 Hz | Normal |
| 1440p 144 Hz | Normal |
| 1440p 165 Hz | Piscadas |
| Outro cabo em 165 Hz | Normal |
| Captura de tela | Normal |
| OSD | Normal |

Conclusão provisória:

> As evidências apontam fortemente para instabilidade na cadeia de transmissão associada ao cabo original quando submetido à maior largura de banda.

---

# Estudos de caso

## Caso 1 — Pontos brancos em 4K

Em 4K, alta taxa de atualização, HDR e cabo longo, surgem pequenos pontos brancos.

Eles desaparecem ao reduzir a taxa de atualização e também após a troca do cabo.

**Conclusão:** fortes evidências de problema de integridade do sinal na transmissão original.

## Caso 2 — Texto colorido e pouco nítido na TV

Vídeos parecem bons, mas letras pequenas apresentam bordas estranhas.

A configuração mostra crominância reduzida.

**Hipótese:** o sinal pode estar usando 4:2:2 ou 4:2:0.

## Caso 3 — Tela dividida horizontalmente durante jogos

A imagem parece formada por duas partes de quadros diferentes, não aparece na captura e ocorre com FPS variável e V-Sync desativado.

**Hipótese prioritária:** screen tearing.

## Caso 4 — Monitor apresenta defeito sem computador conectado

A tela “Sem sinal” e o próprio OSD apresentam uma faixa vertical permanente.

**Conclusão provisória:** a suspeita sobre painel, controlador interno ou conexão interna aumenta significativamente.

## Caso 5 — 144 Hz desapareceu após trocar a dock

O monitor suportava 144 Hz diretamente ou com uma dock anterior, mas uma nova cadeia limita a 60 Hz.

**Investigue:** capacidade da dock, modo alternativo, versão da interface, largura de banda, resolução e outros monitores conectados.

## Caso 6 — Tela preta ao ativar HDR

Sem HDR funciona normalmente. Ao ativá-lo, a tela apaga ou perde sinal.

**Possíveis explicações:** aumento da profundidade de cor, mudança de formato, maior largura de banda, cabo marginal, porta limitada, driver, monitor ou negociação.

---

# Mito ou Evidência?

### “HDMI sempre tem imagem pior que DisplayPort.”

**Mito.**

### “Se o cabo digital funciona, ele sempre funcionará em qualquer resolução.”

**Mito.**

### “Um cabo muito caro produz cores melhores.”

**Mito**, se um cabo mais simples já transmite integralmente o mesmo sinal sem erros.

### “Um problema pode aparecer apenas em 165 Hz.”

**Evidência.**

### “60 FPS e 60 Hz significam exatamente a mesma coisa.”

**Mito.**

### “1 ms é uma medida completamente padronizada entre todos os fabricantes.”

**Mito.**

### “Artefato que não aparece em captura pode estar depois da renderização.”

**Evidência.**

### “Se o menu do monitor apresenta a falha sem computador conectado, a GPU é uma hipótese muito fraca.”

**Evidência.**

### “USB-C sempre transmite vídeo.”

**Mito.**

### “4K não define sozinho a quantidade total de dados transmitida.”

**Evidência.**

---

# Como um laboratório profissional investigaria?

Um diagnóstico de monitor pode envolver:

- padrões de teste;
- colorímetro;
- osciloscópio;
- análise de alimentação;
- gerador de sinais;
- câmera de alta velocidade;
- instrumentos de luminância;
- teste de uniformidade;
- medição de resposta;
- inspeção eletrônica.

Para cabos e interfaces, laboratórios especializados podem analisar:

- integridade do sinal;
- qualidade do olho digital;
- erros;
- jitter;
- atenuação;
- interferência.

> Quanto maior a velocidade de transmissão, mais importante se torna a integridade elétrica do caminho.

---

# O que um perito observaria?

- Qual é a resolução?
- Qual taxa de atualização?
- O problema aparece em 60 Hz?
- Aparece somente em HDR?
- Qual profundidade de cor?
- RGB ou YCbCr?
- Existe adaptador?
- Existe dock?
- Qual porta está sendo utilizada?
- Outro cabo foi testado?
- O defeito aparece na captura?
- O defeito aparece no OSD?
- Aparece sem computador conectado?
- Outro monitor apresenta o mesmo comportamento?
- O problema acompanha o monitor?
- A entrada utilizada suporta aquele modo?
- O cabo é adequado ao requisito?
- Existe VRR?
- O defeito desaparece sem VRR?
- O monitor possui firmware atualizado?
- O problema ocorre somente após suspensão?
- O sistema está detectando corretamente o EDID?
- Há alguma alteração recente?

> **Sintoma → evidência → hipótese → teste → conclusão.**
