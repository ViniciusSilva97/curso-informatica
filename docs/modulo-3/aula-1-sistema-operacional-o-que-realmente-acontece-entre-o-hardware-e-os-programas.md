# Módulo 3 — Sistemas Operacionais
## Investigação da Camada Lógica

# Aula 1 — Sistema Operacional: O Que Realmente Acontece Entre o Hardware e os Programas?

> **Pergunta da investigação**
>
> Se o hardware está funcionando corretamente, por que um computador ainda pode ficar lento, travar, perder funções, negar acesso a arquivos ou impedir que programas sejam executados?

---

# 📁 Dossiê da Investigação

## Caso nº 011 — O computador que estava saudável, mas continuava “doente”

Um computador chega à bancada com a seguinte reclamação:

> “Ele liga normalmente, mas depois que entra no Windows fica lento, alguns programas não abrem e a internet às vezes desaparece.”

Na investigação física, nada crítico é encontrado.

Os testes mostram:

- processador estável;
- memória RAM sem erros detectados;
- SSD sem alertas críticos;
- temperaturas dentro do esperado;
- fonte estável nas condições testadas;
- placa de vídeo funcionando;
- nenhum ruído mecânico anormal.

O equipamento passa pelos testes de hardware.

Mesmo assim, depois do login:

- o uso de CPU sobe sem motivo aparente;
- um programa informa que não possui permissão;
- um serviço deixa de iniciar;
- a interface de rede desaparece temporariamente;
- o sistema registra erros;
- o computador demora para desligar.

Se as peças estão funcionando, onde está o problema?

A partir deste módulo, a investigação muda de camada.

No Módulo 2, observávamos principalmente o computador físico.

Agora investigaremos o sistema que coordena esse hardware.

> **O sistema operacional não é apenas a “tela do computador”. Ele é a camada que administra recursos, aplica regras e cria o ambiente no qual os programas conseguem existir.**

---

# Objetivos da aula

Ao final desta aula, você deverá ser capaz de:

- compreender a função real de um sistema operacional;
- diferenciar firmware, bootloader, kernel, serviços e aplicações;
- compreender a separação entre espaço do kernel e espaço do usuário;
- entender por que programas não acessam o hardware livremente;
- compreender o papel das chamadas de sistema;
- identificar processos e threads como unidades de execução;
- entender o papel básico do escalonador;
- compreender o conceito de memória virtual;
- entender como drivers conectam o kernel aos dispositivos;
- compreender o papel dos sistemas de arquivos;
- reconhecer usuários, grupos e permissões como mecanismos de controle;
- entender o que são serviços e daemons;
- compreender por que logs são evidências fundamentais;
- investigar um problema lógico sem formatar o computador por tentativa.

---

# O sistema operacional não é apenas a interface gráfica

Quando muitas pessoas pensam em Windows, Linux ou macOS, lembram imediatamente de:

- área de trabalho;
- menu iniciar;
- janelas;
- ícones;
- pastas;
- configurações.

Esses elementos são importantes.

Mas representam apenas a parte visível.

Por baixo da interface existe uma estrutura muito maior.

Uma representação simplificada seria:

    Usuário
       ↓
    Aplicações
       ↓
    Bibliotecas e APIs
       ↓
    Chamadas de sistema
       ↓
    Kernel
       ↓
    Drivers
       ↓
    Hardware

O sistema operacional cria uma camada de abstração.

Sem essa camada, cada programa precisaria conhecer diretamente:

- modelo da CPU;
- controlador de armazenamento;
- placa de rede;
- dispositivo USB;
- memória física;
- tela;
- teclado;
- sistema de interrupções;
- detalhes elétricos e lógicos de cada componente.

Isso seria extremamente difícil de manter.

---

# A principal função: administrar recursos

Um computador possui recursos limitados.

Entre eles:

- tempo de CPU;
- memória;
- armazenamento;
- dispositivos;
- conexões;
- arquivos;
- identificadores;
- portas de comunicação.

Vários programas querem utilizar esses recursos ao mesmo tempo.

O sistema operacional precisa decidir:

- quem pode usar;
- quando pode usar;
- quanto pode usar;
- por quanto tempo;
- com quais permissões;
- o que acontece quando existe conflito.

Por isso, uma boa definição é:

> **Sistema operacional é o conjunto de componentes responsáveis por gerenciar os recursos do computador e fornecer serviços controlados para programas e usuários.**

---

# O que acontece depois do botão de energia?

No módulo anterior estudamos a inicialização física.

Agora vamos seguir o processo até a camada lógica.

De forma simplificada:

    Energia
       ↓
    Firmware
       ↓
    POST e inicialização de hardware
       ↓
    Seleção do dispositivo de boot
       ↓
    Bootloader / gerenciador de inicialização
       ↓
    Kernel
       ↓
    Drivers e subsistemas
       ↓
    Serviços
       ↓
    Sessão do usuário
       ↓
    Aplicações

Cada etapa pode falhar de maneira diferente.

---

# Firmware não é sistema operacional

BIOS e UEFI não são Windows, Linux ou macOS.

O firmware prepara a plataforma para que um sistema possa ser iniciado.

Ele pode:

- inicializar dispositivos;
- realizar verificações;
- oferecer configuração básica;
- localizar uma entrada de boot;
- iniciar um carregador.

Depois, a responsabilidade passa progressivamente para o sistema operacional.

---

# Bootloader

O bootloader é responsável por iniciar o carregamento do sistema.

Dependendo da plataforma, podemos encontrar componentes diferentes.

A função conceitual é semelhante:

- localizar o sistema;
- carregar informações necessárias;
- transferir controle para o kernel.

Se essa etapa falha, o computador pode:

- não encontrar sistema;
- entrar em recuperação;
- exibir erro de boot;
- retornar ao firmware.

Isso é diferente de um sistema que inicia e depois apresenta problemas.

---

# O kernel

O kernel é o núcleo do sistema operacional.

Ele executa funções fundamentais relacionadas a:

- processos;
- memória;
- interrupções;
- dispositivos;
- sistemas de arquivos;
- comunicação;
- segurança;
- temporização;
- escalonamento.

Aplicações comuns não deveriam manipular livremente essas estruturas.

O kernel cria uma fronteira de controle.

---

# Por que existe essa fronteira?

Imagine que cada aplicativo pudesse:

- escrever diretamente em qualquer posição da memória;
- desligar dispositivos;
- modificar o armazenamento sem controle;
- acessar arquivos de qualquer usuário;
- programar a CPU como quisesse.

Um único erro poderia destruir todo o sistema.

A separação entre níveis de privilégio reduz esse risco.

---

# Espaço do kernel e espaço do usuário

Uma simplificação útil é dividir o sistema em dois grandes ambientes.

## Espaço do kernel

Região altamente privilegiada.

Aqui ficam componentes responsáveis por operações críticas.

## Espaço do usuário

Onde executam a maior parte dos programas comuns.

Exemplos:

- navegador;
- editor;
- jogo;
- aplicativo de mensagens;
- calculadora;
- gerenciador de arquivos.

Um programa comum normalmente não acessa diretamente o hardware.

Ele solicita operações ao sistema.

---

# Chamadas de sistema

Como um programa pede algo ao kernel?

Por meio de mecanismos conhecidos como chamadas de sistema.

Exemplo conceitual:

    Programa quer ler um arquivo
            ↓
    Solicitação ao sistema operacional
            ↓
    Kernel verifica permissões
            ↓
    Sistema de arquivos localiza os dados
            ↓
    Driver acessa o dispositivo
            ↓
    Dados retornam
            ↓
    Programa recebe o conteúdo

O aplicativo não precisa controlar diretamente o SSD.

Isso é uma abstração.

---

# Uma abstração esconde complexidade

Quando um programa abre:

    C:\Usuarios\Aluno\Documento.txt

ou:

    /home/aluno/documento.txt

ele trabalha com um nome e um caminho.

Por baixo disso existem:

- estruturas do sistema de arquivos;
- metadados;
- blocos;
- permissões;
- cache;
- filas;
- controladores;
- driver;
- dispositivo físico.

Essa é uma das maiores funções do sistema operacional:

> **transformar hardware complexo em interfaces utilizáveis.**

---

# Processos

Quando um programa está em execução, o sistema cria estruturas para representá-lo.

Chamamos uma dessas estruturas de processo.

Um processo normalmente possui:

- identificador;
- memória virtual;
- recursos abertos;
- permissões;
- estado;
- prioridade;
- uma ou mais threads.

Um arquivo executável no disco não é a mesma coisa que um processo em execução.

---

# Programa e processo são coisas diferentes

Programa:

> conjunto de instruções armazenado.

Processo:

> instância em execução desse programa, acompanhada de estado e recursos.

Você pode abrir duas janelas do mesmo aplicativo e existir mais de um processo.

Também pode existir um programa instalado que não possui nenhum processo ativo.

---

# Threads

Uma thread é uma linha de execução dentro de um processo.

Um processo pode possuir:

- uma thread;
- várias threads.

Aplicações modernas frequentemente utilizam múltiplas threads para dividir tarefas.

Exemplos:

- interface gráfica;
- leitura de arquivos;
- rede;
- processamento;
- áudio;
- tarefas em segundo plano.

Threads do mesmo processo compartilham vários recursos.

---

# O escalonador

Existem mais tarefas querendo CPU do que núcleos disponíveis.

O sistema precisa decidir quais threads executam.

Essa função pertence ao escalonamento.

De forma simplificada:

    Thread A
    Thread B
    Thread C
    Thread D
       ↓
    Escalonador
       ↓
    Núcleos da CPU

O sistema alterna e distribui trabalho rapidamente.

Isso cria a sensação de que muitos programas estão funcionando simultaneamente.

---

# CPU em 100% é sempre defeito?

Não.

Pode significar:

- carga legítima;
- compilação;
- renderização;
- atualização;
- indexação;
- antivírus;
- processo travado;
- malware;
- loop de software.

O número sozinho não revela a causa.

Precisamos perguntar:

> Qual processo está consumindo CPU e em qual contexto?

---

# Estado de um processo

Um processo nem sempre está executando instruções naquele instante.

Ele pode estar:

- executando;
- pronto;
- esperando;
- bloqueado;
- suspenso;
- encerrado.

Imagine um programa esperando dados da rede.

Não faria sentido ocupar a CPU constantemente.

Ele pode aguardar um evento.

Quando os dados chegam, volta a ser elegível para execução.

---

# Processos zumbis e processos travados

Em diferentes sistemas existem situações nas quais um processo termina incorretamente ou permanece em estado inesperado.

Mas expressões como:

> “processo travado”

precisam ser investigadas.

Perguntas:

- ele consome CPU?
- responde a eventos?
- está esperando I/O?
- está bloqueado por outro recurso?
- deixou de atualizar a interface?
- possui erro registrado?

Interface congelada não significa necessariamente que todo o processo esteja morto.

---

# Memória virtual

Um processo não trabalha diretamente com a memória física como se pudesse escolher qualquer chip de RAM.

O sistema fornece um espaço de endereçamento virtual.

Isso permite:

- isolamento;
- organização;
- proteção;
- compartilhamento controlado;
- paginação;
- mapeamento de arquivos.

Cada processo pode enxergar um espaço de endereçamento que parece próprio.

---

# Por que isso é importante?

Imagine dois programas tentando utilizar a mesma posição física sem controle.

Um poderia corromper o outro.

A memória virtual ajuda o sistema a criar isolamento.

Uma representação simplificada:

    Processo A
    Espaço virtual A
          ↓
       Sistema
          ↓
        RAM

    Processo B
    Espaço virtual B
          ↓
       Sistema
          ↓
        RAM

Os endereços vistos pelos processos não precisam corresponder diretamente aos endereços físicos da memória.

---

# Paginação

Quando a pressão de memória aumenta, o sistema pode movimentar partes de memória para armazenamento secundário ou utilizar outros mecanismos de gerenciamento.

Isso pode aumentar atividade no SSD.

Por isso, no módulo anterior, vimos um computador com:

- RAM quase cheia;
- SSD muito ativo;
- lentidão.

O SSD parecia ser o culpado.

Mas estava respondendo ao comportamento do gerenciador de memória.

---

# Memória disponível não significa memória desperdiçada

Sistemas modernos utilizam memória livre para:

- cache;
- buffers;
- pré-carregamento;
- dados reutilizáveis.

Por isso:

> RAM ocupada não significa automaticamente problema.

Precisamos interpretar:

- memória disponível;
- compromisso;
- paginação;
- crescimento anormal;
- comportamento dos processos.

---

# Vazamento de memória

Um programa pode continuar reservando memória sem liberá-la adequadamente.

Ao longo do tempo:

    500 MB
       ↓
    1,2 GB
       ↓
    2,5 GB
       ↓
    5 GB
       ↓
    sistema começa a sofrer pressão

Isso pode indicar vazamento.

Mas crescimento de uso não prova vazamento.

Alguns programas utilizam cache propositalmente.

A investigação deve observar se:

- uso cresce continuamente;
- nunca reduz;
- coincide com degradação;
- é reproduzível.

---

# Drivers

Drivers permitem que o sistema operacional controle dispositivos específicos.

Exemplos:

- GPU;
- placa de rede;
- áudio;
- armazenamento;
- USB;
- impressora.

O driver funciona como um componente intermediário entre subsistemas do sistema e o hardware.

---

# Um driver pode causar sintomas muito diferentes

Problemas de driver podem produzir:

- dispositivo ausente;
- falha de inicialização;
- tela preta;
- áudio sem funcionar;
- desempenho baixo;
- tela azul;
- travamento;
- consumo elevado;
- erro de suspensão.

Por isso, “reinstalar todos os drivers” não é método de diagnóstico.

Precisamos primeiro identificar:

- qual dispositivo;
- qual versão;
- quando começou;
- qual evento;
- se existe relação temporal.

---

# Driver errado não significa sempre dispositivo quebrado

Se uma placa de rede desaparece do sistema, hipóteses incluem:

- driver;
- energia;
- dispositivo;
- firmware;
- configuração;
- barramento;
- serviço;
- falha física.

O sistema operacional adiciona novas camadas de possíveis causas.

---

# Sistemas de arquivos

O sistema operacional precisa organizar dados.

Sistemas de arquivos mantêm estruturas relacionadas a:

- nomes;
- diretórios;
- arquivos;
- metadados;
- permissões;
- timestamps;
- alocação;
- integridade.

Exemplos conhecidos incluem:

- NTFS;
- ext4;
- APFS;
- exFAT.

Cada um possui características próprias.

---

# Arquivo é mais que conteúdo

Um arquivo pode possuir:

- nome;
- tamanho;
- proprietário;
- permissões;
- datas;
- atributos;
- localização lógica;
- identificadores;
- dados internos.

Em investigação, metadados podem ser tão importantes quanto o conteúdo.

---

# Caminhos

Windows costuma utilizar caminhos como:

    C:\Users\Aluno\Documentos\relatorio.txt

Linux e outros sistemas Unix-like podem utilizar:

    /home/aluno/documentos/relatorio.txt

Os formatos são diferentes.

Mas o conceito é semelhante:

> localizar um objeto dentro de uma hierarquia.

---

# Permissões

Nem todo usuário deve acessar tudo.

O sistema controla:

- leitura;
- escrita;
- execução;
- propriedade;
- grupos;
- privilégios.

Um erro:

> “Acesso negado”

não significa necessariamente arquivo corrompido.

Pode significar que o sistema está aplicando uma regra de segurança.

---

# Administrador não significa liberdade absoluta

Mesmo uma conta administrativa pode enfrentar mecanismos adicionais.

Isso ocorre porque sistemas modernos tentam reduzir o impacto de:

- erros;
- malware;
- alterações acidentais.

Privilégio deve ser utilizado quando necessário, não como solução universal.

---

# Serviços

Muitas funções precisam continuar executando mesmo sem uma janela aberta.

Exemplos:

- rede;
- atualização;
- impressão;
- sincronização;
- banco de dados;
- servidor;
- autenticação.

No Windows, frequentemente falamos em serviços.

Em Linux e outros ambientes Unix-like, o termo daemon também é comum.

---

# Um serviço parado pode parecer defeito de hardware

Exemplo:

Usuário:

> “A impressora não funciona.”

Hipóteses físicas:

- cabo;
- impressora;
- USB.

Hipóteses lógicas:

- serviço de impressão;
- fila;
- driver;
- permissão;
- configuração.

Outro exemplo:

> “A internet sumiu.”

Pode envolver:

- cabo;
- Wi-Fi;
- placa;
- driver;
- serviço;
- configuração;
- endereço;
- rota;
- DNS.

Diagnóstico exige identificar a camada.

---

# Inicialização automática

Quando o usuário entra no sistema, muitos componentes podem iniciar automaticamente.

Exemplos:

- mensageiros;
- sincronizadores;
- utilitários;
- atualizadores;
- antivírus;
- launchers;
- serviços.

Se muitos elementos iniciarem ao mesmo tempo, podemos observar:

- uso elevado de CPU;
- pressão de RAM;
- atividade de armazenamento;
- atraso na interface.

Isso não significa que o hardware ficou subitamente mais lento.

---

# Kernel, serviços e aplicações

Uma visão simplificada:

    Hardware
       ↓
    Drivers
       ↓
    Kernel
       ↓
    Serviços do sistema
       ↓
    Sessão do usuário
       ↓
    Aplicações

Mas sistemas reais são mais complexos.

Existem:

- bibliotecas;
- APIs;
- componentes de segurança;
- processos auxiliares;
- IPC;
- caches;
- subsistemas.

A representação serve para construir raciocínio.

---

# IPC — comunicação entre processos

Programas frequentemente precisam conversar.

Isso pode ocorrer por mecanismos de comunicação entre processos.

Exemplos conceituais:

- pipes;
- sockets;
- memória compartilhada;
- filas;
- sinais;
- RPC.

Não precisamos dominar cada mecanismo agora.

O importante é compreender:

> um programa pode depender de outro processo ou serviço para funcionar.

---

# Dependências

Imagine:

    Aplicação
       ↓ depende de
    Serviço A
       ↓ depende de
    Serviço B
       ↓ depende de
    Driver

Se o Driver falha, o Serviço B pode falhar.

Então o Serviço A pode falhar.

Por fim, a aplicação pode exibir:

> “Não foi possível conectar.”

O erro aparece na aplicação.

A causa pode estar várias camadas abaixo.

---

# Essa é a nova investigação

No hardware, aprendemos a perguntar:

> Em qual subsistema físico a falha ocorre?

Agora perguntaremos:

> Em qual camada lógica o comportamento se desvia do esperado?

Podemos representar:

    Aplicação
       ↓
    Processo
       ↓
    Serviço
       ↓
    Permissão
       ↓
    Sistema de arquivos
       ↓
    Driver
       ↓
    Kernel
       ↓
    Hardware

---

# Logs: a memória do sistema

Sistemas operacionais registram eventos.

Logs podem informar:

- início de serviços;
- falhas;
- drivers;
- autenticação;
- erros de armazenamento;
- reinicializações;
- atualizações;
- rede;
- segurança.

No Windows, ferramentas importantes incluem:

- Visualizador de Eventos;
- Monitor de Confiabilidade.

No Linux, recursos comuns incluem:

- journalctl;
- dmesg;
- logs de serviços.

No macOS, existem ferramentas e subsistemas próprios de registro.

---

# Log não é diagnóstico automático

Imagine um registro:

> O serviço X foi encerrado inesperadamente.

Isso prova:

> o serviço terminou de maneira inesperada.

Não prova:

> por que terminou.

A causa pode ser:

- bug;
- dependência;
- memória;
- permissão;
- arquivo ausente;
- atualização;
- hardware.

Logs são evidência.

Precisam de contexto.

---

# Horário e sequência

Se uma falha ocorreu às 14:32, procure eventos próximos.

Podemos encontrar:

    14:31:58 — driver reiniciado
    14:32:01 — serviço perdeu comunicação
    14:32:03 — aplicativo encerrou
    14:32:05 — usuário viu erro

Agora existe uma sequência.

Essa ordem pode ajudar a diferenciar:

- causa;
- consequência.

---

# Dentro do Sistema — o que acontece ao abrir um programa?

Quando você clica em um aplicativo, ocorre muito mais do que “abrir uma janela”.

Simplificando:

    Usuário solicita abertura
            ↓
    Sistema localiza o executável
            ↓
    Verifica permissões
            ↓
    Cria estruturas do processo
            ↓
    Mapeia memória
            ↓
    Carrega bibliotecas
            ↓
    Cria thread inicial
            ↓
    Escalonador permite execução
            ↓
    Programa solicita arquivos, rede e dispositivos
            ↓
    Interface aparece

Cada etapa pode falhar.

---

# “O programa não abre” é um sintoma

Hipóteses:

- arquivo ausente;
- dependência ausente;
- permissão;
- configuração;
- biblioteca;
- antivírus;
- corrupção;
- incompatibilidade;
- serviço;
- conta do usuário;
- falta de recursos.

A solução não deve começar por:

> “Formata o computador.”

---

# Formatação apaga a cena lógica

Assim como trocar várias peças destrói evidências físicas, formatar cedo demais remove:

- logs;
- configurações;
- serviços;
- drivers;
- histórico;
- arquivos;
- estados.

Depois da formatação, talvez o problema desapareça.

Mas não aprendemos nada sobre a causa.

E, se a causa for hardware, o defeito pode retornar.

---

# Atualizar tudo também altera a cena

Atualização pode corrigir problemas.

Mas atualizar:

- sistema;
- drivers;
- firmware;
- aplicativos;

tudo ao mesmo tempo elimina rastreabilidade.

O método continua válido:

> **alterar uma variável por vez sempre que possível.**

---

# O caso retorna

Vamos voltar ao computador do início.

Hardware aparentemente saudável.

Depois do login:

- CPU sobe;
- programa não abre;
- rede desaparece;
- sistema demora para desligar.

Nossa investigação começa pelo estado lógico.

---

# Primeira coleta

No Gerenciador de Tarefas observamos:

- CPU em 65%;
- memória em 71%;
- SSD em uso moderado;
- processo desconhecido consumindo CPU;
- vários programas iniciados automaticamente.

Agora temos uma pista.

Mas não sabemos ainda se o processo é:

- legítimo;
- atualização;
- ferramenta do fabricante;
- aplicação travada;
- malware.

---

# Nome estranho não significa malware

Um erro comum é condenar processos apenas pelo nome.

Precisamos descobrir:

- caminho do executável;
- editor;
- assinatura;
- processo pai;
- momento de início;
- comportamento;
- rede;
- permissões;
- contexto.

A investigação de segurança virá mais adiante.

Por enquanto, o princípio é:

> **identifique antes de classificar.**

---

# O processo consome CPU apenas após o login

Esse detalhe sugere que o comportamento está associado à sessão do usuário ou a algo iniciado nesse momento.

Hipóteses:

- aplicativo de inicialização;
- tarefa agendada;
- sincronizador;
- serviço dependente da sessão.

Isso reduz o escopo.

---

# O programa com erro de permissão

O usuário tenta abrir uma pasta de trabalho.

Mensagem:

> Acesso negado.

Outro usuário administrativo consegue abrir.

Agora devemos investigar:

- proprietário;
- permissões;
- grupo;
- herança;
- perfil.

O SSD não é a hipótese principal.

---

# A interface de rede desaparece

No Gerenciador de Dispositivos, a placa ainda aparece.

Depois de alguns minutos, o driver registra erro e o dispositivo reinicializa.

Isso desloca a investigação para:

- driver;
- configuração de energia;
- dispositivo;
- barramento.

O hardware continua possível.

Mas agora temos evidência lógica concreta.

---

# O desligamento demora

Ao desligar, o sistema aguarda um serviço.

O log registra que ele não respondeu dentro do tempo esperado.

Agora o atraso no desligamento possui uma pista diferente do processo de CPU.

Novamente:

> um computador pode ter mais de um problema lógico.

---

# Construindo o mapa do caso

Podemos separar os sintomas:

    Lentidão
      → processo consumindo CPU

    Acesso negado
      → permissões

    Rede intermitente
      → driver/dispositivo/configuração

    Desligamento lento
      → serviço não respondendo

Se tratássemos tudo como:

> “Windows corrompido”

perderíamos precisão.

---

# Ferramentas básicas no Windows

Durante este módulo utilizaremos várias ferramentas nativas.

Entre elas:

## Gerenciador de Tarefas

Permite observar:

- processos;
- desempenho;
- inicialização;
- usuários;
- serviços.

## Monitor de Recursos

Permite aprofundar:

- CPU;
- memória;
- disco;
- rede.

## Monitor de Confiabilidade

Ajuda a observar:

- falhas;
- atualizações;
- eventos ao longo do tempo.

## Visualizador de Eventos

Permite examinar registros detalhados do sistema.

## Informações do Sistema

Ajuda a identificar:

- hardware;
- drivers;
- ambiente;
- configuração.

---

# Ferramentas básicas no Linux

Dependendo da distribuição, podemos encontrar recursos como:

- ps;
- top;
- htop;
- systemctl;
- journalctl;
- dmesg;
- free;
- df;
- mount.

Não precisamos memorizar comandos nesta primeira aula.

Nosso objetivo é entender a pergunta que cada ferramenta responde.

---

# Ferramentas no macOS

O macOS também oferece recursos de diagnóstico e monitoramento.

Exemplos:

- Monitor de Atividade;
- Console;
- Informações do Sistema;
- ferramentas de terminal.

Novamente, o importante é a metodologia.

---

# Uma ferramenta por pergunta

Pergunta:

> Qual processo está usando CPU?

Ferramenta adequada:

> monitor de processos.

Pergunta:

> Qual serviço falhou?

Ferramenta:

> gerenciador de serviços e logs.

Pergunta:

> O dispositivo possui erro de driver?

Ferramenta:

> gerenciador de dispositivos ou logs equivalentes.

Pergunta:

> O sistema está paginando?

Ferramenta:

> monitor de memória.

A ferramenta deve responder a uma hipótese.

---

# O que é um processo pai?

Processos podem iniciar outros processos.

Isso cria relações.

Exemplo:

    Explorer / shell
        ↓
    Aplicativo
        ↓
    Processo auxiliar

Ou:

    Serviço
        ↓
    Processo filho

Essa relação ajuda a entender origem e contexto.

---

# PID

Processos recebem identificadores.

No Windows e em sistemas Unix-like, frequentemente falamos em PID.

O PID ajuda a distinguir instâncias.

Dois processos com o mesmo nome podem possuir PIDs diferentes.

Isso é útil em:

- logs;
- monitoramento;
- scripts;
- diagnóstico.

---

# Prioridade

Sistemas podem atribuir prioridades diferentes.

Mas aumentar prioridade não é solução universal de desempenho.

Se um processo recebe preferência excessiva, outros podem sofrer.

O escalonador utiliza políticas mais complexas que uma simples fila.

---

# Afinidade

Alguns sistemas permitem limitar um processo a determinados processadores lógicos.

Isso pode ser útil em testes específicos.

Mas alterar afinidade sem motivo pode:

- reduzir desempenho;
- mascarar comportamento;
- criar resultados artificiais.

Use apenas quando a hipótese exigir.

---

# Context switch

Quando a CPU alterna entre threads, existe troca de contexto.

O sistema precisa salvar e restaurar informações.

Muitas trocas podem representar sobrecarga.

Mas um número alto não é automaticamente defeito.

Depende da carga.

---

# I/O

I/O significa entrada e saída.

Inclui operações com:

- armazenamento;
- rede;
- dispositivos.

Um processo pode parecer “travado” porque está esperando I/O.

Por isso, CPU baixa não significa que o programa esteja saudável.

---

# Gargalos lógicos

No módulo anterior estudamos gargalos físicos.

Agora veremos gargalos lógicos.

Exemplos:

- thread aguardando disco;
- fila de I/O;
- bloqueio de arquivo;
- serviço indisponível;
- DNS lento;
- permissão;
- memória virtual;
- processo dependente.

O hardware pode estar rápido e o sistema ainda responder lentamente.

---

# Deadlock — quando processos ficam esperando

Um conceito importante é o bloqueio mútuo.

Imagine:

    Processo A possui recurso 1
    e espera recurso 2

    Processo B possui recurso 2
    e espera recurso 1

Nenhum consegue avançar.

Isso é uma representação simplificada de deadlock.

Na prática, sistemas e aplicações utilizam mecanismos para evitar ou detectar situações desse tipo.

---

# Interface congelada não significa CPU parada

Uma aplicação pode ter:

- thread de interface bloqueada;
- outras threads funcionando.

Por isso:

> janela “não respondendo” não significa necessariamente que todo o computador travou.

Precisamos observar o processo e o sistema.

---

# Segurança começa no sistema operacional

Permissões, usuários e isolamento não são apenas detalhes administrativos.

São parte da segurança.

O sistema tenta controlar:

- quem executa;
- o que executa;
- quais arquivos acessa;
- quais dispositivos usa;
- quais privilégios possui.

Mais adiante, isso será essencial para investigação de incidentes.

---

# Usuários

Um sistema pode possuir diferentes contas.

Cada conta pode ter:

- identificador;
- perfil;
- arquivos;
- permissões;
- grupos;
- configurações.

Problema que ocorre apenas em um usuário pode indicar:

- perfil;
- configuração;
- permissão;
- aplicativo por usuário.

Se ocorre em todos, o escopo muda.

---

# Teste com outro usuário

Esse é um exemplo de teste de alto valor.

Sintoma:

> aplicativo falha apenas para um usuário.

Teste:

> abrir com outro perfil.

Se funciona:

- hardware perde força como hipótese;
- instalação global pode estar saudável;
- perfil e permissões ganham relevância.

---

# Serviços e dependências

Um serviço pode depender de outro.

Se o serviço de dependência falha, o problema se propaga.

Por isso:

> “serviço X não inicia”

não significa necessariamente que X esteja corrompido.

Precisamos verificar dependências.

---

# Inicialização do sistema

Depois que o kernel inicia, o sistema precisa levantar componentes.

A sequência varia entre plataformas.

Conceitualmente:

    Kernel
       ↓
    Subsistemas essenciais
       ↓
    Serviços
       ↓
    Login
       ↓
    Sessão
       ↓
    Aplicativos do usuário

Um problema em cada etapa produz sintomas diferentes.

---

# Lentidão antes do login versus depois do login

Essa diferença é valiosa.

## Lento antes do login

Investigue:

- boot;
- drivers;
- serviços essenciais;
- armazenamento;
- firmware;
- sistema.

## Lento depois do login

Investigue também:

- perfil;
- aplicativos de inicialização;
- sincronizadores;
- tarefas do usuário.

O tempo em que o sintoma aparece ajuda a localizar a camada.

---

# Suspensão e hibernação

Esses estados envolvem cooperação entre:

- sistema;
- drivers;
- firmware;
- hardware.

Problema que ocorre apenas ao despertar pode envolver:

- driver;
- energia;
- dispositivo;
- firmware;
- serviço.

Isso mostra como hardware e software se encontram.

---

# Reiniciar e desligar não são sempre equivalentes

Sistemas modernos podem utilizar diferentes mecanismos de inicialização rápida ou preservação de estado.

Em determinadas situações, reiniciar e desligar podem seguir caminhos diferentes.

Por isso, ao documentar um teste, registre exatamente:

- desligou?
- reiniciou?
- suspendeu?
- hibernou?

Não use “reiniciei” para qualquer ação.

---

# Atualizações

Atualizações podem modificar:

- kernel;
- drivers;
- serviços;
- bibliotecas;
- políticas;
- segurança.

Se um problema começa após atualização, a relação temporal é relevante.

Mas atualização recente não é prova de causa.

Precisamos comparar evidências.

---

# Mito ou Evidência?

## “Se o computador liga, o sistema operacional está bom.”

**Mito.**

Boot concluído não garante que todos os subsistemas estejam saudáveis.

---

## “CPU alta significa vírus.”

**Mito.**

CPU alta possui muitas causas possíveis.

---

## “Acesso negado significa arquivo corrompido.”

**Mito.**

Permissões podem explicar o comportamento.

---

## “Driver é apenas um programa que instala o dispositivo.”

**Incompleto.**

Drivers participam da comunicação entre o sistema e o hardware.

---

## “Se formatar e resolver, descobrimos a causa.”

**Mito.**

A formatação pode remover a evidência que permitiria explicar a falha.

---

## “Logs sempre mostram exatamente o que aconteceu.”

**Mito.**

Logs mostram eventos registrados de um ponto de vista específico.

Precisam ser interpretados.

---

# O que um perito observaria?

Uma investigação mais rigorosa pode considerar:

- horário preciso;
- usuário;
- processo;
- PID;
- caminho do executável;
- hash;
- assinatura;
- permissões;
- eventos de autenticação;
- mudanças de serviço;
- alterações de arquivo;
- conexões;
- sequência temporal.

Nem todo diagnóstico cotidiano exige esse nível.

Mas o raciocínio é o mesmo:

> preservar, correlacionar e explicar.

---

# 🔬 Laboratório — construindo o mapa do seu sistema

Nesta aula, não vamos alterar configurações sensíveis.

O objetivo é observar.

## Etapa 1 — Identificação

Registre:

- sistema operacional;
- edição/distribuição;
- versão;
- arquitetura;
- usuário atual.

## Etapa 2 — Processos

Abra o monitor de processos.

Registre:

- três processos com maior uso de CPU;
- três com maior uso de memória;
- quais você reconhece;
- quais precisam de investigação.

Não encerre processos desconhecidos apenas por não reconhecê-los.

## Etapa 3 — Memória

Observe:

- memória total;
- uso;
- disponível;
- paginação ou compromisso, se mostrado.

Pergunte:

> Existe pressão de memória?

## Etapa 4 — Armazenamento

Observe:

- processos com maior I/O;
- atividade do disco;
- comportamento enquanto abre um aplicativo.

## Etapa 5 — Serviços

Identifique alguns serviços ativos.

Escolha um e descubra:

- qual função exerce;
- se inicia automaticamente;
- se depende de outro componente.

Não desative serviços nesta atividade.

## Etapa 6 — Logs

Abra a ferramenta de logs do sistema.

Procure:

- eventos recentes;
- falhas de aplicativo;
- desligamentos;
- atualizações.

Escolha um evento e registre:

- horário;
- origem;
- descrição;
- impacto.

## Etapa 7 — Usuário

Observe:

- conta atual;
- tipo;
- pastas do perfil;
- permissões de um arquivo seu.

---

# Registro do laboratório

Use:

    Sistema:
    Versão:
    Arquitetura:

    Processo com maior CPU:
    Motivo provável:

    Processo com maior RAM:
    Motivo provável:

    Memória disponível:

    Serviço observado:
    Função:

    Evento de log:
    Horário:
    Origem:
    Descrição:

    Hipótese:
    Evidência:
    O que eu testaria a seguir:

O objetivo é começar a pensar em camada lógica.

---

# Estudo de caso 1 — Aplicativo não abre

Sintoma:

> aplicativo fecha imediatamente.

Evidências:

- hardware saudável;
- erro ocorre em um único usuário;
- outro usuário abre normalmente.

Hipóteses prioritárias:

- perfil;
- permissões;
- configuração por usuário;
- arquivos locais.

Formatar todo o computador seria uma intervenção desproporcional.

---

# Estudo de caso 2 — Internet desaparece

Sintoma:

> ícone de rede some depois de suspensão.

Evidências:

- cabo continua conectado;
- dispositivo reaparece após reiniciar;
- log mostra falha do driver ao despertar.

Hipóteses:

- driver;
- gestão de energia;
- firmware;
- dispositivo.

Trocar o roteador imediatamente não seria o primeiro passo.

---

# Estudo de caso 3 — CPU alta após login

Sintoma:

> sistema demora dez minutos para ficar utilizável.

Evidências:

- boot até login é rápido;
- depois do login, vários aplicativos iniciam;
- um sincronizador utiliza CPU e disco intensamente.

Hipótese:

> carga de inicialização do usuário.

O hardware pode estar normal.

---

# Estudo de caso 4 — Acesso negado

Sintoma:

> usuário não consegue editar arquivo.

Evidências:

- arquivo abre;
- outro usuário consegue editar;
- usuário atual possui apenas leitura.

Diagnóstico:

> comportamento compatível com permissões configuradas.

Não existe evidência de corrupção do SSD.

---

# Estudo de caso 5 — Desligamento lento

Sintoma:

> computador demora vários minutos para desligar.

Evidências:

- log mostra serviço aguardando encerramento;
- problema é reproduzível;
- finalização do serviço coincide com a conclusão do desligamento.

Hipótese forte:

> serviço não finaliza no tempo esperado.

Agora precisamos investigar o serviço.

---

# A nova matriz de investigação

No Módulo 2 utilizamos:

    Sintoma
      ↓
    Hardware
      ↓
    Teste
      ↓
    Evidência

Agora adicionamos:

    Sintoma
      ↓
    Camada lógica
      ↓
    Processo / serviço / arquivo / permissão / driver
      ↓
    Log
      ↓
    Teste controlado
      ↓
    Evidência

As duas matrizes se complementam.

---

# Hardware e sistema não são mundos separados

Um defeito físico pode gerar erro lógico.

Exemplo:

    SSD instável
       ↓
    erro de leitura
       ↓
    arquivo não carrega
       ↓
    serviço falha
       ↓
    aplicativo mostra erro

E um problema lógico pode fazer hardware parecer defeituoso.

Exemplo:

    driver incorreto
       ↓
    dispositivo mal configurado
       ↓
    desempenho baixo
       ↓
    usuário culpa a GPU

Diagnóstico profissional precisa atravessar camadas.

---

# 📁 Dossiê da Investigação — abertura do Módulo 3

A partir desta aula, adicione ao seu dossiê uma nova seção:

## Camada lógica

Para cada caso, registre:

- sintoma;
- usuário;
- momento da falha;
- processo relacionado;
- serviço relacionado;
- arquivo relacionado;
- permissão;
- driver;
- log;
- hipótese;
- teste;
- resultado.

Isso criará uma documentação cada vez mais próxima de uma análise profissional.

---

# O que muda daqui para frente?

No Módulo 2, podíamos olhar diretamente para:

- cabos;
- placas;
- ventoinhas;
- conectores.

No sistema operacional, muitas estruturas são invisíveis.

Precisaremos observar:

- tabelas;
- estados;
- logs;
- contadores;
- processos;
- relações.

O investigador passa a depender ainda mais de evidências registradas pelo próprio sistema.

---

# Conexão com a próxima aula

Nesta aula construímos o mapa geral.

Agora sabemos que aplicações executam como processos e que o sistema distribui recursos entre elas.

A próxima investigação vai aprofundar justamente esse ponto.

Vamos observar:

- processos;
- threads;
- prioridades;
- estados;
- consumo de CPU;
- memória;
- processos filhos;
- travamentos;
- aplicações “não respondendo”.

E responderemos:

> **Quando um programa trava, o que realmente está acontecendo dentro do sistema operacional?**

# Próxima aula — Processos e Threads: O Que Está Realmente Rodando no Seu Computador?
