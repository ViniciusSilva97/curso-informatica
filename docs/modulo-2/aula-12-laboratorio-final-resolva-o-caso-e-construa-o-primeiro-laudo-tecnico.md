# Módulo 2 — Investigação Computacional I
## Anatomia do Hardware

# Aula 12 — Laboratório Final: Resolva o Caso e Construa o Primeiro Laudo Técnico

> **Pergunta da investigação**
>
> Diante de um computador com sintomas mistos, informações incompletas e algumas pistas enganosas, você consegue organizar as evidências, testar hipóteses e chegar a uma conclusão técnica defensável?

---

# 📁 Dossiê da Investigação

## Caso final — O computador que reinicia, fica lento e às vezes perde vídeo

Chegamos ao encerramento do Módulo 2.

Até aqui, investigamos separadamente:

- processador;
- memória RAM;
- armazenamento;
- placa-mãe;
- fonte de alimentação;
- refrigeração;
- placa de vídeo;
- monitor e cabos;
- ruídos;
- metodologia de diagnóstico.

Agora essas áreas deixam de aparecer isoladamente.

Você receberá um computador como ele chegaria a uma bancada real:

> **com sintomas misturados, informações incompletas e mais de uma hipótese plausível.**

O objetivo não é adivinhar rapidamente qual peça está com defeito.

O objetivo é construir uma investigação.

---

# O desafio

Uma pequena empresa utiliza um computador para:

- navegação;
- planilhas;
- videoconferências;
- edição leve de imagens;
- treinamento interno;
- ocasionalmente jogos após o expediente.

O responsável relata:

> “O computador ficou estranho nas últimas semanas. Às vezes está muito lento, duas vezes reiniciou durante uma reunião e ontem a tela ficou preta. Hoje demorou para ligar. Acho que a placa de vídeo está queimando.”

A máquina chega à bancada.

Você ainda não deve aceitar nenhuma conclusão.

Temos apenas um relato.

---

# Objetivos do laboratório

Neste laboratório você deverá praticar:

- recepção do equipamento;
- separação entre relato e evidência;
- avaliação de risco;
- construção de linha do tempo;
- inventário de hardware;
- observação inicial;
- interpretação de sensores;
- análise de logs;
- avaliação de armazenamento;
- análise de memória;
- investigação gráfica;
- avaliação de alimentação;
- testes cruzados;
- eliminação de hipóteses;
- validação da correção;
- produção de um laudo técnico.

Não existe uma única ferramenta capaz de resolver todo o caso.

Você precisará raciocinar sobre o conjunto.

---

# Regras do laboratório

Antes de começar, siga quatro regras.

## Regra 1 — Não altere tudo ao mesmo tempo

Cada teste deve responder a uma pergunta.

## Regra 2 — Diferencie fato de interpretação

Exemplo:

**Fato**

> O computador reiniciou durante carga combinada.

**Interpretação**

> A fonte pode estar relacionada.

## Regra 3 — Não condene componentes cedo demais

Um sintoma pode possuir várias causas.

## Regra 4 — Registre o que mudou

Se uma alteração modifica o comportamento, ela se torna evidência.

---

# Fase 1 — Recepção

O cliente entrega o equipamento e informa:

- o problema começou há aproximadamente três semanas;
- o computador já funcionava normalmente antes;
- nenhuma peça foi trocada recentemente;
- o Windows recebeu atualizações automáticas;
- o gabinete foi transportado de um cômodo para outro;
- o computador reiniciou duas vezes em videoconferência;
- uma vez ficou com tela preta, mas o áudio continuou;
- algumas vezes demora para abrir arquivos;
- em certos momentos as ventoinhas ficam mais barulhentas;
- existem arquivos importantes no SSD;
- não existe backup recente.

Nesse momento, ainda não há diagnóstico.

---

# Registro inicial

Um técnico profissional poderia registrar:

```text
Equipamento recebido:
Desktop de uso misto.

Sintomas relatados:
- lentidão intermitente;
- duas reinicializações;
- uma ocorrência de tela preta;
- aumento ocasional de ruído das ventoinhas;
- inicialização lenta em alguns momentos.

Dados importantes:
Sim.

Backup recente:
Não confirmado.

Alterações recentes:
- atualizações automáticas do sistema;
- transporte físico do gabinete.

Intervenções anteriores:
Não informadas.
```

---

# Primeira decisão profissional

Como existem dados importantes sem backup confirmado, qualquer teste que possa aumentar o risco do armazenamento precisa ser avaliado com cuidado.

Ainda não há indicação de falha mecânica grave no dispositivo.

Mesmo assim, a preservação dos dados deve permanecer no planejamento.

---

# Fase 2 — Inspeção externa

Antes de ligar o equipamento, observamos:

- gabinete íntegro;
- nenhum cheiro de queimado;
- nenhum sinal de líquido;
- cabo de energia sem dano aparente;
- cabo DisplayPort conectado;
- monitor externo do laboratório ainda não foi conectado;
- filtro frontal bastante empoeirado;
- gabinete posicionado anteriormente próximo a uma parede;
- nenhuma porta externa quebrada.

Nada exige interrupção imediata.

---

# Fase 3 — Inventário

O computador possui:

```text
CPU.............Ryzen 5 5600
Placa-mãe.......B550
RAM.............16 GB DDR4
                 2 × 8 GB
GPU.............Radeon RX 6600
SSD.............NVMe 1 TB
Fonte...........550 W
Monitor.........2560 × 1440 / 165 Hz
Sistema.........Windows 11
```

A fonte possui potência nominal compatível em princípio com o conjunto.

Mas potência declarada não encerra a investigação.

---

# Fase 4 — Estado físico interno

Com o computador desligado e desconectado, o gabinete é aberto.

Observações:

- grande quantidade de poeira no filtro frontal;
- cooler do processador aparentemente firme;
- dois módulos de memória instalados;
- GPU corretamente fixada;
- cabo de energia da GPU aparentemente encaixado;
- nenhum capacitor visualmente danificado;
- nenhum conector derretido;
- uma ventoinha frontal possui bastante poeira;
- SSD NVMe sem dissipador adicional;
- nenhum cabo encostando nas pás;
- não existem marcas evidentes de líquido.

Nenhuma peça deve ser removida ainda.

---

# O que sabemos até aqui?

Temos:

- poeira;
- histórico de transporte;
- lentidão;
- reinicializações;
- uma tela preta;
- dados importantes;
- aumento de ruído.

Mas ainda não sabemos:

- se a poeira está causando superaquecimento;
- se a memória foi deslocada no transporte;
- se o SSD apresenta falha;
- se a fonte está instável;
- se a GPU possui problema;
- se o cabo ou monitor estão envolvidos;
- se o sistema operacional possui erros relevantes.

---

# Fase 5 — Primeiro acionamento

O computador é ligado em bancada com:

- monitor de referência;
- cabo DisplayPort conhecido;
- teclado e mouse simples;
- rede disponível.

Observações:

- POST concluído;
- sem beeps;
- LEDs de diagnóstico apagam normalmente;
- sistema operacional inicia;
- tempo de inicialização: aproximadamente 58 segundos;
- nenhum erro imediato na tela;
- ventoinhas audíveis, mas sem ruído mecânico anormal.

O computador está utilizável.

---

# Baseline inicial

Após cinco minutos em repouso:

```text
CPU..............4–8%
RAM..............13,8 GB / 16 GB
SSD..............2–15%
GPU..............1–3%

CPU..............47 °C
GPU..............43 °C
GPU Hotspot......51 °C
SSD..............58 °C
```

A primeira anomalia evidente não está na GPU.

A memória já está bastante ocupada em repouso.

---

# Fase 6 — Gerenciador de Tarefas

Os processos mostram:

- navegador com muitas abas;
- aplicativo de videoconferência iniciando automaticamente;
- sincronizador de arquivos;
- ferramenta de edição;
- software de comunicação;
- utilitário do fabricante;
- antivírus;
- alguns aplicativos em segundo plano.

Depois de alguns minutos:

```text
RAM:
14,7 GB / 16 GB

Memória disponível:
aproximadamente 900 MB
```

O sistema começa a utilizar paginação com maior intensidade.

---

# Evidência 1 — Pressão de memória

A lentidão pode ter relação com falta de memória disponível.

Mas isso não explica automaticamente:

- reinicialização;
- tela preta.

Portanto, podemos ter mais de um fenômeno no mesmo computador.

Essa é uma situação comum.

> **Um equipamento pode ter dois problemas diferentes ao mesmo tempo.**

---

# Fase 7 — Armazenamento

O SSD é analisado com ferramenta apropriada.

Dados observados:

```text
Saúde geral..............Sem alerta crítico
Temperatura..............59 °C
Erros críticos...........0
Media/Data Integrity.....0
Unsafe Shutdowns.........Alguns registros históricos
```

Nenhum indicador isolado comprova falha do SSD.

Durante cópia controlada de arquivos:

- velocidade inicialmente normal;
- temperatura sobe para 67 °C;
- desempenho reduz moderadamente;
- não ocorrem erros de leitura;
- não ocorre desconexão;
- nenhum arquivo falha.

---

# Evidência 2 — SSD quente, mas sem falha comprovada

A temperatura merece atenção.

Mas não temos evidência suficiente para afirmar:

> “O SSD está defeituoso.”

A lentidão observada pode estar sendo amplificada pela pressão de memória e paginação.

---

# Fase 8 — Logs do sistema

No Monitor de Confiabilidade aparecem:

- dois desligamentos inesperados;
- um evento de falha do driver gráfico;
- algumas falhas de aplicativo;
- nenhum padrão claro de erro de armazenamento.

No Visualizador de Eventos, próximo a uma das reinicializações:

- evento de desligamento inesperado;
- ausência de uma tela azul registrada;
- nenhum erro definitivo identificando a causa.

---

# Cuidado com o evento de desligamento inesperado

Um evento desse tipo prova que:

> o sistema não foi encerrado normalmente.

Ele não prova sozinho:

- fonte defeituosa;
- placa-mãe defeituosa;
- GPU defeituosa.

Precisamos reconstruir a cadeia causal.

---

# O evento de driver gráfico

A tela preta relatada pelo usuário ganha uma pista.

Mas lembre-se da Aula 8.

Um erro de driver pode ser:

- causa;
- consequência;
- reação do sistema a uma GPU que deixou de responder;
- resultado de alimentação instável;
- problema de software;
- erro específico de aplicação.

O log aumenta a relevância da cadeia gráfica.

Não encerra o diagnóstico.

---

# Fase 9 — Teste da memória

Antes de executar testes mais longos, os programas de inicialização desnecessários são encerrados apenas para estabelecer comparação.

A RAM cai para:

```text
7,1 GB / 16 GB
```

A responsividade melhora de forma perceptível.

Aplicativos abrem mais rapidamente.

A atividade do SSD diminui.

---

# Evidência 3 — Parte da lentidão foi explicada

Temos forte evidência de que a lentidão cotidiana estava relacionada à pressão de memória.

Mas ainda precisamos explicar:

- reinicializações;
- tela preta.

---

# Teste de estabilidade da RAM

É realizado um teste de memória adequado.

Primeira passagem:

```text
0 erros
```

Segunda passagem:

```text
0 erros
```

Isso reduz a suspeita de erro evidente nos módulos.

Mas nenhum teste garante ausência absoluta de qualquer falha possível.

---

# Fase 10 — Temperatura

Carga moderada de CPU:

```text
CPU..............75 °C
Clock............estável
Sem throttling relevante
```

Carga gráfica:

```text
GPU..............74 °C
Hotspot..........89 °C
Ventoinhas.......elevadas
Clock............estável
```

Carga combinada após dez minutos:

```text
CPU..............79 °C
GPU..............76 °C
Hotspot..........93 °C
SSD..............64 °C
```

As temperaturas são relativamente elevadas, mas não aparece throttling severo nem desligamento térmico.

---

# O filtro empoeirado importa?

Sim.

Ele pode:

- reduzir fluxo de ar;
- aumentar temperatura interna;
- elevar rotação das ventoinhas;
- aumentar ruído.

Isso explica parte do relato:

> “As ventoinhas ficam mais barulhentas.”

Mas ainda não explica necessariamente a reinicialização.

---

# Fase 11 — Reprodução da tela preta

Com o monitor e cabo de referência do laboratório:

- 1440p;
- 165 Hz;
- carga gráfica;
- 30 minutos.

Resultado:

```text
Nenhuma perda de sinal.
Nenhum artefato.
Nenhuma tela preta.
```

Com o cabo original do cliente conectado ao monitor de referência:

- 1440p;
- 165 Hz.

Após alguns minutos:

- uma piscada;
- perda de sinal de aproximadamente dois segundos;
- imagem retorna;
- computador continua executando;
- áudio continua.

Captura de tela realizada durante o comportamento:

- nenhuma corrupção visível.

---

# Evidência 4 — A cadeia externa de vídeo ganha força

Agora temos:

- defeito ausente com cabo de referência;
- defeito presente com cabo original;
- sistema permanece funcionando;
- captura sem defeito.

Isso reduz a probabilidade de corrupção do quadro antes da saída.

O cabo original torna-se uma hipótese forte para a tela preta.

---

# Teste controlado de taxa de atualização

Mesmo cabo original:

```text
165 Hz → falha intermitente
144 Hz → uma piscada após longo período
120 Hz → sem falha durante o teste
60 Hz  → sem falha
```

Mesmo monitor.

Mesma GPU.

Mesmo driver.

Mesma resolução.

A variável principal é a taxa de atualização.

Esse comportamento é compatível com um enlace que se torna marginal em maior largura de banda.

---

# Teste com cabo de referência

```text
165 Hz → estável
```

A evidência converge.

A tela preta relatada pelo cliente possui uma causa provável diferente da reinicialização.

---

# Fase 12 — Investigando as reinicializações

O computador ainda não reiniciou na bancada.

O cliente relatou duas ocorrências durante videoconferência.

Isso parece estranho.

Videoconferência não costuma representar a maior carga possível do sistema.

Mas o contexto importa.

Durante uma videoconferência podem ocorrer simultaneamente:

- vídeo;
- aceleração gráfica;
- navegador;
- sincronização;
- várias abas;
- webcam;
- áudio;
- rede;
- outros programas.

Ainda assim, precisamos reproduzir a condição.

---

# Carga isolada de CPU

Resultado:

```text
30 minutos
Estável
```

# Carga isolada de GPU

Resultado:

```text
30 minutos
Estável
```

# Carga de armazenamento

Resultado:

```text
Estável
```

# Carga combinada

Após aproximadamente 14 minutos:

> **o computador reinicia abruptamente.**

Não aparece tela azul.

---

# Evidência 5 — A reinicialização foi reproduzida

Agora possuímos uma condição concreta.

Isso muda completamente a investigação.

Não dependemos apenas do relato do usuário.

---

# O que estava acontecendo antes da reinicialização?

Telemetria registrada:

```text
CPU..............82 °C
GPU..............77 °C
GPU Hotspot......95 °C
SSD..............65 °C

Sem throttling crítico observado.
Sem artefato gráfico.
Sem erro de memória visível.
```

As temperaturas subiram.

Mas não existe evidência clara de que um limite térmico tenha provocado o reinício.

---

# Fase 13 — Inspeção do sistema de alimentação

A fonte é identificada corretamente.

Informações:

```text
Potência nominal........550 W
Idade aproximada........5 anos
Uso.....................frequente
Cabos...................originais
Conectores..............sem dano visível
```

Não há:

- cheiro;
- estalo;
- conector derretido;
- ruído elétrico preocupante.

A idade não prova defeito.

Mas a alimentação continua como hipótese.

---

# O software mostra 12 V normal

Durante parte do teste, o sensor informa valor próximo do esperado.

Isso não elimina a fonte.

Como vimos anteriormente:

- sensores podem ter limitações;
- leitura de software não captura necessariamente transientes;
- estabilidade dinâmica pode falhar mesmo quando médias parecem normais.

---

# Teste cruzado com fonte de referência

É utilizada uma fonte:

- conhecida;
- compatível;
- testada;
- com potência adequada;
- com cabos próprios.

Nenhum cabo modular da fonte antiga é reutilizado.

Esse detalhe é essencial.

---

# Resultado com a fonte de referência

Carga combinada:

```text
30 minutos → estável
45 minutos → estável
60 minutos → estável
```

Nenhuma reinicialização.

---

# Repetição com a fonte original

O sistema é montado novamente com a fonte original.

Mesma condição de teste.

Após aproximadamente 17 minutos:

> reinicialização abrupta.

---

# Evidência 6 — Comportamento acompanha a fonte original

Temos agora uma evidência convergente forte.

```text
Fonte original
→ falha reproduzida

Fonte de referência
→ falha não reproduzida

Fonte original novamente
→ falha reproduzida
```

Isso não exige abrir a fonte.

O sistema de alimentação original se torna a principal causa da reinicialização dentro do escopo dos testes realizados.

---

# Mas existe apenas um defeito?

Não.

Nosso caso apresenta pelo menos três fenômenos diferentes.

## Fenômeno A — Lentidão

Evidências:

- RAM próxima do limite;
- muitos programas;
- paginação;
- SSD trabalhando intensamente;
- melhora ao reduzir carga de memória.

## Fenômeno B — Tela preta

Evidências:

- ocorre com cabo original;
- desaparece com cabo de referência;
- mais frequente em 165 Hz;
- ausente em 120 Hz;
- captura de tela normal;
- sistema continua funcionando.

## Fenômeno C — Reinicialização

Evidências:

- ocorre em carga combinada;
- temperaturas sem limite crítico demonstrado;
- desaparece com fonte de referência;
- retorna com fonte original.

Esse é o ponto mais importante do laboratório.

> **Um relato pode misturar sintomas de causas diferentes.**

---

# O erro que um diagnóstico apressado cometeria

O cliente disse:

> “Acho que a placa de vídeo está queimando.”

Se aceitássemos essa hipótese imediatamente, poderíamos:

- condenar uma GPU funcional;
- ignorar a fonte;
- ignorar o cabo;
- ignorar a pressão de memória;
- gerar custo desnecessário.

O processo investigativo evitou isso.

---

# Fase 14 — Correções propostas

Com base nas evidências:

## 1. Sistema de alimentação

Recomendar substituição da fonte original por unidade adequada e confiável.

A fonte defeituosa não deve ser aberta pelo usuário.

## 2. Cabo de vídeo

Substituir o cabo original por cabo adequado ao modo utilizado.

Validar 1440p 165 Hz depois da troca.

## 3. Pressão de memória

Existem duas abordagens:

- reduzir programas de inicialização e uso simultâneo;
- avaliar expansão de memória conforme a carga real do usuário.

Não devemos vender memória apenas porque “16 GB é pouco”.

Devemos relacionar a recomendação ao uso observado.

## 4. Fluxo de ar

Realizar limpeza adequada de filtros e ventoinhas.

Depois validar temperaturas e ruído.

---

# Fase 15 — O que não foi necessário fazer

Não foi necessário:

- formatar o Windows;
- trocar a GPU;
- atualizar BIOS sem motivo;
- trocar placa-mãe;
- trocar SSD;
- abrir a fonte;
- fazer reflow;
- fazer reballing;
- substituir RAM aleatoriamente.

Isso representa economia de:

- tempo;
- dinheiro;
- risco;
- dados.

---

# Fase 16 — Validação após correção

Depois das intervenções:

- fonte de referência/novo sistema de alimentação adequado;
- cabo DisplayPort confiável;
- limpeza do fluxo de ar;
- redução de programas desnecessários na inicialização.

Novo baseline:

```text
RAM em repouso...........7,4 GB / 16 GB
CPU em repouso...........3–6%
SSD em repouso...........baixo uso

CPU carga combinada......75 °C
GPU......................72 °C
Hotspot..................87 °C
SSD......................57 °C
```

---

# Validação de vídeo

```text
1440p / 165 Hz
60 minutos de uso
Sem piscadas
Sem perda de sinal
Sem tela preta
```

---

# Validação de estabilidade

```text
Carga combinada
60 minutos
Sem reinicialização
```

Depois:

```text
Videoconferência
Navegador
Sincronização
Vídeo
30 minutos
Estável
```

---

# Validação da responsividade

Com a inicialização reorganizada:

- área de trabalho responde mais rapidamente;
- atividade do SSD reduz;
- paginação diminui;
- aplicativos abrem com menor atraso.

Ainda assim, dependendo do padrão de uso da empresa, expansão futura para mais memória pode ser recomendada.

---

# Agora transforme a investigação em documento

O técnico não deve entregar apenas:

> “Troquei a fonte e o cabo.”

O cliente precisa receber uma explicação objetiva.

Outro técnico precisa conseguir compreender o que foi feito.

Por isso construiremos o primeiro **Laudo Técnico Smarteletrovini Academy**.

---

# 📄 Estrutura do primeiro Laudo Técnico

## 1. Identificação

```text
Equipamento:
Desktop

Data da análise:
____/____/____

Responsável:
____________________________
```

---

# 2. Sintoma relatado

Registre somente o que foi informado.

Exemplo:

> Cliente relata lentidão intermitente, reinicializações, uma ocorrência de tela preta, aumento ocasional do ruído das ventoinhas e demora de inicialização.

Não escreva ainda a conclusão.

---

# 3. Estado inicial

Exemplo:

> Equipamento recebido sem sinais externos de dano elétrico ou líquido. Inspeção interna revelou acúmulo de poeira no filtro frontal. Sistema realizou POST e iniciou normalmente em bancada.

---

# 4. Configuração

```text
CPU:
Placa-mãe:
RAM:
GPU:
Armazenamento:
Fonte:
Monitor:
Sistema:
```

---

# 5. Evidências coletadas

Devem ser fatos.

Exemplo:

- RAM chegou a aproximadamente 14,7 GB de 16 GB em uso cotidiano;
- desempenho melhorou após reduzir programas residentes;
- SSD não apresentou erros críticos no teste realizado;
- tela preta foi reproduzida com o cabo original em 165 Hz;
- tela preta não foi reproduzida com cabo de referência;
- reinicialização foi reproduzida em carga combinada;
- falha deixou de ocorrer com fonte de referência;
- falha retornou com a fonte original.

---

# 6. Hipóteses consideradas

Exemplo:

- falha de GPU;
- falha de cabo;
- falha de monitor;
- instabilidade de fonte;
- problema térmico;
- erro de memória;
- falha de armazenamento;
- pressão de memória;
- driver gráfico.

Registrar hipóteses descartadas também é importante.

---

# 7. Testes realizados

Cada teste deve possuir objetivo.

Exemplo:

```text
Teste:
Cabo de referência.

Objetivo:
Verificar se a perda de vídeo acompanha o cabo original.

Resultado:
165 Hz permaneceu estável.
```

---

# 8. Conclusão técnica

A conclusão deve relacionar cada sintoma às evidências.

Exemplo:

> A investigação identificou três fenômenos distintos. A lentidão observada apresentou forte relação com pressão de memória e paginação decorrentes de múltiplos aplicativos simultâneos. A perda de vídeo foi reproduzida com o cabo DisplayPort original em alta taxa de atualização e não ocorreu com cabo de referência, indicando falha de integridade do enlace original. As reinicializações foram reproduzidas sob carga combinada com a fonte original, deixaram de ocorrer com fonte de referência compatível e retornaram após reinstalação da fonte original, constituindo forte evidência de instabilidade no sistema de alimentação original dentro das condições testadas.

Observe a linguagem.

Não escrevemos:

> “A fonte está 100% queimada internamente no componente X.”

Os testes não demonstraram isso.

---

# 9. Procedimentos recomendados

Exemplo:

- substituir a fonte original;
- substituir o cabo DisplayPort;
- realizar limpeza do fluxo de ar;
- revisar programas de inicialização;
- avaliar expansão de RAM conforme carga real;
- realizar backup regular dos dados.

---

# 10. Validação

Exemplo:

> Após substituição da alimentação utilizada no teste, troca do cabo e organização do sistema, foram realizados 60 minutos de carga combinada sem reinicialização e 60 minutos de vídeo em 1440p 165 Hz sem perda de sinal.

---

# 11. Limitações

Todo diagnóstico possui escopo.

Exemplo:

> A análise foi realizada nas condições descritas. Não foi executado diagnóstico eletrônico interno da fonte, nem desmontagem de componentes selados. A ausência de falhas durante o período de validação reduz a probabilidade de recorrência nas condições testadas, mas não constitui garantia de ausência absoluta de qualquer falha futura.

Essa seção demonstra maturidade técnica.

---

# Modelo completo de laudo

```text
LAUDO TÉCNICO — SMARTELETROVINI ACADEMY

1. EQUIPAMENTO
Tipo:
Configuração:
Data:

2. SINTOMA RELATADO
_________________________________________

3. ESTADO INICIAL
_________________________________________

4. EVIDÊNCIAS COLETADAS
- _______________________________________
- _______________________________________
- _______________________________________

5. HIPÓTESES CONSIDERADAS
- _______________________________________
- _______________________________________
- _______________________________________

6. TESTES REALIZADOS
Teste 1:
Objetivo:
Resultado:

Teste 2:
Objetivo:
Resultado:

Teste 3:
Objetivo:
Resultado:

7. CONCLUSÃO TÉCNICA
_________________________________________

8. PROCEDIMENTO RECOMENDADO
_________________________________________

9. VALIDAÇÃO
_________________________________________

10. LIMITAÇÕES DA ANÁLISE
_________________________________________

Responsável:
_________________________________________
```

---

# O que diferencia um laudo de uma opinião?

Compare.

## Opinião

> “Parece que é a fonte.”

## Registro técnico

> A falha foi reproduzida com a fonte original durante carga combinada, não ocorreu durante 60 minutos nas mesmas condições com fonte de referência compatível e voltou a ocorrer após reinstalação da unidade original.

A segunda frase pode ser examinada.

Ela contém:

- condição;
- comparação;
- resultado;
- repetibilidade.

---

# Evidência positiva e evidência negativa

Também é importante registrar quando algo **não aconteceu**.

Exemplos:

- nenhum erro de memória foi detectado;
- nenhum artefato gráfico foi reproduzido;
- nenhum erro crítico do SSD apareceu;
- nenhuma falha ocorreu com cabo de referência.

A ausência de um evento em um teste adequado ajuda a reduzir hipóteses.

---

# Mas ausência de erro não prova perfeição

Se um teste de RAM não encontra erros, isso não significa:

> “A memória é perfeita em todas as condições possíveis.”

Significa:

> “Nenhum erro foi detectado nas condições e duração desse teste.”

Essa distinção deve aparecer na linguagem profissional.

---

# O problema de diagnósticos absolutos

Evite frases como:

- “100% garantido”;
- “não existe nenhuma outra possibilidade”;
- “essa peça nunca mais dará problema”;
- “o computador está perfeito”.

Prefira:

- “não foi reproduzido”;
- “não foram observados erros”;
- “forte evidência”;
- “dentro das condições testadas”;
- “principal hipótese”;
- “falha isolada no escopo realizado”.

---

# 📁 Dossiê da Investigação — versão do aluno

Antes de abrir a solução técnica, registre sua própria análise.

## O que sabemos

```text
1.
2.
3.
4.
5.
```

## O que ainda não sabemos

```text
1.
2.
3.
4.
5.
```

## Hipóteses iniciais

```text
1.
2.
3.
4.
5.
```

## Ordem dos testes

```text
1.
2.
3.
4.
5.
```

## Evidências mais fortes

```text
1.
2.
3.
```

## Hipóteses descartadas ou enfraquecidas

```text
1.
2.
3.
```

## Causas identificadas

```text
Lentidão:
_________________________________________

Tela preta:
_________________________________________

Reinicialização:
_________________________________________
```

## Validação

```text
_________________________________________
```

---

??? note "Solução técnica do caso — abra somente depois de concluir sua investigação"

    A investigação aponta para **três causas principais independentes**.

    **Lentidão**

    A RAM estava próxima da capacidade durante o uso cotidiano, provocando maior paginação e atividade no SSD. A responsividade melhorou quando os programas residentes foram reduzidos. Isso fornece forte evidência de pressão de memória como causa relevante da lentidão.

    **Tela preta**

    A perda de sinal foi reproduzida com o cabo DisplayPort original, especialmente em 165 Hz. O problema não apareceu com cabo de referência nas mesmas condições. A captura de tela permaneceu correta e o sistema continuou executando. O enlace de vídeo original é a principal causa do sintoma observado.

    **Reinicialização**

    A falha foi reproduzida em carga combinada com a fonte original. Com fonte de referência compatível, o sistema permaneceu estável. Após reinstalar a fonte original, a falha voltou a ocorrer. Isso constitui evidência convergente forte de instabilidade do sistema de alimentação original nas condições testadas.

    **Fatores secundários**

    A poeira e o fluxo de ar restrito contribuíam para temperaturas e ruído maiores, mas não foram demonstrados como causa primária das reinicializações.

    O SSD apresentou temperatura elevada, porém não mostrou erros críticos ou falhas de leitura durante os testes executados.

    A GPU não apresentou artefatos, falhas reproduzíveis com cabo de referência ou comportamento que justificasse condená-la.

---

# Um caso pode ter pistas verdadeiras e irrelevantes

Durante o diagnóstico encontramos:

- SSD quente;
- filtro empoeirado;
- evento de driver;
- fonte antiga;
- RAM cheia.

Todas são informações verdadeiras.

Mas nem todas explicam todos os sintomas.

Esse é um dos maiores desafios da investigação real.

> **Evidência relevante é aquela que ajuda a explicar o comportamento observado e resiste a testes de comparação.**

---

# O viés de confirmação

Imagine que você tenha decidido cedo:

> “É a GPU.”

Depois disso, pode começar a interpretar tudo para confirmar sua ideia.

- tela preta → GPU;
- driver falhou → GPU;
- jogo reiniciou → GPU;
- ventoinha aumentou → GPU.

Esse é um exemplo de **viés de confirmação**.

O método investigativo tenta reduzir esse problema exigindo:

- hipóteses alternativas;
- testes controlados;
- evidências contrárias;
- repetição.

---

# Procure também evidências que contradizem sua hipótese

Se você suspeita da GPU, pergunte:

> O que mostraria que a GPU provavelmente não é a causa?

Exemplos:

- falha desaparece com outro cabo;
- GPU funciona em outro sistema;
- captura de tela permanece correta;
- problema depende da fonte;
- defeito ocorre com vídeo integrado.

Um bom investigador tenta falsificar a própria hipótese.

---

# Diagnóstico como processo científico

Existe uma semelhança forte entre diagnóstico técnico e método científico.

```text
Observação
    ↓
Hipótese
    ↓
Previsão
    ↓
Teste
    ↓
Resultado
    ↓
Revisão da hipótese
```

Exemplo:

```text
Hipótese:
o cabo falha em alta largura de banda.

Previsão:
reduzir a taxa de atualização deve diminuir a falha.

Teste:
165 Hz → 120 Hz.

Resultado:
falha desaparece.

Novo teste:
cabo de referência em 165 Hz.

Resultado:
estável.
```

A confiança na hipótese aumenta.

---

# Diagnóstico é redução de incerteza

No início do caso, quase tudo era possível.

```text
GPU?
Fonte?
RAM?
SSD?
Temperatura?
Driver?
Cabo?
Monitor?
Sistema?
Placa-mãe?
```

A cada evidência:

- algumas hipóteses ganham força;
- outras perdem força;
- novas hipóteses podem surgir.

O objetivo é chegar ao menor conjunto plausível de causas sustentadas pelos dados.

---

# A investigação em sete frases

Depois de todo o módulo, podemos representar nosso método assim:

1. **Descreva o sintoma sem assumir a causa.**
2. **Preserve dados e segurança antes de intervir.**
3. **Colete evidências no estado original.**
4. **Construa hipóteses alternativas.**
5. **Altere uma variável por vez.**
6. **Confirme a causa com comparação e repetição.**
7. **Valide e documente a correção.**

Essas sete frases serão reutilizadas em módulos futuros.

---

# O hardware foi apenas o primeiro laboratório

O método que aprendemos não termina em componentes físicos.

Nos próximos módulos poderemos investigar:

- sistemas operacionais;
- processos;
- arquivos;
- permissões;
- serviços;
- rede;
- DNS;
- protocolos;
- logs;
- segurança;
- aplicações;
- APIs;
- bancos de dados;
- automações;
- inteligência artificial.

A estrutura de raciocínio continua semelhante.

---

# Do componente para o sistema

No começo do módulo, a pergunta era:

> “O que faz cada peça?”

Agora a pergunta mudou:

> **“Como essas peças interagem e como suas falhas aparecem no comportamento do sistema?”**

Essa mudança é fundamental.

Conhecer hardware é importante.

Saber investigar sistemas é ainda mais valioso.

---

# Quando o computador deixa de ser uma caixa misteriosa

Depois deste módulo, um computador não deve mais ser visto apenas como:

- processador;
- memória;
- SSD;
- placa de vídeo;
- fonte.

Ele deve ser visto como uma cadeia de subsistemas.

```text
Energia
   ↓
Inicialização
   ↓
Processamento
   ↓
Memória
   ↓
Armazenamento
   ↓
Gráficos
   ↓
Saída
   ↓
Usuário
```

E cada camada produz evidências.

---

# O início da postura profissional

Você não precisa conhecer todos os defeitos possíveis.

Ninguém conhece.

O que diferencia uma investigação técnica é a capacidade de:

- admitir o que ainda não sabe;
- formular boas hipóteses;
- escolher testes apropriados;
- preservar evidências;
- evitar conclusões prematuras;
- reconhecer limites;
- explicar o resultado.

Essa postura será mais importante do que decorar listas de defeitos.

---

# 📁 Encerramento do Dossiê do Módulo 2

Ao terminar este módulo, seu dossiê deve conter registros sobre:

- método de investigação;
- CPU;
- RAM;
- armazenamento;
- placa-mãe;
- fonte;
- refrigeração;
- GPU;
- monitor e cabos;
- ruídos;
- protocolo de bancada;
- caso final;
- primeiro laudo técnico.

Esse material representa a passagem do conhecimento introdutório para a investigação aplicada.

---

# Próxima etapa da formação

Até agora investigamos principalmente o computador físico.

Mas muitos problemas não deixam marcas visíveis em componentes.

Um computador pode apresentar:

- lentidão;
- erro;
- travamento;
- comportamento estranho;
- acesso negado;
- programa que não inicia;
- serviço parado;
- arquivo corrompido;
- processo desconhecido;
- conexão inesperada;

mesmo quando todo o hardware está saudável.

Nos próximos módulos, entraremos na camada lógica.

Começaremos a observar:

```text
Sistema operacional
        ↓
Processos
        ↓
Memória lógica
        ↓
Arquivos
        ↓
Permissões
        ↓
Serviços
        ↓
Logs
        ↓
Rede
        ↓
Segurança
```

A bancada física continua importante.

Mas agora nossa investigação começa a entrar dentro do sistema.

# Próximo módulo — Investigação Computacional II: Sistema Operacional, Processos, Arquivos e Evidências
