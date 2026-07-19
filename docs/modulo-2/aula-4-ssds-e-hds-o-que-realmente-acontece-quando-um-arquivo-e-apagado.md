# Aula 4 — SSDs e HDs: O que realmente acontece quando um arquivo é apagado?

Pergunta da investigação

```text
Quando você esvazia a Lixeira, os dados desaparecem imediatamente?
```

## Dossiê da Investigação
Caso nº 003 — A pasta desaparecida

Um pequeno escritório armazenava documentos importantes em um computador. Durante uma limpeza, um funcionário apagou uma pasta inteira e, logo depois, esvaziou a Lixeira.  
Minutos depois percebeu o erro. A primeira reação foi instalar vários programas de recuperação no mesmo computador e executar diferentes tentativas de restauração.

Alguns arquivos foram recuperados, outros estavam corrompidos, vários nunca apareceram. O que aconteceu?  
O simples ato de apagar os arquivos os destruiu?  
As tentativas de recuperação podem ter piorado a situação?  
O resultado seria diferente se o computador utilizasse um HD em vez de um SSD?  
Hoje investigaremos essas perguntas.

## Objetivos da aula

Ao final desta aula, você será capaz de:

- diferenciar armazenamento magnético e memória flash;
- compreender como HDs e SSDs armazenam informações;
- entender o que normalmente acontece quando um arquivo é apagado;
- reconhecer a influência do comando TRIM;
- interpretar indicadores de saúde do dispositivo;
- utilizar ferramentas gratuitas de diagnóstico e recuperação;
- saber quando interromper tentativas caseiras;
- distinguir recuperação lógica de recuperação física.

## O armazenamento não é a memória RAM
Na aula anterior, vimos que a memória RAM funciona como uma área de trabalho temporária.

O armazenamento tem outra responsabilidade:

**preservar dados mesmo quando o computador é desligado.**

É nele que ficam:

- o sistema operacional;
- os programas instalados;
- documentos;
- fotografias;
- bancos de dados;
- vídeos;
- configurações;
- arquivos temporários;
- registros do sistema.

Hoje os computadores utilizam principalmente dois tipos de dispositivo:

- HD, baseado em armazenamento magnético;
- SSD, baseado em memória flash.

Embora ambos guardem arquivos, internamente funcionam de maneiras muito diferentes.

## Parte 1 — Como funciona um HD

O HD, também chamado de disco rígido, possui partes mecânicas.  

Dentro dele existem pratos revestidos com material magnético, que giram em alta velocidade. Uma cabeça de leitura e gravação se movimenta sobre esses pratos para acessar as informações.  

### Uma representação simplificada seria:


Prato magnético  

│↑│

Cabeça de leitura   

Motor interno  


O HD armazena dados alterando propriedades magnéticas em pequenas regiões do prato.  

Como possui partes móveis, está sujeito a problemas como:

- desgaste mecânico;
- falha do motor;
- danos na cabeça de leitura;
- impactos;
- setores defeituosos;
- ruídos anormais;
- dificuldade de inicialização.

## Parte 2 — Como funciona um SSD

O SSD não utiliza pratos nem cabeças móveis.
Ele armazena dados em chips de **memória flash NAND**.

Sua estrutura inclui, de forma simplificada:

- chips NAND;
- controlador;
- firmware;
- memória de cache, em alguns modelos;
- circuitos de alimentação;
- interface de comunicação.


||Controlador||                   
|------|------|------|                              
|NAND 1|NAND 2|NAND 3|     
||Cache e circuitos auxiliares||  


O controlador do SSD é responsável por tarefas importantes, como:

- localizar os dados;
- distribuir gravações entre as células;
- corrigir determinados erros;
- substituir blocos defeituosos;
- gerenciar desgaste;
- realizar coleta de lixo interna;
- comunicar-se com o sistema operacional.

Por isso, um SSD não é apenas um conjunto de chips de memória.

Ele é um pequeno sistema computacional dedicado ao armazenamento.

## HD versus SSD
|Característica|HD|SSD|
|--------------|--|---|
|Tecnologia|Magnética|Memória flash|
|Partes móveis|Sim|Não|
|Ruído|Pode existir|Normalmente silencioso|
|Resistência a impactos|Menor|Geralmente maior
|Velocidade|Menor|Maior|
|Recuperação de dados apagados|Frequentemente mais viável|Pode ser dificultada pelo TRIM|
|Falhas comuns|Mecânicas e magnéticas|Controlador, NAND, firmware e alimentação|

Essa tabela não significa que todo SSD seja mais confiável que todo HD.  

A confiabilidade depende de fatores como:

- qualidade do projeto;
- temperatura;
- energia elétrica;
- quantidade de gravações;
- firmware;
- condições de uso;
- idade;
- existência de backup.

## O que é um arquivo para o sistema operacional?
Para o usuário, um arquivo é algo como:

```text
contrato_cliente.pdf
```

Para o sistema de arquivos, ele envolve diferentes informações:

- nome;
- tamanho;
- localização;
- permissões;
- datas;
- blocos utilizados;
- metadados;
- referências internas.

O sistema operacional mantém uma espécie de índice para saber onde os dados estão armazenados.

- Em sistemas Windows, é comum encontrarmos o NTFS.

- Em Linux, sistemas como ext4 são frequentes.

- Em dispositivos removíveis, FAT32 e exFAT também aparecem com frequência.

## O que acontece quando um arquivo é apagado?

Em muitos sistemas, apagar um arquivo não significa sobrescrever imediatamente todo o seu conteúdo. De maneira simplificada, o sistema pode:

1. remover ou alterar a referência ao arquivo;
2. marcar o espaço como disponível;
3. permitir que esse espaço seja utilizado posteriormente.

Enquanto os dados antigos não forem sobrescritos, pode existir alguma possibilidade de recuperação. É como retirar uma residência do mapa sem demolir imediatamente o prédio.

O endereço deixou de aparecer no índice, mas a estrutura pode continuar no local. Entretanto, essa analogia funciona melhor para HDs do que para SSDs modernos.

## A Lixeira não é destruição de dados

Quando um arquivo é enviado para a Lixeira, normalmente ele ainda permanece armazenado e pode ser restaurado.   

Ao esvaziar a Lixeira, o sistema remove as referências usadas para a recuperação comum. Mesmo assim, em determinados dispositivos e condições, parte do conteúdo pode continuar fisicamente presente.  

Essa é a razão pela qual programas de recuperação conseguem localizar arquivos que já não aparecem normalmente no sistema.

## O grande complicador: TRIM

Nos SSDs existe um recurso extremamente importante chamado TRIM.

Quando o sistema operacional informa ao SSD que determinados blocos não contêm mais dados necessários, o controlador pode prepará-los para futuras gravações.  

Isso melhora o desempenho e a gestão da memória flash. Porém, também pode reduzir drasticamente a possibilidade de recuperar dados apagados.

Em termos simplificados:

Arquivo apagado  
        ↓  
Sistema marca espaço como livre  
        ↓  
Comando TRIM pode ser enviado  
        ↓  
Controlador do SSD administra os blocos  
        ↓  
Dados podem deixar de estar recuperáveis  

O comportamento exato depende de vários fatores:

- sistema operacional;
- sistema de arquivos;
- modelo do SSD;
- controlador;
- firmware;
- tempo transcorrido;
- uso posterior do dispositivo;
- criptografia;
- suporte ao TRIM;
- coleta de lixo interna.

Por isso, não é correto afirmar que arquivos apagados de SSDs são sempre impossíveis de recuperar. Também não é correto prometer que serão recuperados.

A resposta tecnicamente responsável é:

```text
a recuperação depende do estado do dispositivo, da forma como os dados foram apagados e do que aconteceu depois.
```

## Primeiro princípio da recuperação

Quando dados importantes desaparecem:

```text
pare de usar o dispositivo.
```

Cada nova gravação pode ocupar áreas que ainda contêm fragmentos recuperáveis.  

Algumas ações perigosas incluem:

- instalar programas no mesmo disco;
- baixar arquivos;
- atualizar o sistema;
- executar desfragmentação;
- copiar grandes quantidades de dados;
- formatar repetidamente;
- tentar reparar o sistema de arquivos sem preservar uma cópia;
- continuar usando o computador normalmente.

No caso apresentado no início da aula, a instalação de vários programas no próprio disco pode ter sobrescrito parte dos dados que se pretendia recuperar.

## Recuperação lógica e recuperação física
### Recuperação lógica

Acontece quando o dispositivo ainda funciona eletricamente, mas os dados ficaram inacessíveis devido a situações como:

- exclusão acidental;
- formatação;
- partição perdida;
- sistema de arquivos corrompido;
- tabela de partições danificada;
- falha de software.

Nesses casos, programas podem ajudar.

### Recuperação física

É necessária quando existe defeito no próprio dispositivo, por exemplo:

#### Em HDs
- cabeça de leitura danificada;
- motor travado;
- pratos comprometidos;
- placa eletrônica defeituosa;
- ruídos mecânicos anormais.

#### Em SSDs
- controlador defeituoso;
- falha no firmware;
- NAND danificada;
- circuito de alimentação em curto;
- componentes eletrônicos queimados;
- dispositivo não reconhecido.

A recuperação física costuma exigir laboratório, conhecimento especializado e equipamentos próprios.

## Laboratório: ferramentas gratuitas
### CrystalDiskInfo

O CrystalDiskInfo é usado principalmente para consultar informações de saúde fornecidas pelo próprio dispositivo.

Pode apresentar dados como:

- temperatura;
- horas de funcionamento;
- quantidade de inicializações;
- estado de saúde;
- erros registrados;
- volume de dados gravados;
- alertas relacionados ao S.M.A.R.T.

Ele não recupera arquivos.

Sua função é ajudar no diagnóstico.

### GSmartControl

É uma interface gráfica para consultar informações S.M.A.R.T. e executar testes compatíveis com o dispositivo.

Pode ser útil para:

- verificar atributos;
- executar testes curtos;
- executar testes estendidos;
- identificar alertas;
- acompanhar a evolução de falhas.

### TestDisk

O TestDisk é voltado principalmente para problemas estruturais, como:

- partições perdidas;
- tabelas de partições;
- setores de inicialização;
- determinados problemas no sistema de arquivos.

Ele exige cuidado.

Alterar estruturas de disco sem compreender o procedimento pode piorar a situação.

### PhotoRec

O PhotoRec procura arquivos por assinaturas conhecidas.

Em vez de depender exclusivamente do sistema de arquivos, ele tenta identificar padrões associados a formatos como:

- JPEG;
- PDF;
- ZIP;
- documentos;
- vídeos;
- arquivos compactados.

Essa técnica é conhecida como file carving.

Uma limitação importante é que os arquivos recuperados podem perder:

- nomes originais;
- pastas;
- datas;
- organização anterior.

### Recuva

O Recuva oferece uma interface mais simples para recuperação em determinados cenários.

Pode ser útil em exclusões recentes, especialmente em dispositivos sem danos físicos e quando o espaço ainda não foi sobrescrito.

No entanto, sua simplicidade não elimina os riscos de trabalhar diretamente sobre o dispositivo original.

## A regra profissional: trabalhar sobre uma cópia

Em investigações e recuperações mais cuidadosas, o ideal é não realizar análises destrutivas diretamente sobre o dispositivo original.

O procedimento costuma envolver:

1. preservar o dispositivo;
2. criar uma imagem ou clone;
3. calcular e registrar verificações de integridade, quando necessário;
4. analisar a cópia;
5. manter o original sem alterações.

Uma imagem de disco é uma cópia setor a setor ou bloco a bloco do dispositivo, dependendo do método usado.

Isso permite repetir análises sem modificar continuamente a fonte original.

## Ferramentas especializadas

Laboratórios podem utilizar equipamentos e softwares que não fazem parte da realidade da maioria dos estudantes.

Entre as capacidades profissionais estão:

- clonagem controlada de discos instáveis;
- leitura com tratamento avançado de erros;
- acesso especializado ao firmware;
- reconstrução de estruturas internas;
- trabalho direto com chips NAND;
- recuperação de parâmetros do controlador;
- leitura de dispositivos parcialmente defeituosos.

O objetivo do curso não é ensinar o aluno a executar procedimentos físicos perigosos sem estrutura.

É mostrar:

- como essas técnicas existem;
- por que exigem especialização;
- quais são seus limites;
- quando encaminhar o equipamento.

## Não abra um HD comum

Um erro recorrente é abrir um HD em casa para “ver o que aconteceu”.

Isso pode contaminar os pratos com:

- poeira;
- umidade;
- partículas;
- gordura;
- resíduos.

A distância entre a cabeça e a superfície é extremamente pequena. Uma partícula invisível a olho nu pode causar danos graves.  

Laboratórios especializados utilizam ambientes controlados para determinadas intervenções.

## Não faça o chamado “truque do congelador”

Existe um mito antigo de colocar o HD no congelador para fazê-lo voltar a funcionar.

Além de não ser um procedimento técnico confiável, a condensação pode causar:

- oxidação;
- curto-circuito;
- contaminação;
- dano adicional.

Uma recuperação improvisada pode transformar uma falha parcialmente recuperável em perda definitiva.

## S.M.A.R.T.: o dispositivo fala sobre sua própria saúde

Muitos discos oferecem dados por meio do sistema S.M.A.R.T.
Esse conjunto de informações pode incluir indicadores como:

- setores realocados;
- erros de leitura;
- tentativas de correção;
- temperatura;
- horas de funcionamento;
- blocos defeituosos;
- desgaste estimado;
- dados gravados.

Entretanto, S.M.A.R.T. não é uma profecia.  
Um dispositivo pode falhar sem aviso. Outro pode apresentar alertas e continuar funcionando por algum tempo.  

Devemos interpretar esses dados como evidências, não como garantia absoluta.

## Exemplo investigativo: HD com setores realocados

Um computador apresenta:

- travamentos ao abrir arquivos;
- lentidão;
- ruídos incomuns;
- erros de leitura;
- aumento no número de setores realocados.

Hipótese inicial:

```text
O HD pode estar desenvolvendo falha física e substituindo setores problemáticos por áreas de reserva.
```

A conduta correta não é continuar submetendo o disco a testes agressivos indefinidamente.

A prioridade pode ser:

1. salvar os dados importantes;
2. clonar o dispositivo, quando necessário;
3. substituir o disco;
4. analisar posteriormente a causa.

## Exemplo investigativo: SSD lento

Um SSD apresenta queda de desempenho.

Isso não significa automaticamente que está defeituoso.

Hipóteses possíveis:

- pouco espaço livre;
- temperatura elevada;
- cache esgotada;
- firmware;
- interface limitada;
- operação em modo inadequado;
- uso intenso;
- tarefas em segundo plano;
- criptografia;
- coleta de lixo;
- desgaste;
- problema na placa-mãe;
- benchmark inadequado.

Novamente, o sintoma não é o diagnóstico.

## Dentro da Caixa

Vamos analisar uma ficha técnica:

SSD NVMe

Capacidade.............1 TB
Interface..............PCIe 4.0 x4
Protocolo..............NVMe
Leitura sequencial.....7.000 MB/s
Gravação sequencial....5.000 MB/s
NAND...................TLC
TBW....................600 TB
Garantia...............5 anos

### Capacidade

Representa o espaço disponível para armazenamento.

O sistema operacional pode mostrar um valor menor devido à diferença entre formas de cálculo e ao espaço reservado.

### Interface

Indica o meio de comunicação.

Um SSD PCIe 4.0 pode funcionar em uma plataforma mais antiga, mas com limitações, desde que exista compatibilidade física e lógica.

### NVMe

É um protocolo desenvolvido para armazenamento rápido conectado por PCI Express.

Não é sinônimo de formato físico.

Existem SSDs NVMe em diferentes formatos.

### Leitura e gravação sequenciais

Representam desempenho em transferências de grandes blocos contínuos.

Não descrevem sozinhas a experiência completa.

Tarefas reais também dependem de:

- acessos aleatórios;
- latência;
- filas;
- tamanho dos arquivos;
- cache;
- temperatura;
- controlador.

### TLC

Indica uma forma de armazenar múltiplos bits por célula.

Tipos diferentes de NAND envolvem compromissos entre:

- custo;
- densidade;
- velocidade;
- durabilidade.

### TBW

Significa uma quantidade estimada de terabytes gravados dentro das condições de garantia.

Não representa uma data exata de falha.

## Mito ou Evidência?
### “Formatar destrói todos os dados”  

**Mito.**

Uma formatação rápida normalmente reconstrói estruturas do sistema de arquivos sem necessariamente sobrescrever cada área do dispositivo.

Em SSDs, TRIM e criptografia podem alterar bastante o cenário.

### “Se o CrystalDiskInfo mostrar bom, o disco está perfeito”

**Mito.**

Os dados S.M.A.R.T. são úteis, mas não detectam todas as falhas.

### “Instalar o programa de recuperação no mesmo disco é arriscado”

**Evidência.**

A instalação pode sobrescrever áreas que ainda continham dados recuperáveis.

### “Um arquivo apagado de SSD nunca pode ser recuperado”

**Mito.**

Pode ser muito mais difícil, especialmente após TRIM, mas o resultado depende do cenário.

### “Backup é mais importante que recuperação”

**Evidência.**

Recuperação é incerta. Backup é planejamento.

## O que um perito observaria?

Em uma análise profissional, perguntas importantes seriam:

- O dispositivo é HD ou SSD?
- Está sendo reconhecido pela BIOS ou pelo sistema?
- Existe criptografia?
- O TRIM estava ativo?
- O computador continuou sendo utilizado?
- Houve formatação?
- O dispositivo apresenta ruídos?
- Existem erros S.M.A.R.T.?
- A falha é lógica, eletrônica, mecânica ou de firmware?
- Há necessidade de preservar valor probatório?
- Uma imagem do dispositivo já foi criada?
- As ações realizadas foram documentadas?
- O equipamento pertence ao solicitante ou existe autorização formal?

A última pergunta é essencial.

Investigação não significa acesso irrestrito.

**Dados só devem ser analisados com autorização legítima.**

## Laboratório guiado — diagnóstico seguro

Esta atividade não envolve apagar nem recuperar arquivos importantes.

### Etapa 1 — Identificação

Abra uma ferramenta como CrystalDiskInfo e registre:

- fabricante;
- modelo;
- interface;
- temperatura;
- horas de funcionamento;
- quantidade de inicializações;
- saúde apresentada;
- total de gravações, quando disponível.

### Etapa 2 — Observação

Analise se existem:

- alertas;
- temperaturas elevadas;
- atributos críticos;
- comportamento incomum;
- diferenças entre os dispositivos instalados.

### Etapa 3 — Hipótese

Exemplo:

O SSD apresenta temperatura elevada durante cargas prolongadas, o que pode estar causando redução temporária de desempenho.

### Etapa 4 — Teste controlado

Observe a temperatura em repouso e durante uma tarefa moderada. Não execute testes agressivos em um dispositivo que já apresenta sinais de falha.

### Etapa 5 — Registro

Documente:

- ferramenta utilizada;
- data;
- condições do teste;
- resultados;
- limitações;
- conclusão provisória.

Esse registro fará parte do Dossiê da Investigação.

## Estudo de caso

Um usuário apagou uma pasta de fotografias em um computador com SSD.  

Depois disso:

- esvaziou a Lixeira;
- continuou usando o computador por dois dias;
- instalou três programas de recuperação no mesmo SSD;
- copiou novos vídeos para o dispositivo;
- executou uma atualização do sistema.

Ao buscar ajuda, pergunta se existe garantia de recuperação.

### Análise

Não existe garantia.

As atividades posteriores podem ter:

- sobrescrito áreas anteriormente ocupadas;
- acionado processos internos do SSD;
- contribuído para a limpeza de blocos;
- alterado metadados;
- reduzido as chances de recuperação.

A conduta mais adequada teria sido interromper o uso imediatamente e avaliar a criação de uma cópia do dispositivo.

## Curiosidade técnica — pesquisas em memória flash

Pesquisadores e laboratórios podem estudar a recuperação de dados em memória flash analisando:

- organização física das células;
- páginas e blocos;
- códigos de correção de erros;
- mapeamento lógico;
- tradução feita pelo controlador;
- wear leveling;
- coleta de lixo;
- criptografia;
- estruturas proprietárias do firmware.

Em certos casos, o acesso direto aos chips produz dados brutos que ainda precisam ser reconstruídos. Não basta simplesmente “ler o chip”, é necessário compreender como o controlador distribuiu, codificou, corrigiu e reorganizou as informações.  

Essa complexidade explica por que uma recuperação profissional de SSD pode ser muito mais difícil do que parece.  

## O princípio mais importante desta aula

**A melhor recuperação de dados é aquela que não precisa acontecer.**

A principal proteção contra perda continua sendo uma estratégia adequada de backup.  

Uma prática conhecida é a regra 3-2-1:

- três cópias dos dados;
- em dois tipos de mídia;
- uma cópia mantida fora do ambiente principal.

Ela não elimina todos os riscos, mas reduz bastante a dependência de processos incertos de recuperação.