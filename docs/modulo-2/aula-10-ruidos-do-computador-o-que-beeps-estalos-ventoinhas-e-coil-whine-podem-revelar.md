# Módulo 2 — Investigação Computacional I
## Anatomia do Hardware

# Aula 10 — Ruídos do Computador: O Que Beeps, Estalos, Ventoinhas e Coil Whine Podem Revelar?

> **Pergunta da investigação**
>
> Quando um computador começa a emitir sons diferentes, como descobrir se estamos diante de um comportamento normal, de uma pista diagnóstica ou de um sinal para interromper imediatamente o uso?

---

# 📁 Dossiê da Investigação

## Caso nº 009 — O computador que “cantava” durante os jogos

Um computador funciona normalmente em tarefas leves.

Ao iniciar um jogo, porém, um ruído agudo aparece quase imediatamente.

Quando a taxa de quadros aumenta, o som também muda.

Ao limitar o jogo para 60 FPS, o ruído diminui.

Ao sair do jogo, desaparece quase por completo.

O usuário conclui:

> “A fonte está queimando.”

Outro técnico afirma:

> “É a placa de vídeo.”

Um terceiro sugere trocar todas as ventoinhas.

Mas nenhuma dessas conclusões foi demonstrada.

O som pode estar associado a componentes magnéticos da fonte, da placa de vídeo ou da placa-mãe. Pode ser uma ressonância mecânica. Pode vir de uma ventoinha. Pode variar com a carga sem representar falha iminente.

Agora imagine outro cenário.

O computador produz um estalo forte, surge cheiro de queimado e o vídeo desaparece.

Os dois casos envolvem ruído.

Mas exigem respostas completamente diferentes.

Nesta aula aprenderemos a tratar sons como **evidências**, e não como diagnósticos automáticos.

---

# Objetivos da aula

Ao final desta aula, você deverá ser capaz de:

- compreender por que computadores produzem sons diferentes;
- classificar ruídos mecânicos, aerodinâmicos, hidráulicos e elétricos;
- interpretar códigos sonoros de inicialização sem tratá-los como universais;
- reconhecer ruídos típicos de ventoinhas, rolamentos, HDs e bombas;
- compreender o fenômeno conhecido como *coil whine*;
- diferenciar coil whine de sinais elétricos potencialmente perigosos;
- correlacionar ruído com carga, temperatura, rotação e consumo;
- utilizar gravações e monitoramento para documentar defeitos intermitentes;
- entender quando um ruído exige apenas observação e quando exige interrupção imediata do uso;
- construir uma investigação acústica sem recorrer a desmontagens perigosas.

---

# O som também é uma evidência

Durante um diagnóstico, normalmente observamos:

- imagem;
- temperatura;
- desempenho;
- logs;
- tensões informadas pelos sensores;
- comportamento do sistema operacional.

Mas nossos ouvidos também recebem informações.

Um computador pode produzir sons devido a:

- movimento de ar;
- vibração mecânica;
- motores;
- rolamentos;
- cabeças de leitura de discos rígidos;
- bombas;
- componentes magnéticos;
- expansão térmica;
- contato entre peças;
- falhas elétricas.

Isso significa que o som pode indicar **qual subsistema está se comportando de maneira diferente**.

Mas existe uma regra fundamental:

> **O som ajuda a localizar e caracterizar o problema, mas raramente identifica sozinho a causa definitiva.**

---

# Antes de investigar: descreva o som corretamente

Expressões como:

- “está fazendo barulho”;
- “está estranho”;
- “parece que vai explodir”;

são compreensíveis para um usuário, mas são pouco precisas tecnicamente.

O investigador tenta registrar características mais objetivas.

## Tipo de som

Exemplos:

- agudo;
- grave;
- metálico;
- vibratório;
- repetitivo;
- pulsante;
- contínuo;
- intermitente;
- clique;
- estalo;
- raspagem;
- assobio;
- zumbido;
- chiado;
- gorgolejo.

## Momento em que aparece

- ao pressionar o botão de energia;
- durante o POST;
- ao iniciar o sistema operacional;
- em repouso;
- durante jogos;
- durante renderização;
- ao copiar arquivos;
- depois de alguns minutos;
- ao suspender ou despertar o computador.

## Comportamento

- aumenta com a carga;
- acompanha a rotação das ventoinhas;
- acompanha o FPS;
- aparece somente com o gabinete fechado;
- muda quando a temperatura aumenta;
- ocorre apenas na primeira inicialização;
- surge depois de movimentar o equipamento.

Essas relações são mais importantes que tentar imitar o som com palavras.

---

# Uma classificação útil dos ruídos

Podemos organizar boa parte dos sons de um computador em cinco grupos:

```text
Ruídos do computador
        │
        ├── Sonoros programados
        │      └── beeps / alertas
        │
        ├── Mecânicos
        │      ├── ventoinhas
        │      ├── rolamentos
        │      └── discos rígidos
        │
        ├── Aerodinâmicos
        │      └── movimento de ar
        │
        ├── Hidráulicos
        │      └── bombas e líquido de AIO
        │
        └── Elétricos / eletromecânicos
               ├── coil whine
               ├── transformadores / indutores
               └── falhas elétricas
```

A classificação não é perfeita, mas ajuda a construir hipóteses.

---

# Beeps de inicialização

Antes de existir vídeo na tela, algumas placas-mãe conseguem comunicar problemas por meio de sinais sonoros.

Esses sinais podem ser emitidos por:

- speaker interno;
- buzzer integrado;
- dispositivo conectado ao cabeçalho da placa-mãe.

Em alguns sistemas, a sequência pode representar uma falha detectada durante o POST.

Exemplos de categorias que podem ser indicadas incluem:

- memória;
- processador;
- vídeo;
- inicialização;
- alimentação;
- ausência de determinado componente.

Mas existe um detalhe extremamente importante:

> **Não existe um código de beeps universal válido para todas as placas-mãe.**

A interpretação depende de fatores como:

- fabricante;
- firmware;
- plataforma;
- geração;
- implementação específica.

Portanto, ouvir três beeps não autoriza concluir automaticamente:

> “Memória RAM queimada.”

Primeiro devemos consultar:

- manual da placa-mãe;
- documentação oficial;
- código correspondente ao modelo e firmware utilizados.

---

# Beep code indica etapa, não necessariamente peça queimada

Imagine que a documentação relacione determinado código à memória.

Ainda existem diferentes possibilidades:

- módulo mal encaixado;
- slot com problema;
- incompatibilidade;
- perfil de memória instável;
- contato inadequado do processador;
- controlador de memória;
- firmware;
- módulo realmente defeituoso.

O código informa onde o processo encontrou dificuldade.

Ele não substitui a investigação.

Esse princípio é o mesmo que aprendemos com os LEDs CPU, DRAM, VGA e BOOT da placa-mãe.

---

# Nem todo computador possui speaker

Um computador pode falhar no POST e permanecer completamente silencioso.

Isso não significa que a placa-mãe não detectou o problema.

Ela pode utilizar:

- LEDs de diagnóstico;
- display de códigos;
- indicadores visuais;
- mensagens na tela;
- registros de firmware.

Em algumas máquinas, simplesmente não existe um dispositivo sonoro instalado.

---

# Ventoinhas: o som mais comum do computador

Ventoinhas possuem partes móveis.

Consequentemente, são uma das fontes mais frequentes de ruído.

Elas podem estar presentes em:

- gabinete;
- processador;
- placa de vídeo;
- radiador;
- fonte;
- chipset em alguns projetos.

O som produzido pode vir de diferentes mecanismos.

---

# Ruído do movimento de ar

Uma ventoinha saudável ainda produz som.

Parte dele vem simplesmente do ar atravessando:

- grades;
- filtros;
- dissipadores;
- radiadores;
- cabos;
- painéis restritivos.

Quanto maior a rotação, maior tende a ser o ruído aerodinâmico.

Isso pode produzir um som semelhante a:

> “whoosh”

ou a um fluxo contínuo de ar.

Não é necessariamente defeito.

---

# Turbulência

Quando o ar encontra obstáculos muito próximos das pás, podem surgir sons diferentes.

Exemplos:

- grade muito próxima;
- filtro restritivo;
- painel frontal fechado;
- cabos posicionados diante da ventoinha;
- duas ventoinhas interferindo entre si.

O problema pode estar na geometria do fluxo, e não na ventoinha em si.

---

# Rolamentos

A ventoinha precisa girar em torno de um eixo.

Para isso utiliza algum sistema de rolamento.

Com desgaste, contaminação ou dano mecânico, podem aparecer:

- ronco;
- raspagem;
- vibração;
- ruído irregular;
- dificuldade para iniciar;
- mudança do som conforme a posição do gabinete.

Uma ventoinha que passa a produzir ruído mecânico diferente do comportamento histórico merece inspeção.

---

# Ventoinha tocando em cabo

Um dos problemas mais simples pode produzir um som bastante alarmante.

Uma ponta de cabo pode encostar nas pás.

O resultado pode ser:

- batidas rápidas;
- estalos repetitivos;
- vibração;
- redução de rotação.

A inspeção deve ser feita com segurança.

Não coloque dedos ou objetos em uma ventoinha girando para tentar descobrir a origem do som.

Com o equipamento desligado e desconectado, podemos verificar visualmente:

- posição dos cabos;
- folgas;
- parafusos;
- filtros;
- presença de objetos soltos.

---

# Parafusos e ressonância

Às vezes a ventoinha está perfeitamente saudável, mas transmite vibração para o gabinete.

O gabinete pode funcionar como uma caixa de ressonância.

O resultado é um ruído muito maior que aquele produzido diretamente pela ventoinha.

Possíveis fatores:

- parafusos frouxos;
- painel lateral vibrando;
- filtro encostando no gabinete;
- suporte metálico;
- HD transmitindo vibração;
- ventoinha desalinhada.

Uma pista importante é o som aparecer apenas em determinada faixa de RPM.

Exemplo:

```text
900 RPM  → silencioso
1100 RPM → vibração forte
1300 RPM → vibração diminui
```

Isso sugere uma frequência de ressonância estrutural.

---

# A rotação pode ser uma variável investigativa

Ferramentas como HWiNFO e o próprio firmware podem mostrar RPM de ventoinhas compatíveis.

Se o ruído aparece exatamente quando uma ventoinha passa de 1.000 para 1.200 RPM, encontramos uma correlação importante.

Em sistemas compatíveis, uma curva de ventoinha pode ser ajustada temporariamente para observar a relação entre:

- RPM;
- temperatura;
- ruído.

A alteração deve ser conservadora e monitorada.

Não devemos reduzir a refrigeração a níveis inseguros apenas para “ver se o barulho some”.

---

# Modo Zero RPM

Algumas placas de vídeo e fontes podem parar suas ventoinhas quando a carga é baixa.

Então o comportamento pode ser:

```text
Repouso
→ ventoinhas paradas
→ praticamente sem ruído de ar

Carga
→ temperatura aumenta
→ ventoinhas iniciam
→ ruído aparece
```

Esse início repentino pode assustar quem não conhece o recurso.

Por isso é importante entender o projeto antes de classificar um comportamento como falha.

---

# Discos rígidos: máquinas eletromecânicas

Ao contrário de um SSD, o HDD possui componentes móveis.

Entre eles:

- motor dos pratos;
- conjunto de cabeças;
- atuador;
- mecanismos de posicionamento.

Por isso, um disco rígido normalmente produz algum som durante funcionamento.

---

# Sons normais de um HDD

Dependendo do modelo, podem existir:

- som de rotação;
- pequenos movimentos durante leitura;
- atividade mais perceptível durante acesso intenso;
- som relacionado ao estacionamento das cabeças.

Um HDD completamente silencioso não é uma referência universal.

O que importa é comparar:

- comportamento atual;
- comportamento histórico;
- desempenho;
- erros;
- dados S.M.A.R.T.;
- capacidade de leitura.

---

# Cliques repetitivos em HDD

Cliques fortes, repetitivos e acompanhados de dificuldade de leitura podem indicar um problema sério.

Possíveis causas envolvem:

- tentativa repetida de posicionamento;
- falha de leitura;
- problema no conjunto de cabeças;
- dano de superfície;
- alimentação inadequada;
- firmware;
- falha eletrônica ou mecânica.

A expressão popular **click of death** é usada para descrever alguns desses comportamentos, mas não deve ser tratada como diagnóstico técnico específico.

Dois discos diferentes podem clicar por motivos diferentes.

---

# Quando um HDD começa a fazer ruído anormal

Se existem dados importantes, a prioridade muda.

O objetivo deixa de ser:

> “Vamos testar até descobrir exatamente o defeito.”

E passa a ser:

> **“Vamos reduzir o risco de perder os dados.”**

Repetir dezenas de testes em um disco mecanicamente degradado pode piorar a situação.

Se houver:

- ruído novo e forte;
- lentidão extrema;
- erros de leitura;
- desaparecimento do disco;
- travamentos de I/O;
- dados importantes sem backup;

uma abordagem profissional pode exigir interrupção do uso e avaliação de recuperação de dados.

Isso se conecta diretamente à Aula 4 deste módulo.

---

# CrystalDiskInfo e S.M.A.R.T.

Em um HDD ainda detectado e estável o suficiente para análise lógica, ferramentas como CrystalDiskInfo podem fornecer informações como:

- horas de funcionamento;
- temperatura;
- setores realocados;
- erros registrados;
- indicadores de saúde;
- contadores específicos do fabricante.

Entretanto:

> **S.M.A.R.T. não ouve o disco e não garante que um componente mecânico esteja saudável.**

Um HDD pode apresentar comportamento anormal antes que um indicador simplificado fique vermelho.

Da mesma forma, um atributo alterado precisa ser interpretado dentro do contexto do dispositivo.

---

# E o SSD?

SSDs não possuem:

- pratos;
- cabeças;
- motor de rotação.

Portanto, eles não deveriam produzir cliques mecânicos de leitura como um HDD.

Se um usuário afirma:

> “Meu SSD está clicando.”

precisamos localizar melhor o som.

Ele pode vir de:

- ventoinha próxima;
- placa-mãe;
- placa de vídeo;
- fonte;
- componente eletrônico vibrando;
- gabinete.

Componentes eletrônicos próximos podem emitir ruído, mas não devemos atribuir automaticamente um clique ao armazenamento apenas porque o som parece vir daquela região.

---

# Bombas de water cooler AIO

Sistemas líquidos adicionam outra fonte possível de ruído: a bomba.

Dependendo do projeto, podemos ouvir:

- leve vibração;
- som contínuo de funcionamento;
- breve presença de bolhas após movimentação;
- mudanças de som com a rotação.

Mas sons anormais também podem indicar problemas.

---

# Gorgolejo e bolhas

Como aprendemos na aula de refrigeração, sistemas fechados podem conter alguma quantidade de ar.

Após transporte ou alteração de posição, pequenas bolhas podem se deslocar.

Isso pode produzir temporariamente:

- gorgolejo;
- pequenos ruídos de circulação.

Mas ruído persistente acompanhado de:

- temperatura elevada;
- bomba com rotação irregular;
- perda de desempenho térmico;

merece investigação.

A orientação física do radiador e da bomba também pode influenciar onde o ar se acumula.

---

# Bomba não deve trabalhar sem líquido

Uma bomba depende do fluido para operar conforme o projeto.

Não devemos testar um sistema líquido desmontado fazendo a bomba funcionar “seca” apenas para verificar se gira.

Isso pode danificá-la.

A investigação deve respeitar as orientações do fabricante e utilizar monitoramento seguro.

---

# HWiNFO e velocidade da bomba

Em sistemas compatíveis, o firmware ou softwares de monitoramento podem informar a rotação da bomba.

Isso permite correlacionar:

- ruído;
- RPM;
- temperatura da CPU;
- carga.

Mas uma leitura de RPM existente não prova que a circulação esteja perfeita.

Assim como em outros sensores:

> **é uma evidência, não uma garantia.**

---

# Coil whine

Agora chegamos a um dos ruídos mais confundidos com defeito elétrico.

*Coil whine* é o nome popular dado a um som agudo associado à vibração de componentes magnéticos submetidos a correntes variáveis.

Pode ocorrer em:

- placa de vídeo;
- fonte;
- placa-mãe;
- outros circuitos de alimentação.

Os componentes envolvidos podem incluir:

- indutores;
- bobinas;
- transformadores.

---

# Por que uma bobina pode produzir som?

Circuitos de alimentação trabalham com chaveamento em frequências elevadas.

As forças eletromagnéticas podem produzir pequenas vibrações mecânicas nos componentes e em seus materiais.

Quando parte dessa vibração ou de suas modulações cai dentro da faixa audível, ouvimos um som.

O resultado pode ser:

- assobio;
- chiado agudo;
- zumbido;
- mudança de tonalidade conforme a carga.

---

# Por que coil whine pode acompanhar o FPS?

Uma GPU pode alterar rapidamente sua carga elétrica conforme a quantidade e o tipo de trabalho executado.

Em determinadas cenas, especialmente quando a taxa de quadros é muito alta, o comportamento elétrico do VRM também muda.

Assim, pode ocorrer uma relação como:

```text
Menu do jogo
500 FPS
→ ruído agudo forte

Jogo limitado
60 FPS
→ ruído bem menor
```

Isso não significa que “os quadros por segundo produzem som”.

O que muda é o padrão de carga elétrica do sistema.

---

# Coil whine significa que o componente vai queimar?

Não necessariamente.

Um equipamento pode apresentar coil whine e continuar funcionando normalmente por anos.

A presença do som, isoladamente, não comprova:

- curto;
- sobrecarga;
- falha iminente;
- alimentação inadequada.

Entretanto, o nível de ruído pode ser considerado um problema de qualidade ou conforto acústico.

Também precisamos investigar sinais adicionais.

---

# Coil whine pode mudar ao trocar a fonte?

Sim.

O comportamento acústico de um circuito pode depender da interação entre:

- placa de vídeo;
- fonte;
- carga;
- tensão;
- frequência de chaveamento;
- projeto dos reguladores.

Por isso uma GPU pode produzir determinado ruído em uma máquina e comportamento diferente em outra.

Isso não significa automaticamente que uma das fontes esteja defeituosa.

---

# Limitar FPS pode reduzir coil whine

Se o ruído é claramente associado a cenas com centenas de quadros por segundo, limitar a taxa de quadros pode modificar a carga e reduzir o som.

Esse teste é interessante porque é:

- reversível;
- não invasivo;
- fácil de documentar.

Se o som muda imediatamente junto com o FPS, encontramos uma forte correlação com a carga gráfica.

Mas ainda precisamos localizar qual componente está emitindo o ruído.

---

# Coil whine não é a mesma coisa que arco elétrico

Essa distinção é fundamental.

Um som agudo estável que acompanha a carga pode ser coil whine.

Já sinais como:

- estalos elétricos;
- faíscas;
- cheiro de material queimando;
- fumaça;
- conector derretido;
- falha imediata;

exigem outra resposta.

> **Pare de utilizar o equipamento e interrompa a alimentação com segurança.**

Não continue executando benchmarks para “ver se acontece de novo”.

---

# Estalo único ao ligar ou desligar

Um pequeno som pode ter diferentes origens, incluindo:

- relé;
- expansão ou contração de materiais;
- mecanismo interno de algum dispositivo;
- sistema de áudio;
- alimentação.

Por isso, o contexto é essencial.

Um clique previsível e documentado pelo projeto pode ser normal.

Um estalo novo acompanhado de cheiro, fumaça ou falha não deve ser normalizado.

---

# Zumbido em 50 ou 60 Hz

Alguns equipamentos elétricos podem produzir um zumbido grave relacionado à frequência da rede elétrica ou a seus harmônicos.

Entretanto, localizar e diagnosticar esse tipo de ruído dentro de fontes e circuitos ligados à rede exige conhecimento e instrumentos adequados.

Não abrimos uma fonte para investigar o som.

Como vimos na Aula 6:

> **capacitores internos podem manter energia perigosa mesmo depois de o equipamento ser desconectado.**

A análise interna de fontes deve ser realizada por profissional qualificado.

---

# A fonte de alimentação pode produzir vários sons diferentes

Possíveis fontes acústicas incluem:

- ventoinha;
- rolamento;
- fluxo de ar;
- coil whine;
- relé em determinados projetos;
- vibração mecânica.

Então a frase:

> “Está vindo da fonte.”

não encerra a investigação.

Ainda precisamos caracterizar o tipo de som e verificar se existem sinais de risco.

---

# Nunca abra a fonte para localizar o ruído

Essa regra merece ser repetida.

Não devemos:

- remover a tampa;
- tocar componentes internos;
- medir diretamente o lado da rede sem treinamento;
- improvisar descargas de capacitores;
- introduzir ferramentas em uma fonte energizada.

Podemos investigar externamente:

- quando o som aparece;
- se acompanha carga;
- se acompanha a ventoinha;
- se há cheiro;
- se existem desligamentos;
- se há sinais visíveis nos conectores externos;
- se outra fonte conhecida e adequada altera o comportamento.

---

# Ruído e temperatura devem ser analisados juntos

Considere duas máquinas.

## Máquina A

- ventoinhas muito audíveis;
- temperaturas normais;
- clocks estáveis;
- sem travamentos.

Hipótese inicial:

- curva de ventoinha agressiva;
- gabinete restritivo;
- projeto acústico.

## Máquina B

- ventoinhas praticamente silenciosas;
- CPU atingindo limite térmico;
- clocks caindo;
- ventoinha reportando 0 RPM.

Aqui o silêncio não é uma qualidade.

Ele pode ser evidência de que a refrigeração não está funcionando.

> **Silencioso não significa saudável. Barulhento não significa defeituoso.**

---

# Mudança de ruído após limpeza

Depois de uma manutenção, o computador passa a vibrar.

Isso pode ocorrer se:

- uma ventoinha ficou mal fixada;
- um cabo foi reposicionado perto das pás;
- um filtro não foi encaixado;
- um painel lateral ficou frouxo;
- a máquina foi movimentada e um HDD passou a transmitir mais vibração.

A relação temporal com a intervenção é uma evidência importante.

Sempre que um defeito surge após manutenção, devemos revisar primeiro aquilo que foi alterado.

---

# Mudança de ruído após upgrade

Depois de instalar uma GPU mais potente, o computador fica muito mais barulhento.

Isso pode acontecer mesmo sem defeito.

A nova placa pode:

- consumir mais energia;
- produzir mais calor;
- aquecer o interior do gabinete;
- fazer as ventoinhas da CPU e gabinete acelerarem;
- modificar a carga da fonte;
- introduzir coil whine.

Portanto, o ruído pode ser uma consequência sistêmica do upgrade.

---

# Como localizar um ruído sem desmontar o equipamento energizado

O som pode se refletir no gabinete e enganar nossa percepção.

Uma fonte instalada na parte inferior pode parecer estar emitindo um ruído que realmente vem da GPU.

Um método seguro começa com observação externa.

Registre:

- posição aparente do som;
- momento em que surge;
- relação com carga;
- relação com RPM;
- relação com FPS;
- temperatura;
- consumo informado;
- alterações recentes.

Depois, altere uma variável segura por vez.

---

# O princípio da correlação

Imagine que o ruído aparece durante um jogo.

Você observa:

```text
GPU em 20%  → ruído quase ausente
GPU em 60%  → ruído moderado
GPU em 99%  → ruído forte
```

Essa correlação sugere relação com a carga gráfica.

Mas ainda não sabemos se a origem é:

- GPU;
- fonte;
- ventoinha da GPU;
- ventoinhas do gabinete reagindo ao calor.

Agora registramos também RPM:

```text
GPU 99%
Ventoinha GPU 30% → ruído agudo permanece
Ventoinha GPU 70% → ruído agudo permanece + fluxo de ar aumenta
```

Isso pode reduzir a suspeita de que o som agudo venha exclusivamente das pás.

O diagnóstico avança por eliminação de hipóteses.

---

# Não segure ventoinhas com os dedos

Uma prática inadequada é tocar nas pás para descobrir qual ventoinha está fazendo ruído.

Isso pode:

- machucar;
- quebrar pás;
- danificar o motor;
- introduzir objetos no equipamento energizado.

Se precisamos correlacionar uma ventoinha com o som, utilizamos métodos seguros, como:

- controle por software quando suportado;
- curva temporária no firmware;
- inspeção com o equipamento desligado;
- teste isolado realizado de forma apropriada fora da situação de risco.

---

# O smartphone como instrumento de documentação

Um telefone pode ser extremamente útil durante uma investigação.

Podemos registrar:

- áudio;
- vídeo;
- horário;
- comportamento visual;
- posição aproximada do ruído.

Uma gravação permite comparar:

- antes e depois;
- máquina fria e quente;
- repouso e carga;
- FPS livre e limitado;
- gabinete aberto e fechado, quando seguro e pertinente.

Isso é muito melhor do que depender da memória:

> “Acho que ontem fazia um barulho diferente.”

---

# Limitações da gravação do celular

O microfone de um smartphone possui:

- processamento automático;
- redução de ruído;
- controle de ganho;
- resposta de frequência limitada;
- compressão.

Portanto, ele não é instrumento de metrologia acústica.

Uma gravação serve principalmente para:

- documentação;
- comparação;
- identificação de padrões.

Não devemos interpretar a intensidade registrada como medição profissional de decibéis.

---

# Espectrograma

Softwares de áudio, como Audacity, podem representar um som em função de:

- tempo;
- frequência;
- intensidade relativa.

Um espectrograma pode ajudar a observar se determinado ruído possui:

- frequência relativamente estável;
- múltiplos harmônicos;
- mudanças associadas à carga;
- pulsos repetitivos.

Isso pode ser interessante pedagogicamente para comparar:

- ventoinha;
- coil whine;
- clique;
- ruído de HDD.

Mas um pico em determinada frequência não identifica automaticamente qual componente o produziu.

---

# Ventoinha e frequência do som

Uma ventoinha girando possui uma frequência mecânica relacionada à rotação.

Porém o som percebido não depende apenas do número de rotações.

Também influenciam:

- quantidade de pás;
- geometria;
- turbulência;
- rolamentos;
- ressonância;
- estrutura do gabinete.

Assim, transformar RPM diretamente em “frequência do ruído” seria uma simplificação inadequada.

---

# Vibração do gabinete

Uma vibração pode ser transmitida por:

- ventoinha;
- HDD;
- bomba;
- transformador;
- painel solto.

O gabinete pode amplificá-la.

Isso explica por que um componente parece silencioso quando testado em outra estrutura, mas produz ruído em determinada montagem.

Materiais, pressão dos parafusos e pontos de contato modificam a resposta mecânica.

---

# Ruído de expansão térmica

Materiais aquecem e se expandem.

Ao esfriar, contraem.

Em alguns equipamentos podem ocorrer pequenos estalos devido a mudanças dimensionais em:

- plástico;
- metal;
- dissipadores;
- carcaças.

Esse comportamento pode aparecer após:

- carga intensa;
- desligamento;
- resfriamento.

Mais uma vez, o contexto diferencia um pequeno estalo estrutural de um evento elétrico acompanhado por cheiro ou falha.

---

# Alto-falantes também podem confundir o diagnóstico

Ruídos percebidos “no computador” podem vir do sistema de áudio.

Exemplos:

- interferência;
- aterramento;
- cabo de áudio;
- amplificador;
- caixa de som;
- entrada analógica;
- dispositivo USB.

Um chiado que desaparece ao mutar ou desconectar o sistema de áudio externo pode não ter relação com ventoinhas ou VRM.

A cadeia precisa ser isolada.

---

# Sons do sistema operacional não são beeps de POST

Windows, Linux e outros sistemas podem reproduzir alertas por meio dos alto-falantes.

Esses sons são diferentes de códigos emitidos pelo firmware durante a inicialização.

Pergunta investigativa importante:

> O som existe antes mesmo de o sistema operacional carregar?

Essa diferença ajuda a localizar a camada responsável.

---

# Logs e som podem ser correlacionados

Imagine que um estalo ou perda momentânea de vídeo ocorre às 19:42.

Se registrarmos o horário, podemos procurar no sistema eventos próximos, como:

- reinicialização de driver;
- desligamento inesperado;
- erro de armazenamento;
- falha de aplicativo;
- evento de energia.

A ausência de log não elimina uma falha física.

Mas a correlação temporal pode ser extremamente valiosa.

---

# Estudo de Caso 1 — Ruído agudo somente em menus de jogo

Sintomas:

- jogo normal durante partidas;
- menu chega a centenas de FPS;
- ruído agudo aparece no menu;
- limitar para 120 FPS reduz o som imediatamente;
- temperaturas normais;
- nenhum travamento.

A relação entre o som e a carga elétrica variável torna coil whine uma hipótese forte.

Ainda precisamos localizar se o ruído vem da placa de vídeo ou da fonte.

Não há evidência suficiente para afirmar que qualquer uma delas esteja prestes a falhar.

---

# Estudo de Caso 2 — Vibração em determinada rotação

Sintomas:

- computador silencioso em repouso;
- entre 1.050 e 1.150 RPM surge vibração grave;
- acima de 1.300 RPM o ruído diminui;
- temperaturas normais.

Hipótese importante:

- ressonância mecânica do gabinete ou de algum painel.

A ventoinha pode estar saudável e apenas excitar uma frequência estrutural específica.

---

# Estudo de Caso 3 — Cliques e arquivos demorando para abrir

Sintomas:

- HDD antigo;
- cliques repetitivos;
- sistema congela ao acessar determinadas pastas;
- cópias apresentam erros;
- não existe backup atualizado.

Aqui a prioridade não é executar testes agressivos.

A prioridade é preservar os dados e reduzir a atividade desnecessária do disco.

O ruído, combinado com erros de I/O, muda completamente o nível de risco.

---

# Estudo de Caso 4 — Gorgolejo após transportar o computador

Sintomas:

- computador com AIO;
- ruído de líquido começou após transporte;
- temperaturas continuam normais;
- bomba reporta rotação consistente;
- som diminui após algum tempo de funcionamento.

É possível que o transporte tenha deslocado pequenas bolhas.

Isso não comprova defeito da bomba.

Mas se o ruído persistir e vier acompanhado de piora térmica, o sistema deve ser investigado com mais profundidade.

---

# Estudo de Caso 5 — Estalo, cheiro e desligamento

Sintomas:

- estalo forte;
- computador desliga;
- cheiro de material queimado;
- não inicializa novamente.

A resposta correta não é:

> “Vamos ligar outra vez para reproduzir.”

Esse cenário possui sinais de possível falha elétrica.

O equipamento deve permanecer desligado até avaliação segura.

---

# Estudo de Caso 6 — Ventoinha raspando somente com gabinete em pé

Sintomas:

- gabinete deitado: ruído praticamente desaparece;
- gabinete em posição normal: raspagem retorna;
- rotação oscila;
- ventoinha é antiga.

A mudança com a orientação sugere um problema mecânico relacionado ao eixo ou rolamento.

Essa é uma evidência muito mais específica do que simplesmente dizer que “o computador faz barulho”.

---

# Estudo de Caso 7 — Som após troca da GPU

Antes do upgrade:

- computador relativamente silencioso.

Depois:

- maior fluxo de ar;
- ventoinhas do gabinete aceleram;
- fonte também aumenta a ventilação;
- surge leve coil whine em FPS elevado.

Não existe um único ruído novo.

Todo o perfil acústico da máquina mudou porque:

- consumo aumentou;
- calor aumentou;
- ventilação aumentou;
- comportamento elétrico mudou.

O computador deve ser analisado como sistema.

---

# Mito ou Evidência?

### “Todo coil whine indica defeito grave.”

**Mito.**

Pode ser um comportamento acústico do circuito sem falha funcional.

---

### “Três beeps sempre significam defeito na memória RAM.”

**Mito.**

Os códigos dependem da implementação do firmware e da placa-mãe.

---

### “Um HDD pode produzir sons durante funcionamento normal.”

**Evidência.**

Ele possui componentes eletromecânicos.

---

### “Cliques novos acompanhados de erros de leitura merecem atenção imediata.”

**Evidência.**

Especialmente quando existem dados importantes sem backup.

---

### “Se a ventoinha faz barulho, ela necessariamente está quebrada.”

**Mito.**

O som pode vir do próprio fluxo de ar ou de ressonância estrutural.

---

### “Um ruído que muda junto com o FPS pode fornecer uma pista sobre a carga elétrica da GPU.”

**Evidência.**

Essa correlação é típica em alguns casos de coil whine.

---

### “Se a fonte está fazendo ruído, podemos abri-la para localizar a peça.”

**Mito perigoso.**

A investigação interna de fontes exige profissional qualificado.

---

### “Cheiro de queimado, fumaça ou faíscas mudam imediatamente a prioridade da investigação.”

**Evidência.**

A segurança passa a ser prioridade absoluta.

---

# Como um laboratório profissional investigaria um ruído?

Dependendo do problema, um laboratório pode utilizar:

- microfones de medição;
- analisadores de espectro;
- acelerômetros;
- câmera térmica;
- osciloscópio;
- fontes de bancada em circuitos apropriados;
- instrumentos de vibração;
- inspeção microscópica;
- equipamentos para teste de rolamentos e motores.

Em eletrônica de potência, a investigação pode correlacionar:

- frequência de chaveamento;
- carga;
- corrente;
- vibração;
- temperatura.

Em um HDD, laboratórios de recuperação podem avaliar:

- comportamento mecânico;
- capacidade de leitura;
- erros;
- estabilidade do conjunto;

sem submeter o dispositivo a tentativas desnecessárias de inicialização.

O aluno não precisa possuir esses instrumentos para compreender o método.

---

# 🔬 Laboratório guiado — construindo um mapa acústico do computador

Esta atividade é não invasiva e deve ser realizada apenas em um computador que não apresente sinais de risco elétrico ou mecânico grave.

## Etapa 1 — Estado de referência

Registre:

```text
Computador:
CPU:
GPU:
Fonte:
Armazenamento:
Cooler:
Quantidade de ventoinhas:
Temperatura ambiente aproximada:
```

Observe o computador em repouso.

Registre:

- sons presentes;
- rotação das ventoinhas;
- temperatura;
- uso de CPU;
- uso de GPU;
- atividade de armazenamento.

---

## Etapa 2 — Identificar quando o ruído aparece

Utilize uma tarefa conhecida e segura.

Pode ser:

- abrir aplicações;
- copiar um arquivo não crítico;
- executar um jogo;
- reproduzir vídeo;
- realizar uma tarefa de CPU moderada.

O objetivo não é levar o computador ao limite.

O objetivo é descobrir se o som depende da carga.

---

## Etapa 3 — Registrar sensores

Com HWiNFO ou ferramenta equivalente, acompanhe quando disponível:

- CPU;
- GPU;
- temperaturas;
- RPM;
- consumo;
- uso de armazenamento.

Anote o instante em que o ruído começa.

---

## Etapa 4 — Registrar áudio e vídeo

Utilize o smartphone para documentar:

- som em repouso;
- som durante a condição que reproduz o defeito;
- posição aproximada do ruído;
- comportamento do computador no mesmo momento.

Mantenha distância segura das partes móveis.

---

## Etapa 5 — Alterar uma variável segura

Exemplos:

- limitar FPS;
- mudar temporariamente uma curva de ventoinha dentro de limites seguros;
- executar a mesma tarefa com carga gráfica menor;
- comparar gabinete aberto e fechado quando isso puder ser feito com segurança.

Não altere várias variáveis ao mesmo tempo.

---

## Etapa 6 — Construir uma tabela de correlação

Exemplo:

| Condição | GPU | Ventoinha GPU | FPS | Ruído |
|---|---:|---:|---:|---|
| Área de trabalho | 5% | 0 RPM | — | Quase ausente |
| Jogo limitado | 70% | 1.200 RPM | 60 | Leve |
| Jogo sem limite | 98% | 1.250 RPM | 350 | Agudo forte |

Observe que a rotação praticamente não mudou entre os dois últimos testes, mas o FPS e a carga elétrica mudaram muito.

Isso fortalece a hipótese de um ruído eletromecânico, como coil whine, em vez de simples ruído aerodinâmico das ventoinhas.

---

# Registro para o Dossiê da Investigação

Ao documentar um caso acústico, registre pelo menos:

```text
Sintoma relatado:
Som observado:
Momento em que aparece:
Duração:
Carga associada:
Temperaturas:
RPM:
Alterações recentes:
Sinais de risco presentes ou ausentes:
Testes não invasivos realizados:
Variável alterada em cada teste:
Resultado observado:
Hipótese principal:
Hipóteses ainda possíveis:
Ação recomendada:
```

Esse registro prepara o aluno para a próxima etapa do módulo: transformar observações dispersas em um procedimento técnico completo.

---

# Quando interromper imediatamente o uso

Alguns sinais alteram completamente a prioridade do diagnóstico.

Pare o equipamento e evite novas tentativas de carga quando houver:

- fumaça;
- cheiro de queimado;
- faíscas;
- estalos elétricos fortes;
- cabo ou conector derretido;
- ruído mecânico violento;
- ventoinha quebrada atingindo outros componentes;
- vazamento de líquido;
- choque ou sensação elétrica no gabinete;
- HDD com ruído anormal associado a dados críticos e erros graves de leitura.

O objetivo deixa de ser reproduzir o sintoma.

Passa a ser preservar:

- pessoas;
- equipamento;
- dados;
- evidências.

---

# Quando o ruído pode ser apenas uma característica do projeto

Alguns comportamentos podem ser normais dentro de determinado equipamento:

- fluxo de ar em alta carga;
- ventoinhas acelerando;
- leve funcionamento de bomba;
- atividade mecânica típica de HDD;
- clique de relé previsto pelo projeto;
- coil whine sem instabilidade funcional.

Isso não significa que todo ruído deva ser ignorado.

O investigador compara:

- documentação;
- histórico;
- intensidade;
- mudança recente;
- sintomas associados.

A palavra-chave é **contexto**.

---

# O que um perito observaria?

Um investigador experiente não perguntaria apenas:

> “De onde vem o barulho?”

Ele procuraria estabelecer relações:

- O som aparece antes do sistema operacional?
- Existe código sonoro documentado pelo fabricante?
- O ruído acompanha RPM?
- Acompanha FPS?
- Acompanha atividade do HDD?
- Muda com temperatura?
- Surgiu depois de manutenção?
- Surgiu após transporte?
- Surgiu após upgrade?
- Existe cheiro?
- Há perda de desempenho?
- Existem travamentos?
- Há registros no sistema no mesmo horário?
- O som é mecânico, aerodinâmico, hidráulico ou elétrico?
- O equipamento pode continuar operando com segurança?
- Existem dados que precisam ser preservados antes de novos testes?

A investigação acústica segue exatamente o mesmo método das demais aulas:

> **Sintoma → observação → evidência → hipótese → teste controlado → conclusão provisória → validação.**

---

# Conexão com a próxima investigação

Até agora investigamos componentes individuais:

```text
CPU
RAM
Armazenamento
Placa-mãe
Fonte
Refrigeração
GPU
Monitor
Cabos
Ruídos
```

Mas um computador real não chega à bancada dizendo:

> “Meu problema está exatamente no subsistema de memória.”

O cliente normalmente diz algo como:

> “Ele não liga.”

> “Está lento.”

> “Reinicia sozinho.”

> “Às vezes dá tela preta.”

> “Ontem fez um barulho estranho.”

Na próxima aula deixaremos de investigar componentes isoladamente.

Vamos receber uma máquina desconhecida e construir uma sequência profissional para decidir:

```text
O que observar primeiro?
        ↓
O que preservar?
        ↓
Qual teste vem antes?
        ↓
Quando desmontar?
        ↓
Quando testar software?
        ↓
Quando trocar uma peça de referência?
        ↓
Como separar hipótese de diagnóstico?
```

# Próxima aula — Da Bancada ao Diagnóstico: Como Investigar um Computador Desconhecido

Essa será a aula em que todo o conhecimento do módulo começará a funcionar como um único método de trabalho.