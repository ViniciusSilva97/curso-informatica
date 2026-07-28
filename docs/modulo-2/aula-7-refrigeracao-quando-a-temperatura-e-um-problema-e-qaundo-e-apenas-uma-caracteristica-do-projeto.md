# Aula 7 — Refrigeração: quando a temperatura é um problema e quando é apenas uma característica do projeto?

Pergunta da investigação
```text
Uma CPU operando a 90 °C está necessariamente superaquecendo?
```
## Dossiê da Investigação
Caso nº 006 — O water cooler que quase não mudou a temperatura.  

Um usuário percebeu que seu processador atingia temperaturas elevadas durante renderizações.  

O computador utilizava:

- processador de alto desempenho;
- cooler a ar intermediário;
- gabinete com painel frontal fechado;
- duas ventoinhas;
- pasta térmica aplicada havia poucos meses.

Preocupado, ele comprou um water cooler caro. Após a instalação, repetiu o teste. A diferença máxima foi de apenas 3 °C.

O usuário concluiu:  

**“O water cooler está com defeito.”**

Essa conclusão é válida?

- Talvez o processador esteja usando a margem térmica disponível para alcançar clocks maiores. 
- Talvez o gabinete esteja limitando a entrada de ar.
- Talvez a bomba esteja configurada incorretamente.
- Talvez o teste anterior e o posterior tenham ocorrido em condições diferentes.
- Ou talvez uma redução pequena seja exatamente o resultado esperado naquele cenário.

Hoje investigaremos como o computador produz, transfere e remove calor.

## Objetivos da aula

Ao final desta aula, você será capaz de:

- compreender por que componentes eletrônicos produzem calor;
- diferenciar temperatura, potência térmica e capacidade de refrigeração;
- interpretar temperaturas dentro do contexto do componente;
- entender condução, convecção e radiação térmica;
- reconhecer o papel do dissipador, da pasta térmica e das ventoinhas;
- comparar coolers a ar e sistemas líquidos;
- identificar sinais de thermal throttling;
- investigar problemas de fluxo de ar;
- utilizar softwares gratuitos para coletar evidências;
- reconhecer diagnósticos que exigem inspeção física;
- evitar práticas que podem danificar componentes.

## Todo computador converte energia em calor

Quando um componente eletrônico funciona, parte da energia elétrica utilizada transforma-se em calor.  

Isso ocorre em:

- processadores;
- placas de vídeo;
- reguladores de tensão;
- SSDs;
- memórias;
- fontes;
- chipsets;
- controladores;
- motores e bombas.

Quanto maior a atividade elétrica, maior tende a ser a geração térmica.

Em termos simplificados:  

Energia elétrica  
       ↓  
Trabalho computacional  
       +  
Calor  

O problema não é o componente produzir calor. Isso é esperado!  
O problema surge quando o calor não consegue ser transferido para fora com velocidade suficiente.  

## Temperatura não é a mesma coisa que calor

Esses conceitos são frequentemente tratados como sinônimos, mas não são.

### Temperatura

Indica o estado térmico de um corpo. Pode ser medida em graus Celsius.

## Energia térmica

Representa a quantidade de energia associada ao movimento e à interação das partículas. Um componente pequeno pode atingir temperatura muito alta mesmo contendo menos energia térmica total que um objeto muito maior.

## Potência térmica

Indica a taxa com que o calor é gerado ou removido.

Pode ser relacionada a **watts**. Um processador que dissipa mais energia exige um sistema capaz de transferir essa potência térmica continuamente.

### Uma analogia importante

Imagine duas panelas.

A primeira contém pouca água e recebe uma chama forte, a segunda contém muita água e recebe uma chama fraca.  
A primeira pode atingir uma temperatura alta rapidamente, embora possua menos água. Nos computadores, ocorre algo semelhante!

Um pequeno chip pode concentrar grande quantidade de potência em uma área reduzida. Essa concentração dificulta a transferência de calor.

## O caminho do calor

O calor produzido dentro do processador precisa atravessar várias camadas antes de chegar ao ambiente.

Transistores do processador  
           ↓  
Silício  
           ↓  
Material de interface interno  
           ↓  
Espalhador metálico  
           ↓  
Pasta térmica  
           ↓  
Base do cooler  
           ↓  
Heatpipes ou bloco líquido  
           ↓  
Dissipador ou radiador  
           ↓  
Ar do gabinete  
           ↓  
Ambiente  

Cada etapa oferece alguma resistência à passagem do calor.Se uma delas estiver inadequada, a temperatura pode aumentar.  

## Os três mecanismos de transferência térmica
### Condução

É a transferência de calor através do contato entre materiais.

Exemplos:

- chip para o espalhador metálico;
- espalhador para a pasta térmica;
- pasta térmica para o cooler;
- base do cooler para os heatpipes.

A qualidade do contato influencia diretamente essa transferência.

### Convecção

É a transferência de calor pelo movimento de um fluido. Nos computadores, normalmente esse fluido é o ar.
Também ocorre em sistemas líquidos, onde o fluido circula entre o bloco e o radiador.

Exemplos:

- ventoinha movimentando ar pelo dissipador;
- ar quente saindo do gabinete;
- líquido transportando calor até o radiador.

### Radiação térmica

É a emissão de energia em forma de radiação eletromagnética. Ela existe, mas em computadores convencionais costuma ter importância menor que condução e convecção no sistema principal de refrigeração.

## O processador não tenta permanecer sempre frio

Processadores modernos controlam dinamicamente:

- frequência;
- tensão;
- consumo;
- limites de potência;
- temperatura;
- número de núcleos ativos.

Quando existe margem elétrica e térmica, o processador pode aumentar seu desempenho. Isso significa que a instalação de um cooler melhor nem sempre produz grande redução de temperatura.  

O processador pode utilizar a capacidade adicional para:

- manter clocks mais altos;
- sustentar o boost por mais tempo;
- entregar mais desempenho;
- consumir mais energia dentro dos limites configurados.

Assim, duas situações podem apresentar a mesma temperatura, mas desempenhos diferentes.
```text
Cooler inferior
90 °C
Clock reduzido

Cooler superior
90 °C
Clock mais alto e sustentado
```
Observar apenas a temperatura pode esconder o ganho real.

## Uma temperatura alta é necessariamente perigosa?

Não podemos responder sem contexto.

Precisamos saber:

- qual é o componente;
- qual é o modelo;
- qual sensor está sendo lido;
- qual é o limite definido pelo fabricante;
- qual é a carga;
- por quanto tempo a temperatura permanece elevada;
- se existe redução de clock;
- qual é a temperatura ambiente;
- como o sistema está configurado;
- se a medição está correta.

Um processador pode ser projetado para operar próximo de seu limite térmico durante cargas intensas. Por outro lado, uma temperatura menor pode ser problemática se estiver acompanhada de:

- instabilidade;
- falha de sensor;
- desligamentos;
- componentes periféricos superaquecidos;
- bomba parada;
- falta de contato;
- degradação de desempenho.

A temperatura isolada é apenas uma evidência.

## O que é thermal throttling?

***Thermal throttling*** é a redução automática de desempenho causada por uma condição térmica. Quando o componente se aproxima de determinado limite, ele pode diminuir:

- frequência;
- tensão;
- potência;
- desempenho.

O objetivo é evitar que a temperatura continue subindo de forma descontrolada. 

Carga elevada  
     ↓  
Temperatura aumenta  
     ↓  
Limite térmico alcançado  
     ↓  
Clock é reduzido  
     ↓  
Geração de calor diminui  

Essa proteção não significa que seja desejável operar continuamente no limite em qualquer situação. Ela é uma camada de segurança e controle.

## Como identificar thermal throttling?

Possíveis evidências:

- queda de clock durante carga contínua;
- temperatura próxima do limite;
- indicador térmico ativado no software;
- redução de potência;
- desempenho inferior ao esperado;
- pontuação de benchmark diminuindo ao longo das repetições;
- recuperação do clock após queda de temperatura.

Ferramentas como HWiNFO podem mostrar indicadores relacionados a limites térmicos e de potência. Porém, a interpretação depende do processador e da plataforma.

## Limite térmico e limite de potência não são a mesma coisa

Um processador pode reduzir seu desempenho por diferentes motivos.

### Limite térmico

A temperatura atingiu o limite definido.

### Limite de potência

O processador atingiu a potência máxima permitida pela configuração.

### Limite elétrico

O sistema atingiu alguma restrição de corrente ou tensão.

### Limite de firmware

A placa-mãe ou o fabricante definiu parâmetros específicos.

### Limite de carga

O programa não consegue utilizar mais recursos, assim observar redução de clock não prova automaticamente que o cooler seja insuficiente.

## O papel do dissipador

O dissipador aumenta a área disponível para transferir calor ao ar. Uma peça metálica lisa teria área limitada.  

Ao adicionar aletas, a superfície cresce significativamente.  

Bloco simples:  
████████  

Dissipador com aletas:  
||||||||||||||||||||  

Quanto maior a área útil e melhor o fluxo de ar, maior tende a ser a capacidade de remover calor.

Os materiais mais comuns incluem:

- alumínio;
- cobre;
- combinações dos dois.

O cobre possui boa condutividade térmica, mas é mais pesado e caro. O alumínio é leve, econômico e amplamente utilizado.

## Heatpipes

Muitos coolers a ar utilizam tubos de calor, conhecidos como heatpipes. Eles contêm uma pequena quantidade de fluido em ambiente selado.

O processo simplificado é:

1. o fluido absorve calor na região quente;
2. evapora;
3. desloca-se para a região mais fria;
4. condensa;
5. retorna pela estrutura interna do tubo.

Esse ciclo transporta calor da base para as aletas do dissipador. O heatpipe não é apenas um tubo sólido de metal.  

Ele utiliza mudança de fase para melhorar a transferência térmica.

## Câmara de vapor

Uma câmara de vapor utiliza princípio semelhante ao heatpipe, mas distribui o calor em uma área mais ampla.

Pode ser encontrada em:

- placas de vídeo;
- notebooks;
- dispositivos compactos;
- coolers de alto desempenho.

Ela ajuda a espalhar o calor de uma pequena área para uma superfície maior.

## Para que serve a pasta térmica?

Mesmo superfícies metálicas aparentemente lisas possuem irregularidades. Quando o cooler encosta no processador, pequenos espaços podem permanecer preenchidos por ar.  

O ar conduz calor de maneira muito inferior aos materiais usados na interface térmica. A pasta térmica preenche essas irregularidades.  

Sem pasta:  

Metal   ar   Metal  
████   ░░░   ████  

Com pasta:  

Metal  pasta  Metal  
██████████████████  

A função da pasta não é criar uma camada grossa é substituir o ar nos pequenos espaços.

## Mais pasta térmica melhora a refrigeração?

Não necessariamente. Aplicar pouca pasta pode deixar regiões sem cobertura adequada.  

Aplicar quantidade excessiva pode:

- criar uma camada desnecessariamente espessa;
- dificultar o contato;
- espalhar material para áreas externas;
- causar problemas se o composto for eletricamente condutivo;
- produzir sujeira e dificultar manutenção.

O objetivo é obter cobertura adequada com uma camada fina e uniforme após a pressão do cooler. Não existe um único método universal para todos os formatos de processador e compostos.

Podem ser usados métodos como:

- pequeno ponto central;
- linha;
- padrão específico;
- espalhamento manual;
- aplicação recomendada pelo fabricante.

A melhor orientação é considerar:

- formato do processador;
- viscosidade da pasta;
- tamanho da base;
- instruções do cooler;
- recomendações do fabricante.

## Pasta térmica não corrige pressão inadequada

Mesmo uma pasta excelente não compensa:

- suporte frouxo;
- montagem incorreta;
- película protetora esquecida;
- base desalinhada;
- parafusos apertados de forma desigual;
- cooler incompatível;
- suporte deformado.

O contato mecânico é fundamental.

## A película esquecida

Alguns coolers vêm com uma película de proteção sobre a base. Ela deve ser removida antes da instalação.

Se permanecer, pode causar:

- temperatura elevada;
- subida rápida de temperatura;
- throttling;
- desligamento;
- desempenho reduzido.

Esse é um exemplo de problema simples que pode produzir sintomas semelhantes aos de um cooler defeituoso.

## Ventoinhas: mais rotação não é o único fator

A capacidade de uma ventoinha não depende apenas das rotações por minuto.

Outros fatores incluem:

- diâmetro;
- desenho das pás;
- pressão estática;
- fluxo de ar;
- ruído;
- distância;
- obstruções;
- rolamento;
- controle por PWM ou tensão.

## Fluxo de ar e pressão estática
### Fluxo de ar

Indica a quantidade de ar movimentada.

É importante em áreas mais abertas, como entrada e exaustão do gabinete.

### Pressão estática

Indica a capacidade de empurrar o ar através de resistência.

É especialmente relevante em:

- radiadores;
- dissipadores densos;
- filtros;
- painéis restritivos.

Uma ventoinha com alto fluxo em ambiente aberto pode ter desempenho limitado ao enfrentar um radiador muito denso.

## PWM e controle por tensão
### Controle por tensão

A velocidade é alterada modificando a tensão aplicada.

É comum em ventoinhas de três pinos.

### PWM

Utiliza um sinal de controle para regular a velocidade. É comum em modelos de quatro pinos.

O sistema pode ajustar a rotação de acordo com:

- temperatura da CPU;
- temperatura da placa-mãe;
- sensor externo;
- curva personalizada.

Uma ventoinha pode estar fisicamente funcional, mas configurada com uma curva inadequada.

## Cooler a ar

Um cooler a ar normalmente utiliza:

- base;
- heatpipes;
- torre de aletas;
- uma ou mais ventoinhas.

### Vantagens
- construção relativamente simples;
- menor número de pontos de falha;
- manutenção reduzida;
- bom desempenho em muitos cenários;
- funcionamento mesmo sem bomba;
- fácil inspeção visual.

### Limitações
- tamanho;
- peso;
- possível interferência com memória;
- dependência do fluxo de ar do gabinete;
- distribuição térmica condicionada ao projeto.

## Water cooler do tipo AIO

Um sistema líquido fechado normalmente possui:

- bloco sobre o processador;
- bomba;
- mangueiras;
- radiador;
- ventoinhas;
- líquido interno.

O líquido transporta o calor do bloco até o radiador. No radiador, o calor é transferido para o ar.

Processador  
    ↓  
Bloco  
    ↓  
Líquido aquecido  
    ↓  
Radiador  
    ↓  
Ar movimentado pelas ventoinhas  

### Water cooler não elimina a necessidade de ar

Esse é um erro comum. O sistema líquido apenas transporta o calor até o radiador. O calor ainda precisa ser entregue ao ambiente por meio do ar.

Portanto, um water cooler depende de:

- radiador adequado;
- ventoinhas;
- fluxo de ar;
- bomba funcional;
- montagem correta.

Ele não “faz o calor desaparecer”.

### Pontos de falha de um AIO

Possíveis falhas incluem:

- bomba parada;
- bomba com rotação incorreta;
- bolhas em posição inadequada;
- perda gradual de líquido;
- obstrução interna;
- desgaste;
- ruído;
- ventoinhas paradas;
- radiador coberto por poeira;
- montagem incorreta;
- conector elétrico inadequado;
- curva de rotação mal configurada.

Nem toda falha é visível externamente.

### A posição do radiador importa?

Sim, porque existe ar dentro de muitos sistemas fechados.O objetivo geral é evitar que a bomba permaneça como o ponto mais alto do circuito, onde bolhas podem se acumular.

#### A posição ideal depende:

- do projeto;
- do gabinete;
- da orientação;
- do comprimento das mangueiras;
- da localização da bomba.

Não existe uma única orientação válida para todos os sistemas, mas o princípio físico deve ser respeitado.

## O gabinete participa da refrigeração

Um cooler poderoso pode ter desempenho limitado em um gabinete com entrada de ar restrita.

Possíveis obstáculos:

- painel frontal fechado;
- filtro muito restritivo;
- cabos bloqueando o fluxo;
- poucas entradas de ar;
- exaustão insuficiente;
- ventoinhas invertidas;
- radiador aquecendo o interior;
- gabinete encostado na parede;
- poeira acumulada.

O cooler não trabalha isoladamente, ele faz parte de um sistema térmico.

## Pressão positiva e negativa
### Pressão positiva

Entra mais ar do que sai por meio das ventoinhas. O excesso tende a escapar pelas aberturas.  
Pode ajudar a reduzir entrada de poeira por frestas quando as entradas possuem filtros.

### Pressão negativa

Sai mais ar do que entra. O gabinete puxa ar por diversas aberturas. Isso pode aumentar a entrada de poeira em locais sem filtragem.

### Pressão equilibrada

Entrada e saída permanecem próximas. Na prática, o comportamento depende da resistência dos filtros, do gabinete e das ventoinhas, não basta contar quantas ventoinhas existem.

## Direção correta das ventoinhas

A maioria das ventoinhas movimenta o ar da face mais aberta para o lado onde ficam as hastes estruturais e a etiqueta traseira.

Entretanto, existem modelos de fluxo reverso.

A confirmação deve ser feita por:

- setas no corpo;
- documentação;
- teste de fluxo;
- identificação do modelo.

Uma ventoinha invertida pode quebrar completamente a estratégia de circulação.

## Um gabinete cheio de ventoinhas pode ser pior?

**Sim.** Mais ventoinhas sem planejamento podem criar:

- turbulência;
- recirculação de ar quente;
- ruído excessivo;
- competição entre fluxos;
- pressão inadequada;
- entrada de poeira;
- benefício mínimo.

O objetivo não é instalar a maior quantidade possível.  

É criar um caminho eficiente:  

Ar fresco entra   
       ↓  
Passa pelos componentes  
       ↓  
Absorve calor  
       ↓  
Ar quente sai  

## Temperatura ambiente

Nenhum sistema convencional consegue resfriar o componente abaixo da temperatura do ar de entrada sem utilizar técnicas específicas. Se o ambiente está mais quente, a temperatura dos componentes tende a subir.

Por isso, comparar dois testes exige registrar:

- temperatura ambiente;
- local;
- horário;
- ventilação;
- carga;
- duração;
- configuração.

Uma diferença de 5 °C no ambiente pode alterar significativamente o resultado.

## Temperatura absoluta e diferença térmica

Uma forma útil de comparar é observar a diferença entre a temperatura do componente e a temperatura ambiente.

Exemplo:
```text
Teste A
CPU: 80 °C
Ambiente: 20 °C
Diferença: 60 °C

Teste B
CPU: 83 °C
Ambiente: 28 °C
Diferença: 55 °C
```
Embora a CPU do teste B esteja mais quente em valor absoluto, o sistema de refrigeração pode estar funcionando melhor em relação ao ambiente.

## Dentro da Caixa

Vamos analisar um cooler:

- Tipo..................Cooler a ar
- Altura................158 mm
- Heatpipes.............6
- Ventoinha.............140 mm
- Controle..............PWM
- Rotação máxima........1.500 RPM
- Compatibilidade.......AM5, AM4 e LGA1700
- Altura para memória...variável conforme a posição
- Capacidade declarada..não padronizada entre fabricantes

### Altura

Deve ser compatível com a largura disponível no gabinete.

Um cooler de 158 mm pode não caber em gabinetes que aceitam apenas 155 mm.

### Heatpipes

A quantidade ajuda a descrever o projeto, mas não determina sozinha o desempenho.

Importam também:

- diâmetro;
- contato;
- distribuição;
- qualidade;
- área do dissipador;
- ventoinha.

### Ventoinha de 140 mm

Pode movimentar bastante ar com rotação menor, mas depende do projeto.

### Compatibilidade

O socket precisa ser suportado, mas também devem ser verificados:

- kit de montagem;
- revisão;
- espaço;
- memória;
- placa de vídeo;
- orientação.

### Capacidade térmica declarada

Não existe um método universal usado por todos os fabricantes para declarar capacidade térmica. Comparações diretas exigem testes independentes em condições semelhantes.

## Ferramentas gratuitas
### HWiNFO

Pode apresentar:

- temperatura por núcleo;
- temperatura do pacote;
- clocks;
- potência;
- consumo;
- limites térmicos;
- rotação de ventoinhas;
- velocidade da bomba;
- sinais de throttling.

### HWMonitor

Oferece uma visualização mais simples de vários sensores.É útil para observação inicial, mas deve ser interpretado com cautela quando algum sensor parecer incorreto.

### Core Temp

Focado principalmente em informações térmicas da CPU.

### GPU-Z

Pode monitorar:

- temperatura da GPU;
- temperatura de memória em modelos compatíveis;
- hotspot;
- carga;
- clocks;
- rotação das ventoinhas;
- limites de desempenho.

### Fan Control

Permite criar curvas de ventoinhas em sistemas compatíveis.

É útil para:

- reduzir ruído;
- reagir a diferentes sensores;
- ajustar entrada e exaustão;
- controlar ventoinhas conforme CPU ou GPU.

Configurações incorretas podem reduzir a refrigeração.

### BIOS ou UEFI

Pode permitir:

- monitoramento;
- curvas de ventoinha;
- modos PWM e tensão;
- alertas;
- controle da bomba;
- limites térmicos;
- configuração de potência.

### Testes de carga

Para investigar refrigeração, podemos utilizar cargas controladas. Exemplos conhecidos incluem ferramentas que exercitam CPU ou GPU. Porém, testes intensos exigem cautela.

Antes de executá-los, verifique:

- estabilidade inicial;
- funcionamento das ventoinhas;
- temperatura em repouso;
- ausência de cheiro ou ruído anormal;
- cooler corretamente instalado;
- capacidade da fonte;
- possibilidade de encerrar o teste;
- importância dos dados abertos.

Um dispositivo que já apresenta sinais de falha não deve ser submetido automaticamente a testes extremos.

Benchmark não é diagnóstico completo

### Um benchmark pode ajudar a comparar:

- desempenho;
- temperatura;
- estabilidade;
- clocks;
- repetibilidade.

Mas o resultado depende de:

- versão do programa;
- configuração;
- temperatura ambiente;
- processos em segundo plano;
- firmware;
- memória;
- limites de potência;
- sistema operacional.

Um número isolado não constitui diagnóstico.

## Como realizar um teste comparável
### Etapa 1 — Registrar o ambiente
- temperatura ambiente;
- gabinete fechado ou aberto;
- posição;
- quantidade de ventoinhas;
- perfil de energia.
### Etapa 2 — Estabilizar o sistema

Aguardar alguns minutos em repouso.

### Etapa 3 — Registrar valores iniciais
- temperatura;
- clocks;
- rotação;
- potência;
- ruído.
### Etapa 4 — Aplicar a mesma carga

Utilizar o mesmo programa, versão, duração e configuração.

### Etapa 5 — Observar o comportamento
- temperatura máxima;
- temperatura estabilizada;
- clocks;
- throttling;
- potência;
- rotação;
- estabilidade.
### Etapa 6 — Alterar apenas uma variável

Por exemplo:

- trocar a curva;
- remover temporariamente o painel frontal;
- reposicionar uma ventoinha;
- reinstalar o cooler.

### Etapa 7 — Repetir

Sem controlar as variáveis, não existe comparação confiável.

## Diagnóstico com o painel frontal removido

Uma técnica simples para investigar restrição de entrada de ar é comparar o sistema:

- com o painel frontal instalado;
- com o painel frontal removido temporariamente.

Se a temperatura cair significativamente, isso sugere que a entrada de ar pode estar limitada. Essa técnica não prova que o gabinete seja defeituoso, ela mostra que o fluxo de entrada está influenciando o resultado.

## Diagnóstico com a lateral aberta

Abrir a lateral pode ajudar a investigar o fluxo interno. 
### Se a temperatura cair muito. 
Pode existir:

- entrada insuficiente;
- exaustão inadequada;
- recirculação;
- ventoinhas mal posicionadas;
- painel restritivo.
### Se a temperatura aumentar

A abertura pode ter interrompido um fluxo interno eficiente.

Novamente, a evidência precisa ser interpretada.

## Estudo de Caso 1 — CPU chega rapidamente ao limite

### Sintomas:

- temperatura sobe em segundos;
- clock cai;
- ventoinha está girando;
- cooler foi instalado recentemente;
- temperatura em repouso também está alta.

### Hipóteses:

- película protetora não removida;
- pressão inadequada;
- pasta térmica ausente;
- suporte incorreto;
- bomba parada;
- conector errado;
- leitura incorreta do sensor;
- limite de potência elevado.

A velocidade da subida térmica é uma evidência importante.

## Estudo de Caso 2 — Temperatura alta apenas após 20 minutos

### Sintomas:

- temperatura inicial normal;
- aumento progressivo;
- gabinete aquece;
- ar quente permanece no interior;
- exaustão fraca.

### Hipóteses:

- saturação térmica do gabinete;
- fluxo insuficiente;
- radiador recebendo ar quente;
- filtro obstruído;
- baixa rotação das ventoinhas;
- ambiente quente.

Nesse caso, o cooler pode estar transferindo calor corretamente, mas o gabinete não consegue removê-lo.

## Estudo de Caso 3 — Water cooler novo reduz apenas 3 °C

### Evidências:

- clock médio aumentou;
- consumo aumentou;
- processador manteve boost por mais tempo;
- temperatura final permaneceu próxima;
- ambiente estava 2 °C mais quente no segundo teste.

### Conclusão provável:

O novo sistema pode estar oferecendo mais capacidade térmica, utilizada pelo processador para sustentar maior desempenho, sem produzir grande queda na temperatura máxima.  

A análise correta deve comparar desempenho, potência, clocks e ambiente.

## Estudo de Caso 4 — Computador desliga após trocar a pasta térmica

### Sintomas:

- sistema funcionava antes;
- cooler foi removido;
- após a manutenção, a CPU aquece rapidamente;
- o computador desliga.

### Hipóteses:

- cooler mal fixado;
- cabo da ventoinha desconectado;
- bomba desconectada;
- suporte instalado incorretamente;
- película mantida;
- pasta insuficiente;
- excesso de força;
- componente deslocado durante a manutenção.

O fato de o problema surgir imediatamente após uma intervenção aumenta a relevância dessa alteração na investigação.

## Estudo de Caso 5 — GPU quente e CPU normal

### Configuração:

- gabinete compacto;
- placa de vídeo de alta potência;
- CPU com cooler adequado;
- poucas entradas inferiores;
- GPU próxima do painel.

### Evidências:

- CPU: temperatura normal;
- GPU: temperatura elevada;
- hotspot muito acima da temperatura média;
- ventoinhas da GPU em alta rotação;
- melhora significativa com a lateral aberta.

### Hipóteses:

- entrada de ar insuficiente para a GPU;
- recirculação do ar quente;
- pasta térmica ou pads;
- dissipador sujo;
- contato inadequado;
- curva de ventoinha;
- gabinete restritivo.

Cada componente pode enfrentar um problema térmico diferente.

## Hotspot da GPU

Algumas GPUs apresentam:

- temperatura média do chip;
- temperatura do ponto mais quente, chamada hotspot.

A diferença entre essas leituras pode ajudar a investigar:

- distribuição térmica;
- contato do dissipador;
- aplicação da interface térmica;
- variação interna do chip.

Uma diferença elevada não produz, sozinha, diagnóstico definitivo é necessário considerar o projeto e os limites do modelo.

## SSD também pode sofrer throttling térmico

SSDs NVMe podem atingir temperaturas elevadas durante cargas intensas. Quando isso ocorre, o controlador pode reduzir o desempenho.

Possíveis fatores:

- ausência de dissipador;
- dissipador com película não removida;
- posição abaixo da GPU;
- pouco fluxo de ar;
- carga prolongada;
- controlador de alto desempenho;
- ambiente quente.

### Sintomas:

- transferência começa rápida;
- velocidade cai após algum tempo;
- temperatura aumenta;
- desempenho retorna após resfriamento.

## Memórias e VRM também precisam de refrigeração

O foco costuma permanecer na CPU e GPU, mas outros componentes podem aquecer.

### VRM

Pode limitar a CPU ou causar instabilidade quando opera acima da capacidade térmica.

### Memória RAM

Perfis elevados de tensão e frequência podem aumentar a temperatura.

### Memória da GPU

Pode exigir contato adequado com pads térmicos e dissipador.

### Chipset

Pode utilizar dissipador ativo ou passivo.

Um sistema aparentemente bem refrigerado na CPU ainda pode ter problemas em outra região.

## Poeira não é apenas uma questão estética

A poeira pode:

- obstruir filtros;
- reduzir passagem de ar;
- cobrir aletas;
- desequilibrar ventoinhas;
- aumentar ruído;
- elevar temperaturas;
- reter umidade;
- contribuir para contaminação.

A limpeza deve ser feita com:

- equipamento desligado;
- cabo removido;
- cuidado contra estática;
- ventoinhas imobilizadas ao usar ar;
- métodos adequados.

Não se deve deixar uma ventoinha girar descontroladamente com jatos de ar. Além de risco mecânico, ela pode gerar tensão no circuito.

## Ar comprimido inadequado

Alguns recipientes podem liberar:

- líquido;
- propelente;
- umidade;
- resíduos.

Compressores também podem lançar água ou óleo se não possuírem filtragem adequada. A limpeza precisa considerar o equipamento utilizado.

## Mito ou Evidência?
### “Quanto menor a temperatura, melhor em qualquer situação”

#### Mito.

Temperatura deve ser avaliada junto com desempenho, ruído, potência e limites do componente.

### “Um water cooler sempre é superior a um cooler a ar”

#### Mito.

O desempenho depende do projeto, radiador, bomba, ventoinhas, gabinete, carga e instalação.

### “Aplicar mais pasta térmica sempre melhora a transferência”

#### Mito.

O excesso pode prejudicar o contato e criar uma camada desnecessária.

### “Abrir a lateral sempre melhora a refrigeração”

#### Mito.

Pode melhorar sistemas com fluxo ruim ou piorar sistemas bem organizados.

### “A temperatura ambiente influencia as medições”

#### Evidência.

Comparações devem considerar o ar de entrada.

### “Uma CPU pode manter a mesma temperatura com cooler melhor e entregar mais desempenho”

#### Evidência.

O processador pode utilizar a margem disponível para elevar clocks e potência.

### “Se a bomba aparece com RPM, o water cooler está necessariamente funcionando corretamente”

#### Mito.

A leitura confirma apenas um sinal informado pelo sistema. Ainda podem existir falhas de circulação, obstrução, bolhas, desgaste ou leitura incorreta.

## O que um perito observaria?
- Qual sensor está sendo analisado?
- Qual é o modelo exato do componente?
- Qual é a temperatura ambiente?
- A carga é reproduzível?
- O problema ocorre em repouso ou sob carga?
- A temperatura sobe instantaneamente ou gradualmente?
- Existe throttling?
- Os clocks caem?
- A potência muda?
- As ventoinhas respondem à temperatura?
- A bomba está conectada ao cabeçalho correto?
- O cooler está pressionado adequadamente?
- A película foi removida?
- O fluxo do gabinete está correto?
- O problema surgiu após alguma intervenção?
- O painel frontal restringe o ar?
- Existe poeira?
- CPU, GPU, SSD, VRM e memória foram analisados separadamente?
- A comparação foi feita nas mesmas condições?
- Existe risco de continuar o teste?

## Quando interromper o teste

Pare imediatamente diante de sinais como:

- cheiro de queimado;
- fumaça;
- bomba emitindo ruído anormal intenso;
- vazamento;
- líquido sobre componentes;
- temperatura subindo sem estabilizar;
- ventoinha travada;
- desligamentos repetidos;
- deformação de conectores;
- estalos;
- falha elétrica.

A prioridade é preservar pessoas, dados e equipamentos.

## Laboratório guiado — mapa térmico do computador

Esta atividade utilizará apenas monitoramento e observação.

### Etapa 1 — Identificação

Registre:

- processador;
- cooler;
- placa de vídeo;
- gabinete;
- quantidade e posição das ventoinhas;
- temperatura ambiente aproximada;
- software utilizado.

### Etapa 2 — Repouso

Após alguns minutos sem carga intensa, registre:

- temperatura da CPU;
- temperatura da GPU;
- temperatura do SSD;
- rotação das ventoinhas;
- clock;
- potência, quando disponível.

### Etapa 3 — Carga moderada

Execute uma tarefa real, como:

- compactar arquivos;
- exportar vídeo curto;
- executar jogo;
- realizar benchmark moderado.

Registre os valores ao longo do tempo.

### Etapa 4 — Observe a curva

Pergunte:

- a temperatura sobe rapidamente?
- estabiliza?
- continua crescendo?
- as ventoinhas aceleram?
- o clock é mantido?
- existe throttling?
- o gabinete expulsa ar quente?

### Etapa 5 — Alteração controlada

Mude apenas uma variável segura.

Exemplos:

- remover temporariamente o painel frontal;
- aumentar a rotação das ventoinhas;
- fechar programas em segundo plano;
- ajustar uma curva segura.

### Etapa 6 — Repetição

Repita a mesma carga e compare.

### Etapa 7 — Conclusão provisória

Exemplo:

A remoção temporária do painel frontal reduziu a temperatura da GPU e do processador, indicando que a entrada de ar do gabinete participa da limitação térmica.