# Módulo 2 — Investigação Computacional I
## Anatomia do Hardware

# Aula 11 — Da Bancada ao Diagnóstico: Como Investigar um Computador Desconhecido

> **Pergunta da investigação**
>
> Quando um computador chega até você apenas com a descrição “não está funcionando direito”, como transformar um relato vago em um diagnóstico técnico, reproduzível e defensável?

---

# 📁 Dossiê da Investigação

## Caso nº 010 — O computador que “tem vários problemas”

Uma pequena empresa entrega um computador para análise.

O relato inicial é curto:

> “Ele está lento, às vezes reinicia, ontem ficou sem vídeo e hoje demorou para ligar.”

Nenhum componente foi identificado como defeituoso.

Não sabemos:

- quando o problema começou;
- se houve queda de energia;
- se alguém abriu o computador;
- se alguma peça foi trocada;
- se o problema ocorre em repouso ou sob carga;
- se existem dados importantes sem backup;
- se o sistema foi atualizado;
- se há superaquecimento;
- se a fonte é adequada;
- se o armazenamento está saudável;
- se a memória apresenta erros;
- se o problema está no hardware ou no sistema operacional.

Esse é um cenário muito mais próximo da realidade do que receber uma máquina com a causa já conhecida.

Um técnico inexperiente pode começar imediatamente a:

- trocar memória;
- reinstalar o Windows;
- atualizar BIOS;
- limpar o gabinete;
- trocar pasta térmica;
- testar outra fonte;
- formatar o SSD.

Mas existe um problema.

Cada alteração modifica a cena original.

Depois de várias intervenções, talvez o defeito desapareça.

Mas não saberemos por quê.

Pior: podemos destruir evidências, introduzir novos problemas ou colocar dados importantes em risco.

A partir desta aula, todas as peças que estudamos separadamente passam a fazer parte de um único procedimento.

> **O objetivo de um diagnóstico profissional não é adivinhar rapidamente. É reduzir a incerteza de maneira controlada.**

---

# Objetivos da aula

Ao final desta aula, você deverá ser capaz de:

- transformar um relato genérico em sintomas observáveis;
- organizar uma investigação antes de abrir o equipamento;
- separar informação do cliente, observação técnica e conclusão;
- definir prioridades de segurança e preservação de dados;
- realizar inspeção inicial sem alterar desnecessariamente a máquina;
- estabelecer uma configuração de referência;
- escolher a ordem adequada dos testes;
- utilizar configuração mínima quando necessário;
- aplicar testes cruzados sem criar falsas conclusões;
- diferenciar hipótese, evidência e diagnóstico confirmado;
- reconhecer quando parar a investigação;
- documentar alterações realizadas durante o processo;
- validar se a correção realmente resolveu a causa original;
- produzir um registro técnico compreensível para outro profissional.

---

# Diagnóstico começa antes de ligar o computador

Um erro frequente é pensar que o diagnóstico começa quando pressionamos o botão de energia.

Na realidade, ele começa no primeiro contato com o equipamento.

Antes de qualquer teste, precisamos descobrir:

- quem utiliza a máquina;
- para qual finalidade;
- qual é o sintoma percebido;
- quando começou;
- o que mudou antes do problema;
- com que frequência ocorre;
- se existem dados importantes;
- se alguém já tentou corrigir;
- quais alterações foram realizadas.

A entrevista não é burocracia.

Ela reduz o espaço de busca.

---

# O relato do usuário não é o diagnóstico

Considere:

> “Meu SSD está ruim.”

Isso parece uma conclusão técnica.

Mas talvez o usuário queira dizer:

- o computador demora para iniciar;
- arquivos demoram para abrir;
- o sistema congela;
- ouviu alguém dizer que era o SSD.

O investigador deve converter a conclusão do cliente em um sintoma observável.

Em vez de registrar:

> SSD com defeito.

Registre:

> Usuário relata demora de aproximadamente três minutos entre o acionamento e a área de trabalho, além de congelamentos ao abrir arquivos.

Agora temos algo testável.

---

# Sintoma relatado e sintoma reproduzido

Esses dois conceitos devem permanecer separados.

## Sintoma relatado

É aquilo que o usuário afirma ter observado.

Exemplo:

> “O computador reinicia durante jogos.”

## Sintoma reproduzido

É aquilo que o técnico conseguiu observar em condições documentadas.

Exemplo:

> Durante 18 minutos de carga gráfica, o equipamento reiniciou sem tela azul quando GPU e CPU estavam sob carga simultânea.

A diferença é importante.

Um relato pode estar correto, incompleto ou impreciso.

O diagnóstico precisa se apoiar em evidências que possam ser verificadas.

---

# Primeiro princípio: preservar antes de modificar

Antes de limpar, atualizar, formatar ou desmontar, pergunte:

> **Existe alguma informação que podemos perder?**

Isso inclui:

- arquivos do cliente;
- registros do sistema;
- logs;
- configurações;
- histórico do defeito;
- estado físico da máquina;
- posição dos cabos;
- códigos de erro;
- mensagens na tela.

Se o problema envolve armazenamento, corrupção de dados ou possível falha física, a prioridade pode ser a preservação dos dados, e não a continuidade do teste.

A Aula 4 já mostrou um princípio que agora se torna parte do nosso protocolo:

> **quanto mais importante o dado, menor deve ser a tolerância a testes destrutivos ou desnecessários.**

---

# Segundo princípio: risco vem antes da curiosidade

Nem todo computador deve ser ligado imediatamente.

Interrompa a investigação normal se existirem sinais como:

- cheiro de queimado;
- fumaça;
- líquido;
- cabo derretido;
- conector escurecido;
- faísca;
- estalo elétrico forte;
- fonte visivelmente danificada;
- componente solto em região energizada;
- marcas de carbonização;
- choque ao tocar o gabinete;
- bateria de notebook deformada;
- dispositivo de armazenamento com ruído mecânico grave e dados importantes.

Nesses casos, “ver se ainda liga” pode aumentar o dano.

---

# A ordem geral de uma investigação

Podemos organizar o diagnóstico em etapas.

```text
1. Recepção e entrevista
        ↓
2. Preservação e segurança
        ↓
3. Inspeção externa
        ↓
4. Documentação do estado inicial
        ↓
5. Reprodução do sintoma
        ↓
6. Coleta de evidências
        ↓
7. Formulação de hipóteses
        ↓
8. Testes de baixo risco
        ↓
9. Isolamento de subsistemas
        ↓
10. Testes cruzados
        ↓
11. Correção
        ↓
12. Validação
        ↓
13. Registro final
```

Essa sequência não é rígida.

Um computador que não liga exige um caminho diferente de um computador que funciona, mas apresenta lentidão.

O método permanece o mesmo:

> **observar antes de concluir.**

---

# Etapa 1 — Recepção e entrevista

Uma boa entrevista procura transformar palavras vagas em condições específicas.

Perguntas úteis incluem:

- Quando o problema começou?
- O computador funcionava normalmente antes?
- Houve queda de energia?
- Houve transporte?
- Alguma peça foi instalada?
- Algum cabo foi trocado?
- O sistema foi atualizado?
- O problema ocorre todos os dias?
- Ocorre em algum programa específico?
- O computador reinicia ou apenas perde vídeo?
- Acontece logo ao ligar ou depois de algum tempo?
- Existe algum ruído novo?
- O equipamento ficou molhado?
- Alguém abriu o gabinete?
- Alguma tentativa de reparo já foi realizada?
- Existem arquivos importantes sem backup?

A entrevista também deve registrar o contexto de uso.

Um computador usado para:

- escritório;
- jogos;
- edição;
- servidor;
- automação comercial;
- desenvolvimento;

enfrenta cargas e prioridades diferentes.

---

# Linha do tempo do defeito

Uma técnica extremamente útil é reconstruir a sequência temporal.

Exemplo:

```text
Segunda-feira:
GPU nova instalada.

Terça-feira:
primeiro jogo executado.

Quarta-feira:
primeira reinicialização.

Sexta-feira:
novo driver instalado.

Sábado:
reinicializações ficaram mais frequentes.
```

Isso não prova causalidade.

Mas destaca alterações relevantes.

A pergunta passa a ser:

> O defeito começou depois de qual mudança?

---

# Etapa 2 — Preservação

Antes de modificar o sistema, podemos registrar:

- fotografias;
- vídeos;
- posição dos cabos;
- mensagens de erro;
- tela do firmware;
- versão do sistema;
- logs;
- configuração;
- etiquetas;
- números de modelo.

Se a máquina ainda funciona, também podemos registrar:

- temperaturas;
- clocks;
- consumo;
- saúde do armazenamento;
- utilização de memória;
- erros do sistema;
- eventos próximos ao horário da falha.

Esse registro cria uma referência.

---

# Etapa 3 — Inspeção externa

Antes de abrir o gabinete, observe:

- estado do cabo de energia;
- monitor e cabo de vídeo;
- posição do seletor da fonte, se existir;
- periféricos conectados;
- portas danificadas;
- USB quebrado;
- cheiro;
- ruído;
- acúmulo extremo de poeira;
- sinais de líquido;
- parafusos ausentes;
- deformações;
- impactos;
- etiquetas de garantia ou manutenção.

Também registre o ambiente.

Alguns problemas dependem de:

- tomada;
- estabilizador inadequado;
- extensão;
- temperatura;
- poeira;
- umidade;
- posição do gabinete.

---

# O ambiente também pode causar sintomas

Imagine que o computador funcione perfeitamente na bancada, mas apresente falhas no escritório.

Isso pode ocorrer devido a:

- alimentação elétrica;
- periférico específico;
- cabo;
- rede;
- temperatura do ambiente;
- tomada;
- monitor;
- dispositivo USB;
- posição física;
- vibração.

Por isso, “não reproduziu na bancada” não significa automaticamente que o usuário esteja enganado.

Pode significar que removemos justamente a variável responsável.

---

# Etapa 4 — Inventário do equipamento

Antes dos testes, registre a configuração.

Exemplo:

```text
CPU.............Ryzen 5 5600
Placa-mãe.......B550
RAM.............2 × 8 GB DDR4
GPU.............Radeon RX 6600
SSD.............NVMe 1 TB
Fonte...........550 W
Sistema.........Windows 11
Monitor.........1080p 144 Hz
```

Quando possível, registre também:

- fabricante;
- modelo;
- revisão;
- BIOS/UEFI;
- versão de driver;
- capacidade;
- idade aproximada.

Esse inventário é essencial para verificar compatibilidade.

---

# Não confie apenas no nome comercial

“Fonte de 600 W” é informação insuficiente.

“SSD de 1 TB” também.

“16 GB de RAM” também.

Para diagnóstico, precisamos de mais contexto.

Uma fonte pode ser:

- antiga;
- de projeto inadequado;
- sem conectores apropriados;
- incapaz de entregar a potência de forma estável.

Dois módulos de 8 GB podem possuir:

- frequências diferentes;
- timings diferentes;
- fabricantes diferentes;
- chips diferentes.

Um inventário técnico precisa ir além do número principal da embalagem.

---

# Etapa 5 — Estado inicial

Quando for seguro ligar o equipamento, não comece imediatamente com um teste pesado.

Primeiro observe.

Durante a inicialização:

- ventoinhas iniciam?
- existem LEDs de diagnóstico?
- há beeps?
- aparece imagem?
- o POST demora?
- o firmware exibe algum aviso?
- armazenamento é reconhecido?
- data e hora estão corretas?
- o sistema inicia?
- há reinicializações?

Depois do sistema operacional:

- demora para ficar responsivo?
- aparecem mensagens?
- existe atividade anormal?
- temperaturas sobem rapidamente?
- ventoinhas aceleram?
- disco permanece em 100%?
- RAM está quase cheia?
- CPU permanece ocupada sem razão aparente?

---

# O valor da observação passiva

Muitas informações podem ser coletadas sem alterar nada.

Exemplos:

- HWiNFO;
- Gerenciador de Tarefas;
- Monitor de Confiabilidade;
- Visualizador de Eventos;
- CrystalDiskInfo;
- GPU-Z;
- CPU-Z;
- firmware;
- informações do sistema.

Mas mesmo a coleta precisa ser proporcional ao problema.

Se um HDD está falhando mecanicamente, instalar várias ferramentas no próprio disco pode ser inadequado.

---

# Etapa 6 — Reproduzir o sintoma

Um defeito reproduzível é muito mais fácil de investigar.

Se o cliente diz:

> “Reinicia em jogos.”

Precisamos saber:

- qual jogo;
- depois de quanto tempo;
- em qual resolução;
- em qual qualidade;
- com qual temperatura;
- se ocorre em todos os jogos;
- se ocorre em carga de CPU;
- se ocorre em carga de GPU;
- se ocorre em carga combinada.

Se o cliente diz:

> “Fica lento.”

Precisamos definir o que significa lento:

- inicialização?
- abrir programas?
- copiar arquivos?
- navegar?
- renderizar?
- iniciar jogo?
- trocar de janela?

---

# Não transforme todo diagnóstico em benchmark

Benchmarks são ferramentas.

Não são o diagnóstico.

Se a falha ocorre ao copiar arquivos, talvez um teste gráfico seja irrelevante.

Se ocorre ao acordar da suspensão, um stress test de CPU pode não reproduzir nada.

O teste deve representar a hipótese.

> **Escolha o teste que responde a uma pergunta.**

---

# Um teste precisa ter uma pergunta

Exemplo ruim:

> “Vou rodar vários programas para ver se dá erro.”

Exemplo melhor:

> “Quero descobrir se a reinicialização está relacionada à carga simultânea da CPU e GPU.”

Agora podemos definir um teste apropriado.

Outro exemplo:

> “Quero saber se o problema acompanha este módulo de memória.”

Então podemos alterar a posição ou testar outro módulo de referência, controlando as demais variáveis.

---

# Etapa 7 — Criar hipóteses

Depois da coleta inicial, criamos hipóteses.

Imagine:

- reinicialização sem tela azul;
- somente sob carga;
- temperaturas normais;
- problema começou após instalar GPU nova;
- fonte antiga;
- adaptador de energia presente.

Hipóteses:

1. fonte inadequada ou instável;
2. adaptador ou conector;
3. GPU defeituosa;
4. placa-mãe;
5. driver;
6. memória;
7. instalação elétrica.

Não devemos escolher uma única hipótese cedo demais.

---

# Hipótese não é diagnóstico

Esta distinção precisa acompanhar todo o curso.

## Hipótese

> A fonte pode estar causando a reinicialização.

## Evidência

> A falha ocorre somente sob carga combinada e começou após a instalação de uma GPU de maior consumo.

## Teste

> Reproduzir a mesma carga com fonte de referência compatível e cabos corretos.

## Resultado

> A falha desaparece com a fonte de referência e retorna com a fonte original.

## Conclusão

Agora existe evidência muito mais forte relacionando o defeito à alimentação original.

---

# A árvore de hipóteses

Uma maneira profissional de raciocinar é organizar hipóteses por subsistema.

```text
Sintoma: reinicialização sob carga
        │
        ├── Energia
        │     ├── fonte
        │     ├── cabo
        │     └── tomada
        │
        ├── Temperatura
        │     ├── CPU
        │     ├── GPU
        │     └── VRM
        │
        ├── Memória
        │     ├── RAM
        │     └── controlador
        │
        ├── Software
        │     ├── driver
        │     └── sistema
        │
        └── Placa
              ├── GPU
              └── placa-mãe
```

Cada teste deve eliminar ou fortalecer partes dessa árvore.

---

# Priorize testes de alto valor e baixo risco

Nem todos os testes têm o mesmo custo.

Um bom primeiro teste tende a ser:

- rápido;
- reversível;
- seguro;
- informativo;
- pouco invasivo.

Exemplo:

Se um computador apresenta perda de vídeo, testar outro cabo é muito mais simples do que desmontar a GPU.

Se o problema começou depois de habilitar um perfil de memória, restaurar parâmetros padrão pode ser mais informativo do que trocar imediatamente os módulos.

---

# O princípio da menor intervenção

Sempre que possível:

> **mude o mínimo necessário para responder à próxima pergunta.**

Isso melhora a rastreabilidade.

Se você:

- limpa;
- desmonta;
- troca pasta;
- muda BIOS;
- reinstala driver;
- troca RAM;

tudo ao mesmo tempo, você perde a capacidade de saber qual ação teve efeito.

---

# Etapa 8 — Inspeção interna

Quando a abertura do gabinete é justificada e segura, registre o estado antes de alterar.

Observe:

- cabos soltos;
- conectores parcialmente inseridos;
- memória mal encaixada;
- GPU inclinada;
- poeira;
- ventoinhas bloqueadas;
- sinais de líquido;
- corrosão;
- parafusos soltos;
- marcas de calor;
- conectores escurecidos;
- cabos pressionados;
- peças não compatíveis;
- adaptadores;
- montagem do cooler;
- objetos metálicos.

Não comece limpando antes de observar.

A sujeira também pode ser evidência.

---

# Fotografe antes de desmontar

Fotografias podem registrar:

- posição dos cabos;
- conectores;
- montagem;
- orientação;
- sinais de líquido;
- marcas;
- etiqueta da fonte;
- posição das memórias;
- conexões do painel frontal.

Isso ajuda tanto na investigação quanto na remontagem.

---

# Configuração mínima

Quando o computador não realiza POST ou apresenta falha de inicialização, pode ser útil reduzir o sistema ao mínimo necessário.

Uma configuração típica pode incluir:

- placa-mãe;
- CPU;
- cooler;
- um módulo de RAM;
- fonte;
- vídeo integrado ou GPU necessária.

Dispositivos não essenciais podem ser removidos temporariamente:

- discos adicionais;
- placas de expansão;
- USBs;
- RGB;
- acessórios;
- periféricos secundários.

O objetivo é reduzir variáveis.

---

# Configuração mínima não significa desmontar sem critério

Cada remoção precisa ter uma razão.

Antes:

> Sistema não completa POST.

Depois:

> Sistema completa POST após remover dispositivo X.

Agora o dispositivo X, sua alimentação ou sua interação com o sistema ganha relevância.

Mas ainda precisamos confirmar.

---

# Um módulo de RAM por vez

Se o sistema apresenta falhas relacionadas à memória, podemos comparar:

- módulo A;
- módulo B;
- slot 1;
- slot 2;
- parâmetros padrão.

Isso ajuda a separar:

- módulo;
- slot;
- controlador;
- configuração.

Exemplo:

```text
Módulo A no slot 2 → funciona
Módulo B no slot 2 → falha
Módulo B no slot 4 → falha
```

A suspeita sobre o módulo B aumenta.

Outro padrão:

```text
Módulo A no slot 2 → falha
Módulo B no slot 2 → falha
Módulo A no slot 4 → funciona
Módulo B no slot 4 → funciona
```

Agora o slot ou sua cadeia de comunicação ganha relevância.

---

# Testes cruzados

Um teste cruzado utiliza uma peça conhecida para comparar comportamentos.

Exemplos:

- outra fonte;
- outro módulo de RAM;
- outra GPU;
- outro cabo;
- outro monitor;
- outro SSD;
- outro computador.

O valor do teste vem da comparação controlada.

---

# Peça de referência precisa ser realmente confiável

Uma peça “que estava guardada” não é automaticamente uma boa referência.

Uma fonte antiga desconhecida pode introduzir outro defeito.

Um módulo de memória sem histórico pode ser instável.

Uma GPU muito menos potente pode não reproduzir a mesma carga elétrica.

Por isso, uma referência ideal deve ser:

- compatível;
- conhecida;
- estável;
- adequada ao teste.

---

# Cuidado com conclusões falsas em testes cruzados

Exemplo:

GPU A consome 250 W e causa reinicialização.

GPU B consome 75 W e funciona.

Conclusão errada:

> GPU A está defeituosa.

Outra hipótese continua forte:

> A fonte pode não suportar a carga da GPU A.

O teste eliminou algumas possibilidades, mas não todas.

---

# Trocar peças não é o mesmo que diagnosticar

Substituir componentes até o problema desaparecer é uma técnica de isolamento rudimentar.

Ela pode funcionar em alguns casos.

Mas apresenta limitações:

- custo;
- risco;
- tempo;
- possibilidade de danificar peças boas;
- conclusões equivocadas;
- ausência de documentação.

O objetivo do curso é transformar troca de peças em **teste controlado**, não em tentativa aleatória.

---

# Etapa 9 — Diagnóstico de energia

Quando suspeitamos de alimentação, revisamos o que aprendemos na Aula 6.

Observe:

- modelo da fonte;
- idade;
- conectores;
- capacidade;
- cabos originais;
- adaptadores;
- sinais de aquecimento;
- comportamento sob carga;
- histórico de upgrades.

Lembre-se:

> uma leitura de 12 V em software não prova que a fonte esteja saudável.

Testes profissionais podem exigir instrumentos e cargas apropriadas.

---

# Etapa 10 — Diagnóstico térmico

Quando o defeito depende do tempo ou da carga, temperatura torna-se variável importante.

Observe:

- CPU;
- GPU;
- hotspot;
- SSD;
- VRM, quando disponível;
- rotação das ventoinhas;
- bomba;
- clock;
- potência.

Pergunte:

- o sintoma aparece sempre na mesma faixa térmica?
- o clock reduz?
- o gabinete satura depois de alguns minutos?
- abrir temporariamente o painel altera o comportamento?

A correlação temporal é essencial.

---

# Etapa 11 — Diagnóstico de armazenamento

Sintomas que podem envolver armazenamento:

- inicialização lenta;
- travamentos durante acesso;
- arquivos corrompidos;
- erros de leitura;
- desaparecimento do disco;
- I/O elevado;
- ruídos em HDD.

Mas cuidado:

Um computador lento não implica automaticamente SSD ruim.

Pode existir:

- RAM insuficiente;
- CPU ocupada;
- antivírus;
- atualização;
- aplicação;
- sistema corrompido;
- paginação.

A saúde do armazenamento é uma parte da investigação.

---

# Etapa 12 — Diagnóstico de memória

Possíveis sintomas:

- tela azul;
- travamentos aleatórios;
- erros de aplicação;
- corrupção;
- falha de POST;
- reinicialização.

Mas erros de memória podem ter origem em:

- módulo;
- slot;
- controlador;
- CPU;
- tensão;
- perfil XMP/EXPO;
- firmware;
- placa-mãe.

Por isso, “teste de memória falhou” ainda precisa de interpretação.

---

# Etapa 13 — Diagnóstico gráfico

Retomamos a Aula 8.

Pergunte:

- artefato aparece antes do sistema?
- aparece na captura?
- ocorre apenas em uma aplicação?
- acompanha a GPU para outro computador?
- depende da VRAM?
- depende da temperatura?
- ocorre somente com alta taxa de atualização?

O caminho da imagem deve ser dividido entre:

- renderização;
- transmissão;
- exibição.

---

# Etapa 14 — Diagnóstico de monitor e cabo

Retomamos a Aula 9.

Um problema visual pode estar em:

- GPU;
- porta;
- cabo;
- adaptador;
- dock;
- monitor;
- painel.

Testes como:

- outro cabo;
- outra porta;
- outro monitor;
- OSD;
- captura de tela;

podem reduzir drasticamente as hipóteses.

---

# Etapa 15 — Ruídos como evidência

Retomamos a Aula 10.

Pergunte:

- o som acompanha RPM?
- acompanha FPS?
- acompanha acesso ao HDD?
- começou após transporte?
- é mecânico?
- é elétrico?
- existe cheiro ou aquecimento?
- muda com a posição?

O ruído deve ser correlacionado com outras variáveis.

---

# Software ou hardware?

Essa divisão parece simples, mas muitas falhas atravessam as duas camadas.

Exemplo:

Um driver pode fazer a GPU entrar em um estado de carga que revela instabilidade elétrica.

Um firmware pode configurar a memória de maneira incompatível.

Um sistema corrompido pode produzir sintomas semelhantes a falha de armazenamento.

A pergunta mais útil não é:

> “É hardware ou software?”

Mas:

> **Qual camada contém a evidência mais forte neste momento?**

---

# Boot por ambiente alternativo

Em alguns casos, iniciar o computador por outro ambiente pode ajudar a separar hipóteses.

Por exemplo:

- sistema live;
- instalação de teste;
- outro SSD conhecido.

Se o defeito persiste fora do sistema original, algumas hipóteses de software perdem força.

Mas isso precisa ser feito com cuidado, especialmente quando há dados importantes.

---

# Não formate para diagnosticar cedo demais

Formatação é uma alteração enorme.

Ela apaga ou substitui:

- sistema;
- drivers;
- logs;
- configurações;
- evidências.

Se o defeito desaparece após formatar, ainda podemos não saber qual era a causa.

Por isso, “formatar para ver se resolve” deve ser uma etapa tardia e justificada.

---

# Logs: testemunhas digitais

Sistemas operacionais registram eventos úteis.

No Windows, podemos consultar:

- Monitor de Confiabilidade;
- Visualizador de Eventos;
- histórico de atualizações;
- Gerenciador de Dispositivos.

No Linux, podemos utilizar recursos como:

- `journalctl`;
- `dmesg`;
- logs de serviços;
- logs do kernel.

Um log não deve ser tratado como sentença.

Ele mostra o que o sistema percebeu.

---

# O horário importa

Se o computador reiniciou às 15:42, procure eventos próximos desse horário.

Podemos correlacionar:

- falha de driver;
- erro de armazenamento;
- perda de energia;
- serviço encerrado;
- problema de barramento.

A correlação temporal ajuda a reconstruir a sequência.

---

# Erro consequente e erro causador

Um dos conceitos mais importantes do diagnóstico é diferenciar causa e consequência.

Imagine:

1. a fonte perde estabilidade;
2. a GPU para de responder;
3. o driver registra erro;
4. o sistema reinicia.

O log do driver pode ser verdadeiro.

Mas ele pode registrar uma consequência, não a causa primária.

Da mesma forma:

1. SSD trava;
2. sistema deixa de responder;
3. aplicação gera erro;
4. usuário culpa o programa.

O erro visível nem sempre nasceu onde apareceu.

---

# Cadeia causal

Uma forma de pensar é:

```text
Evento inicial
     ↓
Componente afetado
     ↓
Sintoma intermediário
     ↓
Erro registrado
     ↓
Sintoma percebido pelo usuário
```

Nosso trabalho é tentar voltar pela cadeia.

---

# Correlação não é causalidade

Se um erro aparece ao mesmo tempo que o defeito, isso aumenta sua relevância.

Mas ainda precisamos testar.

Exemplo:

> toda vez que o computador trava, o SSD está em 100%.

Isso pode significar:

- SSD é a causa;
- SSD está apenas respondendo a paginação causada por falta de RAM;
- antivírus está lendo muitos arquivos;
- aplicação está fazendo I/O intenso.

Precisamos observar o sistema inteiro.

---

# Testes sob controle

Antes de cada teste, registre:

- objetivo;
- variável alterada;
- condição inicial;
- duração;
- resultado esperado;
- critério de interrupção.

Exemplo:

```text
Objetivo:
verificar se o problema depende da taxa de atualização.

Variável:
165 Hz → 120 Hz.

Mantido:
mesmo cabo, porta, resolução, driver e monitor.

Resultado:
falha não ocorreu em 30 minutos.
```

Agora temos informação útil.

---

# O conceito de baseline

Baseline é uma referência de funcionamento.

Pode ser:

- configuração padrão;
- sistema estável;
- comportamento em repouso;
- temperatura ambiente;
- resultado antes de uma alteração.

Sem baseline, comparar “melhorou” ou “piorou” fica subjetivo.

Exemplo:

Antes:

```text
Boot: 75 s
```

Depois:

```text
Boot: 28 s
```

Isso é mais útil que:

> “Agora parece rápido.”

---

# Repetibilidade

Um resultado único pode ser coincidência.

Sempre que seguro, tente verificar se o comportamento se repete.

Exemplo:

```text
Teste 1 → reiniciou em 12 min
Teste 2 → reiniciou em 11 min
Teste 3 → reiniciou em 13 min
```

Isso sugere um padrão forte.

Depois de uma alteração:

```text
Teste 1 → 30 min estável
Teste 2 → 30 min estável
Teste 3 → 30 min estável
```

A evidência da correção fica muito mais forte.

---

# Defeitos intermitentes

São alguns dos casos mais difíceis.

O computador pode funcionar:

- horas;
- dias;
- apenas frio;
- apenas quente;
- apenas depois de suspensão;
- apenas em determinada carga.

Nesses casos, documentar condições é fundamental.

Registre:

- temperatura ambiente;
- tempo ligado;
- aplicação;
- carga;
- posição;
- periféricos;
- horário;
- ruídos;
- logs.

---

# Não tente “forçar” o defeito de maneira perigosa

É aceitável reproduzir uma carga de forma controlada.

Não é aceitável:

- bloquear ventoinhas;
- aquecer componentes artificialmente com ferramentas improvisadas;
- causar curto;
- abrir fonte;
- exceder limites de tensão;
- retirar proteções.

O laboratório profissional utiliza procedimentos e instrumentos apropriados.

O curso ensina raciocínio, não improvisação perigosa.

---

# Quando atualizar BIOS/UEFI?

Atualização de firmware pode ser relevante quando existem evidências de:

- incompatibilidade de CPU;
- correções conhecidas;
- problemas de memória;
- vulnerabilidade;
- bug documentado.

Mas atualização de BIOS não deve ser usada como tentativa genérica.

Antes de atualizar:

- confirme modelo;
- revisão;
- versão atual;
- motivo;
- arquivo correto;
- procedimento oficial;
- estabilidade elétrica.

Se o computador é instável, uma atualização mal interrompida pode criar outro problema.

---

# Quando reinstalar driver?

A reinstalação pode ser justificada quando:

- problema começou após atualização;
- instalação está corrompida;
- dispositivo apresenta erro;
- existe regressão conhecida;
- teste com outra versão faz sentido.

Mas antes registre a versão atual.

Caso contrário, perdemos a referência.

---

# Quando limpar o computador?

Limpeza pode ser necessária.

Mas em uma investigação, observe primeiro.

Fotografe:

- poeira;
- obstrução;
- filtros;
- ventoinhas;
- vazamento;
- corrosão.

Depois da limpeza, se o defeito desaparecer, essas evidências ajudam a explicar a causa.

---

# Quando trocar pasta térmica?

Não por calendário automático.

Ela deve ser considerada quando existem evidências como:

- contato inadequado;
- manutenção anterior;
- comportamento térmico anormal;
- cooler removido;
- material degradado.

Se a temperatura está normal, trocar pasta apenas por tentativa adiciona uma variável desnecessária.

---

# Diagnóstico por exclusão

Às vezes não conseguimos observar diretamente a causa.

Mas podemos eliminar alternativas.

Exemplo:

- monitor trocado → falha continua;
- cabo trocado → continua;
- driver limpo → continua;
- outra fonte → continua;
- GPU em outro PC → falha acompanha.

A hipótese sobre a própria GPU fica mais forte.

Isso é diagnóstico por exclusão.

Mas a exclusão só é válida se os testes forem adequados.

---

# O conceito de evidência convergente

Uma conclusão forte raramente depende de um único sinal.

Imagine:

- SSD relata erros S.M.A.R.T.;
- sistema registra erros de I/O;
- arquivos apresentam falha;
- o problema acompanha o SSD para outro computador;
- outro SSD funciona no sistema original.

Essas evidências convergem.

Isso é muito mais convincente que:

> “O CrystalDiskInfo ficou amarelo.”

---

# Três níveis de conclusão

Vamos adotar uma classificação simples.

## Nível 1 — Suspeita

Existem indícios, mas poucos testes.

> Possível falha na alimentação.

## Nível 2 — Hipótese forte

Várias evidências convergem.

> A falha ocorre sob carga e desaparece com fonte de referência.

## Nível 3 — Diagnóstico confirmado dentro do escopo do teste

A causa foi isolada de maneira reproduzível.

> A fonte original reproduz a falha em condições controladas; a fonte de referência não reproduz, mantendo os demais elementos constantes.

Mesmo assim, um relatório profissional deve declarar limites.

---

# Limites do diagnóstico

Nem sempre conseguimos afirmar:

> “Este componente interno exato falhou.”

Podemos chegar a:

> “A placa de vídeo apresenta falha interna reproduzível.”

Isso pode ser suficiente para decidir:

- reparar;
- substituir;
- encaminhar a laboratório.

Não invente precisão que os testes não fornecem.

---

# Quando encaminhar

Encaminhar não é fracasso.

É reconhecer o limite do equipamento e da competência disponível.

Considere encaminhamento quando houver:

- reparo BGA;
- análise de VRM;
- curto interno;
- recuperação de dados;
- firmware especializado;
- fonte aberta;
- placa com líquido;
- microsoldagem;
- diagnóstico eletrônico avançado.

O bom profissional sabe onde termina sua bancada.

---

# O estado conhecido bom

Uma das ferramentas mais poderosas do laboratório é possuir referências conhecidas.

Exemplos:

- fonte testada;
- módulo de RAM confiável;
- cabo de vídeo certificado;
- monitor de referência;
- SSD de teste;
- teclado simples;
- pendrive bootável;
- pasta de drivers oficiais.

Esses itens reduzem o número de variáveis.

---

# Etiquetagem de peças

Em um ambiente profissional, peças de referência devem ser identificadas.

Exemplo:

```text
FONTE-REF-01
Testada em: 2026-09
Estado: OK
Uso: diagnóstico
```

Isso evita utilizar acidentalmente uma peça defeituosa como referência.

---

# Organizando a bancada

Uma bancada de diagnóstico precisa facilitar controle.

Itens úteis incluem:

- iluminação adequada;
- bandejas para parafusos;
- etiquetas;
- pulseira/medidas ESD adequadas;
- cabos conhecidos;
- documentação;
- ferramentas manuais corretas;
- espaço limpo;
- área para peças removidas.

A organização também reduz defeitos criados pelo próprio técnico.

---

# ESD — descarga eletrostática

Componentes eletrônicos podem ser sensíveis a descarga eletrostática.

Boas práticas incluem:

- ambiente adequado;
- aterramento apropriado;
- evitar superfícies altamente eletrostáticas;
- manipular placas pelas bordas;
- utilizar proteção ESD quando aplicável.

Não devemos apoiar componentes diretamente sobre:

- carpetes;
- tecidos sintéticos;
- superfícies inadequadas.

---

# Parafusos também são evidência

Parafuso errado pode:

- encostar em trilha;
- perfurar região inadequada;
- causar curto;
- deformar placa;
- impedir contato correto.

Durante desmontagem:

- separe;
- identifique;
- registre.

Especialmente em notebooks, tamanhos semelhantes podem possuir comprimentos diferentes.

---

# Cabos e conectores

Não force conectores.

Antes de remover, identifique:

- trava;
- orientação;
- tipo;
- função.

Conectores de:

- ventoinhas;
- RGB;
- USB interno;
- painel frontal;
- antenas;
- flat cables;

podem ser frágeis.

Criar um defeito durante o diagnóstico é uma das piores situações possíveis.

---

# Ferramentas de software por objetivo

Em vez de decorar programas, organize-os pela pergunta.

## Identificação

- CPU-Z;
- GPU-Z;
- informações do sistema.

## Sensores

- HWiNFO;
- ferramentas do fabricante.

## Armazenamento

- CrystalDiskInfo;
- GSmartControl;
- ferramentas oficiais.

## Logs

- Monitor de Confiabilidade;
- Visualizador de Eventos;
- journalctl;
- dmesg.

## Memória

- diagnóstico apropriado de RAM;
- ferramentas bootáveis quando necessário.

## Desempenho

- Gerenciador de Tarefas;
- monitores de recursos;
- benchmarks específicos.

A ferramenta vem depois da pergunta.

---

# Cuidado com programas “milagrosos”

Evite depender de ferramentas que prometem:

- corrigir todos os drivers;
- reparar qualquer erro;
- aumentar desempenho automaticamente;
- limpar registro;
- recuperar tudo com um clique.

Durante diagnóstico, essas ferramentas podem:

- alterar o sistema;
- instalar software;
- remover evidências;
- criar novos problemas.

Prefira ferramentas conhecidas e procedimentos transparentes.

---

# Documentação durante o diagnóstico

Não espere terminar para escrever.

Registre conforme avança.

Uma tabela simples ajuda:

| Horário | Ação | Evidência | Resultado |
|---|---|---|---|
| 14:10 | Ligado equipamento | POST normal | Sistema iniciou |
| 14:18 | Carga gráfica | GPU 99% | Reiniciou |
| 14:30 | Fonte de referência | Mesma carga | Estável |
| 15:05 | Fonte original | Mesma carga | Reiniciou |

Essa sequência permite que outra pessoa compreenda o raciocínio.

---

# O que mudou?

Após cada intervenção, registre explicitamente.

Exemplo:

> Única alteração: cabo DisplayPort substituído.

Ou:

> Perfil EXPO desativado; demais parâmetros mantidos.

Isso protege o diagnóstico contra confusão.

---

# Validação da correção

Um erro comum é parar assim que o computador “volta a funcionar”.

Correção não é apenas desaparecer o sintoma uma vez.

Precisamos perguntar:

- o defeito foi reproduzido antes?
- a mesma condição foi repetida depois?
- houve tempo suficiente de teste?
- todos os sintomas desapareceram?
- surgiu algum efeito colateral?
- temperaturas permanecem adequadas?
- desempenho está normal?
- logs permanecem limpos?

---

# Corrigir não significa apenas substituir

Uma correção pode ser:

- reconectar;
- atualizar;
- restaurar configuração;
- melhorar fluxo de ar;
- substituir cabo;
- substituir peça;
- reparar;
- remover software;
- corrigir firmware;
- orientar o usuário.

O importante é tratar a causa identificada.

---

# Validação negativa

Também precisamos comprovar que a correção não criou outro problema.

Exemplo:

Depois de reduzir uma frequência de memória, os travamentos desapareceram.

Mas:

- desempenho caiu?
- a memória está configurada corretamente?
- a redução apenas mascarou um módulo defeituoso?

A validação precisa considerar o sistema como um todo.

---

# Caso integrado 1 — O computador que reinicia durante jogos

Relato:

> “Reinicia quando jogo.”

Inventário:

- CPU intermediária;
- GPU recente;
- fonte antiga;
- 16 GB RAM;
- SSD saudável.

Observação:

- repouso normal;
- CPU em carga isolada normal;
- GPU em carga isolada normal;
- carga combinada provoca reinicialização;
- temperaturas adequadas;
- sem tela azul.

Histórico:

- problema começou após upgrade da GPU.

Hipóteses prioritárias:

- fonte;
- conectores;
- cabo de alimentação;
- GPU;
- placa-mãe.

Teste cruzado:

- fonte de referência adequada;
- mesmos componentes;
- mesmos cabos apropriados;
- mesma carga.

Resultado:

- sistema estável.

Retorno à fonte original:

- falha reproduzida.

Conclusão técnica:

> Existe forte evidência de falha ou inadequação do sistema de alimentação original sob carga combinada.

Observe que não foi necessário abrir a fonte.

---

# Caso integrado 2 — O computador “muito lento”

Relato:

> “O SSD está estragado.”

Estado inicial:

- CPU 18%;
- RAM 97%;
- SSD com atividade frequente;
- vários aplicativos abertos;
- paginação intensa;
- saúde do SSD sem alertas relevantes.

Teste:

- fechar aplicações não essenciais;
- consumo de RAM cai;
- paginação reduz;
- responsividade melhora.

Conclusão:

> A lentidão está fortemente associada à pressão de memória e paginação, não existindo evidência suficiente para condenar o SSD.

O relato do cliente continha uma conclusão.

O diagnóstico revelou outra causa.

---

# Caso integrado 3 — Sem vídeo depois da limpeza

Relato:

> “Depois que limpei, parou de dar imagem.”

Inspeção:

- ventoinhas giram;
- LED DRAM permanece aceso;
- memória foi removida durante a limpeza.

Hipóteses:

- módulo mal encaixado;
- slot;
- contato;
- dano;
- configuração.

Teste:

- equipamento desligado;
- inspeção;
- reinstalação correta de um módulo;
- configuração mínima.

Resultado:

- POST normal.

Conclusão:

> O problema foi introduzido durante a manutenção e estava relacionado ao encaixe da memória.

A linha do tempo foi decisiva.

---

# Caso integrado 4 — Tela preta após 20 minutos

Relato:

> “A placa de vídeo morreu.”

Observações:

- sistema inicia;
- jogos funcionam inicialmente;
- hotspot sobe progressivamente;
- ventoinhas atingem alta rotação;
- tela preta após aproximadamente 20 minutos;
- áudio continua;
- gabinete muito restritivo.

Teste:

- fluxo de ar melhorado temporariamente;
- mesma carga;
- temperaturas menores;
- falha deixa de ocorrer.

Conclusão:

> Existe forte relação entre condição térmica e perda de vídeo; a GPU não pode ser considerada “queimada” apenas pelo sintoma inicial.

---

# Caso integrado 5 — Arquivos somem e sistema congela

Relato:

> “Windows está corrompido.”

Evidências:

- erros de leitura;
- SSD desaparece ocasionalmente;
- logs de armazenamento;
- falhas de arquivo;
- problema acompanha o SSD em outro sistema.

Prioridade:

- preservar dados.

Conclusão:

> O armazenamento torna-se a principal hipótese. Reinstalar o sistema antes de proteger os dados seria inadequado.

---

# Caso integrado 6 — Falha apenas no escritório

Na bancada:

- computador passa horas estável.

No cliente:

- reinicia duas vezes ao dia.

Diferenças:

- nobreak antigo;
- impressora USB específica;
- monitor diferente;
- temperatura ambiente maior.

O próximo passo não é declarar:

> “Não há defeito.”

É investigar as variáveis ambientais.

O local de uso faz parte do sistema.

---

# Uma metodologia para defeitos que não reproduzem

Quando o defeito não aparece na bancada:

1. refine o relato;
2. descubra frequência;
3. identifique condições;
4. examine logs;
5. compare ambiente;
6. peça registro em vídeo, se apropriado;
7. procure alterações recentes;
8. evite trocar peças sem evidência.

Defeito intermitente exige paciência e documentação.

---

# O conceito de “não encontrado”

Às vezes o resultado correto é:

> Falha não reproduzida nas condições de teste.

Isso é melhor que inventar uma causa.

O relatório pode registrar:

- quais testes foram feitos;
- por quanto tempo;
- em quais condições;
- o que foi observado;
- quais limitações permaneceram.

Um profissional pode concluir que não existem evidências suficientes naquele momento.

---

# O que não fazer

Durante uma investigação, evite:

- atualizar tudo ao mesmo tempo;
- formatar antes de coletar evidências;
- abrir fonte;
- usar cabos modulares de outra fonte sem compatibilidade confirmada;
- forçar conectores;
- testar hardware com sinais de queimado;
- executar stress test sem monitoramento;
- utilizar forno ou soprador para “reviver” GPU;
- repetir testes agressivos em HDD degradado;
- misturar peças sem registrar;
- alterar BIOS sem saber a configuração original;
- declarar peça defeituosa por um único software.

---

# O que um técnico experiente faz diferente?

Ele não necessariamente conhece todos os defeitos de memória.

A diferença está no processo.

Ele tende a:

- observar primeiro;
- perguntar melhor;
- reduzir variáveis;
- usar referências confiáveis;
- alterar uma coisa por vez;
- comparar resultados;
- registrar;
- reconhecer limites;
- validar depois da correção.

Esse comportamento é mais valioso que decorar centenas de sintomas.

---

# 🔬 Laboratório guiado — protocolo de diagnóstico completo

Nesta atividade, o objetivo não é encontrar um defeito específico.

É praticar o processo.

Escolha um computador funcional.

Não provoque falhas.

## Fase 1 — Identificação

Registre:

- fabricante/modelo;
- CPU;
- placa-mãe;
- memória;
- armazenamento;
- GPU;
- fonte;
- monitor;
- sistema operacional.

## Fase 2 — Inspeção

Sem desmontar desnecessariamente, observe:

- cabos;
- poeira;
- ruídos;
- posição;
- conectores externos;
- fluxo de ar.

## Fase 3 — Estado de repouso

Registre:

- CPU;
- RAM;
- armazenamento;
- GPU;
- temperaturas;
- ventoinhas.

## Fase 4 — Carga real

Execute uma tarefa normal do usuário.

Pode ser:

- navegação;
- jogo;
- compactação;
- edição;
- vídeo.

Registre como o sistema reage.

## Fase 5 — Logs

Observe se existem eventos relevantes no mesmo período.

## Fase 6 — Baseline

Crie uma pequena ficha do comportamento saudável da máquina.

Exemplo:

```text
Boot.....................32 s
CPU em repouso...........3–7%
RAM......................5,2 GB
CPU carga moderada.......68 °C
GPU jogo.................72 °C
Hotspot..................86 °C
SSD......................42 °C
Ruído....................normal
```

Esse baseline pode ser utilizado em investigações futuras.

---

# Ficha de diagnóstico

Um modelo simples pode possuir:

```text
EQUIPAMENTO
Modelo:
Data:
Responsável:

RELATO DO USUÁRIO
Sintoma:

HISTÓRICO
Quando começou:
Alterações recentes:
Tentativas anteriores:

SEGURANÇA
Dados importantes:
Sinais elétricos:
Sinais mecânicos:

CONFIGURAÇÃO
CPU:
RAM:
Placa-mãe:
GPU:
Armazenamento:
Fonte:
Sistema:

SINTOMA REPRODUZIDO
Condição:
Tempo:
Resultado:

EVIDÊNCIAS
1.
2.
3.

HIPÓTESES
1.
2.
3.

TESTES
Teste:
Variável:
Resultado:

CONCLUSÃO
Estado:

CORREÇÃO
Procedimento:

VALIDAÇÃO
Condição:
Resultado:

LIMITAÇÕES
Observações:
```

Esse documento será a base da próxima aula.

---

# Como um laboratório profissional trabalharia?

Um laboratório bem organizado tenta manter:

- cadeia de registro;
- peças de referência;
- instrumentos calibrados quando necessário;
- procedimentos;
- histórico;
- identificação de equipamentos;
- controle de alterações.

Em ambientes especializados, podem existir:

- multímetros;
- osciloscópios;
- fontes de bancada;
- câmeras térmicas;
- analisadores;
- microscópios;
- estações de retrabalho;
- duplicadores de armazenamento;
- ferramentas forenses.

Mas nenhum instrumento substitui a pergunta correta.

Um osciloscópio usado sem hipótese produz apenas formas de onda.

---

# Do diagnóstico ao laudo

A próxima etapa da formação será transformar todo esse processo em um documento técnico.

Não basta saber:

> “Era a fonte.”

Precisamos ser capazes de explicar:

- qual era o sintoma;
- como ele foi reproduzido;
- quais evidências foram coletadas;
- quais hipóteses foram descartadas;
- qual teste isolou a causa;
- qual correção foi realizada;
- como a correção foi validada;
- quais limitações permaneceram.

Isso transforma conhecimento técnico em trabalho profissional.

---

# Conexão com a próxima investigação

Até aqui, estudamos componentes individualmente e depois reunimos todos em um protocolo de diagnóstico.

Na próxima aula, o aluno não receberá o defeito pronto.

Ele receberá um caso completo.

Haverá:

- relato do cliente;
- configuração da máquina;
- fotografias descritas;
- temperaturas;
- logs;
- dados de armazenamento;
- comportamento da memória;
- resultados de testes;
- algumas pistas relevantes;
- outras pistas que parecem importantes, mas não são.

O objetivo será construir uma investigação do início ao fim e produzir o primeiro relatório técnico do curso.

# Próxima aula — Laboratório Final: Resolva o Caso e Construa o Primeiro Laudo Técnico
