# **Aula 8 - Placa de Vídeo: nem todo artefato significa GPU queimada**

**Pergunta da investigação**

Quando surgem linhas, pontos coloridos, travamentos ou telas pretas, como descobrir se o problema está na GPU, na memória de vídeo, no driver, na alimentação, no cabo ou no monitor?

# ** Dossiê da investigação**

## **Caso nº 007 - Os artefatos que apareciam somente durante jogos**

Um computador usado para jogos começou a apresentar os seguintes sintomas:

- pequenos quadrados coloridos em algumas texturas;
- sombras piscando;
- travamento após aproximadamente vinte minutos;
- tela preta por alguns segundos;
- retorno do vídeo acompanhado de uma mensagem relacionada ao driver;
- reinicializações ocasionais em jogos mais pesados.

Durante atividades comuns, como navegar na internet e editar documentos, o computador funcionava aparentemente bem.

O proprietário pesquisou o problema e encontrou diagnósticos diferentes:

"A GPU queimou."

"É defeito na memória de vídeo."

"É só reinstalar o driver."

"Precisa fazer reballing."

"A fonte não está aguentando."

Todas essas hipóteses são possíveis em determinados cenários.

Nenhuma delas, porém, pode ser considerada correta sem evidências.

Nosso objetivo não será adivinhar qual componente falhou. Será descobrir:

1. em quais condições o defeito aparece;
2. em qual etapa do processamento gráfico ocorre a corrupção;
3. quais hipóteses são compatíveis com os sintomas;
4. quais testes eliminam possibilidades;
5. quando interromper os testes e encaminhar a placa a um laboratório.

# **Objetivos da aula**

Ao final desta aula, você será capaz de:

- compreender a arquitetura funcional de uma placa de vídeo;
- diferenciar GPU, VRAM, VRM, VBIOS e sistema de exibição;
- entender o caminho percorrido até a imagem aparecer no monitor;
- classificar diferentes tipos de artefatos;
- distinguir falhas de renderização de falhas na transmissão do sinal;
- reconhecer problemas térmicos, elétricos e de software;
- investigar travamentos e reinicializações do driver;
- utilizar ferramentas gratuitas de monitoramento e diagnóstico;
- compreender as limitações dos testes de estresse;
- avaliar criticamente procedimentos como reflow e reballing;
- documentar uma investigação reproduzível e baseada em evidências.

# **Uma placa de vídeo é um sistema computacional completo**

A expressão "placa de vídeo" pode transmitir a ideia de que existe apenas um chip responsável por criar imagens.

Na realidade, uma placa de vídeo dedicada reúne vários subsistemas.

┌────────────────┐

│ PLACA DE VÍDEO │

├────────────────┤

│ GPU │

│ Memória de vídeo - VRAM │

│ Controladores de memória │

│ VRM e circuitos de alimentação │

│ Firmware - VBIOS │

│ Interface PCI Express │

│ Mecanismo de exibição │

│ Codificadores e decodificadores de vídeo │

│ Sensores │

│ Sistema de refrigeração │

│ Portas HDMI e DisplayPort │

└───────────────────────────┘

Cada uma dessas regiões pode produzir sintomas diferentes.

Por isso, a frase "a placa de vídeo está com defeito" ainda é muito genérica.

Um diagnóstico mais preciso deve procurar responder:

- Qual subsistema está falhando?
- A falha é permanente ou intermitente?
- O problema depende de temperatura, carga ou frequência?
- Existe corrupção de dados ou apenas perda de sinal?
- O sistema operacional continua funcionando?
- O defeito aparece antes do carregamento dos drivers?

# **Uma GPU**

A **GPU - Graphics Processing Unit** é o principal processador da placa.

Ela foi projetada para executar grandes quantidades de operações paralelas, especialmente aquelas relacionadas a:

- geometria;
- iluminação;
- texturas;
- sombras;
- rasterização;
- computação;
- processamento de imagens;
- inteligência artificial;
- codificação e decodificação de vídeo.

A GPU não produz a imagem final completamente sozinha.

Ela depende da memória, dos drivers, do processador principal, do sistema operacional, da alimentação e do mecanismo de exibição.

# **A memória de vídeo - VRAM**

A VRAM é uma memória dedicada ao trabalho gráfico.

Ela pode armazenar:

- texturas;
- modelos tridimensionais;
- mapas de sombras;
- buffers de profundidade;
- quadros já renderizados;
- informações intermediárias;
- dados utilizados em cálculos;
- recursos de programas profissionais;
- estruturas usadas em inteligência artificial.

Uma representação simplificada seria:

Jogo ou programa

↓

Driver gráfico

↓

Comandos enviados à GPU

↓

GPU processa a cena

↕

VRAM armazena dados temporários

↓

Quadro final

↓

Mecanismo de exibição

↓

Monitor

Uma falha na VRAM pode corromper informações antes ou durante o processamento.

Isso pode produzir:

- texturas incorretas;
- blocos coloridos;
- padrões repetidos;
- objetos deformados;
- travamentos;
- erros que surgem apenas quando determinada quantidade de memória é utilizada.

Entretanto, um artefato visual não prova automaticamente que a VRAM esteja defeituosa.

# **O controlador de memória**

Entre a GPU e a VRAM existe um sistema responsável por organizar a comunicação.

Problemas nessa região podem envolver:

- controlador interno da GPU;
- chips de memória;
- trilhas da placa;
- alimentação da memória;
- soldagem;
- frequência instável;
- temperatura;
- configuração de firmware.

Por isso, mesmo quando um teste aponta erros relacionados à memória gráfica, ainda pode ser necessário investigar mais de uma região física.

# **O VRM da placa de vídeo**

O **VRM - Voltage Regulator Module** converte a energia recebida da fonte em tensões adequadas para:

- núcleo gráfico;
- memória;
- controladores;
- circuitos auxiliares.

A placa pode receber 12 V da fonte, mas a GPU trabalha com tensões muito mais baixas e cuidadosamente controladas.

Fonte fornece 12 V

↓

VRM da placa de vídeo

↓

Tensão do núcleo gráfico

Tensão da memória

Tensões auxiliares

Um problema no VRM pode causar:

- instabilidade sob carga;
- tela preta;
- desligamento;
- redução de frequência;
- superaquecimento;
- falha de inicialização;
- danos em outros componentes da placa.

O VRM também possui componentes que aquecem e dependem do sistema de refrigeração.

# **VBIOS**

A placa de vídeo possui um firmware frequentemente chamado de **VBIOS**.

Ele contém parâmetros relacionados a:

- inicialização;
- frequências;
- tensões;
- limites de potência;
- comportamento das ventoinhas;
- identificação do dispositivo;
- compatibilidade;
- configuração da memória.

Problemas podem surgir após:

- modificação inadequada;
- atualização incorreta;
- uso de firmware incompatível;
- interrupção durante gravação;
- tentativa de aplicar VBIOS de outro modelo.

A atualização ou modificação do VBIOS não deve ser tratada como procedimento comum de diagnóstico.

# **Interface PCI Express**

A comunicação principal entre a placa de vídeo e o computador ocorre pelo PCI Express.

Precisamos considerar:

- geração da interface;
- número de faixas;
- contato físico;
- estado do slot;
- configuração do firmware;
- compatibilidade;
- integridade das trilhas;
- alimentação fornecida pelo slot.

Uma placa pode utilizar fisicamente um conector x16, mas operar eletricamente com menos pistas, dependendo:

- do modelo da placa;
- do processador;
- da placa-mãe;
- de outros dispositivos instalados;
- da organização da plataforma.

Também é normal que algumas placas reduzam temporariamente a velocidade do link em repouso para economizar energia. A velocidade máxima pode aparecer somente durante uma carga gráfica.

Portanto, observar uma geração reduzida no GPU-Z enquanto a placa está ociosa não comprova defeito.

# **O mecanismo de exibição**

Mesmo depois que a GPU conclui o quadro, ele ainda precisa ser enviado ao monitor.

Essa etapa envolve:

- framebuffer;
- mecanismo de exibição;
- sincronização;
- porta de saída;
- cabo;
- entrada do monitor;
- processamento interno da tela;
- painel.

Consequentemente, o problema pode estar depois da renderização.

Aplicativo

↓

GPU renderiza

↓

Quadro armazenado

↓

Mecanismo de exibição

↓

Porta HDMI ou DisplayPort

↓

Cabo

↓

Monitor

↓

Imagem observada

Essa separação é essencial para investigar artefatos.

# **O que é um artefato gráfico?**

Artefato é qualquer alteração visual inesperada que não deveria fazer parte da imagem original.

Exemplos:

- pontos brilhantes;
- pixels coloridos;
- linhas;
- blocos;
- padrões quadriculados;
- texturas incorretas;
- polígonos esticados;
- sombras piscando;
- imagens duplicadas;
- cores alteradas;
- partes da tela corrompidas;
- quadros incompletos.

A aparência do artefato pode fornecer pistas, mas raramente determina sozinha a causa.

# **Classificação dos sintomas**

## **1\. Pontos brilhantes ou "estrelas"**

Pequenos pontos podem aparecer principalmente em resoluções ou frequências elevadas.

Hipóteses:

- cabo inadequado;
- cabo danificado;
- conexão incompleta;
- largura de banda insuficiente;
- problema à porta;
- interferência;
- monitor;
- instabilidade gráfica.

Se os pontos desaparecem ao reduzir temporariamente a resolução ou a taxa de atualização, o caminho de transmissão merece atenção especial.

## **2\. Blocos ou padrões repetidos**

Padrões geométricos repetidos podem sugerir corrupção de dados.

Hipóteses:

- VRAM;
- controlador de memória;
- overclock de memória;
- temperatura;
- motorista;
- aplicação;
- alimentação da memória;
- defeito físico.

A repetição pode ocorrer porque estruturas semelhantes da memória estão sendo lidas incorretamente.

Ainda assim, não é possível condenar um chip específico apenas observando a imagem.

## **3\. Texturas erradas**

Exemplos:

- paredes com cores incorretas;
- objetos cobertos por padrões estranhos;
- texturas piscando;
- partes do cenário sem definição.

Hipóteses:

- bug do jogo;
- arquivos corrompidos;
- motorista;
- VRAM;
- falta de memória gráfica;
- overclock;
- configuração gráfica;
- compilação de shaders.

Quando o problema ocorre apenas em um jogo, a possibilidade de falha específica do software aumenta.

## **4\. Polígonos esticados**

Objetos podem parecer deformados, com triângulos ou linhas atravessando a tela.

Hipóteses:

- processamento geométrico;
- motorista;
- shader;
- dados corrompidos;
- instabilidade da GPU;
- VRAM;
- falha da aplicação.

Esse sintoma pode ser causado tanto por software quanto por hardware.

## **5\. Tela preta**

Uma tela preta possui várias interpretações possíveis.

### **Tela preta, mas o áudio continua**

O sistema pode continuar executando enquanto o sinal de vídeo é perdido.

Hipóteses:

- driver reiniciado;
- traz;
- cabo;
- monitor;
- mecanismo de exibição;
- instabilidade da GPU;
- alimentação;
- mudança de modo de vídeo.

### **Tela preta e computador reinicia**

Hipóteses:

- fonte;
- proteção elétrica;
- GPU;
- temperatura;
- placa-mãe;
- Motorista crítico;
- memória RAM;
- instabilidade geral.

### **Tela preta desde o acionamento**

Hipóteses:

- GPU não inicializada;
- conector de alimentação;
- slot;
- firmware;
- processador sem vídeo integrado;
- cabo conectado à saída errada;
- monitor;
- placa defeituosa.

"Tela preta" é um sintoma, não um diagnóstico.

## **6\. Travamento com imagem congelada**

Hipóteses:

- motorista;
- GPU;
- VRAM;
- CPU;
- memória RAM;
- armazenamento;
- jogo;
- fonte;
- temperatura;
- sistema operacional.

Se o áudio continua, o sistema pode estar parcialmente ativo.

Se todo o computador deixa de responder, a investigação precisa considerar componentes além da placa de vídeo.

## **7\. Reinicialização do driver**

Sistemas operacionais modernos podem detectar que a GPU deixou de responder e tentar reinicializar o subsistema gráfico.

No Windows, esse mecanismo é relacionado ao conceito de **TDR - Timeout Detection and Recovery**.

Em termos simplificados:

Sistema envia trabalho para a GPU

↓

GPU demora ou deixa de responder

↓

Sistema detecta o atraso

↓

Driver gráfico é reinicializado

↓

Imagem pode apagar e retornar

Esse evento pode ocorrer devido a:

- motorista;
- aplicação;
- GPU instável;
- VRAM;
- overclock;
- temperatura;
- falta momentânea de alimentação;
- falha do sistema;
- carga computacional problemática.

A reinicialização do driver não prova, sozinha, que o problema é exclusivamente de software.

# **Em qual momento o artefato aparece?**

Essa é uma das perguntas mais importantes da investigação.

## **Artefato aparece antes do sistema operacional**

Exemplos:

- logotipo da placa-mãe;
- tela de firmware;
- menu de inicialização;
- instalação do sistema.

Nesse caso, o driver principal do sistema operacional ainda não está atuando.

Hipóteses mais relevantes:

- placa de vídeo;
- VRAM;
- VBIOS;
- cabo;
- monitor;
- traz;
- slot;
- alimentação.

Isso reduz bastante a probabilidade de o problema ser causado apenas pelo driver instalado no sistema.

## **Artefato aparece somente depois de carregar o sistema**

Hipóteses:

- motorista;
- resolução;
- taxa de atualização;
- aceleração gráfica;
- configuração;
- aplicação;
- gerenciamento de energia;
- hardware ativado apenas em estados de maior desempenho.

O hardware não está automaticamente inocentado.

Ao carregar o driver, a placa pode passar a usar:

- frequências mais altas;
- recursos avançados;
- aceleração 3D;
- modos de energia diferentes;
- mais VRAM.

Uma falha física pode aparecer somente nessa etapa.

## **Artefato aparece somente sob carga**

Hipóteses:

- temperatura;
- potência;
- VRM;
- fonte;
- instabilidade de clock;
- VRAM;
- controlador;
- fluxo de ar.

O comportamento dependente de carga é uma evidência muito importante.

## **Artefato aparece somente após alguns minutos**

Isso sugere uma variável que se modifica com o tempo.

Possibilidades:

- aquecimento;
- saturação térmica;
- VRAM atingindo temperatura elevada;
- VRM aquecendo;
- fonte entrando em condição instável;
- memória sendo progressivamente ocupada;
- vazamento de memória do programa;
- degradação após carga contínua.

# **O teste da captura de tela**

Uma técnica simples consiste em produzir uma captura de tela enquanto o artefato está visível.

## **Se o artefato aparece na captura**

Isso sugere que a corrupção já estava presente no quadro produzido ou armazenado pelo sistema.

Hipóteses:

- aplicação;
- motorista;
- GPU;
- VRAM;
- composição gráfica;
- framebuffer.

## **Se o artefato não aparece na captura**

A falha pode estar em uma etapa posterior à captura.

Hipóteses:

- traz;
- cabo;
- monitor;
- processamento da tela;
- caminho de exibição.

Entretanto, essa técnica possui limitações.

Alguns problemas de:

- sobreposição de vídeo;
- digitalização;
- sincronização;
- composição;
- caminho de exibição;

podem não ser registrados corretamente pela captura.

Portanto:

A captura de tela ajuda a localizar a etapa da falha, mas não constitui prova definitiva.

Uma fotografia ou gravação externa do monitor também deve ser preservada como evidência.

# **A importância de reproduzir o defeito**

Antes de testar qualquer hipótese, precisamos conseguir reproduzir o problema de maneira relativamente controlada.

Inscreva-se:

- programa utilizado;
- versão;
- resolução;
- configurações gráficas;
- duração até a falha;
- temperatura ambiente;
- driver instalado;
- frequência da GPU;
- frequência da memória;
- consumo;
- temperatura;
- uso de VRAM;
- comportamento do sistema.

Exemplo:

Jogo.........................Aplicação A

Resolução....................2560 × 1440

Qualidade....................Alta

Driver.......................Versão registrada

Tempo até o defeito..........18 a 22 minutos

Temperatura da GPU...........78 °C

Hotspot......................102 °C

Uso da GPU...................99%

Uso de VRAM..................10,8 GB

Clock da memória.............valor registrado

Sintoma......................Blocos coloridos e tela preta

Sem esse registro, torna-se difícil comparar antes e depois de cada alteração.

# **O princípio da alteração única**

Durante o diagnóstico, devemos modificar apenas uma variável por vez.

Exemplo inadequado:

- atualizar o driver;
- trocar o cabo;
- reduzir o clock;
- abrir o gabinete;
- trocar a fonte;
- reinstalar o jogo;

tudo ao mesmo tempo.

Mesmo que o problema desapareça, não saberemos qual mudança foi responsável.

Exemplo adequado:

1. reproduzir e registrar;
2. trocar apenas o cabo;
3. repetir o teste;
4. registrar;
5. restaurar ou manter a alteração;
6. modificar a próxima variável.

Esse método transforma tentativas em investigação.

# **Primeira etapa - Confirmar a cadeia de vídeo**

Antes de testar a placa sob carga, elimine problemas simples.

Verifique:

- cabo completamente encaixado;
- porta correta;
- monitor configurado para a entrada adequada;
- presença de adaptadores;
- danos no conector;
- outra porta disponível;
- outro cabo conhecido;
- outro monitor;
- taxa de atualização;
- resolução;
- HDR ou recursos avançados.

Esses testes são:

- rápidos;
- pouco invasivos;
- de baixo risco;
- úteis para reduzir hipóteses.

# **Segunda etapa - Determinar se o problema é específico de uma aplicação**

Pergunte:

- O defeito ocorre em todos os jogos?
- Ocorre em programas profissionais?
- Ocorre ao reproduzir vídeos?
- Ocorre na área de trabalho?
- Ocorre em uma instalação limpa?
- Ocorre em APIs gráficas diferentes?
- Ocorre em outra versão do programa?

Se o problema aparece apenas em uma aplicação, investigue:

- integridade dos arquivos;
- atualizações;
- shaders;
- modificações;
- configurações;
- incompatibilidade;
- bug conhecido;
- consumo de VRAM;
- recursos específicos.

Não devemos submeter imediatamente a placa a procedimentos físicos por causa de um defeito isolado em um único programa.

# **Terceira etapa - Retornar às configurações padrão**

Overclock e undervolt alteram as condições de operação.

Antes de concluir que existe defeito, registre e restaure temporariamente:

- relógio da GPU;
- clock da memória;
- limite de potência;
- curva de tensão;
- curva de ventoinha;
- parâmetros do processador;
- perfil da memória RAM.

Até mesmo um ajuste que funcionou durante meses pode se tornar instável devido a:

- temperatura ambiente;
- envelhecimento;
- atualização de driver;
- mudança de carga;
- alteração de firmware;
- novo programa mais exigente.

A estabilidade não é garantida para sempre.

# **Quarta etapa - Analisar o driver**

## **Atualização não significa automaticamente melhoria**

Um driver novo pode:

- corrigir falhas;
- adicionar compatibilidade;
- melhorar desempenho;
- introduzir regressões;
- alterar gerenciamento de energia;
- mudar a compilação de shaders.

A investigação pode exigir comparar:

- versão atual;
- versão anterior estável;
- instalação limpa;
- driver fornecido pelo fabricante do notebook;
- driver genérico do fabricante da GPU.

Em notebooks, o fabricante do equipamento pode aplicar personalizações específicas.

## **Instalação limpa**

Uma instalação limpa procura reduzir resíduos de versões anteriores.

O procedimento deve ser feito com:

- driver correto;
- modelo confirmado;
- sistema compatível;
- ponto de restauração ou backup quando necessário;
- documentação do que foi removido e instalado.

Ferramentas de remoção profunda, como utilitários especializados, devem ser usadas com cuidado. Elas não são a primeira resposta para todo problema.

## **Monitor de Confiabilidade e Visualizador de Eventos**

No Windows, essas ferramentas podem ajudar a encontrar:

- falhas do driver;
- travamentos do aplicativo;
- desligamentos inesperados;
- erros de hardware;
- horários exatos dos eventos;
- padrões de repetição.

O registro não deve ser interpretado isoladamente.

Uma reinicialização inesperada indica que o sistema não foi encerrado corretamente, mas não determina automaticamente se a causa foi fonte, GPU, temperatura ou outra falha.

# **Quinta etapa - Monitoramento**

## **GPU-Z**

Pode apresentar:

- modelo identificado;
- revisão;
- tipo e quantidade de VRAM;
- largura do barramento;
- versão do VBIOS;
- Interface PCI Express;
- relógios;
- sensores;
- limite de desempenho;
- carga;
- temperatura.

Uma aplicação importante é observar o estado da interface PCI Express durante carga, não apenas em repouso.

## **HWiNFO**

Pode registrar:

- Temperatura da GPU;
- ponto de acesso;
- temperatura da memória, quando suportada;
- consumo;
- tensão informada;
- velocidade das ventoinhas;
- relógio central;
- clock da memória;
- utilização;
- limites térmicos;
- limites de potência;
- erros ou contadores disponíveis.

É recomendável usar a função de registro para criar um histórico.

O valor máximo sozinho pode esconder a sequência do problema.

## **MSI Afterburner**

Pode ser usado para monitoramento e exibição de métricas durante jogos.

Entretanto, alterações de clock e tensão devem ser evitadas até que exista uma hipótese clara.

No contexto inicial do curso, sua função principal será observar:

- carga;
- temperatura;
- relógio;
- consumo;
- VRAM;
- taxa de quadros;
- tempo de quadro.

## **Gerenciador de Tarefas**

Pode mostrar:

- Interface de GPU;
- mecanismo utilizado;
- memória dedicada;
- memória compartilhada;
- processos consumidores;
- atividade de codificação e decodificação.

Ele é útil para triagem, mas oferece menos profundidade que ferramentas especializadas.

# **Frametime e percepção de travamento**

A taxa de quadros média não conta toda a história.

Um jogo pode apresentar 90 quadros por segundo e ainda parecer travado se os quadros forem entregues de forma irregular.

O **frametime** representa o tempo entre os quadros.

Exemplo:

Quadros regulares:

11 ms - 11 ms - 12 ms - 11 ms

Quadros irregulares:

9 ms - 10 ms - 65 ms - 8 ms

Picos de frametime podem ser causados por:

- compilação de shaders;
- carregamento de dados;
- falta de VRAM;
- CPU;
- armazenamento;
- motorista;
- processo em segundo plano;
- temperatura;
- paginação;
- instabilidade.

Nem toda "travada da GPU" é defeito físico na placa.

# **Falta de VRAM não é o mesmo que VRAM defeituosa**

Quando a aplicação exige mais memória do que está disponível, podem ocorrer:

- quedas de desempenho;
- texturas carregando lentamente;
- uso de memória compartilhada;
- travamentos;
- gaguejar;
- redução automática de qualidade;
- fechamento do programa.

Isso não significa necessariamente que a VRAM esteja danificada.

Precisamos diferenciar:

VRAM insuficiente

≠

VRAM fisicamente defeituosa

## **VRAM insuficiente**

A capacidade não atende à carga.

## **VRAM defeituosa**

Os dados armazenados ou transferidos podem sofrer corrupção.

As duas situações podem provocar sintomas gráficos, mas exigem soluções completamente diferentes.

# **Testes de memória gráfica**

Existem ferramentas capazes de exercitar a memória da placa.

Elas podem ajudar a identificar:

- erros durante gravação e leitura;
- instabilidade com determinada ocupação;
- falha dependente de temperatura;
- problema relacionado ao clock.

Porém, um teste que não encontra erros não garante perfeição.

A falha pode:

- ocorrer somente em determinada temperatura;
- depender de um padrão específico;
- aparecer em outro nível de tensão;
- envolver o controlador;
- ser intermitente;
- acontecer apenas em uma aplicação.

Da mesma forma, um erro detectado não identifica automaticamente qual chip físico está com defeito.

# **Testes de estresse**

Ferramentas como OCCT e outros programas de carga podem exercitar:

- GPU;
- VRAM;
- consumo;
- temperatura;
- fonte;
- estabilidade geral.

Entretanto, testes intensos não devem ser executados indiscriminadamente.

Antes de começar:

- confirme que as ventoinhas funcionam;
- verifique a temperatura inicial;
- encerre trabalhos importantes;
- mantenha o monitoramento visível;
- defina critérios de interrupção;
- evite testar hardware com cheiro, fumaça ou danos;
- não utilize carga extrema em uma placa já instável sem necessidade.

O objetivo é reproduzir o problema de forma controlada, não "forçar até quebrar".

# **Quando interromper um teste**

Pare imediatamente diante de:

- cheiro de queimado;
- fumaça;
- faísca;
- conector aquecido;
- cabo escurecido;
- ventoinha parada;
- temperatura aumentando sem controle;
- ruído elétrico anormal;
- vazamento;
- repetidos desligamentos;
- perda de vídeo acompanhada de sinais elétricos;
- deformação física.

Segurança é mais importante que concluir o benchmark.

# **temperatura da GPU**

A leitura principal representa uma região ou estimativa térmica do chip.

Seu significado depende do modelo.

Não existe um único valor universal que determine falha em todas as GPUs.

Precisamos verificar:

- limite do fabricante;
- comportamento de frequência;
- estabilidade;
- carga;
- temperatura ambiente;
- projeto do cooler.

# **Ponto de acesso**

O hotspot representa uma leitura relacionada à região mais quente observada pelos sensores internos.

A diferença entre a temperatura principal e o hotspot pode ajudar a investigar:

- distribuição térmica;
- contato;
- pressão;
- pasta térmica;
- superfície;
- concentração de carga.

Entretanto, a interpretação depende do projeto específico.

Uma diferença alta é uma evidência a ser investigada, não uma autorização automática para desmontar a placa.

# **Temperatura da memória**

Algumas placas fornecem leitura da memória; outras não.

Temperaturas elevadas podem estar associadas a:

- carga pesada;
- pads inadequados;
- dissipador sem contato;
- fluxo de ar;
- mineração anterior;
- montagem incorreta;
- projeto da placa;
- ambiente.

A substituição de thermal pads exige conhecer:

- espessura;
- compressibilidade;
- posição;
- condutividade;
- pressão final.

Um pad com espessura errada pode melhorar o contato da memória e piorar o contato da GPU, ou vice-versa.

Portanto, não deve ser substituído por tentativa.

# **Sistema de refrigeração da GPU**

A refrigeração pode envolver:

- base de metal;
- tubos de calor;
- câmara de vapor;
- dissipador;
- ventoinhas;
- pasta térmica;
- almofadas térmicas;
- placa traseira;
- fluxo de ar do gabinete.

Problemas possíveis:

- dissipador sujo;
- ventoinha defeituosa;
- curva inadequada;
- pasta degradada;
- pads danificados;
- pressão desigual;
- Tubo de calor comprometido;
- gabinete restritivo;
- recirculação de ar quente.

A temperatura da GPU deve ser analisada juntamente com:

- rotação das ventoinhas;
- ponto de acesso;
- relógio;
- consumo;
- temperatura ambiente;
- desempenho;
- tempo até a falha.

# **Alimentação da placa de vídeo**

A energia pode vir:

- slot PCI Express;
- de conectores auxiliares;
- de ambos.

Problemas de alimentação podem envolver:

- fonte inadequada;
- cabo incorreto;
- adaptador;
- conector parcialmente encaixado;
- terminal danificado;
- cabo modular incompatível;
- divisão inadequada da carga;
- queda durante transitórios;
- VRM da própria placa.

Uma leitura normal por software não comprova a integridade da alimentação durante eventos rápidos.

# **Um cabo ou dois cabos de alimentação?**

Determinadas placas possuem mais de um conector auxiliar.

Dependendo da potência, da fonte e das orientações do fabricante, pode ser preferível utilizar cabos separados em vez de um único cabo com duas derivações.

A decisão deve considerar:

- manual da placa;
- documentação da fonte;
- corrente;
- conectores;
- projeto do cabo;
- consumo.

Não existe uma regra simplificada aplicável a todas as fontes e placas.

# **Instabilidade da fonte ou defeito da GPU?**

Considere este cenário:

- a imagem desaparece durante carga;
- os ventiladores continuam girando;
- o computador reinicia;
- o problema começou após instalar uma GPU mais potente;
- a fonte é antiga;
- foi utilizado adaptador;
- temperaturas estão normais.

A fonte se torna uma hipótese importante.

Mas precisamos considerar também:

- GPU defeituosa;
- cabo de alimentação;
- slot;
- placa-mãe;
- motorista;
- memória;
- curto;
- limite de potência;
- instalação elétrica.

O teste com uma fonte de referência adequada pode ajudar a isolar a variável.

# **PCI Express e mau contato**

Problemas no encaixe podem produzir:

- ausência de vídeo;
- detecção intermitente;
- funcionamento em modo reduzido;
- travamentos;
- erros sob movimentação;
- falha após transporte.

A investigação pode incluir, com o equipamento desligado e desconectado:

- inspeção do slot;
- confirmação do travamento físico;
- verificação de apoio da placa;
- observação de empenamento;
- inspeção dos contatos;
- teste em outro slot compatível;
- remoção de extensores ou risers.

Risers e extensores podem introduzir:

- perda de sinal;
- incompatibilidade de geração;
- instabilidade;
- limitações;
- mau contato.

Um teste direto no slot principal pode ser útil.

# **O peso da placa**

Placas grandes podem exercer força sobre o slot.

Isso pode causar:

- inclinação;
- mau contato;
- tensão mecânica;
- deformação;
- danos após transporte.

Um suporte pode ajudar, mas precisa ser instalado sem empurrar excessivamente a placa para cima.

O objetivo é sustentar, não deformar.

# **Teste com vídeo integrado**

Quando o processador possui gráficos integrados, podemos remover temporariamente a placa dedicada e testar o sistema com a saída da placa-mãe.

Esse teste ajuda a responder:

- o computador ainda está estável sem a GPU dedicada?
- o problema visual desaparece?
- o sistema operacional funciona?
- outros componentes permanecem normais?

Entretanto, o desaparecimento do problema não prova imediatamente que o núcleo da GPU esteja defeituoso.

Também foram removidos:

- cabos de alimentação da GPU;
- carga adicional sobre a fonte;
- driver específico;
- Vaga ocupada;
- calor produzido pela placa.

O resultado reduz hipóteses, mas precisa ser interpretado corretamente.

# **Teste da placa em outro computador**

Instalar a GPU em outro sistema compatível pode ser um teste muito útil.

Porém, o segundo computador deve possuir:

- fonte adequada;
- slot compatível;
- espaço físico;
- cabos corretos;
- sistema estável;
- drivers apropriados.

## **Se o defeito acompanha a placa**

A suspeita sobre a própria placa aumenta.

## **Se o defeito desaparece**

Pode existir interação com:

- fonte;
- placa-mãe;
- motorista;
- firmware;
- sistema operacional;
- cabo;
- gabinete;
- temperatura.

Mesmo um teste cruzado precisa ser documentado.

# **Teste de outra GPU no computador original**

Esse teste também pode ajudar.

Se uma placa conhecida funciona normalmente no mesmo sistema, a suspeita sobre a primeira GPU aumenta.

Mas é necessário comparar:

- consumo;
- conectores;
- geração;
- motorista;
- tamanho;
- carga.

Uma GPU de baixo consumo funcionando normalmente não prova que a fonte suporta uma GPU de alto desempenho.

# **Artefato na BIOS: o que isso elimina?**

Quando o artefato aparece no firmware, podemos reduzir a prioridade de hipóteses como:

- driver gráfico do Windows;
- configuração de um jogo;
- arquivos de uma aplicação;
- aceleração específica do navegador.

Continuam relevantes:

- GPU;
- VRAM;
- VBIOS;
- cabo;
- monitor;
- traz;
- slot;
- alimentação.

A palavra correta é "reduzir", não "eliminar absolutamente", pois ainda podem existir interações de firmware e modos de vídeo.

# **Artefato apenas em vídeos**

Se o problema surge ao reproduzir vídeos, investigue:

- aceleração de hardware;
- decodificador;
- motorista;
- navegador;
- codec;
- mecanismo de vídeo da GPU;
- HDR;
- proteção de conteúdo;
- cabo;
- monitor.

A GPU possui blocos especializados para vídeo. Uma falha nesse cenário não significa necessariamente que os núcleos gráficos usados em jogos estejam defeituosos.

# **Artefato apenas no navegador**

Possíveis hipóteses:

- aceleração de hardware;
- motorista;
- navegador;
- extensão;
- composição da área de trabalho;
- codec;
- atualização recente.

Um teste controlado pode comparar o navegador:

- com aceleração ativada;
- com aceleração desativada;
- sem extensões;
- em outro perfil;
- em outro navegador.

A alteração deve ser registrada.

# **Artefato apenas em um monitor**

Se o computador utiliza dois monitores e apenas um apresenta falhas, investigue:

- cabo;
- traz;
- taxa de atualização;
- resolução;
- monitor;
- HDR;
- sincronização adaptativa;
- adaptador;
- largura de banda.

Também é útil inverter os cabos e as portas.

Pergunta central:

O problema acompanha o monitor, o cabo ou a saída da placa?

# **Resolução e taxa de atualização**

Quanto maior a resolução e a taxa de atualização, maior pode ser a quantidade de dados transmitida.

Problemas podem surgir quando:

- o cabo não atende à largura de banda;
- o adaptador possui limitação;
- a porta trabalha em uma versão inferior;
- a profundidade de cor foi aumentada;
- o HDR está ativo;
- existe compressão ou negociação inadequada.

Se o problema desaparece ao reduzir temporariamente a taxa de atualização, isso não condena automaticamente a GPU.

A cadeia de transmissão deve ser investigada.

# **Drivers, firmware e sistema operacional**

A camada de software inclui:

- Driver de GPU;
- núcleo;
- sistema operacional;
- bibliotecas gráficas;
- APIs;
- jogo ou programa;
- compiladores de shaders;
- serviços em segundo plano;
- sobreposições;
- ferramentas de monitoramento.

Sobreposições podem ser fornecidas por:

- plataformas de jogos;
- gravadores;
- aplicativos de comunicação;
- monitoramento;
- Software e GPU.

Conflitos podem provocar:

- travamentos;
- imagem preta;
- falhas na captura;
- queda de desempenho.

Desabilitar temporariamente overlays é um teste válido quando o problema aparece somente em determinadas aplicações.

# **Malware também pode afetar desempenho?**

Sim, embora não seja a primeira hipótese em todo caso.

Programas maliciosos podem:

- usar uma GPU;
- realizar mineração;
- consumir memória;
- alterar drivers;
- causar instabilidade;
- interferir no sistema.

A investigação deve considerar:

- processos desconhecidos;
- uso da GPU em repouso;
- inicialização automática;
- alterações recentes;
- integridade do sistema.

Esse ponto conecta a aula ao futuro módulo de Segurança da Informação.

# **Linux e investigação gráfica**

Em sistemas Linux, algumas evidências podem ser encontradas em:

- registros do kernel;
- mensagens do driver;
- registros da sessão gráfica;
- ferramentas específicas do fabricante;
- informações do PCI Express.

Dependendo da GPU e do driver, podem ser usados recursos como:

- journalctl;
- dmesg;
- ferramentas do driver;
- utilitários de monitoramento;
- informações do sistema.

A interpretação exige considerar:

- driver proprietário ou aberto;
- servidor gráfico;
- núcleo;
- distribuição;
- firmware.

A ausência de um erro explícito no registro não garante ausência de falha física.

# **Erros de hardware registrados pelo sistema**

Algumas plataformas conseguem registrar eventos relacionados a:

- barramento PCI Express;
- memória;
- comunicação;
- correções;
- falhas de dispositivo.

Esses registros ajudam a correlacionar o horário do problema com a atividade da GPU.

Entretanto, um erro no barramento pode ser causado por:

- placa de vídeo;
- slot;
- placa-mãe;
- riser;
- alimentação;
- firmware;
- sinalização.

O registro indica a região do problema, não necessariamente a peça exata.

# **Reflow e reballing não são sinônimos**

Esses termos são frequentemente usados incorretamente.

## **Refluxo**

Consiste em aquecer uma soldagem existente para que o material passe por um novo ciclo térmico.

Procedimentos improvisados com:

- forno doméstico;
- soprador;
- secador;
- festa;
- aquecimento sem controle;

não constituem diagnóstico profissional.

Podem:

- deformar a placa;
- deslocar componentes;
- danificar conectores;
- degradar capacitores;
- liberar vapores;
- produzir curto;
- mascarar temporariamente o defeito;
- destruir evidências.

Uma melhora temporária após aquecimento não prova qual componente estava com defeito.

A temperatura pode modificar temporariamente:

- contato;
- resistência;
- expansão de materiais;
- comportamento de semicondutores.

## **Reballing**

O reballing envolve remover um componente BGA, limpar as conexões e refazer suas esferas de solda antes da reinstalação.

É um procedimento especializado que exige:

- estação adequada;
- controle térmico;
- alinhamento;
- perfil de temperatura;
- experiência;
- inspeção;
- conhecimento da placa.

Mesmo um reballing tecnicamente perfeito não corrige:

- núcleo gráfico danificado;
- VRAM defeituosa;
- controlador interno falho;
- trilha rompida;
- VRM defeituoso;
- firmware corrompido.

Reballing só faz sentido quando existem evidências de que a falha está relacionada às conexões BGA.

Usá-lo como solução universal é substituir diagnóstico por tentativa.

# **Por que algumas placas "voltam" depois de aquecidas?**

Uma melhora temporária pode ocorrer porque o calor modifica momentaneamente:

- expansão dos materiais;
- contato elétrico;
- microfissuras;
- propriedades de componentes;
- umidade;
- resistência.

Isso não significa que a placa foi reparada.

Se a causa não foi identificada e corrigida, o problema pode retornar.

Além disso, sucessivos ciclos térmicos improvisados podem agravar o dano.

# **Como um laboratório profissional investigaria?**

Dependendo do sintoma e do valor do equipamento, um laboratório pode utilizar:

- fonte de bancada;
- multímetro;
- osciloscópio;
- câmera térmica;
- microscópio;
- estação de retrabalho;
- planos;
- vistas do conselho;
- análise de sinais;
- teste de tensões;
- inspeção de curtos;
- comparação com placa funcional;
- diagnóstico da VRAM;
- análise de firmware.

Uma investigação eletrônica pode procurar:

- tensões ausentes;
- curto em determinada linha;
- componente aquecendo anormalmente;
- sequência incorreta de inicialização;
- falha de alimentação;
- comunicação interrompida;
- chip de memória com erros.

O estudante não precisa possuir esses equipamentos para compreender o raciocínio.

O objetivo é reconhecer que um diagnóstico avançado depende de medições, e não apenas da aparência do defeito.

# **Fluxo profissional de diagnóstico**

1\. Confirmar e documentar o sintoma

↓

2\. Determinar quando ele aparece

↓

3\. Verificar cabo, monitor e portas

↓

4\. Restaurar configurações padrão

↓

5\. Analisar aplicação e driver

↓

6\. Monitorar temperatura, clock e potência

↓

7\. Avaliar alimentação e PCI Express

↓

8\. Realizar testes controlados

↓

9\. Fazer testes cruzados

↓

10\. Encaminhar para diagnóstico eletrônico

Não é obrigatório executar todas as etapas em todos os casos.

A sequência deve ser adaptada às evidências e aos riscos.

# **Matriz investigativa**

| **Sintoma**                           | **Evidência importante**                 | **Hipóteses prioritárias**                    |
| ------------------------------------- | ---------------------------------------- | --------------------------------------------- |
| Artefatos na UEFI                     | O sistema operacional ainda não carregou | GPU, VRAM, cabo, monitor, VBIOS               |
| ---                                   | ---                                      | ---                                           |
| Falha em um único jogo                | Outros programas funcionam               | Aplicação, arquivos, driver, configuração     |
| ---                                   | ---                                      | ---                                           |
| Tela preta com áudio                  | Sistema continua parcialmente ativo      | Driver, cabo, porta, sinal, GPU               |
| ---                                   | ---                                      | ---                                           |
| Reinicialização completa sob carga    | Sistema perde estabilidade geral         | Fonte, GPU, temperatura, placa-mãe            |
| ---                                   | ---                                      | ---                                           |
| Erros após aquecimento                | O tempo e a temperatura influenciam      | Refrigeração, VRAM, VRM, GPU                  |
| ---                                   | ---                                      | ---                                           |
| Problema em apenas um monitor         | Outro monitor funciona                   | Cabo, porta, monitor, configuração            |
| ---                                   | ---                                      | ---                                           |
| Artefato aparece na captura           | Corrupção existe antes da tela           | Aplicação, driver, GPU, VRAM                  |
| ---                                   | ---                                      | ---                                           |
| Artefato não aparece na captura       | Pode estar após o framebuffer            | Cabo, porta, monitor, scanout                 |
| ---                                   | ---                                      | ---                                           |
| Queda de desempenho sem artefatos     | Clock ou potência diminuem               | Temperatura, limite de potência, CPU          |
| ---                                   | ---                                      | ---                                           |
| Erro apenas com alta ocupação de VRAM | Problema depende da capacidade usada     | VRAM insuficiente, chip defeituoso, aplicação |
| ---                                   | ---                                      | ---                                           |

A tabela orienta a investigação, mas não substitui os testes.

# **Laboratório guiado - investigação não invasiva**

Esta atividade não exige desmontar a placa.

## **Etapa 1 - Identificação**

Inscreva-se:

- fabricante;
- modelo;
- quantidade e tipo de VRAM;
- versão do driver;
- versão do VBIOS;
- Interface PCI Express;
- fonte utilizada;
- conectores de alimentação;
- monitor;
- cabo;
- resolução;
- taxa de atualização.

## **Estágio 2 - Estado inicial**

Sem executar carga intensa, registre:

- Temperatura da GPU;
- ponto de acesso;
- temperatura da memória, quando disponível;
- relógio;
- Interface de GPU;
- uso da VRAM;
- velocidade das ventoinhas;
- consumo.

Observe também:

- uso inesperado em repouso;
- ventoinhas paradas;
- ruído;
- oscilação;
- processos utilizando a GPU.

## **Etapa 3 - Reprodução**

Utilize a aplicação em que o defeito costuma ocorrer.

Inscreva-se:

- horário de início;
- tempo até a falha;
- temperaturas;
- relógios;
- consumo;
- uso de VRAM;
- limite de desempenho;
- comportamento das ventoinhas;
- descrição exata do sintoma.

## **Etapa 4 - Evidência visual**

Faça:

- captura de tela;
- fotografia externa;
- gravação;
- anotação do momento;
- registro dos sensores.

Compare a captura com a fotografia.

## **Etapa 5 - Testes da cadeia de exibição**

Altere uma variável por vez:

1. outro cabo;
2. outra porta;
3. outra entrada do monitor;
4. outro monitor;
5. resolução temporariamente menor;
6. taxa de atualização temporariamente menor.

Registre cada resultado.

## **Etapa 6 - Configurações padrão**

Desative temporariamente:

- overclock;
- subtensão;
- perfil personalizado;
- limite de potência alterado;
- curva extrema;
- overlays desnecessários.

Repita o teste.

## **Etapa 7 - Software**

Avalie:

- integridade da aplicação;
- versão do driver;
- instalação limpa, quando justificada;
- outra aplicação;
- registros do sistema;
- Monitor de Confiabilidade;
- processos em segundo plano.

## **Etapa 8 - Conclusão provisória**

Exemplo:

Os artefatos aparecem somente após alta ocupação da VRAM, continuam presentes em duas aplicações diferentes, são registrados na captura de tela e permanecem após a restauração das configurações padrão. Cabo e monitor foram descartados. As evidências aumentam a suspeita sobre o subsistema de memória gráfica, mas ainda não identificam se a origem está nos chips, no controlador, na alimentação ou na placa.

Essa é uma conclusão técnica.

Ela reconhece o que foi demonstrado e o que ainda não foi confirmado.

# **Estudo de Caso 1 - Artefatos na UEFI**

Sintomas:

- blocos coloridos desde a inicialização;
- problema visível no menu do firmware;
- mesmo comportamento em dois monitores;
- dois cabos testados;
- placa utiliza configurações padrão;
- artefato acompanha a GPU para outro computador.

## **Análise**

As evidências reduzem significativamente a probabilidade de:

- jogo;
- driver principal do sistema;
- cabo;
- monitor;
- sistema operacional.

A suspeita sobre o hardware da placa aumenta.

Ainda pode ser necessário investigar:

- GPU;
- VRAM;
- VBIOS;
- alimentação;
- trilhas;
- soldagem.

# **Estudo de Caso 2 - Pontos brilhantes em alta frequência**

Sintomas:

- imagem normal em 60 Hz;
- pontos aparecem em 144 Hz;
- problema ocorre apenas em um monitor;
- desaparece com outro cabo;
- capturas de tela permanecem normais.

## **Conclusão provisória**

As evidências apontam primeiro para a cadeia de transmissão, especialmente o cabo anterior.

Não há base para concluir que a GPU está queimada.

# **Estudo de Caso 3 - Tela preta e reinicialização do driver**

Sintomas:

- tela apaga por três segundos;
- áudio continua;
- imagem retorna;
- sistema registra reinicialização do driver;
- problema surgiu após atualização;
- temperaturas normais;
- configurações padrão;
- versão anterior do driver não apresentava o defeito.

## **Conclusão provisória**

Existe forte relação temporal com a atualização.

Uma regressão de driver é hipótese prioritária.

O hardware não pode ser considerado absolutamente descartado, mas a evidência favorece primeiro a investigação da camada de software.

# **Estudo de Caso 4 - Travamento após aquecimento**

Sintomas:

- placa funciona por aproximadamente vinte minutos;
- hotspot sobe continuamente;
- clock começa a cair;
- ventoinhas atingem rotação máxima;
- artefatos surgem pouco antes do travamento;
- temperatura cai significativamente com o painel frontal removido.

## **Conclusão provisória**

O problema apresenta forte dependência térmica.

Devem ser investigados:

- fluxo de ar;
- dissipador;
- ventoinhas;
- contato;
- pasta térmica;
- almofadas;
- temperatura da memória;
- VRM.

Ainda não existe fundamento para afirmar que o chip gráfico esteja permanentemente danificado.

# **Estudo de Caso 5 - Reinicialização após upgrade**

Sintomas:

- computador era estável com GPU anterior;
- nova placa possui consumo muito maior;
- fonte antiga;
- adaptador utilizado;
- sistema reinicia sob carga simultânea de CPU e GPU;
- teste leve da GPU isolada nem sempre reproduz a falha.

## **Conclusão provisória**

A alimentação se torna uma hipótese central.

O teste precisa considerar:

- fonte;
- adaptador;
- conectores;
- carga combinada;
- transitórios;
- cabos;
- recomendações do fabricante.

A GPU nova não deve ser condenada antes de testar uma alimentação adequada.

# **Mito ou Evidência?**

## **"Artefatos sempre significam que a GPU queimou"**

**Mito.**

Podem envolver VRAM, driver, cabo, monitor, temperatura, alimentação, software e outros subsistemas.

## **"Se o artefato aparece na UEFI, o driver do Windows é a causa"**

**Mito.**

O driver principal do Windows ainda não está operando nessa etapa.

## **"Se o problema aparece apenas em um jogo, a placa está inocentada"**

**Mito.**

O jogo pode ativar uma carga ou recurso que expõe uma instabilidade física.

## **"Captura de tela e fotografia externa podem ajudar a localizar a falha"**

**Evidência.**

A comparação pode indicar se a corrupção ocorre antes ou depois do caminho de exibição.

## **"Uma placa pode passar em um teste e falhar em outro"**

**Evidência.**

Diferentes testes utilizam unidades, padrões, memória e níveis de potência distintos.

## **"Reballing corrige qualquer placa que apresenta artefatos"**

**Mito.**

Ele não corrige chip danificado, VRAM defeituosa, VRM, firmware ou diversas outras falhas.

## **"Uma redução de clock pode ser proteção térmica ou limite de potência"**

**Evidência.**

É necessário verificar qual limite está ativo.

## **"O desaparecimento do problema com outra GPU prova que a fonte está perfeita"**

**Mito.**

A segunda GPU pode exigir muito menos energia.

# **O que um perito observaria?**

- O defeito aparece antes do sistema operacional?
- O artefato é registrado em captura de tela?
- A falha acompanha a placa em outro computador?
- O problema ocorre em todos os programas?
- Existe relação com temperatura?
- A ocupação da VRAM influencia o sintoma?
- O clock da memória está padrão?
- O driver foi alterado recentemente?
- Existem erros no sistema?
- A interface PCI Express está estável?
- Há riser ou extensor?
- A fonte é adequada?
- Os cabos pertencem ao modelo da fonte?
- Os conectores estão totalmente inseridos?
- Há sinais de aquecimento nos terminais?
- O hotspot apresenta comportamento anormal?
- As ventoinhas respondem corretamente?
- A placa sofreu queda, transporte ou manutenção?
- O VBIOS foi modificado?
- Existem indícios de mineração ou uso intenso anterior?
- As tentativas realizadas foram documentadas?
- Um teste de estresse é realmente necessário e seguro?
- O caso já exige diagnóstico eletrônico?

# **Desafio do Dossiê**

Uma placa de vídeo apresenta:

- funcionamento normal na área de trabalho;
- artefatos em dois jogos diferentes;
- erros apenas após 8 GB de VRAM ocupados;
- captura de tela registra a corrupção;
- outro cabo não altera o comportamento;
- outro monitor não altera o comportamento;
- clocks estão em padrão;
- temperaturas da GPU e hotspot permanecem dentro do comportamento esperado;
- instalação limpa do driver não resolve;
- a placa apresenta o mesmo defeito em outro computador.

Elabore uma investigação contendo:

1. evidências já coletadas;
2. hipóteses que perderam força;
3. subsistemas que permanecem sob suspeita;
4. por que a ocupação da memória é relevante;
5. limitações de um teste de VRAM;
6. por que ainda não é possível identificar um chip específico;
7. qual seria o próximo nível de diagnóstico;
8. qual conclusão provisória poderia ser apresentada ao cliente.