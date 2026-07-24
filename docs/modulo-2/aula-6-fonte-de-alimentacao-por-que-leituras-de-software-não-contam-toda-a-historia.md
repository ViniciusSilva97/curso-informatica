# Aula 6 — Fonte de alimentação: por que leituras de software não contam toda a história?

## Pergunta da investigação

```text
Um programa consegue confirmar que a fonte está funcionando corretamente?
```
## Dossiê da Investigação
Caso nº 005 — O computador que desliga apenas durante jogos

Um cliente relata que o computador funciona normalmente para:

- navegar na Internet;
- editar documentos;
- assistir a vídeos;
- participar de videoconferências.

Entretanto, poucos minutos após iniciar um jogo, o equipamento desliga repentinamente.

- Não aparece tela azul.
- Não surge mensagem de erro.

O computador simplesmente perde energia. Depois de alguns segundos, ele pode ser ligado novamente.  

Ao verificar um programa de monitoramento, o cliente observa:

```text
Linha de 12 V: 12,096 V
Linha de 5 V:   5,040 V
Linha de 3,3 V: 3,328 V
```

Ele conclui:  

**“As tensões estão corretas. Portanto, a fonte não pode ser o problema.”**

Essa conclusão é válida?   

As leituras apresentadas pelo software são realmente medidas diretamente na saída da fonte?  

O defeito pode aparecer apenas quando o computador exige mais energia?  

Hoje investigaremos essas questões.  

## Objetivos da aula

Ao final desta aula, você será capaz de:

- compreender a função real da fonte de alimentação;
- diferenciar potência, tensão, corrente e eficiência;
- interpretar especificações sem depender apenas do valor em watts;
- entender por que leituras de software possuem limitações;
- reconhecer sintomas associados a falhas de alimentação;
- compreender o papel das proteções elétricas;
- diferenciar teste superficial de diagnóstico profissional;
- identificar riscos que exigem encaminhamento especializado;
- avaliar uma fonte com base em projeto, aplicação e evidências.

## A fonte não “cria energia”

É comum ouvir que a fonte “fornece energia ao computador”. A frase é útil, mas precisa ser aprofundada.  

**A fonte recebe energia elétrica da rede e a converte para níveis adequados aos componentes internos.**  

Em uma fonte ATX típica, a energia alternada da tomada é transformada em tensões contínuas utilizadas pelo computador.  

Rede elétrica em corrente alternada  
                ↓  
Filtragem e conversão  
                ↓  
Tensões contínuas controladas  
                ↓  
Placa-mãe, processador, GPU, SSD e demais componentes  

A fonte precisa realizar essa conversão com:

- estabilidade;
- segurança;
- eficiência;
- baixo nível de ruído elétrico;
- capacidade para responder às variações de carga.

Portanto, não basta entregar energia. Ela precisa entregar energia dentro de condições aceitáveis.

## Os quatro conceitos fundamentais

Antes de investigar uma fonte, precisamos separar quatro grandezas frequentemente confundidas.

### Tensão

A tensão elétrica é medida em volts.  

No computador, encontramos linhas como:

- 12 V;
- 5 V;
- 3,3 V.

Uma analogia simples é pensar na tensão como a pressão que impulsiona a corrente pelo circuito.  

### Corrente

A corrente elétrica é medida em amperes. Ela representa o fluxo de carga elétrica.  
Componentes diferentes exigem correntes distintas de acordo com a carga de trabalho.  
Uma placa de vídeo pode solicitar muito mais corrente durante um jogo do que quando está exibindo apenas a área de trabalho.

### Potência

A potência é medida em watts.  

Em corrente contínua, uma relação simplificada é:  

**Potência = Tensão × Corrente**

Exemplo:  

**12 V × 10 A = 120 W**

Isso não significa que uma fonte de 650 W entrega 650 W permanentemente. Esse valor representa sua capacidade nominal dentro das condições especificadas pelo fabricante.  

**O computador consome apenas o que exige em cada momento.**

### Eficiência

Eficiência é a relação entre a energia retirada da tomada e a energia efetivamente entregue ao computador.

Imagine que uma fonte retire 500 W da rede e entregue 450 W aos componentes.  

Eficiência = 450 ÷ 500  
Eficiência = **90%**  

Os 50 W restantes não desaparecem. Grande parte é dissipada como calor durante a conversão.  

Uma fonte mais eficiente tende a:

- desperdiçar menos energia;
- gerar menos calor para a mesma carga;
- exigir menos esforço de refrigeração.

Eficiência, porém, não é sinônimo automático de qualidade geral. Uma fonte pode apresentar boa eficiência em determinadas condições e ainda possuir limitações em outros aspectos do projeto.

## Por que a linha de 12 V é tão importante?

Em computadores modernos, grande parte da potência é utilizada pela linha de 12 V.

Ela alimenta, direta ou indiretamente:

- processador;
- placa de vídeo;
- ventoinhas;
- bombas de sistemas de refrigeração;
- reguladores da placa-mãe;
- reguladores da GPU.

A placa-mãe e a placa de vídeo utilizam circuitos reguladores para converter os 12 V em tensões muito menores, adequadas aos chips.  

Por exemplo:  

Fonte fornece 12 V  
        ↓  
VRM da placa-mãe  
        ↓
Tensão adequada ao processador  

Assim, uma fonte pode apresentar sintomas principalmente quando CPU e GPU aumentam simultaneamente sua demanda.  

## Potência total não conta toda a história

Duas fontes podem anunciar 600 W e serem completamente diferentes.  

### Fonte A
- projeto bem dimensionado;
- componentes de qualidade;
- proteções adequadas;
- boa regulação;
- capacidade real na linha de 12 V;
- documentação clara;
- fabricante identificável.

### Fonte B
- potência de pico usada como propaganda;
- capacidade limitada na linha de 12 V;
- componentes inferiores;
- ausência de proteções;
- etiqueta pouco transparente;
- projeto antigo ou inadequado.

A informação “600 W” sozinha não permite concluir que as duas fontes atendem ao mesmo computador.

## Dentro da Caixa

Vamos analisar uma etiqueta simplificada:

- Potência nominal........650 W
- Entrada.................100–240 V
- Linha +12 V.............54 A
- Potência em +12 V.......648 W
- Linha +5 V..............20 A
- Linha +3,3 V............20 A
- Certificação de eficiência..............80 PLUS Gold
- Formato.................ATX
- Proteções declaradas....OCP, OVP, UVP, SCP, OTP e OPP

Agora vamos interpretar.

### Potência nominal

É a capacidade declarada para operação nas condições definidas pelo fabricante. Precisamos verificar se esse valor corresponde à potência contínua ou apenas a um pico momentâneo.

### Entrada de 100 a 240 V

Indica que a fonte foi projetada para trabalhar em uma ampla faixa de tensão da rede. Em muitos modelos modernos, a seleção é automática.  

Fontes antigas podem possuir chave manual de tensão(saí fora desses modelos kkk). Configurar incorretamente essa chave pode causar danos graves.

### Linha de 12 V com 54 A

Calculando:

```text
12 V × 54 A = 648 W
```

Isso indica que quase toda a potência nominal pode ser entregue pela linha de 12 V.

Essa característica é importante em sistemas modernos.

### 80 PLUS Gold

A certificação informa níveis mínimos de eficiência em condições de teste definidas pelo programa.  

Ela não certifica isoladamente:

- qualidade dos capacitores;
- durabilidade;
- nível de ripple;
- todas as proteções;
- comportamento em transitórios;
- silêncio;
- qualidade geral do projeto.

É uma informação relevante, mas não deve ser utilizada como único critério de compra.

## O que são proteções elétricas?

Uma fonte bem projetada pode incluir mecanismos de proteção.

As siglas mais comuns são:

|Sigla|Função geral|
|-----|-------------|
|OCP    |Proteção contra corrente excessiva|
|OVP	|Proteção contra tensão excessiva|
|UVP	|Proteção contra tensão abaixo do limite|
|OPP	|Proteção contra potência excessiva|
|SCP	|Proteção contra curto-circuito|
|OTP	|Proteção contra temperatura excessiva|

Essas proteções procuram interromper ou limitar o funcionamento quando uma condição perigosa é detectada.

Elas não tornam a fonte indestrutível.

Também não substituem:

- aterramento adequado;
- instalação elétrica correta;
- proteção contra surtos;
- manutenção;
- escolha de potência apropriada.

## Fonte modular, semimodular e não modular
### Não modular

Todos os cabos são fixos.  

Vantagens:

- construção mais simples;
- normalmente menor custo;
- ausência de conectores modulares intermediários.

Desvantagens:

- maior quantidade de cabos dentro do gabinete;
- organização mais difícil.

### Semimodular

Alguns cabos essenciais são fixos e os demais removíveis.  

### Modular

Os cabos podem ser conectados conforme a necessidade.  

Isso facilita:

- organização;
- montagem;
- fluxo de ar;
- substituição de cabos compatíveis.

Mas existe um risco importante.  

**Cabos modulares não são universalmente intercambiáveis.**

Dois cabos podem possuir conectores fisicamente iguais no lado da fonte e, ainda assim, utilizar pinagens diferentes.  

Usar o cabo modular de outro modelo pode causar:  

- curto-circuito;
- queima de SSD;
- danos à placa de vídeo;
- danos à placa-mãe;
- perda de dados.

O cabo deve ser compatível exatamente com a fonte ou oficialmente aprovado pelo fabricante.  

## Conectores não devem ser confundidos
### ATX principal

Alimenta a placa-mãe.

### EPS ou CPU

Alimenta a região responsável pelo processador.

### PCI Express

É usado tradicionalmente em placas de vídeo.

### SATA

Alimenta SSDs, HDs e outros dispositivos compatíveis.

## Conectores modernos de alta potência

Placas de vídeo recentes podem utilizar conectores específicos com maior capacidade.  

Esses conectores exigem:

- encaixe completo;
- cabo adequado;
- ausência de tensão mecânica excessiva;
- curvatura apropriada;
- compatibilidade com a fonte;
- instalação conforme a documentação.

Um conector parcialmente inserido pode aumentar a resistência elétrica e provocar aquecimento.

## O problema dos adaptadores

Adaptadores podem ser úteis em situações específicas, mas também podem introduzir riscos.

Exemplos problemáticos:

- adaptar conectores SATA para alimentação de GPU;
- utilizar cabos de baixa qualidade;
- dividir corrente excessiva em um único cabo;
- empilhar adaptadores;
- usar conectores danificados;
- empregar extensões sem especificação confiável.

O fato de um adaptador permitir o encaixe físico não significa que ele suporte a corrente necessária com segurança.

## Por que a carga muda?

O consumo do computador não é constante.

Em repouso:

- CPU: baixa utilização
- GPU: baixa utilização
- Ventoinhas: rotação reduzida
- Consumo total: menor

Durante um jogo ou renderização:

- CPU: maior carga
- GPU: maior carga
- VRMs: maior trabalho
- Ventoinhas: maior rotação
- Consumo total: maior

Alguns componentes podem apresentar picos de consumo muito rápidos.  

A fonte precisa responder a essas variações sem:

- deixar a tensão cair excessivamente;
- produzir oscilações inadequadas;
- acionar proteções indevidamente;
- perder estabilidade.

Por isso, uma fonte pode funcionar no uso leve e falhar apenas sob carga.

## O que são transitórios?

Um transiente é uma mudança rápida na demanda elétrica. Imagine uma GPU saindo de um estado de baixo consumo para alta carga em poucos instantes.  

A fonte precisa adaptar sua entrega rapidamente.  

Uma unidade inadequada pode:

- desligar;
- apresentar queda momentânea;
- acionar proteção;
- provocar instabilidade.

Esse tipo de comportamento dificilmente será compreendido apenas observando uma leitura estática na tela. 

## A grande limitação das leituras de software

Programas como HWiNFO e ferramentas da placa-mãe podem apresentar valores de tensão. Porém, esses números geralmente vêm de sensores e circuitos de monitoramento da própria placa-mãe.  

Eles não são necessariamente uma medição direta e precisa na saída da fonte.  

O caminho pode ser simplificado assim:  
Fonte  
  ↓  
Placa-mãe  
  ↓  
Circuito sensor  
  ↓  
Controlador de monitoramento  
  ↓  
Firmware ou driver  
  ↓  
Programa  
  ↓  
Valor exibido  

Cada etapa pode introduzir:

- arredondamento;
- atraso;
- calibração imperfeita;
- baixa taxa de amostragem;
- leitura incorreta;
- identificação errada do sensor.

Por isso:
```text
Uma leitura aparentemente normal no software não comprova que a fonte esteja saudável.
```

## O software consegue detectar ripple?

Não de forma confiável por meio dos sensores comuns da placa-mãe.  

### O que é ripple?

Após a conversão da energia, a tensão contínua não é necessariamente uma linha perfeitamente estável.  

Pode existir uma pequena ondulação residual.  

Tensão ideal:
**───────────────**

Tensão com ondulação:
**~─~─~─~─~─~─~─**

Ripple excessivo pode afetar:

- estabilidade;
- vida útil dos componentes;
- reguladores;
- armazenamento;
- funcionamento sob carga.

Para observar adequadamente esse comportamento, laboratórios utilizam instrumentos como **osciloscópio e procedimentos específicos.**  

O multímetro comum normalmente não mostra toda a forma de onda necessária para essa análise.

## O que um multímetro consegue medir?

Um multímetro pode ajudar a verificar:

- presença de tensão;
- valores aproximados nas linhas;
- continuidade;
- determinadas quedas;
- alguns curtos;
- comportamento básico.

Ele pode ser muito mais confiável do que a leitura de software para determinadas verificações. Entretanto, ele não mostra tudo.  

Um multímetro comum pode deixar de revelar:

- oscilações extremamente rápidas;
- ripple detalhado;
- transitórios;
- comportamento dinâmico complexo;
- falhas que ocorrem em milissegundos.

## O que um osciloscópio acrescenta?

O osciloscópio permite observar sinais ao longo do tempo.  

Ele pode revelar:

- ripple;
- ruído;
- quedas momentâneas;
- comportamento durante mudanças de carga;
- instabilidades rápidas.

Mas usar um osciloscópio corretamente exige:

- conhecimento técnico;
- pontas de prova adequadas;
- configuração correta;
- cuidados com aterramento;
- interpretação da forma de onda.

Ter o equipamento não significa automaticamente saber realizar o diagnóstico.

## Testadores simples de fonte

Existem testadores comerciais que verificam se determinadas linhas estão presentes e dentro de uma faixa aproximada.  

Eles podem ser úteis como triagem.  

Porém, apresentam limitações:

- testam com pouca ou nenhuma carga real;
- não reproduzem o comportamento de CPU e GPU;
- não analisam adequadamente ripple;
- podem não revelar falhas intermitentes;
- não avaliam qualidade interna.

Uma fonte pode passar em um testador simples e falhar quando o computador exige potência elevada.  

## O teste do clipe

Algumas pessoas fazem uma ponte em pinos específicos do conector para ligar a fonte fora do computador.  

Esse procedimento é conhecido informalmente como “teste do clipe”.  

O teste apenas pode mostrar que a fonte iniciou e acionou sua ventoinha ou suas saídas básicas.  

Ele não comprova:

- estabilidade;
- potência real;
- qualidade;
- funcionamento sob carga;
- ausência de ripple;
- saúde dos componentes internos.

Além disso, realizar a ponte nos pinos errados pode causar curto-circuito. Neste curso, não trataremos esse procedimento como prova de funcionamento.

## Nunca abra uma fonte de alimentação

Mesmo desconectada da tomada, uma fonte pode manter cargas perigosas em capacitores internos.

Abrir a unidade pode expor o aluno a:

- choque elétrico;
- queimaduras;
- curto-circuito;
- incêndio;
- danos ao equipamento.

**A investigação interna de uma fonte deve ser realizada apenas por profissional qualificado, com conhecimento em eletrônica e procedimentos de segurança.**

Esta aula ensina a compreender a tecnologia e reconhecer seus limites. Ela não autoriza intervenções perigosas.

## Sintomas que podem estar relacionados à fonte

Possíveis sintomas incluem:

- computador não liga;
- desligamento repentino;
- reinicialização sob carga;
- instabilidade em jogos;
- falha ao iniciar a placa de vídeo;
- cheiro de queimado;
- ruído elétrico;
- acionamento frequente de proteções;
- comportamento diferente após instalar um componente mais potente;
- conectores aquecidos;
- cabos ou terminais escurecidos.

Nenhum desses sintomas prova sozinho que a fonte é a causa.  

Também podem estar envolvidos:

- placa-mãe;
- VRM;
- memória RAM;
- temperatura;
- GPU;
- driver;
- tomada;
- cabo elétrico;
- filtro de linha;
- instalação elétrica;
- curto no gabinete;
- configuração de firmware.

## Coil whine é defeito?

O chamado coil whine é um ruído agudo produzido pela vibração de componentes magnéticos, como indutores.

Pode ocorrer em:  

- fontes;
- placas de vídeo;
- placas-mãe;
- outros circuitos de potência.

Ele pode variar conforme:

- carga;
- taxa de quadros;
- projeto;
- combinação entre componentes;
- frequência de operação.

Coil whine não significa obrigatoriamente falha elétrica iminente.  

Porém, ruídos acompanhados de:

- cheiro;
- faísca;
- aquecimento anormal;
- instabilidade;
- estalos;

exigem interrupção do uso e avaliação técnica.

## Dimensionamento da fonte

Escolher uma fonte não consiste apenas em somar o consumo declarado de todos os componentes.

É necessário considerar:

- PU;
- GPU;
- quantidade de dispositivos;
- picos transitórios;
- eficiência;
- margem operacional;
- envelhecimento;
- futuras expansões;
- qualidade da fonte;
- conectores disponíveis;
- recomendações do fabricante.

Uma fonte extremamente superdimensionada também não oferece automaticamente benefícios proporcionais. O objetivo é operar em uma faixa adequada, com capacidade e qualidade suficientes.

## Calculadoras de potência

Fabricantes e sites oferecem calculadoras que estimam a potência necessária. Essas ferramentas são úteis como ponto de partida, mas o resultado depende das informações inseridas e das margens adotadas.

Elas não substituem a análise de:

- modelo exato da GPU;
- consumo real;
- comportamento transitório;
- qualidade da fonte;
- conectores;
- recomendações técnicas.

Uma calculadora produz uma estimativa.  

Não um laudo.

## Certificação de eficiência não é selo absoluto de qualidade

Considere duas afirmações:
```text
“A fonte possui 80 PLUS Gold, portanto é excelente.”
```
```text
“A fonte não possui selo, portanto é necessariamente ruim.”
```
As duas são simplificações. Uma certificação de eficiência avalia um aspecto importante.  

Mas uma análise completa também deve considerar:

- projeto;
- fabricante real;
- plataforma interna;
- proteções;
- capacitores;
- regulação;
- ripple;
- ventilação;
- ruído;
- garantia;
- testes independentes;
- capacidade em diferentes temperaturas.

## Laboratório: investigação não invasiva

Nesta atividade, não abriremos a fonte nem realizaremos medições em circuitos energizados.

### Etapa 1 — Identificação

Com o computador desligado e sem remover proteções perigosas, consulte a etiqueta ou documentação da fonte e registre:

- fabricante;
- modelo;
- potência;
- corrente na linha de 12 V;
- certificação;
- proteções declaradas;
- quantidade de conectores;
- formato;
- tempo de garantia.

### Etapa 2 — Análise da configuração

Registre os principais consumidores:

- processador;
- placa de vídeo;
- quantidade de SSDs e HDs;
- ventoinhas;
- bomba de refrigeração, quando existir;
- placas adicionais.

### Etapa 3 — Coleta de sintomas

Pergunte:

- O desligamento ocorre em repouso ou apenas sob carga?
- O problema começou após um upgrade?
- Existe cheiro, ruído ou aquecimento?
- O equipamento reinicia ou perde energia completamente?
- Há registro no sistema?
- O problema ocorre em outra tomada?
- Os conectores estão corretamente instalados?
- Foram usados adaptadores?

### Etapa 4 — Monitoramento

Com uma ferramenta como HWiNFO, observe:

- temperatura da CPU;
- temperatura da GPU;
- carga dos componentes;
- momento exato da falha;
- clocks;
- limites de potência;
- sensores de tensão, apenas como referência.

Registre claramente:
```text
As leituras de tensão por software são indícios auxiliares e não comprovam a qualidade elétrica da fonte.
```

### Etapa 5 — Hipóteses

Exemplo:  
```text
O computador desliga apenas quando CPU e GPU entram em carga simultânea. A fonte é uma hipótese relevante, mas ainda devem ser investigados temperatura, conectores, VRM, curto e estabilidade dos componentes.
```

## Estudo de Caso 1 — Fonte de 500 W em computador gamer

Configuração:

- Processador........Ryzen 7
- Placa de vídeo.....modelo de alto desempenho
- Memória............32 GB
- Armazenamento......2 SSDs
- Fonte..............500 W sem modelo identificável
- Sintoma............desligamento durante jogos

### Evidências
- uso leve funciona normalmente;
- desligamento ocorre sob carga;
- temperaturas estão dentro da faixa esperada;
- fonte possui etiqueta genérica;
- potência na linha de 12 V não está clara;
- placa de vídeo foi instalada recentemente.

### Hipóteses
- fonte subdimensionada;
- potência anunciada não corresponde à capacidade real;
- cabo inadequado;
- adaptador;
- conector mal encaixado;
- proteção contra sobrecarga;
- falha da GPU;
- instabilidade elétrica.

A fonte se torna uma hipótese forte, mas o diagnóstico ainda precisa de confirmação controlada.  

Uma abordagem comum é testar com uma fonte de referência:

- conhecida;
- compatível;
- de potência adequada;
- com cabos corretos.

### Estudo de Caso 2 — Leitura de 11,4 V no software

Um programa mostra:
```text
Linha de 12 V: 11,4 V
```

O computador funciona normalmente.  

Devemos concluir imediatamente que a fonte está fora da especificação?

**Não.**  

Primeiro precisamos considerar:

- sensor incorretamente identificado;
- calibração;
- erro do software;
- placa-mãe;
- valor sem precisão;
- leitura obtida em local diferente da saída da fonte.

A próxima etapa seria confirmar por meio de método de medição adequado. O software levantou uma hipótese. Não produziu uma conclusão.

### Estudo de Caso 3 — Computador reinicia, mas registra erro térmico

Um computador reinicia durante renderização. O usuário culpa a fonte.

O monitoramento revela:

- CPU atingindo temperatura limite;
- queda de clock;
- ventoinha do cooler sem aumentar rotação;
- registro de superaquecimento;
- fonte com carga estimada moderada.

Neste caso, as evidências apontam primeiro para o sistema térmico. A semelhança entre sintomas demonstra por que o diagnóstico não pode ser baseado apenas na aparência do problema.

### Estudo de Caso 4 — SSD queimado após troca da fonte

O usuário substituiu uma fonte modular e reutilizou os cabos antigos porque “os conectores encaixavam”.  

Após ligar o computador:

- dois SSDs deixaram de ser reconhecidos;
- surgiu cheiro de queimado;
- outros componentes permaneceram ligados.

Hipótese principal:
```text
A pinagem dos cabos modulares pode ser diferente, apesar da aparência física semelhante.
```
Esse caso demonstra uma regra essencial:
```text
Ao trocar uma fonte modular, substitua também os cabos pelos fornecidos com a nova unidade, salvo confirmação oficial de compatibilidade.
```

## Mito ou Evidência?
### “Se a ventoinha da fonte gira, ela está boa”

Mito.  

A fonte pode iniciar e falhar sob carga ou apresentar problemas elétricos não visíveis.

### “Uma fonte de 700 W sempre é melhor que uma de 550 W”

Mito.  

Potência é apenas um dos critérios. Projeto e capacidade real também importam.

### “O software mede diretamente a saída da fonte”

Mito.  

Normalmente, ele exibe dados obtidos por sensores da placa-mãe.

### “Uma fonte pode causar defeitos intermitentes”

Evidência.  

Falhas podem aparecer apenas sob carga, temperatura ou determinada condição elétrica.

### “Cabos modulares de fontes diferentes podem ser incompatíveis”

Evidência.  

A pinagem do lado da fonte pode variar entre modelos.

### “80 PLUS garante todas as proteções e a qualidade interna”

Mito.  

A certificação se concentra em eficiência energética sob condições específicas.

### “Abrir uma fonte desconectada é sempre seguro”

**Mito perigoso.**

Capacitores internos podem manter tensão elevada.

## O que um perito observaria?
- Qual é o modelo exato da fonte?
- A potência é contínua ou de pico?
- Quanto ela entrega na linha de 12 V?
- Há proteções documentadas?
- O problema ocorre sob qual carga?
- Houve upgrade recente?
- Os cabos utilizados pertencem ao próprio modelo?
- Existem adaptadores?
- Há conectores aquecidos ou escurecidos?
- O desligamento é instantâneo ou acompanhado de erro?
- Temperaturas foram descartadas?
- A instalação elétrica foi verificada?
- Existe uma fonte de referência para comparação?
- As leituras de software foram tratadas apenas como indícios?
- O equipamento apresenta risco de incêndio ou choque?
- O caso exige interrupção imediata do uso?

## Quando interromper o uso

Desligue e desconecte o equipamento diante de sinais como:

- cheiro de queimado;
- fumaça;
- faíscas;
- estalos;
- cabo derretido;
- conector escurecido;
- aquecimento intenso;
- líquido;
- choque no gabinete;
- ruído elétrico acompanhado de instabilidade.

Nesses casos, a prioridade não é concluir o teste.

**É preservar a segurança.**