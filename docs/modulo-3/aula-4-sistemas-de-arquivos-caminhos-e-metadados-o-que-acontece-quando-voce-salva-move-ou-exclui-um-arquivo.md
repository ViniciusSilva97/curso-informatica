# Módulo 3 — Sistemas Operacionais
## Investigação da Camada Lógica

# Aula 4 — Sistemas de Arquivos, Caminhos e Metadados: O Que Acontece Quando Você Salva, Move ou Exclui um Arquivo?

> **Pergunta da investigação**
>
> Se um arquivo “sumiu”, foi realmente apagado, apenas movido, renomeado, ocultado ou tornou-se inacessível por alguma regra do sistema?

---

# 📁 Dossiê da Investigação

## Caso nº 014 — O arquivo que desapareceu sem deixar “vestígios”

Um usuário relata:

> “Eu tinha uma planilha na pasta Documentos. Ontem ela estava lá. Hoje sumiu. Procurei na Lixeira e não encontrei. Acho que o SSD apagou o arquivo sozinho.”

O computador inicia normalmente.

O SSD não apresenta alertas críticos.

Outros arquivos estão acessíveis.

A pasta continua existindo.

Mas o documento não aparece onde o usuário espera.

A frase:

> “o arquivo sumiu”

é um **sintoma**.

Não é ainda uma causa.

Hipóteses possíveis incluem:

- arquivo movido;
- arquivo renomeado;
- extensão alterada;
- pasta diferente;
- sincronização em nuvem;
- arquivo oculto;
- permissão;
- exclusão;
- Lixeira esvaziada;
- aplicação salvando em outro caminho;
- perfil de usuário diferente;
- link quebrado;
- arquivo temporário;
- corrupção lógica;
- erro físico do armazenamento.

Nosso trabalho é reduzir incerteza.

---

# O objetivo desta aula

Ao final desta investigação, você deverá ser capaz de:

- entender o que é um sistema de arquivos;
- diferenciar armazenamento físico de organização lógica;
- compreender arquivos, diretórios e caminhos;
- diferenciar caminho absoluto e relativo;
- compreender extensão, nome e conteúdo;
- entender metadados;
- interpretar tamanho lógico e espaço ocupado;
- compreender timestamps sem tratá-los como verdade absoluta;
- diferenciar copiar, mover, renomear e excluir;
- entender por que mover no mesmo volume pode ser muito diferente de copiar;
- compreender a Lixeira como mecanismo lógico;
- entender por que exclusão não significa necessariamente apagamento físico imediato;
- compreender o impacto do TRIM em SSDs;
- entender links simbólicos e hard links;
- compreender inodes de forma introdutória;
- entender MFT no NTFS de forma conceitual;
- compreender journaling;
- interpretar arquivos ocultos e atributos;
- reconhecer problemas de sincronização e caminhos;
- usar ferramentas seguras para observar metadados;
- construir uma investigação antes de tentar recuperar ou sobrescrever dados.

---

# Sistema de arquivos não é o SSD

O SSD é o dispositivo físico.

O sistema de arquivos é uma estrutura lógica usada para organizar dados nesse dispositivo.

Podemos imaginar:

    SSD / HDD / dispositivo
           ↓
    partição / volume
           ↓
    sistema de arquivos
           ↓
    diretórios
           ↓
    arquivos
           ↓
    aplicações e usuários

Isso significa que um problema em um arquivo pode existir mesmo quando o dispositivo físico está saudável.

---

# O que um sistema de arquivos precisa resolver?

Ele precisa responder perguntas como:

- onde estão os dados?
- qual é o nome do arquivo?
- em qual diretório ele está?
- qual é o tamanho?
- quem é o proprietário?
- quem pode acessar?
- quando foi modificado?
- quais blocos pertencem a ele?
- quais blocos estão livres?
- como manter consistência após falhas?

Sem essa organização, o armazenamento seria apenas uma sequência enorme de blocos.

---

# Arquivo não é apenas “conteúdo”

Quando pensamos em:

    relatorio.docx

vemos um documento.

Mas o sistema pode armazenar informações relacionadas a:

- nome;
- tamanho;
- datas;
- atributos;
- proprietário;
- permissões;
- localização lógica;
- identificadores;
- conteúdo.

Essas informações formam metadados.

---

# Metadados

Metadados são dados sobre dados.

Exemplos:

- nome do arquivo;
- tamanho;
- data de modificação;
- proprietário;
- permissões;
- extensão;
- atributos;
- identificador interno.

Em uma investigação, metadados podem responder perguntas que o conteúdo sozinho não responde.

---

# O nome do arquivo não é o arquivo inteiro

Se você renomear:

    relatorio.docx

para:

    projeto-final.docx

o conteúdo pode permanecer exatamente igual.

O nome mudou.

Os dados não necessariamente mudaram.

---

# Extensão não é conteúdo

Um erro comum é acreditar que a extensão define o tipo real do arquivo.

Renomear:

    foto.jpg

para:

    foto.txt

não transforma a imagem em texto.

A extensão é uma convenção importante.

Mas o conteúdo interno continua sendo o que era.

---

# Ferramentas podem identificar o tipo pelo conteúdo

No Linux, por exemplo, o comando:

    file nome-do-arquivo

pode analisar características internas.

No Windows, diferentes ferramentas também podem inspecionar cabeçalhos e formatos.

Isso ajuda quando:

- extensão foi alterada;
- arquivo está sem extensão;
- nome não corresponde ao conteúdo.

---

# Caminhos

Um caminho informa onde um objeto está dentro de uma hierarquia.

Windows:

    C:\Users\Aluno\Documents\relatorio.docx

Linux:

    /home/aluno/documentos/relatorio.odt

macOS:

    /Users/aluno/Documents/relatorio.pages

Os formatos variam.

O conceito é o mesmo:

> localizar um objeto em uma árvore de diretórios.

---

# Caminho absoluto

Um caminho absoluto parte de uma referência completa.

Exemplo no Windows:

    C:\Users\Aluno\Documents\relatorio.docx

Exemplo em Linux:

    /home/aluno/documentos/relatorio.odt

Ele tenta indicar a localização completa dentro daquele contexto.

---

# Caminho relativo

Um caminho relativo depende do diretório atual.

Exemplo:

    documentos\relatorio.docx

ou:

    ./documentos/relatorio.odt

O mesmo caminho relativo pode apontar para locais diferentes dependendo de onde o programa está executando.

---

# Por que isso causa erros?

Imagine um script que salva:

    resultado.txt

sem caminho completo.

Onde ele será criado?

Depende do diretório de trabalho.

O usuário pode procurar em:

    Documentos

enquanto o arquivo foi criado em:

    pasta do projeto

Esse arquivo não desapareceu.

Foi salvo em outro lugar.

---

# Diretório atual

Processos possuem um contexto.

Um deles pode ser o diretório atual de trabalho.

No terminal, comandos relativos dependem dele.

Windows PowerShell:

    Get-Location

Linux/macOS:

    pwd

Esses comandos respondem:

> onde estou agora?

---

# Diretório não é apenas “pasta visual”

A interface gráfica apresenta diretórios como pastas.

Mas o sistema de arquivos mantém estruturas próprias.

Uma pasta exibida na interface é uma representação dessas estruturas.

Isso é importante quando trabalhamos com:

- terminal;
- scripts;
- APIs;
- servidores;
- containers.

---

# Nome igual não significa mesmo arquivo

Podemos ter:

    C:\Projeto\config.json

e:

    C:\Backup\config.json

Mesmo nome.

Arquivos diferentes.

Em Linux:

    /etc/config
    /home/aluno/config

Também são objetos diferentes.

Sempre registre o caminho completo.

---

# Windows e letras de unidade

No Windows, volumes frequentemente aparecem como:

    C:
    D:
    E:

Essas letras são pontos de acesso ao volume.

Elas não fazem parte do hardware físico em si.

Um mesmo dispositivo pode conter:

- mais de um volume;
- diferentes letras;
- partições.

---

# Linux e árvore única

Em sistemas Unix-like, dispositivos e volumes podem ser montados dentro de uma única árvore.

Exemplo:

    /
    ├── home
    ├── var
    ├── mnt
    └── media

Um dispositivo externo pode aparecer em um ponto de montagem.

---

# Ponto de montagem

Montar significa tornar um sistema de arquivos acessível em determinado ponto da hierarquia.

Exemplo:

    /mnt/dados

ou:

    /media/usuario/USB

Se um volume não estiver montado onde esperado, o usuário pode concluir:

> “meus arquivos sumiram.”

Na verdade, o volume pode simplesmente não estar acessível naquele ponto.

---

# O mesmo caminho pode apontar para contextos diferentes

Em sistemas com rede, containers ou ambientes virtuais, o caminho:

    /dados

pode existir em vários ambientes diferentes.

Por isso, sempre considere:

- sistema;
- usuário;
- volume;
- container;
- sessão.

---

# Sistemas de arquivos conhecidos

Exemplos:

- NTFS;
- exFAT;
- FAT32;
- ext4;
- APFS.

Cada um possui:

- estruturas;
- limites;
- recursos;
- comportamento.

Não existe um único modelo universal.

---

# NTFS

NTFS é amplamente utilizado no Windows.

Ele suporta recursos como:

- permissões;
- journaling;
- metadados;
- links;
- arquivos grandes;
- atributos.

Uma estrutura importante é a MFT.

---

# MFT — Master File Table

No NTFS, a Master File Table mantém registros relacionados aos arquivos e diretórios.

Podemos imaginar:

    arquivo
       ↓
    registro de metadados
       ↓
    referências aos dados

Isso é uma simplificação.

O importante é entender:

> o nome exibido na pasta e os blocos físicos do conteúdo são relacionados por estruturas do sistema de arquivos.

---

# ext4

ext4 é comum em sistemas Linux.

Ele utiliza estruturas como:

- inodes;
- diretórios;
- blocos;
- journaling.

O inode é um conceito central.

---

# Inode

Um inode armazena metadados relacionados a um arquivo.

Ele não precisa armazenar o nome do arquivo da maneira que um iniciante imagina.

O diretório associa nomes a identificadores internos.

Uma simplificação:

    diretório
       ↓
    "relatorio.txt"
       ↓
    inode 81234
       ↓
    metadados + localização dos dados

Isso ajuda a entender hard links.

---

# APFS

APFS é usado em sistemas Apple modernos.

Ele foi projetado para recursos contemporâneos como:

- snapshots;
- clonagem;
- criptografia;
- eficiência em SSD.

A implementação é diferente de NTFS e ext4.

Mas os princípios investigativos permanecem:

> caminho, metadados, conteúdo e estrutura lógica são coisas relacionadas, mas diferentes.

---

# exFAT

exFAT é comum em dispositivos removíveis e compartilhamento entre plataformas.

Ele é conveniente para:

- pendrives;
- cartões;
- discos externos.

Mas não oferece o mesmo conjunto de recursos de NTFS ou ext4.

---

# FAT32

FAT32 ainda aparece em alguns dispositivos.

Possui limitações conhecidas, como:

- tamanho máximo de arquivo de 4 GiB menos 1 byte;
- recursos mais simples.

Se um usuário tenta copiar arquivo maior que o limite, pode receber erro mesmo com espaço livre suficiente.

---

# Espaço livre não é o único limite

Imagine:

    pendrive
    espaço livre: 20 GB

arquivo:

    8 GB

Usuário:

> “tem espaço, por que não copia?”

Se o sistema de arquivos for FAT32, o problema pode ser o limite por arquivo.

Não é falta de espaço total.

---

# Tamanho lógico e espaço ocupado

Um arquivo pode ter:

    tamanho lógico: 100 MB

mas ocupar quantidade física diferente dependendo de:

- tamanho de cluster/bloco;
- compressão;
- arquivos esparsos;
- deduplicação;
- sistema de arquivos.

Por isso, interfaces podem mostrar:

- tamanho;
- tamanho em disco.

---

# Cluster ou unidade de alocação

Sistemas de arquivos agrupam armazenamento em unidades.

Se um arquivo muito pequeno ocupa parte de uma unidade, o restante pode não ser utilizado por outro arquivo naquela mesma unidade, dependendo do sistema.

Isso explica por que:

> tamanho lógico ≠ espaço ocupado necessariamente.

---

# Arquivos esparsos

Um arquivo esparso pode ter tamanho lógico grande sem ocupar fisicamente todo esse espaço.

Exemplo:

    tamanho lógico: 100 GB
    espaço físico usado: muito menor

Isso pode ocorrer em:

- máquinas virtuais;
- bancos de dados;
- backups;
- imagens de disco.

---

# Compressão

Alguns sistemas de arquivos podem comprimir dados.

Então:

    tamanho lógico
       ≠
    espaço físico

Pode haver economia.

Mas compressão também possui custo de CPU.

---

# Salvar um arquivo

Quando um programa salva, a sequência pode envolver:

    aplicação
       ↓
    chamada ao sistema
       ↓
    cache
       ↓
    sistema de arquivos
       ↓
    driver
       ↓
    armazenamento

O “salvar” não é necessariamente uma única escrita simples.

---

# Cache de escrita

O sistema pode manter dados temporariamente em memória antes de gravá-los fisicamente.

Isso melhora desempenho.

Mas cria uma distinção entre:

- aplicação recebeu confirmação;
- dado já chegou ao dispositivo;
- dado está persistido de forma durável.

---

# Flush

Uma operação de flush solicita que dados pendentes sejam encaminhados para armazenamento.

Aplicações críticas e sistemas de arquivos usam mecanismos de sincronização para reduzir risco de perda.

Mesmo assim, detalhes variam.

---

# Queda de energia durante gravação

Se o computador perde energia enquanto estruturas estão sendo modificadas, podemos ter:

- dados incompletos;
- metadados inconsistentes;
- arquivo parcialmente atualizado.

Sistemas modernos usam técnicas para reduzir o risco.

Uma delas é journaling.

---

# Journaling

Um sistema de arquivos com journal registra determinadas operações antes ou durante sua aplicação definitiva.

A ideia é facilitar recuperação de consistência após falha.

Isso não significa:

> todos os arquivos estão protegidos contra perda de dados.

O journal pode proteger principalmente estruturas do sistema de arquivos.

Conteúdo de usuário pode seguir regras diferentes.

---

# Journaling não é backup

Um sistema de arquivos pode continuar consistente e o arquivo ainda estar:

- corrompido;
- desatualizado;
- perdido;
- sobrescrito.

Backup continua necessário.

---

# Copiar

Copiar normalmente cria outro objeto com conteúdo equivalente.

Exemplo:

    origem
       ↓
    leitura
       ↓
    gravação
       ↓
    destino

O novo arquivo pode ter:

- outro identificador;
- novos metadados;
- horários diferentes.

---

# Mover no mesmo volume

Quando um arquivo é movido dentro do mesmo sistema de arquivos, a operação pode ser muito rápida.

Por quê?

Porque o sistema pode alterar estruturas de diretório sem copiar todo o conteúdo.

Exemplo:

    C:\PastaA\video.mkv
       ↓
    C:\PastaB\video.mkv

O conteúdo físico pode permanecer onde está.

A referência muda.

---

# Mover entre volumes

Agora imagine:

    C:\video.mkv
       ↓
    D:\video.mkv

Se C: e D: forem volumes diferentes, o sistema geralmente precisa:

- ler origem;
- criar destino;
- copiar dados;
- remover origem.

Isso é muito mais parecido com:

> copiar + excluir.

---

# Renomear

Renomear normalmente altera metadados ou entrada de diretório.

Não é necessário regravar todos os dados do arquivo.

Por isso, renomear arquivo de 100 GB pode ser quase instantâneo.

---

# “O arquivo foi movido em um segundo”

Isso não significa:

> 100 GB foram fisicamente copiados em um segundo.

Se foi no mesmo volume, provavelmente a estrutura lógica foi alterada.

---

# Excluir

Quando um arquivo é excluído, o que acontece?

A resposta depende de:

- sistema de arquivos;
- aplicação;
- Lixeira;
- dispositivo;
- configurações.

Mas um princípio importante é:

> exclusão lógica não significa necessariamente sobrescrever imediatamente todos os dados físicos.

---

# Lixeira

Em interfaces gráficas, excluir pode primeiro mover o objeto para uma área especial.

Isso permite restauração.

Nesse caso, o conteúdo continua existindo normalmente.

A localização lógica mudou.

---

# Shift + Delete no Windows

Ao usar exclusão que ignora a Lixeira, o sistema pode remover a referência do arquivo sem passar pelo mecanismo de recuperação da interface.

Isso ainda não significa necessariamente sobrescrever cada byte imediatamente.

---

# O que acontece em um HDD?

Em um HDD, após exclusão lógica, blocos podem ser marcados como disponíveis.

Enquanto não forem sobrescritos, parte do conteúdo pode permanecer recuperável.

Mas recuperação nunca deve ser prometida.

---

# O que acontece em um SSD?

SSDs possuem comportamento adicional.

Sistemas modernos podem emitir comandos como TRIM.

Isso informa ao SSD que determinadas regiões não precisam mais preservar dados válidos.

O controlador pode apagá-las internamente posteriormente.

Isso pode reduzir drasticamente a possibilidade de recuperação.

---

# TRIM não é “apagamento instantâneo garantido”

O comportamento depende de:

- sistema;
- SSD;
- firmware;
- controlador;
- garbage collection;
- tempo.

Não devemos afirmar:

> “TRIM apaga imediatamente.”

Devemos dizer:

> TRIM permite que o SSD trate aqueles blocos como descartáveis, tornando recuperação muito menos previsível.

---

# Primeira regra em recuperação

Se dados importantes foram excluídos:

> **pare de escrever no dispositivo.**

Por quê?

Novas gravações podem reutilizar espaço anteriormente associado ao arquivo.

---

# Não instale ferramenta de recuperação no mesmo disco

Se possível, evite.

A instalação pode sobrescrever dados que você tenta recuperar.

O procedimento profissional costuma priorizar:

- preservação;
- imagem/clonagem;
- trabalho sobre cópia.

Isso se conecta ao que aprendemos no módulo anterior.

---

# Excluir e sobrescrever são coisas diferentes

Excluir:

> remover ou invalidar referências lógicas.

Sobrescrever:

> gravar novos dados sobre regiões antes utilizadas.

Em HDD, essa diferença é fundamental.

Em SSD, mecanismos internos tornam o cenário mais complexo.

---

# Metadados de tempo

Arquivos possuem datas.

Podemos encontrar:

- criação;
- modificação;
- acesso;
- mudança de metadados.

Os nomes e comportamentos variam por sistema.

---

# Timestamps não são prova absoluta

Horários podem ser alterados por:

- cópia;
- restauração;
- sincronização;
- mudança de fuso;
- programas;
- sistema de arquivos;
- ferramentas.

Em investigação, timestamp é evidência contextual.

Não verdade absoluta.

---

# Windows e datas

O Windows normalmente apresenta propriedades como:

- criado em;
- modificado em;
- acessado em.

Mas comportamento pode variar.

Copiar um arquivo pode alterar determinadas datas.

---

# Linux e stat

No Linux, o comando:

    stat arquivo.txt

pode mostrar informações como:

- size;
- blocks;
- inode;
- access;
- modify;
- change.

“Change” não significa “data de criação”.

Ele está relacionado à mudança de metadados do inode.

---

# Birth time

Alguns sistemas de arquivos suportam um timestamp de criação, às vezes chamado birth time.

Nem todos suportam.

Nem todas as ferramentas exibem.

Não presuma disponibilidade universal.

---

# Hash

Um hash resume matematicamente o conteúdo.

Exemplos de algoritmos usados em verificação:

- SHA-256;
- SHA-512.

Se dois arquivos possuem o mesmo SHA-256, existe forte evidência de que o conteúdo é idêntico.

---

# Hash não é nome

Se:

    original.docx

e:

    copia-renomeada.docx

têm o mesmo hash, o conteúdo pode ser igual apesar do nome diferente.

---

# PowerShell e hash

No Windows:

    Get-FileHash .\arquivo.iso -Algorithm SHA256

Esse comando calcula hash.

Não modifica o arquivo.

---

# Linux e hash

Um comando comum:

    sha256sum arquivo.iso

---

# Hash e integridade

Podemos usar hash para verificar:

- download;
- cópia;
- imagem forense;
- arquivo antes/depois.

Mas hash não responde:

- quem criou;
- quando;
- por quê.

---

# Arquivos ocultos

Um arquivo pode existir e não aparecer na interface padrão.

Isso pode ocorrer por:

- atributo oculto;
- configuração da interface;
- nome específico;
- regra de sistema.

---

# Windows

Arquivos podem possuir atributos como:

- Hidden;
- System;
- ReadOnly;
- Archive.

Esses atributos influenciam comportamento e exibição.

---

# PowerShell

Podemos observar:

    Get-Item .\arquivo.txt | Select-Object Name, Attributes

Ou listar ocultos:

    Get-ChildItem -Force

---

# Linux e arquivos ocultos

No Linux e outros Unix-like, nomes iniciados por ponto são normalmente tratados como ocultos pela interface.

Exemplo:

    .config

Não existe necessariamente um atributo “hidden” equivalente ao Windows.

É uma convenção de nome.

---

# Mostrar ocultos

Linux:

    ls -la

Isso inclui nomes iniciados por ponto.

---

# “Arquivo oculto” não significa malware

Arquivos legítimos também podem estar ocultos.

O atributo sozinho não define intenção.

---

# Hard link

Um hard link é outro nome que referencia o mesmo objeto de dados em sistemas que suportam o recurso.

Em uma simplificação Unix-like:

    nomeA
       ↓
    inode 9001
       ↑
    nomeB

Ambos apontam para o mesmo inode.

---

# Excluir um hard link não necessariamente elimina os dados

Se:

    nomeA → inode 9001
    nomeB → inode 9001

e apagamos:

    nomeA

o objeto ainda possui uma referência:

    nomeB

Os dados continuam existindo.

---

# Link count

No Linux, comandos podem mostrar quantidade de links.

Exemplo:

    ls -li

Isso pode exibir:

- inode;
- link count;
- nome.

---

# Link simbólico

Um link simbólico funciona de maneira diferente.

Ele aponta para um caminho.

Exemplo:

    atalho
       ↓
    /dados/projeto/config.json

Se o destino for removido, o link pode continuar existindo, mas ficar quebrado.

---

# Link quebrado

Usuário:

> “O arquivo não abre.”

Na verdade, ele clicou em um link simbólico cujo destino não existe mais.

O arquivo original pode ter sido:

- movido;
- renomeado;
- volume desmontado.

---

# Atalho do Windows não é exatamente symlink

Um arquivo .lnk da interface Windows possui comportamento próprio.

Não devemos confundir:

- atalho .lnk;
- symbolic link;
- junction;
- hard link.

São mecanismos diferentes.

---

# Junctions e reparse points

NTFS possui mecanismos como reparse points.

Eles permitem comportamentos especiais.

Junctions e symbolic links podem redirecionar caminhos.

Isso é útil, mas pode confundir diagnóstico.

---

# Um caminho pode não representar armazenamento local

Exemplo:

    C:\Dados

pode estar relacionado a:

- pasta local;
- junction;
- link;
- sincronização;
- rede;
- volume montado.

Observe antes de assumir.

---

# Sincronização em nuvem

Serviços de nuvem adicionam outra camada.

Exemplos:

- OneDrive;
- Google Drive;
- Dropbox;
- iCloud Drive.

O arquivo exibido pode estar:

- totalmente local;
- parcialmente local;
- somente online;
- sincronizando;
- com conflito.

---

# Placeholder

Alguns sistemas mostram arquivos como placeholders.

Eles aparecem na pasta, mas o conteúdo pode precisar ser baixado sob demanda.

Se a rede falha, o usuário pode dizer:

> “meu arquivo não abre.”

O problema pode estar na disponibilidade do conteúdo remoto.

---

# Arquivos “somente online”

Nesse cenário, o nome e metadados podem existir localmente.

O conteúdo completo não.

Isso muda completamente a investigação.

---

# Conflito de sincronização

Dois dispositivos editando ao mesmo tempo podem gerar:

- versões duplicadas;
- nomes alterados;
- conflitos;
- arquivos movidos.

O documento “sumido” pode existir em:

- pasta de conflito;
- lixeira da nuvem;
- outro dispositivo;
- histórico de versões.

---

# Perfil de usuário

No Windows:

    C:\Users\Vinicius\Documents

e:

    C:\Users\OutroUsuario\Documents

são locais diferentes.

Se o usuário entrou em outro perfil, seus arquivos podem parecer ausentes.

---

# Perfil temporário

Em algumas falhas, o Windows pode iniciar com perfil temporário.

Sintomas:

- área de trabalho “vazia”;
- documentos não aparecem;
- configurações parecem resetadas.

O arquivo pode continuar intacto no perfil original.

---

# Pasta redirecionada

Empresas podem redirecionar:

- Desktop;
- Documents;
- Downloads.

Essas pastas podem apontar para:

- servidor;
- OneDrive;
- outro local.

Sempre descubra o caminho real.

---

# Variáveis de ambiente

Caminhos podem ser construídos usando variáveis.

Exemplo no Windows:

    %USERPROFILE%

No PowerShell:

    $env:USERPROFILE

No Linux:

    $HOME

Isso ajuda scripts a funcionar para vários usuários.

---

# Nomes e diferenças entre maiúsculas/minúsculas

Sistemas de arquivos e sistemas operacionais podem tratar nomes de maneira diferente.

Em muitos ambientes Windows:

    Arquivo.txt

e:

    arquivo.txt

podem ser considerados o mesmo nome.

Em Linux, geralmente são distintos.

---

# Mas não simplifique demais

Comportamento de case sensitivity pode depender de:

- sistema de arquivos;
- configuração;
- volume;
- aplicação.

Não use uma regra absoluta sem considerar o ambiente.

---

# Caracteres especiais

Alguns sistemas restringem caracteres em nomes.

Um arquivo válido em um sistema pode causar problema ao ser transferido para outro.

Isso aparece em:

- compartilhamentos;
- ZIP;
- Git;
- sincronização;
- sistemas multiplataforma.

---

# Caminhos longos

O Windows historicamente teve limitações de caminho em várias APIs.

Sistemas modernos podem oferecer suporte a caminhos maiores quando configurados e utilizados por aplicações compatíveis.

Portanto:

> “Windows só aceita 260 caracteres”

é uma simplificação desatualizada.

Ainda assim, aplicações antigas podem apresentar problemas.

---

# Arquivo aberto

Quando um processo abre um arquivo, o sistema cria estruturas para representá-lo.

No Windows, podemos ter handles.

Em Linux, descritores de arquivo.

---

# Excluir arquivo aberto no Windows

Dependendo de como o arquivo foi aberto e das flags de compartilhamento, a exclusão pode ser bloqueada.

Usuário pode receber:

> “O arquivo está em uso.”

---

# Excluir arquivo aberto em Unix-like

Em muitos sistemas Unix-like, um arquivo pode ser removido do diretório enquanto um processo ainda mantém o descritor aberto.

O nome desaparece.

Mas os dados continuam acessíveis ao processo até o último descritor ser fechado.

---

# O arquivo desapareceu, mas espaço não voltou

Esse é um caso clássico em Linux.

Processo mantém arquivo grande aberto.

O usuário exclui o nome.

O comando de diretório não mostra mais o arquivo.

Mas o espaço continua ocupado.

Por quê?

Porque o processo ainda possui referência ao objeto.

---

# Ferramentas podem revelar arquivos excluídos ainda abertos

Ferramentas como lsof, quando disponíveis, podem ajudar.

Exemplo:

    lsof | grep deleted

Isso pode indicar arquivos removidos que ainda possuem descritores abertos.

---

# Não reinicie antes de observar

Se o problema envolve arquivos abertos, reiniciar pode liberar descritores e alterar a evidência.

Registre antes.

---

# Permissões

Mesmo quando o arquivo existe, o usuário pode não conseguir:

- ler;
- modificar;
- excluir;
- listar.

Isso envolve permissões.

A próxima aula aprofundará esse tema.

Por enquanto, lembre:

> “não consigo acessar” não significa “não existe”.

---

# “Arquivo inexistente” versus “acesso negado”

Esses sintomas são diferentes.

Se o sistema retorna:

    Access denied

ele reconheceu o objeto, mas bloqueou a operação.

Se retorna:

    File not found

o caminho pode estar incorreto ou o objeto não está ali.

---

# Erro de caminho

Aplicação:

> “arquivo não encontrado.”

Hipóteses:

- caminho errado;
- drive desconectado;
- volume desmontado;
- nome alterado;
- link quebrado;
- variável incorreta.

Não conclua corrupção.

---

# Journaling e recuperação

Após desligamento incorreto, o sistema pode realizar verificação.

Ele tenta restaurar consistência estrutural.

Isso pode resultar em:

- correções;
- arquivos órfãos;
- registros recuperados.

Mas novamente:

> consistência não significa conteúdo intacto.

---

# Corrupção lógica

Um sistema de arquivos pode apresentar inconsistências por:

- desligamento abrupto;
- falha de hardware;
- driver;
- software;
- bug;
- dispositivo removido durante escrita.

Sintomas:

- arquivos inacessíveis;
- nomes estranhos;
- diretórios perdidos;
- erros de leitura.

---

# Corrupção lógica não prova defeito físico

Um único erro pode ocorrer após queda de energia.

Mas se corrupção retorna repetidamente, precisamos investigar:

- SSD/HDD;
- memória;
- controladora;
- alimentação;
- cabos;
- sistema.

Hardware e lógica se encontram novamente.

---

# CHKDSK

No Windows, chkdsk pode verificar estruturas do sistema de arquivos.

Mas é uma ferramenta que pode modificar o volume quando usada com determinadas opções.

Em caso de dados críticos:

> não execute reparo destrutivo antes de preservar o conteúdo.

---

# fsck

Em Linux e outros sistemas Unix-like, fsck e ferramentas relacionadas verificam sistemas de arquivos.

Da mesma forma:

> reparar altera estruturas.

Para dados importantes, preserve primeiro.

---

# Recuperação e cadeia de custódia

Em cenário forense ou profissional:

- documente;
- minimize escrita;
- faça imagem;
- gere hash;
- trabalhe sobre cópia;
- registre ferramentas e horário.

Nosso curso não exige laboratório forense completo agora.

Mas o princípio já deve estar incorporado.

---

# O caso retorna

Vamos voltar à planilha “desaparecida”.

O usuário diz:

> “Estava em Documentos.”

Primeiro observamos o perfil atual.

Descobrimos:

    C:\Users\TempUser

O usuário normalmente utiliza:

    C:\Users\Marcos

Temos uma pista.

---

# Perfil diferente

Ao abrir:

    C:\Users\Marcos\Documents

a planilha está lá.

Ela nunca foi excluída.

O usuário havia entrado em um perfil temporário.

---

# Diagnóstico

Sintoma:

> arquivo desapareceu.

Causa real:

> sessão iniciou em perfil diferente.

O SSD não apagou nada.

---

# O que teria acontecido se formatássemos?

Perderíamos:

- perfil original;
- logs;
- configuração;
- evidência.

E talvez os arquivos.

Essa é exatamente a situação em que diagnóstico lógico evita desastre.

---

# Outra possibilidade: arquivo movido

Usuário arrastou sem perceber.

Pesquisa revela:

    C:\Users\Marcos\Desktop\Projetos\planilha.xlsx

O arquivo existe.

O caminho mudou.

---

# Outra possibilidade: sincronização

OneDrive moveu Documentos para:

    C:\Users\Marcos\OneDrive\Documents

A pasta antiga parece vazia.

O arquivo continua existindo em outro caminho.

---

# Outra possibilidade: link quebrado

Atalho na área de trabalho aponta para:

    D:\Projetos\planilha.xlsx

Mas D: é um HD externo desconectado.

O atalho continua.

O destino não.

---

# Outra possibilidade: exclusão real

A planilha foi excluída.

Não está na Lixeira.

Nesse caso:

1. interrompa gravações;
2. identifique o dispositivo;
3. avalie importância;
4. preserve;
5. só depois considere recuperação.

---

# A ordem da investigação

    Sintoma
       ↓
    identificar caminho esperado
       ↓
    confirmar usuário/perfil
       ↓
    pesquisar nome/extensão
       ↓
    verificar ocultos
       ↓
    verificar sincronização
       ↓
    verificar links
       ↓
    verificar Lixeira
       ↓
    verificar logs/histórico
       ↓
    considerar recuperação

Essa ordem reduz risco.

---

# Ferramentas no Windows

## Explorer

Use a barra de endereço para conferir o caminho real.

Não confie apenas no nome visual da pasta.

---

# Propriedades

Podem mostrar:

- tipo;
- tamanho;
- localização;
- datas;
- atributos.

---

# PowerShell

Listar:

    Get-ChildItem

Incluir ocultos:

    Get-ChildItem -Force

Ver metadados:

    Get-Item .\arquivo.txt | Format-List *

Calcular hash:

    Get-FileHash .\arquivo.txt -Algorithm SHA256

---

# Procurar arquivo pelo nome

Exemplo:

    Get-ChildItem C:\Users\Marcos -Recurse -Filter "planilha*.xlsx" -ErrorAction SilentlyContinue

Esse comando pode ser lento em árvores grandes.

Use com escopo restrito quando possível.

---

# Ferramentas no Linux

Listar:

    ls -la

Metadados:

    stat arquivo.txt

Tipo:

    file arquivo.txt

Inode:

    ls -li arquivo.txt

Hash:

    sha256sum arquivo.txt

---

# find

Pesquisar por nome:

    find /home/aluno -name "relatorio*"

Pode ser muito poderoso.

Use escopo adequado.

---

# readlink

Para link simbólico:

    readlink link

Ou:

    readlink -f link

Isso ajuda a descobrir o destino.

---

# df e mount

Podem ajudar a verificar:

- volumes;
- sistemas de arquivos;
- pontos de montagem.

Exemplos:

    df -h

    mount

---

# macOS

Ferramentas úteis incluem:

- Finder;
- Get Info;
- Spotlight;
- Terminal;
- stat;
- file;
- shasum.

O princípio continua igual.

---

# Não use busca como prova final

Encontrar um arquivo com mesmo nome não prova que é o mesmo arquivo.

Compare:

- caminho;
- tamanho;
- datas;
- hash;
- conteúdo.

---

# Hash e cópia

Se copiamos um arquivo de forma íntegra:

    origem SHA-256 = A
    destino SHA-256 = A

temos forte evidência de conteúdo idêntico.

---

# Duplicados

Dois arquivos podem ser duplicados mesmo com nomes diferentes.

Exemplo:

    relatorio-final.docx
    relatorio-final-2.docx

Hash idêntico.

Isso ajuda em organização e investigação.

---

# Arquivos temporários

Aplicações podem criar:

- arquivos temporários;
- lock files;
- backups;
- autosave.

Quando um programa fecha incorretamente, esses arquivos podem permanecer.

---

# Autosave

Em caso de crash, um aplicativo pode recuperar dados a partir de:

- temporários;
- versões;
- autosave.

Antes de assumir perda total, investigue mecanismos da aplicação.

---

# Arquivo de lock

Programas podem criar um pequeno arquivo para indicar:

> “este documento está aberto.”

Se ele permanecer após crash, o programa pode achar que o arquivo ainda está em uso.

---

# Extensões duplas

Um arquivo pode ser:

    relatorio.pdf.exe

Se a interface oculta extensões conhecidas, o usuário pode enxergar:

    relatorio.pdf

Isso é um risco de segurança.

---

# Mostrar extensões

Para investigação, é recomendável enxergar a extensão real.

Isso reduz confusão e ajuda segurança.

---

# O nome pode enganar

Não confie apenas no ícone.

Um ícone pode vir de:

- associação de arquivo;
- aplicação;
- extensão.

Verifique o tipo real quando necessário.

---

# MIME type

Em ambientes web e Unix-like, MIME types ajudam a classificar conteúdo.

Exemplo:

    image/png
    application/pdf
    text/plain

Isso é outra camada de identificação.

---

# Associações de arquivo

No Windows, abrir:

    .pdf

com determinado programa depende de associação.

Se associação quebra, o usuário pode dizer:

> “PDF não abre.”

O arquivo pode estar perfeitamente íntegro.

---

# Caminho de rede

Arquivos podem estar em:

    \\servidor\compartilhamento\relatorio.xlsx

Se a rede falha, o arquivo parece “sumir”.

Não é armazenamento local.

---

# Unidade mapeada

Uma letra como:

    Z:

pode representar recurso de rede.

Se Z: some, isso não significa que o HD foi removido.

Pode ser:

- autenticação;
- VPN;
- servidor;
- rede.

---

# A camada de armazenamento pode ser remota

Por isso, pergunte:

> onde os dados realmente estão?

Pode ser:

- SSD local;
- NAS;
- servidor;
- nuvem;
- pendrive;
- VM;
- container.

---

# Mito ou Evidência?

## “Se não está na pasta, foi apagado.”

**Mito.**

Pode ter sido movido, ocultado, redirecionado ou estar em outro perfil.

---

## “Mover um arquivo grande sempre copia todos os dados.”

**Mito.**

No mesmo volume, a operação pode alterar apenas metadados.

---

## “Excluir significa zerar os bytes.”

**Mito.**

A exclusão lógica pode apenas liberar referências.

---

## “TRIM apaga o arquivo instantaneamente.”

**Simplificação incorreta.**

TRIM informa ao SSD que blocos podem ser descartados.

---

## “Arquivo com extensão .jpg é necessariamente uma imagem.”

**Mito.**

Extensão e conteúdo são coisas diferentes.

---

## “Data de modificação prova exatamente quando alguém editou.”

**Mito.**

Timestamps precisam de contexto.

---

## “Journaling é backup.”

**Mito.**

Ele ajuda consistência, não substitui cópia de segurança.

---

## “Arquivo oculto é malware.”

**Mito.**

Ocultação pode ser totalmente legítima.

---

# 🔬 Laboratório — seguindo o rastro de um arquivo

Nesta aula, trabalharemos apenas com arquivos de teste.

Não use documentos importantes.

---

# Etapa 1 — Crie o arquivo

Crie:

    investigacao.txt

Conteúdo:

    Smarteletrovini Academy
    Laboratório de sistemas de arquivos

---

# Etapa 2 — Registre metadados

No Windows:

    Get-Item .\investigacao.txt | Format-List Name,FullName,Length,CreationTime,LastWriteTime,Attributes

No Linux:

    stat investigacao.txt

Registre:

- caminho;
- tamanho;
- data;
- atributos.

---

# Etapa 3 — Calcule o hash

Windows:

    Get-FileHash .\investigacao.txt -Algorithm SHA256

Linux:

    sha256sum investigacao.txt

Salve o hash.

---

# Etapa 4 — Renomeie

Renomeie:

    investigacao.txt

para:

    evidencia.txt

Calcule o hash novamente.

Pergunta:

> o conteúdo mudou?

---

# Etapa 5 — Mova no mesmo volume

Mova para outra pasta no mesmo volume.

Observe:

- velocidade;
- caminho;
- hash.

O hash deve permanecer igual se o conteúdo não mudou.

---

# Etapa 6 — Copie

Faça uma cópia.

Agora temos:

    evidencia.txt
    evidencia-copia.txt

Compare hashes.

---

# Etapa 7 — Altere apenas um caractere

Edite uma letra.

Calcule hash novamente.

O resultado deve mudar completamente.

Isso demonstra sensibilidade do hash ao conteúdo.

---

# Etapa 8 — Arquivo oculto

Windows:

    attrib +h evidencia-copia.txt

Depois:

    Get-ChildItem -Force

Para desfazer:

    attrib -h evidencia-copia.txt

Linux:

    mv evidencia-copia.txt .evidencia-copia.txt

Observe a diferença.

---

# Etapa 9 — Link simbólico

Se você estiver confortável e tiver permissões adequadas, crie um link simbólico em um ambiente de teste.

No Linux:

    ln -s evidencia.txt link-evidencia.txt

Observe:

    ls -l

No Windows, a criação de symlink pode exigir permissões/configuração.

Não é obrigatório nesta aula.

---

# Etapa 10 — Registre

No Dossiê:

    Arquivo original:
    Caminho:
    Tamanho:
    Hash:
    Data:

    Após renomear:
    Caminho:
    Hash:

    Após mover:
    Caminho:
    Hash:

    Após copiar:
    Hash da cópia:

    Após editar:
    Novo hash:

---

# O que o laboratório demonstra?

Renomear:

> muda o nome, não necessariamente o conteúdo.

Mover:

> pode mudar apenas referência/caminho.

Copiar:

> cria outro objeto.

Editar:

> altera conteúdo.

Hash:

> ajuda a verificar integridade do conteúdo.

---

# Estudo de caso 1 — Documento “sumiu”

Evidências:

- usuário entrou em perfil temporário;
- pasta original existe;
- arquivo está no perfil anterior.

Conclusão:

> arquivo não foi excluído.

---

# Estudo de caso 2 — Pendrive com espaço, mas arquivo não copia

Evidências:

- FAT32;
- arquivo de 7,8 GB;
- 40 GB livres.

Conclusão:

> limite por arquivo do sistema de arquivos.

---

# Estudo de caso 3 — Disco não libera espaço após excluir log

Linux:

- log de 20 GB excluído;
- df continua mostrando uso;
- processo servidor ainda mantém descritor.

Conclusão:

> arquivo foi removido do diretório, mas permanece aberto.

---

# Estudo de caso 4 — Atalho não abre

Evidências:

- .lnk aponta para D:;
- D: era HD externo;
- HD não está conectado.

Conclusão:

> atalho existe, destino não está disponível.

---

# Estudo de caso 5 — Arquivo mudou de nome na nuvem

Evidências:

- sincronização em dois computadores;
- conflito;
- serviço criou versão duplicada.

Conclusão:

> investigar histórico de versões e conflitos.

---

# Estudo de caso 6 — “Arquivo corrompido”

Sintoma:

> programa não abre .docx.

Evidências:

- extensão é .docx;
- ferramenta de tipo identifica executável;
- arquivo veio por e-mail suspeito.

Conclusão:

> nome/extensão enganosa.

Isso também tem implicações de segurança.

---

# Estudo de caso 7 — Documento excluído em SSD

Evidências:

- usuário apagou;
- Lixeira vazia;
- SSD com TRIM;
- sistema continuou em uso por várias horas.

Conclusão:

> recuperação é incerta e pode ser inviável.

A primeira ação deveria ter sido reduzir gravações.

---

# O que um profissional avançado observaria?

Dependendo do caso:

- MFT;
- inodes;
- journaling;
- USN Journal;
- atributos;
- Alternate Data Streams;
- extents;
- snapshots;
- volume shadow copies;
- timestamps;
- hashes;
- file signatures;
- links;
- ACLs.

Não precisamos dominar tudo agora.

Mas já reconhecemos que o arquivo possui uma história lógica.

---

# USN Journal

No NTFS, o USN Change Journal pode registrar alterações em objetos do volume.

Ele pode ser útil em investigação avançada.

Não é um log simples de “quem fez o quê”.

Mas pode fornecer evidências sobre mudanças.

---

# Alternate Data Streams

NTFS pode associar streams adicionais a um arquivo.

O conteúdo visível principal não é necessariamente a única sequência de dados associada ao objeto.

É um recurso legítimo.

Também pode ter relevância em segurança.

---

# Snapshots

Alguns sistemas suportam snapshots.

Eles registram um estado lógico do sistema de arquivos em determinado momento.

Isso pode ajudar:

- backup;
- recuperação;
- comparação.

Mas snapshot não substitui backup externo.

---

# Versionamento

Aplicações e nuvem podem manter versões.

Quando um arquivo é alterado ou sobrescrito, versões anteriores podem continuar disponíveis.

Sempre investigue antes de declarar perda definitiva.

---

# Backup

A melhor recuperação continua sendo:

> restauração de uma cópia conhecida.

Estratégias de backup reduzem dependência de ferramentas de recuperação.

---

# A regra 3-2-1 continua válida

Uma orientação clássica é manter:

- 3 cópias;
- 2 tipos de mídia;
- 1 cópia fora do ambiente principal.

Hoje isso pode ser adaptado.

O importante é reduzir pontos únicos de falha.

---

# O arquivo como evidência

Em suporte comum, queremos recuperar funcionamento.

Em investigação mais rigorosa, queremos preservar também contexto.

Por isso registramos:

- caminho;
- hash;
- timestamps;
- tamanho;
- origem;
- usuário.

---

# Caminho também é evidência

Compare:

    C:\Windows\System32\app.exe

com:

    C:\Users\Aluno\Downloads\app.exe

O nome pode ser igual.

O caminho muda completamente a interpretação.

---

# O conteúdo também precisa de contexto

Um hash confirma integridade.

Mas não prova legitimidade.

Arquivo malicioso também pode ter hash estável.

Precisamos combinar evidências.

---

# A investigação por camadas

Quando um arquivo “some”:

    usuário
       ↓
    aplicação
       ↓
    caminho
       ↓
    perfil
       ↓
    diretório
       ↓
    sistema de arquivos
       ↓
    volume
       ↓
    armazenamento

A causa pode estar em qualquer camada.

---

# Não culpe o armazenamento cedo demais

O SSD é apenas uma hipótese.

Antes de condená-lo, investigue:

- usuário;
- perfil;
- caminho;
- link;
- sincronização;
- permissão;
- Lixeira;
- sistema de arquivos.

---

# 📁 Dossiê da Investigação — nova ficha

## Ficha de arquivo

    Data/hora:
    Usuário:
    Sistema operacional:

    Nome:
    Caminho completo:
    Extensão:
    Tipo identificado:
    Tamanho:
    Tamanho em disco:
    Hash SHA-256:

    Criação:
    Modificação:
    Acesso:
    Outros timestamps:

    Atributos:
    Proprietário:
    Permissões:
    Link/symlink:
    Volume:
    Sistema de arquivos:

    Sintoma:
    Hipótese:
    Teste:
    Resultado:
    Conclusão:

Essa ficha será especialmente útil em:

- arquivos desaparecidos;
- corrupção;
- duplicidade;
- malware;
- sincronização;
- recuperação.

---

# Conexão com a próxima aula

Agora sabemos que um arquivo pode existir e ainda assim o usuário não conseguir acessá-lo.

Isso nos leva a uma pergunta fundamental:

> **Quem decide quem pode ler, modificar, executar ou excluir um arquivo?**

A resposta envolve:

- usuários;
- grupos;
- permissões;
- proprietário;
- ACLs;
- privilégios;
- elevação;
- herança.

Na próxima aula, vamos investigar por que:

> “Acesso negado”

nem sempre é erro.

Às vezes, é exatamente o sistema operacional funcionando corretamente.

# Próxima aula — Usuários, Grupos e Permissões: Por Que o Sistema Diz “Acesso Negado”?
