# Módulo 3 — Sistemas Operacionais
## Investigação da Camada Lógica

# Aula 3 — Memória Virtual e Paginação: Por Que o Sistema Usa o SSD Mesmo Quando Você Não Pediu?

> **Pergunta da investigação**
>
> Se um computador ainda possui memória RAM instalada, por que o sistema operacional pode começar a usar o SSD, ficar lento e mostrar números de memória que parecem não fazer sentido?

---

# 📁 Dossiê da Investigação

## Caso nº 013 — O computador com 16 GB que “usa o SSD como RAM”

Um usuário relata:

> “Meu computador tem 16 GB de RAM, mas quando abro navegador, editor, Discord e uma máquina virtual, o SSD começa a trabalhar muito. O Windows diz que a memória está quase cheia. Então o sistema está usando o SSD como RAM?”

A frase parece simples.

Mas ela mistura vários conceitos diferentes:

- memória física;
- memória virtual;
- memória comprometida;
- working set;
- cache;
- paginação;
- arquivo de paginação;
- memória comprimida;
- falhas de página;
- memória compartilhada;
- memória privada.

Se tratarmos tudo como “RAM cheia”, podemos diagnosticar errado.

---

# O objetivo desta aula

Ao final desta investigação, você deverá ser capaz de:

- diferenciar memória física de memória virtual;
- entender por que cada processo enxerga seu próprio espaço de endereçamento;
- compreender páginas e mapeamentos;
- diferenciar memória residente de memória comprometida;
- interpretar o conceito de commit;
- entender o papel do arquivo de paginação no Windows;
- entender o papel de swap em Linux;
- compreender page faults sem tratá-los automaticamente como erro;
- diferenciar page fault leve e acesso que exige I/O;
- compreender working set;
- entender cache e memória standby;
- compreender por que RAM “ocupada” pode ser saudável;
- reconhecer pressão de memória;
- entender memória comprimida;
- interpretar sinais de paginação excessiva;
- reconhecer vazamento de memória;
- entender por que desativar o pagefile pode piorar o sistema;
- investigar lentidão sem culpar o SSD ou a RAM prematuramente.

---

# A memória que o programa enxerga não é a RAM diretamente

Na aula anterior, vimos que um processo possui um espaço de memória próprio.

Agora vamos aprofundar.

Um processo não recebe simplesmente:

> “este pedaço físico do pente de RAM é seu.”

Em vez disso, o sistema operacional cria uma visão virtual.

De forma simplificada:

    Processo
       ↓
    Endereços virtuais
       ↓
    Mapeamentos do sistema
       ↓
    Memória física / armazenamento / arquivos

O processo trabalha com endereços virtuais.

O sistema operacional e o hardware de gerenciamento de memória fazem a tradução necessária.

---

# Por que usar memória virtual?

Porque ela permite várias coisas importantes:

- isolamento entre processos;
- proteção;
- organização;
- compartilhamento controlado;
- mapeamento de arquivos;
- uso eficiente da memória física;
- abstração da localização real dos dados.

Sem isso, cada aplicação precisaria conhecer diretamente onde seus dados estão na RAM.

---

# Cada processo enxerga seu próprio espaço

Imagine dois processos.

    Processo A
    endereço virtual 0x1000
          ↓
    página física X

    Processo B
    endereço virtual 0x1000
          ↓
    página física Y

Os dois podem usar o mesmo endereço virtual.

Mas os dados reais podem estar em lugares físicos diferentes.

Isso é uma das bases do isolamento moderno.

---

# A CPU participa dessa tradução

Processadores modernos possuem mecanismos de gerenciamento de memória.

Um componente importante é a MMU — Memory Management Unit.

Ela ajuda a traduzir:

    endereço virtual
        ↓
    endereço físico

A tradução utiliza estruturas mantidas pelo sistema operacional.

Essas estruturas são geralmente organizadas em tabelas de páginas.

---

# Páginas

A memória virtual costuma ser gerenciada em blocos chamados páginas.

Em muitos sistemas, um tamanho comum é 4 KiB.

Mas isso não deve ser tratado como valor universal.

Podem existir:

- páginas padrão;
- páginas grandes;
- tamanhos diferentes conforme arquitetura e sistema.

O conceito importante é:

> o sistema administra memória em unidades discretas, não byte a byte.

---

# Page table

O sistema precisa registrar como páginas virtuais se relacionam com recursos reais.

Conceitualmente:

    Página virtual A
        → página física 42

    Página virtual B
        → página física 91

    Página virtual C
        → ainda não residente

    Página virtual D
        → mapeada para arquivo

Essas relações permitem que o processo utilize um espaço lógico contínuo mesmo quando os dados físicos estão espalhados.

---

# TLB — Translation Lookaside Buffer

Traduzir endereços consultando tabelas o tempo todo seria caro.

Processadores usam caches especializados para traduções recentes.

Um deles é a TLB.

Ela guarda traduções utilizadas recentemente.

Isso reduz o custo de muitos acessos.

---

# A memória virtual é maior que a RAM?

Frequentemente sim.

Mas isso precisa ser entendido corretamente.

Um processo pode possuir um espaço de endereçamento virtual enorme sem ocupar toda essa quantidade de RAM.

Reservar espaço de endereço não significa necessariamente consumir memória física imediatamente.

---

# Reservar não é o mesmo que comprometer

Em sistemas como Windows, existem conceitos diferentes.

## Reserva

O sistema separa uma faixa do espaço de endereçamento virtual.

Ainda pode não existir armazenamento comprometido para todas essas páginas.

## Commit

O sistema assume a obrigação de fornecer armazenamento para aquelas páginas caso sejam necessárias.

Isso é mais importante para capacidade real.

---

# Commit não é “RAM usada”

Esse é um dos pontos que mais confundem.

No Windows, a memória comprometida representa memória virtual privada que precisa de suporte de armazenamento pelo sistema.

Em termos práticos, o limite de commit está relacionado principalmente a:

- RAM;
- arquivos de paginação;
- reservas internas do sistema.

Por isso, você pode ver:

    RAM usada: 11 GB

mas:

    Commit: 18 GB / 28 GB

Os números medem coisas diferentes.

---

# Commit charge

O valor de commit atual representa quanto o sistema prometeu suportar.

O limite representa a capacidade total disponível para esse compromisso.

Se o commit se aproxima do limite, o sistema entra em situação crítica.

Isso pode ocorrer mesmo quando a leitura superficial de “RAM em uso” parece não explicar tudo.

---

# Por que o pagefile existe?

No Windows, o arquivo de paginação é um mecanismo de suporte à memória virtual.

Ele pode armazenar páginas que não precisam permanecer residentes na RAM naquele momento.

Mas sua função não é apenas:

> “substituir RAM quando ela acaba.”

Ele participa da política de memória do sistema.

---

# Desativar o pagefile não transforma o computador em máquina “mais rápida”

Esse é um mito comum.

Sem pagefile:

- o limite de commit pode cair;
- algumas cargas podem falhar antes;
- dumps de memória podem ser afetados;
- aplicativos podem receber falha de alocação.

O sistema perde flexibilidade.

Ter muita RAM não significa automaticamente que o arquivo de paginação é inútil.

---

# “Mas SSD é muito mais lento que RAM”

Correto.

RAM possui latência e largura de banda muito superiores.

Se o sistema precisa buscar páginas constantemente no armazenamento, o impacto pode ser grande.

O problema não é a existência do pagefile.

O problema é:

> **pressão de memória acompanhada de atividade de paginação suficiente para prejudicar a carga real.**

---

# Resident versus não residente

Uma página pode fazer parte do espaço virtual de um processo sem estar atualmente na RAM.

Quando está na RAM, dizemos que está residente.

Um processo pode ter:

- grande espaço virtual;
- parte residente;
- parte não residente;
- páginas compartilhadas;
- páginas mapeadas.

---

# Working set

No Windows, um conceito importante é o working set.

Ele representa, de forma simplificada, o conjunto de páginas de um processo que está residente na memória física naquele momento.

Isso muda com o tempo.

O sistema pode:

- adicionar páginas;
- remover páginas;
- compartilhar páginas.

Por isso, o valor de memória de um processo não é uma verdade única.

---

# “Quanto de RAM este programa usa?”

Essa pergunta parece simples.

Mas pode significar:

- working set;
- private working set;
- commit privado;
- memória compartilhada;
- memória virtual reservada.

Ferramentas diferentes podem mostrar números diferentes porque medem coisas diferentes.

---

# Memória privada

Memória privada é aquela associada especificamente ao processo.

Ela não pode simplesmente ser contabilizada como compartilhada com vários processos.

Em uma investigação de vazamento, esse valor pode ser muito útil.

---

# Memória compartilhada

Bibliotecas e outros recursos podem ser compartilhados entre processos.

Se dez processos utilizam a mesma biblioteca, não devemos imaginar necessariamente dez cópias físicas completas na RAM.

O sistema pode compartilhar páginas.

---

# Mapear arquivo em memória

Sistemas operacionais podem mapear arquivos no espaço de endereçamento.

Isso permite que aplicações tratem partes de arquivos como regiões de memória.

O sistema cuida de carregar páginas conforme necessário.

Esse mecanismo é muito usado.

---

# Page fault não significa falha física

O termo “fault” assusta.

Mas uma page fault pode ser parte normal do funcionamento do sistema.

Ela ocorre quando o processo acessa uma página que exige intervenção do sistema operacional.

---

# Falha de página leve

Uma page fault pode ser resolvida sem ler dados do armazenamento físico.

Exemplos:

- página já está em memória;
- página compartilhada já existe;
- mapeamento pode ser atualizado rapidamente.

Esses eventos são comuns.

---

# Falha que exige I/O

Em outros casos, o sistema precisa buscar dados.

Pode precisar ler:

- arquivo;
- executável;
- biblioteca;
- pagefile;
- swap.

Isso é muito mais caro.

O acesso ao armazenamento possui latência muito maior que o acesso à RAM.

---

# Hard fault no Windows

Ferramentas do Windows podem usar o termo hard fault.

Ele não significa:

> defeito físico no hardware.

Significa que a página necessária precisou ser recuperada de armazenamento em vez de simplesmente resolvida em memória.

Essa distinção é essencial.

---

# Por que o SSD trabalha ao abrir um programa?

Porque o sistema precisa carregar:

- executável;
- bibliotecas;
- arquivos;
- dados.

Isso não é necessariamente paginação por falta de RAM.

Disco ativo não significa automaticamente:

> “Windows está usando SSD como RAM.”

---

# O SSD pode trabalhar por vários motivos

Exemplos:

- leitura de aplicativo;
- gravação de arquivo;
- cache;
- atualização;
- antivírus;
- indexação;
- sincronização;
- pagefile;
- logs.

A investigação precisa identificar:

> qual processo e qual tipo de I/O?

---

# Cache

RAM não utilizada pode ser aproveitada para acelerar o sistema.

O sistema pode manter dados recentemente acessados em cache.

Isso é bom.

Quando um aplicativo precisa de memória, parte desse cache pode ser reaproveitada.

---

# RAM vazia não é objetivo

Se o computador possui 32 GB e apenas 5 GB estão realmente necessários para aplicações, deixar 27 GB completamente inúteis seria desperdício.

O sistema pode usar parte desse espaço para:

- cache;
- standby;
- pré-carregamento;
- estruturas internas.

A memória pode ser “ocupada” e ainda estar prontamente reutilizável.

---

# Memória disponível

Um número muito mais útil que “livre” isoladamente é a memória disponível.

Ela pode incluir memória:

- livre;
- reutilizável rapidamente;
- em standby.

Por isso:

> pouca memória livre não significa necessariamente falta de memória.

---

# Standby

No Windows, páginas podem permanecer em uma lista de standby.

Elas ainda contêm dados potencialmente úteis.

Mas podem ser reaproveitadas se outra aplicação precisar.

Isso é eficiente.

---

# Cache do Linux

Linux também utiliza agressivamente RAM para cache.

Comandos podem mostrar:

- free;
- used;
- buff/cache;
- available.

Iniciantes frequentemente olham apenas “used” e concluem:

> “Linux consumiu toda a RAM.”

Mas boa parte pode ser cache recuperável.

---

# free no Linux

Um comando comum:

    free -h

Pode exibir:

- total;
- used;
- free;
- shared;
- buff/cache;
- available.

O campo available é muito importante para interpretar capacidade real de atender novas cargas.

---

# Swap no Linux

Linux pode utilizar swap.

Swap pode existir em:

- partição;
- arquivo;
- outros mecanismos suportados.

Assim como o pagefile, swap não deve ser entendido apenas como:

> RAM extra lenta.

Ele faz parte da política de gerenciamento de memória.

---

# swappiness

Linux possui parâmetros que influenciam a tendência de utilização de swap.

Um conceito conhecido é swappiness.

Mas alterar esse valor por receita pronta pode ser um erro.

O comportamento ideal depende de:

- carga;
- servidor;
- desktop;
- memória;
- armazenamento;
- aplicações.

---

# OOM — Out Of Memory

Quando o sistema não consegue satisfazer demandas de memória, pode ocorrer situação de falta de memória.

No Linux, mecanismos como o OOM killer podem encerrar processos para preservar o sistema.

Isso é diferente de:

> “o sistema ficou um pouco lento.”

É uma situação de pressão extrema.

---

# Pressão de memória

O conceito central desta aula é pressão.

Não existe um único número mágico.

Devemos observar um conjunto:

- memória disponível;
- commit;
- page faults;
- atividade de armazenamento;
- latência;
- swap/pagefile;
- crescimento de processos;
- responsividade.

---

# Um cenário saudável

    RAM total.............16 GB
    Em uso................10 GB
    Disponível............6 GB
    Commit................12 / 28 GB
    Pagefile I/O..........baixo
    Sistema...............responsivo

Mesmo com 10 GB usados, não há evidência de problema.

---

# Um cenário de pressão

    RAM total.............16 GB
    Em uso................15,5 GB
    Disponível............300 MB
    Commit................24 / 28 GB
    Hard faults...........altos e persistentes
    SSD...................muito ativo
    Sistema...............lento

Agora o conjunto sugere pressão séria.

---

# Um cenário de vazamento

Imagine um serviço:

    08:00 → 500 MB
    10:00 → 1,4 GB
    12:00 → 3,2 GB
    14:00 → 5,7 GB
    16:00 → 8,9 GB

Sem carga proporcional.

Sem liberação.

Reiniciar o serviço faz voltar para 500 MB.

Isso é compatível com hipótese de vazamento.

Ainda precisamos investigar.

---

# Vazamento de memória

Um vazamento ocorre quando um programa mantém memória que deveria ter sido liberada.

Consequências possíveis:

- crescimento progressivo;
- pressão;
- paginação;
- lentidão;
- falha de alocação;
- crash.

---

# Mas cache pode parecer vazamento

Um programa pode intencionalmente manter dados em cache.

Perguntas:

- memória cresce até estabilizar?
- cai quando necessário?
- responde à pressão?
- está associada a dados ativos?
- crescimento é ilimitado?

Não rotule cedo.

---

# Memória comprimida

Sistemas modernos podem comprimir páginas em memória.

A ideia é:

> comprimir dados pouco ativos em vez de enviá-los imediatamente para armazenamento.

Isso troca parte do custo de I/O por:

- CPU;
- compressão;
- descompressão.

---

# No Windows

O Windows utiliza mecanismos de compressão de memória.

Isso pode aparecer em ferramentas de monitoramento.

A memória comprimida não é “memória falsa”.

São dados reais mantidos em forma comprimida para economizar espaço físico.

---

# Em Linux

Linux pode utilizar tecnologias como zswap ou zram, dependendo da configuração.

Elas também exploram compressão.

Não são obrigatórias em todas as distribuições.

---

# Por que compressão pode ajudar?

Considere:

    1 GB de páginas
       ↓
    comprimidas para 500 MB

Isso permite manter dados em RAM.

Evita parte do acesso ao SSD.

Mas consome CPU.

É uma troca.

---

# Quando RAM começa a faltar

O sistema pode adotar várias estratégias.

De forma conceitual:

    reduzir caches
       ↓
    remover páginas pouco usadas
       ↓
    comprimir
       ↓
    paginar
       ↓
    negar novas alocações em situação extrema

A ordem e detalhes variam.

---

# Não existe “RAM cheia” como um único evento

A situação depende de:

- tipo das páginas;
- possibilidade de descarte;
- memória compartilhada;
- cache;
- commit;
- armazenamento;
- política do sistema.

Dois computadores com 95% de RAM podem ter comportamentos completamente diferentes.

---

# Memória anônima e memória baseada em arquivo

Em sistemas Unix-like, uma distinção útil é:

## File-backed

Páginas derivadas de arquivos.

Se forem limpas, podem ser descartadas e lidas novamente do arquivo.

## Anonymous

Memória que não possui um arquivo original simples para ser recarregado.

Pode precisar de swap se for removida da RAM.

Isso ajuda a entender por que algumas páginas são mais fáceis de descartar que outras.

---

# Dirty pages

Uma página “dirty” contém alterações ainda não gravadas no armazenamento correspondente.

Antes de descartá-la, o sistema pode precisar escrever.

Isso introduz I/O.

---

# Flush

O sistema periodicamente grava dados pendentes.

Picos de disco podem estar associados a:

- flush;
- cache;
- banco de dados;
- arquivos modificados.

Não atribua todo I/O ao pagefile.

---

# Copy-on-write

Um conceito importante em sistemas modernos é copy-on-write.

Dois contextos podem compartilhar páginas enquanto ninguém altera.

Quando um deles escreve, o sistema cria uma cópia privada.

Isso melhora eficiência.

---

# Fork no Linux

Em sistemas Unix-like, fork cria um novo processo baseado no atual.

Com copy-on-write, não é necessário duplicar imediatamente toda a memória física.

As páginas podem ser compartilhadas até uma escrita ocorrer.

---

# Memória virtual e segurança

Isolamento de memória impede que um processo comum leia ou altere livremente a memória de outro.

Isso ajuda a proteger:

- estabilidade;
- confidencialidade;
- integridade.

Privilégios especiais ainda podem permitir inspeção em cenários controlados.

---

# ASLR

Address Space Layout Randomization altera a localização de certas regiões no espaço de endereçamento.

Isso dificulta alguns tipos de exploração.

Ele mostra que memória virtual também participa da segurança.

---

# NX / DEP

Sistemas modernos podem marcar regiões como não executáveis.

Isso ajuda a impedir execução de código onde deveria existir apenas dado.

No Windows, isso se relaciona ao DEP.

Em outras plataformas existem mecanismos equivalentes.

---

# 32 bits versus 64 bits

Arquiteturas de 32 bits possuem espaço de endereçamento muito mais limitado.

Aplicações 32-bit podem encontrar limites mesmo em máquinas com muita RAM.

Arquiteturas 64-bit ampliam enormemente o espaço possível.

---

# 4 GB em 32 bits

Um espaço de 32 bits possui:

    2³² = 4.294.967.296 endereços

Se cada endereço representa um byte:

    aproximadamente 4 GiB

Mas o espaço disponível a um processo pode ser menor dependendo da arquitetura e configuração.

---

# Um aplicativo 32-bit pode ficar sem espaço virtual antes da RAM física acabar

Isso é importante.

Computador:

    32 GB de RAM

Aplicação:

    32-bit

Ela pode encontrar limite de espaço de endereçamento mesmo com muita RAM livre.

O problema não é capacidade física total.

---

# Fragmentação virtual

Mesmo havendo capacidade total, um programa pode precisar de uma região contígua de endereço virtual.

Dependendo do contexto, fragmentação pode impedir uma alocação específica.

Esse problema foi mais relevante em aplicações 32-bit.

---

# Memória física também possui limitações

O sistema precisa reservar regiões e estruturas internas.

Nem toda RAM instalada aparece necessariamente como memória disponível ao usuário.

Firmware, hardware e arquitetura podem influenciar.

---

# GPU integrada e memória compartilhada

GPUs integradas podem utilizar memória do sistema.

Isso pode reduzir memória disponível para outras cargas.

Mas a contabilização varia conforme plataforma.

Não conclua:

> “a RAM sumiu.”

Observe a reserva real.

---

# Máquinas virtuais

Uma VM pode reservar grande quantidade de memória.

Exemplo:

    Host...............16 GB
    VM.................8 GB
    Navegador..........3 GB
    Editor.............2 GB
    Sistema............restante

Agora a margem fica pequena.

O problema pode surgir rapidamente.

---

# Containers

Containers não funcionam exatamente como VMs.

Mas podem ter limites de memória.

Em Linux, cgroups podem controlar recursos.

Um processo dentro de container pode sofrer pressão mesmo quando o host ainda possui memória.

---

# Browser moderno

Navegadores utilizam muitos processos.

Cada aba, extensão e componente pode consumir memória.

O total pode ser grande.

Mas isso também melhora isolamento.

Não existe um único “processo navegador” representando tudo.

---

# O caso retorna

Nosso usuário possui:

- 16 GB de RAM;
- navegador;
- editor;
- Discord;
- máquina virtual.

Observação:

    RAM em uso...........15,4 GB
    Disponível...........420 MB
    Commit...............25 / 30 GB
    SSD..................alto uso
    Hard faults..........persistentes

O sistema está lento.

Agora temos evidências de pressão real.

---

# Primeira hipótese

> A carga ativa excede confortavelmente a memória física disponível e o sistema precisa movimentar páginas com frequência.

Essa hipótese prevê:

- baixa memória disponível;
- hard faults;
- I/O;
- latência;
- melhora ao reduzir carga.

---

# Teste controlado

Fechamos a máquina virtual.

Resultado:

    RAM em uso...........9,8 GB
    Disponível...........5,9 GB
    Commit...............15 / 30 GB
    Hard faults..........caem drasticamente
    SSD..................reduz atividade
    Sistema..............responsivo

A hipótese ganha força.

---

# Mas fechar a VM não prova que a VM está defeituosa

A máquina virtual pode estar funcionando perfeitamente.

Ela apenas consome um recurso real.

O problema é capacidade versus carga.

---

# Soluções possíveis

Dependendo da necessidade:

- reduzir aplicativos simultâneos;
- reduzir memória atribuída à VM;
- expandir RAM;
- revisar processos desnecessários;
- corrigir vazamento, se existir.

A solução deve responder à causa.

---

# “Compre mais RAM” não é sempre resposta

Antes de recomendar expansão, pergunte:

- carga é legítima?
- existe vazamento?
- programa anormal?
- VM superdimensionada?
- pagefile configurado?
- aplicação 32-bit?

Mais RAM não corrige todos os problemas de memória.

---

# Pagefile fixo é melhor?

Não existe regra universal.

Deixar o sistema gerenciar é apropriado para muitos ambientes.

Definir tamanho manual pode ser necessário em cenários específicos.

Mas receitas como:

> “sempre use 1,5 × a RAM”

não devem ser tratadas como verdade moderna universal.

---

# Colocar pagefile em SSD estraga o SSD?

SSDs possuem desgaste por escrita.

Mas isso não significa que o pagefile deva ser evitado.

SSDs modernos são projetados para carga de escrita significativa.

Em uso normal, desativar mecanismos do sistema por medo genérico de desgaste pode causar mais problemas que benefícios.

Avalie:

- workload;
- TBW;
- monitoramento;
- necessidade real.

---

# Pagefile em HDD

Se paginação pesada ocorrer em HDD, o impacto pode ser muito maior devido à latência e acesso aleatório.

SSD reduz a penalidade.

Mas ainda é muito mais lento que RAM.

---

# O que causa thrashing?

Thrashing ocorre quando o sistema gasta grande parte do tempo movendo páginas e atendendo faltas de memória em vez de realizar trabalho útil.

Sintomas:

- sistema extremamente lento;
- armazenamento muito ativo;
- baixa memória disponível;
- aplicativos demorando para alternar;
- hard faults constantes.

---

# Thrashing não é apenas “disco em 100%”

Disco em 100% pode ocorrer por:

- cópia;
- atualização;
- antivírus;
- indexação;
- banco de dados.

Para caracterizar thrashing, precisamos relacionar:

- memória;
- paginação;
- I/O;
- latência.

---

# Memória e latência

A hierarquia de memória existe porque cada nível possui custo diferente.

Conceitualmente:

    Registradores
       ↓
    Cache CPU
       ↓
    RAM
       ↓
    SSD
       ↓
    armazenamento remoto

Quanto mais longe da CPU, maior tende a ser a latência.

Por isso, page faults que exigem armazenamento são caros.

---

# Localidade

Programas tendem a reutilizar dados próximos no tempo ou espaço.

Chamamos isso de localidade.

## Localidade temporal

Dados usados recentemente podem ser usados novamente.

## Localidade espacial

Dados próximos aos usados podem ser acessados em seguida.

Caches e páginas exploram esse comportamento.

---

# Working set como conjunto ativo

Podemos imaginar o working set como:

> páginas que um processo precisa ativamente em um intervalo.

Se o working set de todas as cargas cabe confortavelmente na RAM:

- sistema tende a permanecer responsivo.

Se não cabe:

- aumenta disputa;
- páginas são removidas;
- precisam retornar;
- paginação cresce.

---

# Memória disponível e folga

Para uma máquina interativa, não queremos operar permanentemente no limite.

Folga permite absorver:

- picos;
- novas abas;
- atualizações;
- tarefas temporárias.

Dimensionamento deve considerar comportamento real.

---

# Ferramentas no Windows

## Gerenciador de Tarefas

Na aba de desempenho, podemos observar:

- Em uso;
- Disponível;
- Comprometida;
- Em cache;
- pools;
- velocidade da RAM.

Esses números ajudam a criar o panorama.

---

# Monitor de Recursos

Pode mostrar:

- hard faults;
- memória física;
- processos;
- commit;
- working set.

É útil para relacionar processo e pressão.

---

# RAMMap

A ferramenta RAMMap, da Sysinternals, permite análise mais profunda da utilização da memória física.

Pode ajudar a entender:

- listas;
- arquivos;
- processos;
- standby;
- driver allocations.

É uma ferramenta avançada.

---

# Process Explorer

Pode mostrar métricas relacionadas a memória por processo.

Útil para investigar crescimento e commit.

---

# PowerShell

Para observação inicial:

    Get-Process | Sort-Object WorkingSet64 -Descending | Select-Object -First 10 ProcessName, Id, WorkingSet64

Esse comando lista processos com working set elevado.

Mas lembre-se:

> working set não é o único número de memória relevante.

---

# Ferramentas no Linux

## free

    free -h

Ajuda a observar memória geral.

---

# vmstat

    vmstat 1

Pode mostrar atividade relacionada a:

- processos;
- memória;
- swap;
- I/O;
- CPU.

É uma ferramenta muito útil.

---

# top e htop

Permitem observar:

- RES;
- VIRT;
- SHR;
- CPU;
- processos.

Mas os campos precisam ser entendidos.

---

# VIRT

Em ferramentas Linux, VIRT pode ser enorme.

Isso não significa que toda aquela memória está fisicamente na RAM.

Inclui espaço virtual mapeado.

---

# RES

RES representa memória residente.

É mais próximo do quanto está fisicamente presente naquele momento.

---

# SHR

SHR indica uma estimativa de memória compartilhável/compartilhada.

Não some valores de vários processos ingenuamente.

Você pode contar a mesma memória mais de uma vez.

---

# smem

Ferramentas como smem podem apresentar métricas como PSS.

PSS distribui páginas compartilhadas proporcionalmente entre processos.

Pode fornecer uma visão mais justa do consumo.

Nem sempre está instalada.

---

# PSS — Proportional Set Size

Imagine uma página de 12 MB compartilhada por 3 processos.

Em PSS, cada processo poderia receber aproximadamente:

    4 MB

Isso evita contabilizar 12 MB para cada um.

---

# USS

Unique Set Size tenta representar memória exclusiva do processo.

É útil em certas análises.

Novamente, nenhuma métrica isolada responde tudo.

---

# MacOS

O Monitor de Atividade apresenta conceitos como:

- pressão da memória;
- memória física;
- memória usada;
- arquivos em cache;
- swap utilizado.

A métrica de pressão é particularmente útil para interpretar o estado do sistema.

---

# Pressão é mais importante que percentual isolado

Essa ideia vale para todas as plataformas.

Perguntar apenas:

> “Quantos por cento de RAM está usando?”

é insuficiente.

Pergunte:

- há memória disponível?
- há paginação?
- há latência?
- há crescimento anormal?
- há swap?
- o sistema responde bem?

---

# Mito ou Evidência?

## “RAM usada deve ser sempre a menor possível.”

**Mito.**

Cache e uso eficiente são desejáveis.

---

## “Page fault significa defeito.”

**Mito.**

Muitas page faults são normais.

---

## “Hard fault significa SSD quebrado.”

**Mito.**

Significa necessidade de recuperar página de armazenamento.

---

## “Se existe pagefile, o computador está usando SSD como RAM o tempo todo.”

**Mito.**

A existência do arquivo não prova atividade intensa.

---

## “Desativar pagefile sempre melhora desempenho.”

**Mito.**

Pode reduzir o limite de commit e prejudicar estabilidade.

---

## “Mais RAM sempre corrige lentidão.”

**Mito.**

Se o gargalo for CPU, I/O, rede ou software, o ganho pode ser mínimo.

---

## “Linux usa toda a RAM porque está mal otimizado.”

**Mito.**

Grande parte pode estar sendo usada como cache reutilizável.

---

# 🔬 Laboratório — investigando pressão de memória

O laboratório será apenas de observação e carga segura.

Não altere pagefile ou swap nesta etapa.

---

# Etapa 1 — Baseline

Reinicie apenas se isso fizer parte da sua rotina de teste.

Espere o sistema estabilizar.

Registre:

    RAM total:
    Em uso:
    Disponível:
    Cache:
    Commit:
    Swap/pagefile em uso:

---

# Etapa 2 — Identifique os maiores consumidores

No Windows:

- Gerenciador de Tarefas;
- Monitor de Recursos.

No Linux:

- top;
- htop;
- ps.

Registre cinco processos.

---

# Etapa 3 — Abra uma carga conhecida

Exemplos:

- várias abas;
- editor;
- IDE;
- VM;
- arquivo grande.

Evite criar situação extrema.

Observe:

- memória disponível;
- commit;
- I/O;
- responsividade.

---

# Etapa 4 — Compare antes e depois

Tabela:

| Métrica | Antes | Depois |
|---|---:|---:|
| RAM em uso | | |
| Disponível | | |
| Commit | | |
| Swap/pagefile | | |
| Hard faults | | |
| SSD | | |

---

# Etapa 5 — Feche uma carga grande

Observe por alguns minutos.

Pergunte:

- memória cai imediatamente?
- cache permanece?
- disponível aumenta?
- I/O reduz?

Não espere que todos os números retornem exatamente ao baseline.

---

# Etapa 6 — Procure crescimento contínuo

Escolha um processo.

Observe por 10 a 15 minutos.

Registre:

    0 min:
    5 min:
    10 min:
    15 min:

Pergunte:

> o crescimento corresponde à atividade?

---

# Etapa 7 — Windows

No Gerenciador de Tarefas, observe:

- Em uso;
- Disponível;
- Comprometida;
- Em cache.

Anote os valores.

---

# Etapa 8 — Linux

Execute:

    free -h

Depois:

    vmstat 1

Observe alguns ciclos.

Não encerre processos.

---

# 📁 Registro do laboratório

Adicione ao Dossiê:

    Sistema operacional:
    RAM física:
    Memória disponível:
    Commit:
    Swap/pagefile:
    Processo de maior consumo:
    Working set/RES:
    Crescimento observado:
    Atividade de armazenamento:
    Sintoma:
    Hipótese:
    Teste:
    Resultado:
    Conclusão:

---

# Estudo de caso 1 — RAM em 85%, sistema rápido

Evidências:

- 32 GB instalados;
- 27 GB em uso/cache;
- 5 GB disponíveis;
- pouca paginação;
- sistema responsivo.

Conclusão:

> não há evidência de problema apenas pelo percentual.

---

# Estudo de caso 2 — RAM em 95%, SSD em 100%

Evidências:

- disponível abaixo de 200 MB;
- hard faults persistentes;
- commit próximo do limite;
- alternar janelas demora;
- SSD com I/O intenso.

Conclusão:

> forte evidência de pressão de memória com paginação relevante.

---

# Estudo de caso 3 — Processo usa 8 GB e está saudável

Aplicação:

- edição de vídeo;
- projeto grande;
- uso estável;
- memória disponível ainda adequada.

Conclusão:

> consumo alto pode ser legítimo.

---

# Estudo de caso 4 — Serviço cresce sem parar

Evidências:

- começa com 300 MB;
- sobe 200 MB por hora;
- não libera;
- commit aumenta;
- após reiniciar o serviço volta ao início.

Hipótese forte:

> vazamento ou retenção anormal.

---

# Estudo de caso 5 — “SSD lento”

Usuário relata:

> “Quando abro a VM, o SSD fica em 100%.”

Evidências:

- RAM quase cheia;
- hard faults aumentam;
- pagefile ativo;
- ao fechar VM, disco normaliza.

Conclusão:

> SSD está respondendo à pressão de memória.

Não há evidência de defeito físico no SSD.

---

# Estudo de caso 6 — Aplicativo 32-bit falha com muita RAM livre

Evidências:

- host possui 64 GB;
- processo é 32-bit;
- erro ocorre ao crescer espaço virtual;
- outros aplicativos funcionam.

Hipótese:

> limite de espaço de endereçamento da aplicação.

Adicionar mais RAM física pode não resolver.

---

# Diagnóstico por correlação

Não queremos um número isolado.

Queremos correlacionar:

    memória disponível cai
       ↓
    hard faults sobem
       ↓
    SSD aumenta I/O
       ↓
    latência cresce
       ↓
    sistema perde responsividade

Essa sequência é muito mais forte.

---

# Diagnóstico por intervenção mínima

Teste:

> fechar uma carga grande.

Se:

    disponível sobe
    hard faults caem
    I/O reduz
    responsividade volta

a hipótese de pressão ganha força.

---

# Não confunda causa e efeito

SSD em 100% pode ser consequência da falta de memória.

A causa pode ser:

- carga legítima;
- memória insuficiente;
- vazamento;
- configuração.

Se trocarmos o SSD sem entender isso, o sintoma pode continuar.

---

# Memória é um sistema

Precisamos pensar em conjunto:

    Aplicação
       ↓
    Endereços virtuais
       ↓
    Commit
       ↓
    Working set
       ↓
    RAM
       ↓
    Cache / standby
       ↓
    Pagefile / swap
       ↓
    Armazenamento

Cada camada possui função própria.

---

# O que um profissional avançado observaria?

Dependendo do caso:

- commit por processo;
- working set;
- private bytes;
- page fault rate;
- hard faults;
- standby lists;
- pool paginado;
- pool não paginado;
- PSS;
- RSS;
- swap-in;
- swap-out;
- reclaim;
- major/minor faults;
- traces do kernel.

Não precisamos dominar tudo agora.

Mas já sabemos interpretar o princípio.

---

# Pools do kernel

O próprio kernel utiliza memória.

No Windows, podemos observar conceitos como:

- paged pool;
- non-paged pool.

Drivers e kernel também podem vazar recursos.

Se o consumo cresce anormalmente, o problema pode não estar em um aplicativo comum.

---

# Non-paged pool

Algumas estruturas precisam permanecer residentes.

Não podem simplesmente ser paginadas.

Crescimento anormal pode indicar:

- driver;
- componente do kernel.

Esse tipo de investigação é mais avançado.

---

# Memória e drivers

Um driver defeituoso pode:

- alocar memória;
- não liberar;
- crescer pools;
- causar instabilidade.

Então “RAM acabando” não significa sempre:

> aplicativo usando demais.

---

# O sistema operacional precisa sobreviver à pressão

Um bom gerenciador de memória tenta equilibrar:

- desempenho;
- disponibilidade;
- cache;
- isolamento;
- estabilidade.

O objetivo não é manter RAM vazia.

É manter o sistema útil.

---

# A pergunta correta

Em vez de:

> “Quanto de RAM está usando?”

Pergunte:

> “A carga ativa cabe confortavelmente na memória física e o sistema consegue atender páginas sem gerar latência perceptível?”

Essa pergunta é muito mais profissional.

---

# 📁 Dossiê da Investigação — nova ficha

## Ficha de memória

    Data/hora:
    Sistema:
    RAM física:
    Disponível:
    Commit atual:
    Limite de commit:
    Cache:
    Swap/pagefile:
    Processo:
    Working set/RES:
    Memória privada:
    Hard/major faults:
    I/O:
    Sintoma:
    Hipótese:
    Teste:
    Resultado:
    Conclusão:

Use essa ficha sempre que investigar:

- lentidão;
- congelamentos;
- swap;
- pagefile;
- vazamento;
- consumo excessivo.

---

# Conexão com a próxima aula

Memória virtual mostrou que o sistema operacional cria abstrações.

Agora vamos explorar outra abstração essencial:

> arquivos e diretórios.

Quando você salva:

    relatorio.docx

o sistema precisa decidir:

- onde os dados ficam;
- quais metadados existem;
- quem é o proprietário;
- quem pode ler;
- quem pode modificar;
- o que significa excluir;
- como caminhos funcionam;
- como sistemas de arquivos organizam tudo.

E uma nova investigação surgirá:

> **Se um arquivo “sumiu”, ele foi realmente apagado?**

# Próxima aula — Sistemas de Arquivos, Caminhos e Metadados: O Que Acontece Quando Você Salva, Move ou Exclui um Arquivo?
