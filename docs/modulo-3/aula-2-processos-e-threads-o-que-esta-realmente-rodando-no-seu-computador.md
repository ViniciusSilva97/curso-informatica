# Módulo 3 — Sistemas Operacionais
## Investigação da Camada Lógica

# Aula 2 — Processos e Threads: O Que Está Realmente Rodando no Seu Computador?

> **Pergunta da investigação**
>
> Quando um programa trava, consome 100% da CPU ou aparece como “não respondendo”, o que realmente está acontecendo dentro do sistema operacional?

---

# 📁 Dossiê da Investigação

## Caso nº 012 — O programa que “travava o computador inteiro”

Um usuário relata:

> “Quando abro o programa de edição, o computador fica muito lento. Às vezes aparece ‘Não respondendo’, a ventoinha acelera e eu preciso esperar vários minutos.”

A primeira reação poderia ser:

> “O processador não aguenta.”

Mas essa conclusão é prematura.

O computador possui:

- CPU de seis núcleos;
- 16 GB de RAM;
- SSD;
- temperaturas normais;
- hardware aprovado nos testes anteriores.

Ao reproduzir o problema, observamos:

- o programa abre normalmente;
- ao importar um projeto grande, a interface deixa de responder;
- o uso total de CPU fica em aproximadamente 32%;
- um dos núcleos permanece próximo de 100%;
- o disco apresenta picos;
- a memória aumenta gradualmente;
- o restante do sistema continua funcionando;
- depois de algum tempo, a aplicação volta a responder.

O computador travou?

Ou apenas uma parte do programa ficou ocupada?

Para responder, precisamos entender:

- processo;
- thread;
- estado;
- escalonamento;
- espera;
- uso de CPU;
- I/O;
- memória;
- relações entre processos.

---

# O objetivo desta aula

Ao final desta investigação, você deverá ser capaz de:

- diferenciar programa, processo e thread;
- compreender o que é um PID;
- interpretar uma árvore de processos;
- entender processos pai e filho;
- compreender estados de execução;
- entender o papel do escalonador;
- interpretar uso total e uso por núcleo;
- diferenciar CPU ocupada de processo esperando;
- compreender tempo de usuário e tempo de kernel;
- entender prioridade sem tratá-la como “turbo”;
- compreender troca de contexto;
- interpretar I/O de processos;
- entender handles e descritores de arquivo;
- reconhecer processos em segundo plano;
- compreender processos órfãos e zumbis em sistemas Unix-like;
- entender por que uma interface pode congelar sem o processo inteiro morrer;
- reconhecer bloqueios e deadlocks conceitualmente;
- utilizar ferramentas do Windows e Linux para observar processos;
- construir uma investigação antes de encerrar processos ou reiniciar o computador.

---

# Programa, processo e thread não são sinônimos

Essa diferença é fundamental.

## Programa

Um programa é um conjunto de instruções armazenado.

Exemplo:

    editor.exe

ou:

    /usr/bin/python3

Enquanto está no armazenamento, ele não está necessariamente executando.

---

# Processo

Quando o sistema inicia uma instância de um programa, cria estruturas para representá-la.

Essa instância em execução é um processo.

O processo possui contexto próprio.

Pode incluir:

- identificador;
- espaço de memória;
- arquivos abertos;
- credenciais;
- ambiente;
- estado;
- recursos;
- uma ou mais threads.

---

# Thread

A thread é uma unidade de execução dentro de um processo.

Um processo pode ter:

- uma thread;
- duas threads;
- dezenas;
- centenas.

Aplicações modernas frequentemente dividem trabalho entre várias threads.

---

# Um exemplo simples

Imagine um navegador.

Ele pode ter atividades diferentes:

- interface;
- rede;
- renderização;
- áudio;
- vídeo;
- extensões;
- abas;
- processos auxiliares.

Isso não significa que tudo acontece dentro de uma única sequência de instruções.

Parte do trabalho pode ser distribuída entre:

- threads;
- processos auxiliares;
- GPU;
- serviços.

---

# Por que dividir trabalho?

Separar tarefas pode permitir:

- melhor responsividade;
- paralelismo;
- isolamento;
- aproveitamento de múltiplos núcleos;
- menor impacto quando uma parte falha.

Mas também aumenta complexidade.

É necessário coordenar:

- dados;
- locks;
- filas;
- eventos;
- sincronização.

---

# PID — Process Identifier

Cada processo precisa ser identificado.

O sistema utiliza um identificador.

Frequentemente chamamos esse número de PID.

Exemplo:

    navegador.exe
    PID 4312

Outra instância do mesmo programa pode possuir:

    navegador.exe
    PID 5880

O nome é igual.

O processo não é o mesmo.

---

# O PID não é permanente

Um PID pode ser reutilizado depois que um processo termina.

Portanto:

> PID identifica uma instância em um determinado momento.

Em uma investigação, registre também:

- horário;
- nome;
- caminho;
- usuário;
- processo pai.

---

# Processo pai e processo filho

Processos podem iniciar outros processos.

Podemos representar:

    shell
      ↓
    aplicativo
      ↓
    processo auxiliar

Ou:

    serviço
      ↓
    trabalhador
      ↓
    subprocesso

Essa relação forma árvores.

---

# Por que a árvore de processos importa?

Imagine encontrar:

    powershell.exe
        ↓
    programa-desconhecido.exe

A relação pode ser relevante.

Outro exemplo:

    navegador.exe
        ↓
    renderer.exe

Isso pode ser completamente esperado.

O contexto muda a interpretação.

---

# Nome sozinho não basta

Dois arquivos podem possuir nomes semelhantes.

Um processo legítimo pode executar em:

    C:\Windows\System32

enquanto outro arquivo com nome parecido pode estar em:

    C:\Users\Usuario\Downloads

Isso não prova malícia.

Mas muda a investigação.

Sempre que necessário, observe:

- caminho;
- assinatura;
- editor;
- processo pai;
- usuário;
- horário.

---

# O processo possui memória própria?

Conceitualmente, cada processo recebe um espaço de endereçamento virtual.

Ele enxerga seu próprio ambiente.

Isso ajuda a criar isolamento.

Porém, processos podem compartilhar recursos de maneira controlada.

Exemplos:

- memória compartilhada;
- arquivos;
- sockets;
- bibliotecas;
- objetos do sistema.

---

# Threads compartilham o processo

Threads do mesmo processo geralmente compartilham elementos como:

- memória do processo;
- arquivos abertos;
- recursos comuns.

Mas cada thread precisa de informações próprias para executar.

Por exemplo:

- registradores;
- pilha;
- estado;
- contador de instrução.

---

# Por que isso importa no diagnóstico?

Uma aplicação pode possuir:

- processo ativo;
- CPU baixa;
- interface congelada.

Isso parece contraditório.

Mas a thread responsável pela interface pode estar:

- esperando;
- bloqueada;
- ocupada;
- presa em uma operação.

Enquanto outras threads continuam vivas.

---

# “Não respondendo” não significa “processo morto”

Em interfaces gráficas, o sistema espera que a aplicação processe mensagens e eventos.

Se a thread responsável pela interface deixa de responder em tempo adequado, o sistema pode marcá-la como:

> Não respondendo.

O processo ainda pode:

- executar;
- calcular;
- ler arquivos;
- esperar rede;
- voltar a responder.

---

# O erro clássico

Usuário vê:

> Não respondendo.

Conclusão:

> O programa morreu.

Nem sempre.

Precisamos observar:

- CPU;
- disco;
- memória;
- estado;
- duração;
- I/O;
- logs.

---

# Um programa pode estar ocupado legitimamente

Imagine uma aplicação compactando um arquivo enorme em uma única thread.

Um núcleo pode chegar a 100%.

Uso total do processador pode parecer baixo.

Em uma CPU com muitos núcleos, isso é esperado.

---

# 100% de um núcleo não é 100% do processador inteiro

Suponha uma CPU com oito processadores lógicos.

Uma thread ocupa completamente apenas um.

De forma simplificada:

    Núcleo lógico 1 → 100%
    Núcleo lógico 2 → 0%
    Núcleo lógico 3 → 0%
    Núcleo lógico 4 → 0%
    Núcleo lógico 5 → 0%
    Núcleo lógico 6 → 0%
    Núcleo lógico 7 → 0%
    Núcleo lógico 8 → 0%

A média total pode aparecer próxima de:

    12,5%

Isso não significa que a thread possa usar mais CPU automaticamente.

Ela pode ser essencialmente sequencial.

---

# Paralelismo não acontece por mágica

Para usar vários núcleos, o software precisa conseguir dividir trabalho.

Nem toda tarefa pode ser paralelizada de maneira eficiente.

Existem dependências.

Exemplo:

    Etapa B depende de A
    Etapa C depende de B

Nesse caso, não é simples executar tudo ao mesmo tempo.

---

# Concorrência e paralelismo

Os termos se relacionam, mas não são idênticos.

## Concorrência

Várias tarefas progridem ao longo do tempo.

## Paralelismo

Várias tarefas executam fisicamente ao mesmo tempo em diferentes unidades de execução.

Um sistema pode ter concorrência mesmo com um único núcleo, alternando rapidamente entre tarefas.

---

# O escalonador

O sistema operacional decide quais threads podem usar a CPU.

Essa função pertence ao escalonador.

Uma representação simplificada:

    Threads prontas
       ↓
    Escalonador
       ↓
    Processadores lógicos

O escalonador considera várias informações.

Por exemplo:

- prioridade;
- estado;
- políticas;
- afinidade;
- carga;
- tempo;
- características do sistema.

---

# Uma thread não fica sempre executando

Ela pode alternar entre estados.

Uma simplificação didática:

    Pronta
      ↓
    Executando
      ↓
    Esperando
      ↓
    Pronta novamente

---

# Estado pronto

A thread pode executar.

Mas está aguardando oportunidade de CPU.

---

# Estado executando

Está utilizando CPU naquele momento.

---

# Estado de espera

Está aguardando algum evento.

Exemplos:

- leitura do disco;
- resposta de rede;
- lock;
- temporizador;
- entrada do usuário.

---

# Esperar não é o mesmo que travar

Imagine:

    programa solicita dados da internet
        ↓
    rede ainda não respondeu
        ↓
    thread espera

Isso pode ser comportamento normal.

Se a interface foi mal projetada e depende da mesma thread, o usuário pode perceber congelamento.

---

# CPU baixa pode coexistir com lentidão

Um aplicativo lento com CPU baixa pode estar esperando:

- disco;
- rede;
- outro processo;
- serviço;
- lock;
- resposta externa.

Por isso:

> CPU baixa não prova que “não há nada acontecendo”.

---

# I/O — entrada e saída

Processos interagem com recursos externos à CPU.

Chamamos muitas dessas operações de I/O.

Exemplos:

- leitura de SSD;
- gravação;
- rede;
- periféricos;
- pipes.

Um processo pode passar grande parte do tempo esperando I/O.

---

# CPU-bound e I/O-bound

Dois conceitos úteis.

## CPU-bound

A tarefa é limitada principalmente por processamento.

Exemplos:

- cálculo;
- compressão;
- renderização de CPU;
- compilação.

## I/O-bound

A tarefa passa muito tempo esperando entrada e saída.

Exemplos:

- leitura massiva;
- cópia;
- consulta remota;
- rede lenta.

---

# O mesmo programa pode mudar de comportamento

Durante uma operação:

    carregar projeto
        → I/O intenso

Depois:

    processar dados
        → CPU intensa

Depois:

    salvar
        → I/O novamente

Precisamos observar o momento.

---

# Tempo de usuário e tempo de kernel

O uso de CPU pode ser dividido conceitualmente entre diferentes modos.

## Tempo de usuário

Execução de código no espaço do usuário.

## Tempo de kernel

Tempo gasto executando operações privilegiadas do sistema.

Se um processo gera muita atividade de sistema, parte do tempo pode aparecer associada ao kernel.

---

# Por que isso ajuda?

Um processo que faz muitas chamadas de sistema pode produzir:

- alto I/O;
- atividade de rede;
- manipulação de arquivos;
- operações com dispositivos.

A distribuição entre tempo de usuário e kernel ajuda investigações mais avançadas.

---

# Context switch — troca de contexto

Quando a CPU deixa uma thread e passa para outra, o sistema precisa preservar e restaurar informações.

Chamamos isso de troca de contexto.

De forma simplificada:

    Thread A executa
       ↓
    salva contexto A
       ↓
    carrega contexto B
       ↓
    Thread B executa

---

# Muitas trocas de contexto são ruins?

Não necessariamente.

Sistemas multitarefa realizam muitas trocas.

Um número elevado pode ser normal.

Mas em alguns cenários, excesso pode indicar:

- muitas threads;
- sincronização excessiva;
- alta frequência de eventos;
- desenho ineficiente.

Novamente, contexto é essencial.

---

# Thread demais também pode prejudicar

Criar mais threads não garante mais desempenho.

Pode aumentar:

- memória;
- sincronização;
- contenção;
- trocas de contexto;
- complexidade.

Existe um ponto em que mais paralelismo produz sobrecarga.

---

# Prioridade

Sistemas permitem diferentes prioridades de execução.

Prioridade influencia a preferência do escalonador.

Mas não transforma um processador lento em rápido.

---

# Aumentar prioridade não cria capacidade

Se uma CPU está saturada, aumentar prioridade de um processo significa:

> ele pode receber preferência sobre outros.

Isso pode melhorar responsividade daquele processo.

Mas pode prejudicar:

- interface;
- áudio;
- serviços;
- outros programas.

---

# Não altere prioridade por tentativa

Em diagnóstico, alterar prioridade cedo demais muda a cena.

Primeiro observe:

- comportamento original;
- uso;
- estado;
- carga;
- dependências.

Depois teste uma hipótese específica.

---

# Afinidade

Alguns sistemas permitem definir em quais processadores lógicos uma tarefa pode executar.

Isso é afinidade.

Exemplo conceitual:

    Processo A
    permitido em CPU 0 e CPU 1

A afinidade pode ser útil em:

- testes;
- compatibilidade;
- cargas específicas.

Mas não deve ser usada como “otimização universal”.

---

# Handles no Windows

Processos precisam referenciar objetos do sistema.

No Windows, um conceito importante é handle.

Um processo pode possuir handles para:

- arquivos;
- eventos;
- processos;
- threads;
- chaves de registro;
- objetos de sincronização.

---

# Descritores de arquivo em sistemas Unix-like

Em Linux e outros sistemas Unix-like, encontramos descritores de arquivo.

Eles podem representar:

- arquivos;
- sockets;
- pipes;
- dispositivos.

O conceito ajuda a entender como processos acessam recursos.

---

# “Arquivo em uso”

Se um processo mantém um arquivo aberto, outro programa pode encontrar restrições dependendo das regras do sistema e da aplicação.

Sintoma:

> Não foi possível excluir o arquivo porque está sendo usado.

Pergunta:

> Qual processo possui uma referência ativa para esse arquivo?

Isso é investigação de processo.

---

# Vazamento de handles

Assim como memória, um programa pode deixar de liberar recursos.

Ao longo do tempo:

    300 handles
       ↓
    2.000
       ↓
    10.000
       ↓
    50.000

Isso pode contribuir para instabilidade.

Mas aumento não prova vazamento.

Precisamos observar crescimento anormal e contínuo.

---

# Threads e sincronização

Quando várias threads compartilham dados, precisam evitar conflitos.

Mecanismos de sincronização podem incluir conceitos como:

- mutex;
- semáforo;
- evento;
- lock;
- condição.

O objetivo é controlar acesso concorrente.

---

# Corrida — race condition

Imagine duas threads alterando o mesmo dado sem coordenação.

O resultado pode depender da ordem de execução.

Isso pode gerar comportamento:

- intermitente;
- difícil de reproduzir;
- aparentemente aleatório.

Esse tipo de problema é chamado de condição de corrida.

---

# Deadlock

Considere:

    Thread A possui Recurso 1
    e espera Recurso 2

    Thread B possui Recurso 2
    e espera Recurso 1

Nenhuma avança.

Temos um bloqueio mútuo.

Esse é o conceito de deadlock.

---

# Nem todo congelamento é deadlock

Uma aplicação pode congelar por:

- cálculo longo;
- I/O lento;
- servidor remoto;
- lock temporário;
- bug;
- loop;
- falta de memória.

Precisamos de evidência antes de usar o termo.

---

# Processo órfão

Em sistemas Unix-like, um processo pode continuar existindo depois que seu processo pai termina.

O sistema precisa tratá-lo adequadamente.

Essa situação é diferente de processo zumbi.

---

# Processo zumbi

Um processo zumbi em sistemas Unix-like já terminou a execução, mas ainda possui uma pequena entrada na tabela de processos porque seu estado de término ainda não foi coletado pelo pai.

Ele não é:

- um processo usando CPU normalmente;
- um programa “ressuscitado”;
- necessariamente malware.

É um estado específico de gerenciamento de processos.

---

# O nome “zumbi” confunde

Em cursos superficiais, a palavra pode criar a impressão de um programa morto que continua executando.

Não é isso.

O processo já terminou sua execução.

O que permanece é informação administrativa até que o sistema/processo responsável a recolha.

---

# Processos em segundo plano

Nem todo processo possui janela.

Podem existir processos associados a:

- serviços;
- atualizadores;
- sincronização;
- drivers auxiliares;
- segurança;
- impressão;
- banco de dados;
- áudio.

Não encerre um processo apenas porque você não vê interface.

---

# Serviço não é exatamente o mesmo que processo

Um serviço é uma função administrada pelo sistema.

Ele pode estar associado a:

- um processo próprio;
- um processo compartilhado;
- múltiplos componentes.

Em alguns sistemas, vários serviços podem existir dentro de um mesmo processo host.

Por isso:

> processo e serviço não devem ser tratados como sinônimos.

---

# Árvore de processos

Uma árvore permite observar origem.

Exemplo didático:

    sistema
      ├── serviço A
      │    └── trabalhador
      ├── shell
      │    ├── navegador
      │    │    ├── renderizador
      │    │    └── GPU helper
      │    └── editor
      └── serviço B

Isso é muito mais informativo do que uma lista plana.

---

# Ferramentas no Windows

## Gerenciador de Tarefas

Permite observar:

- processos;
- CPU;
- memória;
- disco;
- rede;
- GPU;
- usuários;
- inicialização.

É excelente para uma primeira triagem.

---

# Aba Detalhes

A aba de detalhes pode mostrar informações mais técnicas.

Dependendo da configuração, podemos observar:

- PID;
- status;
- usuário;
- CPU;
- memória;
- prioridade;
- arquitetura.

Colunas adicionais podem ser ativadas.

---

# Monitor de Recursos

Permite observar relações mais detalhadas entre:

- CPU;
- disco;
- rede;
- memória.

É útil quando a pergunta é:

> Qual processo está gerando esta atividade?

---

# PowerShell

Para observação, podemos utilizar:

    Get-Process

Isso lista processos.

Podemos selecionar propriedades:

    Get-Process | Select-Object Id, ProcessName, CPU

Esse comando apenas consulta informações.

---

# tasklist

Outra ferramenta nativa:

    tasklist

Ela exibe processos ativos e seus identificadores.

Não é tão rica quanto ferramentas gráficas, mas é útil em diagnóstico e automação.

---

# Process Explorer

A suíte Sysinternals da Microsoft oferece ferramentas avançadas.

Process Explorer pode ajudar a observar:

- árvore de processos;
- handles;
- threads;
- assinaturas;
- imagens carregadas;
- relações pai/filho.

É uma ferramenta profissional muito valiosa.

Nesta aula, porém, o objetivo é entender os conceitos antes de depender de ferramentas avançadas.

---

# Ferramentas no Linux

## ps

Comando clássico para observar processos.

Exemplo:

    ps aux

Ele pode mostrar:

- usuário;
- PID;
- CPU;
- memória;
- comando.

---

# top

Permite observação dinâmica.

Pode mostrar:

- carga;
- processos;
- CPU;
- memória;
- estados.

---

# htop

Quando disponível, fornece uma interface mais amigável e interativa.

Mas não está instalado em todos os sistemas.

---

# pstree

Pode mostrar relações hierárquicas.

Exemplo:

    pstree

Isso ajuda a visualizar processos pai e filho.

---

# /proc

Em muitos sistemas Linux, informações sobre processos são expostas pelo pseudo-sistema de arquivos /proc.

Exemplo conceitual:

    /proc/1234/

onde 1234 seria um PID.

Ali podem existir informações sobre:

- status;
- memória;
- arquivos abertos;
- linha de comando.

É um recurso poderoso para investigação.

---

# Não precisamos decorar comandos

O curso não quer formar usuários que apenas repetem comandos.

Queremos formar investigadores.

A pergunta vem primeiro.

Depois escolhemos a ferramenta.

---

# Pergunta: quem usa CPU?

Windows:

- Gerenciador de Tarefas;
- Monitor de Recursos;
- PowerShell.

Linux:

- top;
- htop;
- ps.

---

# Pergunta: quem abriu determinado arquivo?

Ferramentas avançadas podem ajudar a identificar:

- handles;
- descritores;
- processos associados.

---

# Pergunta: qual processo iniciou este processo?

Precisamos observar:

- PPID;
- árvore;
- histórico;
- ferramenta apropriada.

---

# Pergunta: o processo está executando ou esperando?

Precisamos analisar:

- CPU;
- estado;
- I/O;
- threads;
- dependências.

---

# O caso volta à bancada

Vamos retornar ao programa de edição.

Sintomas:

- interface “Não respondendo”;
- um núcleo em 100%;
- uso total de CPU em 32%;
- disco com picos;
- memória aumentando;
- sistema continua utilizável.

---

# Primeira hipótese

> O programa está utilizando uma thread principal para trabalho pesado.

Essa hipótese prevê:

- um núcleo muito ocupado;
- interface pouco responsiva;
- processo ainda vivo;
- retorno da interface após concluir a tarefa.

---

# Teste

Observamos o comportamento por alguns minutos.

Resultados:

- uso do mesmo núcleo permanece alto;
- atividade de disco ocorre ao carregar recursos;
- memória estabiliza;
- nenhuma falha é registrada;
- ao concluir a importação, CPU cai;
- interface volta a responder;
- arquivo aparece corretamente.

---

# Conclusão parcial

O comportamento é compatível com:

> tarefa pesada executada de maneira que bloqueia temporariamente a responsividade da interface.

Isso é diferente de:

> falha do processador.

---

# A ventoinha acelerou

Isso também fazia parte da reclamação.

Com CPU trabalhando, consumo e temperatura aumentam.

O sistema de refrigeração responde.

Portanto:

    carga legítima
       ↓
    temperatura sobe
       ↓
    ventoinha acelera

A ventoinha não prova defeito.

---

# E a memória aumentando?

Durante a importação, o programa carrega dados.

A memória sobe.

Depois estabiliza.

Isso não demonstra vazamento.

Se continuasse crescendo indefinidamente a cada operação, sem liberação, a hipótese de vazamento ficaria mais relevante.

---

# Uma investigação ruim

    Programa não responde
        ↓
    “CPU fraca”
        ↓
    troca de processador

---

# Uma investigação melhor

    Programa não responde
        ↓
    observar processo
        ↓
    identificar thread/carga
        ↓
    correlacionar CPU, I/O e memória
        ↓
    verificar se tarefa conclui
        ↓
    comparar comportamento
        ↓
    concluir

---

# Quando encerrar um processo?

Às vezes é necessário.

Mas antes, pergunte:

- existem dados não salvos?
- o programa ainda está fazendo I/O?
- existe operação crítica?
- é um processo do sistema?
- sabemos o impacto?
- a investigação precisa preservar o estado?

Encerrar deve ser decisão consciente.

---

# Não finalize processos críticos aleatoriamente

Encerrar processos do sistema pode causar:

- perda de sessão;
- instabilidade;
- desligamento;
- perda de dados;
- comportamento imprevisível.

Durante o curso, priorizaremos observação segura.

---

# Reiniciar apaga evidências voláteis

Ao reiniciar, perdemos informações como:

- processos ativos;
- PIDs;
- memória volátil;
- conexões;
- handles;
- estado de threads.

Por isso, se a investigação for importante:

> observe e registre antes de reiniciar.

---

# Tempo de CPU

Ferramentas podem mostrar tempo acumulado de CPU.

Isso é diferente de porcentagem instantânea.

Um processo pode:

- ter usado muita CPU anteriormente;
- estar ocioso agora.

A interpretação precisa considerar janela temporal.

---

# Uso instantâneo também engana

Um pico rápido pode desaparecer antes de ser observado.

Ferramentas de monitoramento e histórico ajudam.

Em investigação avançada, podemos registrar:

- contadores;
- traces;
- eventos;
- perfis.

---

# Amostragem

Muitos monitores trabalham por amostragem.

Eles observam em intervalos.

Portanto, um número exibido é uma representação do período.

Isso explica pequenas diferenças entre ferramentas.

---

# Processo com 0% pode trabalhar

Se o uso é muito pequeno ou intermitente, a interface pode arredondar para zero.

Não conclua:

> “esse processo nunca usa CPU.”

---

# Processo suspenso

Alguns sistemas podem suspender processos temporariamente.

Isso reduz consumo quando não precisam executar.

Aplicativos modernos podem ser suspensos em determinados cenários.

Suspenso não significa encerrado.

---

# Prioridade de I/O

Além da CPU, sistemas podem aplicar políticas sobre operações de entrada e saída.

Um processo em segundo plano pode receber tratamento diferente de uma tarefa interativa.

Isso ajuda a preservar responsividade.

---

# QoS e classes de trabalho

Sistemas modernos utilizam várias políticas para equilibrar:

- responsividade;
- eficiência;
- energia;
- desempenho.

O escalonamento real é muito mais complexo que uma fila simples.

Nosso modelo serve para diagnóstico inicial.

---

# Processos e segurança

Um processo executa com um contexto de segurança.

Isso influencia:

- arquivos que pode acessar;
- operações permitidas;
- recursos disponíveis.

Por isso, o mesmo executável pode se comportar diferente quando executado:

- por outro usuário;
- com outro nível de privilégio.

---

# Elevação de privilégio

Executar como administrador pode mudar permissões.

Mas isso não deve ser usado como:

> “tente como administrador até funcionar.”

Primeiro pergunte:

> por que o programa precisa de privilégio?

Se um aplicativo comum exige privilégios inesperados, isso merece análise.

---

# Processo e ambiente

Processos podem herdar informações do ambiente.

Exemplos:

- variáveis;
- diretório atual;
- credenciais;
- sessão.

Diferenças de ambiente podem explicar:

> funciona em um terminal, mas não em outro.

---

# DLLs e bibliotecas

Processos carregam bibliotecas.

Uma falha pode envolver:

- versão;
- arquitetura;
- dependência;
- conflito;
- arquivo ausente.

Então:

> processo fecha ao iniciar

não significa necessariamente erro no executável principal.

---

# Crash

Crash significa que a execução terminou de forma anormal.

Pode ocorrer por:

- acesso inválido à memória;
- exceção não tratada;
- biblioteca;
- bug;
- driver;
- corrupção;
- recursos.

Um crash é diferente de uma aplicação que continua viva, mas não responde.

---

# Hang

Hang é um termo usado para descrever uma aplicação que permanece ativa, mas deixa de progredir ou responder adequadamente.

Pode estar relacionado a:

- deadlock;
- espera infinita;
- I/O;
- loop;
- bloqueio.

Precisamos descobrir qual.

---

# Loop de CPU

Um programa pode entrar em uma repetição que consome CPU continuamente.

Sintomas:

- uso alto;
- pouca ou nenhuma progressão;
- comportamento reproduzível.

Isso é diferente de esperar I/O.

---

# Espera infinita

Uma thread pode aguardar um evento que nunca ocorre.

Uso de CPU pode permanecer baixo.

A aplicação parece congelada.

Esse é um bom exemplo de por que:

> CPU baixa não significa ausência de problema.

---

# Wait chain

Ferramentas avançadas podem analisar cadeias de espera.

A ideia é descobrir:

> esta thread espera o quê?

E talvez:

> o recurso depende de qual outra thread?

Isso pode revelar bloqueios.

---

# Contenção

Quando muitas threads disputam o mesmo recurso, temos contenção.

Exemplo:

    Thread A
    Thread B
    Thread C
       ↓
    mesmo lock

Mesmo com vários núcleos, as threads podem acabar esperando.

Paralelismo teórico não garante desempenho real.

---

# Escalabilidade

Um programa que usa 2 threads muito bem pode não dobrar desempenho com 4, 8 ou 16.

Razões:

- parte sequencial;
- sincronização;
- memória;
- cache;
- I/O;
- sobrecarga.

Por isso, avaliar desempenho exige entender a carga.

---

# O sistema também possui processos

Nem tudo é aplicativo do usuário.

O sistema executa componentes relacionados a:

- sessões;
- serviços;
- segurança;
- rede;
- áudio;
- interface;
- gerenciamento.

Muitos são essenciais.

---

# PIDs muito baixos são sempre sistema?

Não devemos utilizar regras simplistas.

A convenção varia entre sistemas.

No Linux, PID 1 possui papel especial.

No Windows, a arquitetura é diferente.

Conheça o sistema antes de interpretar.

---

# PID 1 no Linux

Em sistemas Linux modernos, o PID 1 geralmente corresponde ao processo de inicialização do espaço do usuário.

Em muitas distribuições, é o systemd.

Ele possui responsabilidades especiais.

Mas não devemos generalizar para todos os sistemas operacionais.

---

# O processo idle

Sistemas podem representar tempo ocioso de maneiras específicas.

No Windows, existe o conceito de System Idle Process.

Um valor alto normalmente indica:

> CPU ociosa.

Isso é contraintuitivo para iniciantes.

“Idle 95%” não significa:

> processo usando 95% para fazer algo.

Significa que grande parte da capacidade está ociosa.

---

# Mito ou Evidência?

## “100% de CPU significa processador defeituoso.”

**Mito.**

Pode ser carga legítima ou problema de software.

---

## “Não respondendo significa que o processo morreu.”

**Mito.**

Ele pode estar ocupado ou esperando.

---

## “Mais threads sempre deixa o programa mais rápido.”

**Mito.**

Sincronização e sobrecarga podem reduzir desempenho.

---

## “Se um processo não tem janela, é suspeito.”

**Mito.**

Muitos serviços e componentes funcionam em segundo plano.

---

## “Prioridade alta melhora qualquer programa.”

**Mito.**

Pode apenas deslocar recursos de outras tarefas.

---

## “CPU baixa significa que o aplicativo está saudável.”

**Mito.**

Ele pode estar bloqueado ou esperando I/O.

---

## “Processo zumbi está executando escondido.”

**Mito.**

Em sistemas Unix-like, é um estado administrativo após término.

---

# 🔬 Laboratório — observando processos sem alterar o sistema

O objetivo é coletar evidências.

Não encerre processos importantes.

---

# Etapa 1 — Abra seu monitor de processos

No Windows:

- Gerenciador de Tarefas.

No Linux:

- Monitor do Sistema;
- top;
- htop, se disponível.

Observe por dois minutos sem abrir nada novo.

---

# Etapa 2 — Registre cinco processos

Para cada processo, anote:

    Nome:
    PID:
    Usuário:
    CPU:
    Memória:
    Possui interface?
    Função provável:

---

# Etapa 3 — Abra um aplicativo conhecido

Escolha algo simples:

- navegador;
- editor de texto;
- calculadora.

Observe:

- surge um ou vários processos?
- quem é o processo pai?
- CPU aumenta?
- memória aumenta?

---

# Etapa 4 — Abra uma segunda instância

Se o aplicativo permitir, abra novamente.

Pergunte:

> surgiu outro PID?

Isso mostra a diferença entre:

- programa;
- instância.

---

# Etapa 5 — Observe CPU por núcleo

Abra uma operação segura.

Exemplo:

- carregar uma página pesada;
- compactar arquivo de teste;
- abrir projeto conhecido.

Observe:

- todos os núcleos sobem?
- apenas alguns?
- existe um núcleo muito ocupado?

Registre.

---

# Etapa 6 — Observe I/O

Durante abertura de um arquivo grande, veja:

- atividade de armazenamento;
- processo responsável;
- duração.

Pergunte:

> a tarefa é limitada por CPU ou por I/O?

---

# Etapa 7 — Observe a árvore

Se sua ferramenta permitir, encontre:

- processo pai;
- processos filhos.

Registre:

    Pai:
    Filho:
    Relação provável:

---

# Etapa 8 — PowerShell no Windows

Execute apenas para observação:

    Get-Process

Depois:

    Get-Process | Sort-Object CPU -Descending | Select-Object -First 10 Id, ProcessName, CPU

Compare com o Gerenciador de Tarefas.

---

# Etapa 9 — Linux

Se estiver em Linux:

    ps aux

Depois:

    ps -eo pid,ppid,comm,%cpu,%mem --sort=-%cpu

Compare:

- PID;
- PPID;
- CPU;
- memória.

---

# Etapa 10 — Não conclua rápido

Escolha o processo com maior CPU.

Responda:

- é esperado?
- quanto tempo permanece alto?
- existe uma tarefa em andamento?
- CPU cai depois?
- qual evidência explica o comportamento?

---

# 📁 Registro do laboratório

Adicione ao Dossiê:

    Sistema operacional:
    Data e horário:

    Processo observado:
    PID:
    Processo pai:
    CPU:
    Memória:
    I/O:
    Número aproximado de threads:

    Sintoma:
    Hipótese:
    Evidência:
    Teste:
    Resultado:
    Conclusão:

---

# Estudo de caso 1 — Um núcleo em 100%

Sintoma:

> programa parece lento.

CPU:

    total → 18%
    um núcleo → 100%

O programa realiza uma tarefa sequencial.

Conclusão:

> existe saturação de uma linha de execução, não da CPU inteira.

Trocar para uma CPU com mais núcleos pode não resolver proporcionalmente.

Desempenho por núcleo pode importar mais nesse cenário.

---

# Estudo de caso 2 — 3% de CPU e aplicação congelada

Sintoma:

> aplicativo não responde.

Evidências:

- CPU baixa;
- processo continua ativo;
- rede possui latência;
- interface volta quando servidor responde.

Conclusão:

> comportamento compatível com espera de I/O/rede.

---

# Estudo de caso 3 — CPU alta depois de fechar a janela

Usuário fecha a interface.

Mas um processo continua ativo.

Hipóteses:

- tarefa em segundo plano;
- fechamento incompleto;
- serviço auxiliar;
- bug.

Primeiro identifique a função.

Não finalize imediatamente.

---

# Estudo de caso 4 — Muitos processos do navegador

Usuário vê vinte processos.

Conclusão precipitada:

> “O navegador está duplicado e com vírus.”

Mas navegadores modernos podem usar múltiplos processos para:

- abas;
- renderização;
- extensões;
- GPU;
- isolamento.

Quantidade sozinha não prova anomalia.

---

# Estudo de caso 5 — Memória cresce ao longo do dia

Sintoma:

> programa começa com 800 MB e termina com 9 GB.

Perguntas:

- crescimento é contínuo?
- cai ao fechar documentos?
- cache é liberado?
- ocorre em toda execução?
- sistema começa a paginar?

A hipótese de vazamento cresce se o comportamento for:

- contínuo;
- reproduzível;
- sem liberação proporcional.

---

# Estudo de caso 6 — Sistema lento, CPU baixa

Evidências:

- CPU 8%;
- RAM quase cheia;
- SSD com alto I/O;
- paginação intensa.

Conclusão:

> CPU não é o gargalo principal.

Processos ajudam a localizar quem está consumindo memória e gerando I/O.

---

# O método aplicado a processos

## 1. Sintoma

> Programa não responde.

## 2. Observação

> Processo continua ativo.

## 3. Evidência

> CPU baixa, I/O de rede ativo.

## 4. Hipótese

> Espera por resposta externa.

## 5. Teste

> Observar rede e reproduzir com conectividade diferente.

## 6. Resultado

> Interface retorna assim que operação remota conclui.

## 7. Conclusão

> Comportamento ligado à espera de rede, não à falha física da CPU.

---

# O que um profissional avançado observaria?

Em uma análise mais profunda, poderíamos investigar:

- pilhas de threads;
- wait states;
- contadores;
- handles;
- DLLs;
- chamadas de sistema;
- traces;
- eventos do kernel;
- amostragem de CPU;
- perfis de desempenho.

Ferramentas especializadas podem incluir analisadores de desempenho e depuradores.

Mas a lógica continua igual.

---

# Um profiler não é mágico

Ferramentas de profiling ajudam a responder:

> onde o programa gasta tempo?

Podem revelar:

- função pesada;
- espera;
- alocação;
- contenção.

Mas os dados precisam ser interpretados.

---

# Tempo de parede e tempo de CPU

Imagine uma tarefa que leva:

    10 segundos no relógio

Mas utiliza:

    2 segundos de CPU

Isso significa que os outros 8 segundos podem ter sido gastos:

- esperando;
- bloqueada;
- dormindo;
- em I/O.

Tempo total e tempo de CPU não são iguais.

---

# Latência versus throughput

## Latência

Tempo para concluir uma operação individual.

## Throughput

Quantidade total de trabalho por unidade de tempo.

Um sistema pode ter:

- bom throughput;
- latência ruim.

Para aplicações interativas, latência importa muito.

---

# Responsividade

Um computador “rápido” precisa responder ao usuário.

Mesmo que uma tarefa pesada execute corretamente, a interface deve idealmente continuar responsiva.

Esse é um problema de projeto de software e escalonamento de trabalho.

---

# Por que isso importa para suporte técnico?

Porque o técnico precisa separar:

- hardware insuficiente;
- software mal otimizado;
- configuração;
- operação legítima;
- bug;
- recurso externo lento.

Sem observar processos, tudo vira:

> “computador lento.”

---

# O diagnóstico não deve começar pela troca de peças

Um processo consumindo CPU não significa:

> compre outro processador.

Precisamos descobrir:

- qual tarefa;
- se é esperada;
- se conclui;
- se a aplicação escala;
- se existe erro.

---

# O diagnóstico também não deve começar pelo encerramento

Encerrar o processo pode remover o sintoma.

Mas não explica:

- por que aconteceu;
- quando começou;
- como reproduzir;
- qual recurso estava esperando.

Observe primeiro.

---

# Processos como evidência

Processos revelam o estado atual do sistema.

Eles podem indicar:

- programas ativos;
- tarefas em segundo plano;
- consumo;
- origem;
- relações.

Mas são evidências voláteis.

Depois de reiniciar, o cenário muda.

---

# A importância do horário

Registre:

    21:05 — aplicação abriu
    21:06 — CPU subiu
    21:07 — interface não respondeu
    21:08 — disco caiu
    21:09 — aplicação voltou

Essa linha do tempo vale muito mais que:

> “travou por alguns minutos.”

---

# A importância de reproduzir

Se o comportamento ocorre sempre ao:

- importar arquivo;
- conectar a servidor;
- abrir projeto;
- carregar extensão;

temos uma condição reproduzível.

Isso permite testar uma variável de cada vez.

---

# O que não devemos fazer

Evite:

- finalizar processos aleatoriamente;
- desativar serviços sem entender;
- instalar “otimizadores”;
- aumentar prioridade de tudo;
- limpar RAM com programas milagrosos;
- formatar sem investigação.

Essas ações podem mascarar a causa.

---

# “Limpadores de RAM”

Sistemas modernos gerenciam memória de maneira sofisticada.

Ferramentas que prometem “liberar RAM” podem:

- forçar descarte de cache;
- aumentar paginação;
- criar sensação temporária de espaço livre.

RAM vazia não é objetivo.

O objetivo é uso eficiente e responsivo.

---

# O processo certo pode usar muita RAM

Um editor trabalhando com projeto grande pode legitimamente utilizar vários gigabytes.

O que importa é:

- necessidade;
- comportamento;
- estabilidade;
- pressão geral.

---

# O processo errado pode usar pouca RAM e ainda causar problema

Um serviço usando 50 MB pode:

- bloquear recurso;
- falhar repetidamente;
- gerar erros;
- impedir inicialização.

Quantidade de memória não define importância.

---

# Investigação por camada

Quando um programa apresenta problema, tente identificar:

    Aplicação
       ↓
    Processo
       ↓
    Threads
       ↓
    Recursos
       ↓
    Serviço / driver / I/O
       ↓
    Kernel
       ↓
    Hardware

A falha pode estar em qualquer ponto.

---

# Relação com a Aula 1

Na Aula 1, vimos que o sistema operacional administra recursos.

Agora enxergamos uma parte concreta desse gerenciamento.

O escalonador distribui CPU.

O sistema mantém:

- processos;
- threads;
- estados;
- identificadores;
- recursos.

A abstração começa a ficar observável.

---

# 📁 Dossiê da Investigação — atualização

Adicione uma nova ficha:

## Ficha de processo

    Nome:
    PID:
    Usuário:
    Caminho:
    Processo pai:
    Filhos:
    CPU:
    Memória:
    I/O:
    Estado:
    Threads:
    Horário observado:
    Comportamento esperado:
    Comportamento observado:
    Hipótese:
    Teste:
    Resultado:

Essa ficha será reutilizada em aulas futuras.

---

# Conexão com a próxima aula

Processos não trabalham apenas com CPU.

Eles precisam de memória.

Até agora, sabemos que cada processo recebe um espaço virtual.

Mas isso abre novas perguntas:

- de onde vem essa memória?
- por que um processo enxerga endereços que não correspondem diretamente à RAM?
- o que acontece quando a memória física fica cheia?
- o que são páginas?
- o que significa commit?
- por que o SSD começa a trabalhar quando falta RAM?
- quando paginação é normal?
- quando ela se torna um problema?
- o que é cache?
- por que “RAM livre” não é necessariamente melhor?

Na próxima aula, vamos investigar a memória do ponto de vista do sistema operacional.

# Próxima aula — Memória Virtual e Paginação: Por Que o Sistema Usa o SSD Mesmo Quando Você Não Pediu?
