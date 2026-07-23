# Aula 5 - Placa-mãe: A cena onde todos os componentes se encontram

## Pergunta da investigação

```text
Quando o computador liga, mas não apresenta imagem, como descobrir qual componente está impedindo a inicialização?
```

## Dossiê da Investigação
## Caso nº 004 — O computador que “liga”, mas não inicia

Um cliente relata:

**“O computador liga, as ventoinhas giram e os LEDs acendem, mas não aparece nada na tela.”**

Ao pressionar o botão de energia, observamos:

- ventoinhas funcionando;
- iluminação do gabinete acesa;
- nenhum sinal de vídeo;
- teclado aparentemente sem resposta;
- ausência do som de inicialização do sistema;
- LED vermelho aceso na placa-mãe.

O computador realmente iniciou?  
O problema está no monitor?  
Na memória RAM?  
Na placa de vídeo?  
No processador?    
Na fonte?  
Ou na própria placa-mãe?  
Hoje aprenderemos a investigar esse tipo de situação.

## Objetivos da aula

Ao final desta aula, você será capaz de:

- compreender o papel da placa-mãe;
- identificar seus principais circuitos e conexões;
- diferenciar alimentação elétrica de inicialização do sistema;
- entender as etapas básicas do POST;
- interpretar LEDs, códigos sonoros e displays de diagnóstico;
- reconhecer problemas de compatibilidade;
- realizar uma investigação inicial de forma controlada;
- compreender os limites dos diagnósticos feitos por software.

## A placa-mãe não é apenas uma “placa que conecta peças”

Essa definição é comum:

**“A placa-mãe conecta todos os componentes do computador.”**  

Ela está correta, mas é incompleta.  
A placa-mãe também participa de funções como:

- distribuição de energia;
- comunicação entre os componentes;
- inicialização do hardware;
- configuração do sistema;
- controle de interfaces;
- armazenamento do firmware;
- leitura de sensores;
- gerenciamento de dispositivos;
- sincronização de sinais;
- proteção elétrica básica.

Ela funciona como a infraestrutura sobre a qual o computador inteiro opera.

Podemos compará-la a uma cidade:

- as trilhas são as vias;
- os conectores são os terminais;
- os barramentos transportam dados;
- os reguladores distribuem energia;
- o firmware define regras iniciais;
- os componentes são os edifícios e serviços.

Se essa infraestrutura falhar, vários sintomas diferentes podem aparecer.

## O que significa “o computador ligou”?

Quando ventoinhas giram e LEDs acendem, sabemos apenas que alguma energia chegou ao sistema. Isso não significa que o computador concluiu sua inicialização.

Existe uma diferença importante entre:

Receber energia  
      ↓  
Iniciar os componentes  
      ↓  
Executar o firmware  
      ↓  
Testar o hardware  
      ↓  
Localizar o sistema operacional  
      ↓  
Carregar o sistema  

Um computador pode parar em qualquer uma dessas etapas. Por isso, dizer que ele “liga” é uma descrição insuficiente. O investigador precisa descobrir até onde a inicialização avançou.

## POST: o primeiro exame do computador

Ao receber energia e iniciar, o sistema executa uma sequência de verificações conhecida como POST — **Power-On Self-Test**.

De forma simplificada, o firmware verifica componentes essenciais, como:

- processador;
- memória RAM;
- vídeo;
- dispositivos básicos;
- configurações de inicialização.

Caso um componente essencial não seja reconhecido, o processo pode ser interrompido antes que qualquer imagem seja apresentada.  

Uma sequência simplificada seria:

Energia estabilizada  
        ↓  
Processador inicia  
        ↓  
Firmware é executado  
        ↓  
Memória é identificada e treinada  
        ↓  
Vídeo é inicializado  
        ↓  
Dispositivos são detectados  
        ↓  
Sistema operacional é procurado  

A ordem exata varia conforme a plataforma.

## BIOS e UEFI

A placa-mãe possui um firmware responsável pelas primeiras etapas de inicialização. Historicamente, esse firmware era conhecido como BIOS.  
Computadores modernos normalmente utilizam UEFI, que oferece recursos mais avançados.  

Entre suas funções estão:

- detectar componentes;
- configurar parâmetros;
- controlar a ordem de inicialização;
- inicializar dispositivos;
- disponibilizar configurações de segurança;
- entregar o controle ao sistema operacional.

No uso cotidiano, muitas pessoas continuam chamando a interface de “BIOS”, mesmo quando tecnicamente se trata de **UEFI**.

## A bateria não alimenta o computador inteiro

A pequena bateria instalada na placa-mãe costuma gerar confusão. Ela não mantém o processador, a memória ou o sistema funcionando.  
Sua função principal é preservar determinadas informações quando o computador está sem energia, como:

- relógio do sistema;
- data;
- algumas configurações do firmware.

Quando essa bateria fica fraca, podem surgir sintomas como:

- data e hora incorretas;
- configurações que não permanecem salvas;
- mensagens relacionadas ao CMOS;
- necessidade de reconfigurar opções após desligar da tomada.

Uma bateria fraca normalmente não explica, sozinha, todos os casos em que um computador não apresenta vídeo.

## Principais regiões da placa-mãe
### Socket do processador

É a interface física e elétrica entre o processador e a placa-mãe.

Pode possuir contatos delicados.  

Danos, sujeira, pressão inadequada ou processador incompatível podem impedir a inicialização.

### Slots de memória RAM

Recebem os módulos de memória.
Problemas podem ocorrer por:

- módulo mal encaixado;
- contatos sujos;
- slot defeituoso;
- configuração incompatível;
- módulo defeituoso;
- controlador de memória;
- perfil de desempenho instável.

### Slots PCI Express

São utilizados por componentes como:

- placas de vídeo;
- placas de rede;
- controladoras;
- placas de captura;
- unidades de expansão.

O formato físico não informa sozinho a quantidade de pistas elétricas realmente disponíveis. Um slot com tamanho x16 pode, dependendo do projeto, operar eletricamente com menos pistas.

### Conectores de armazenamento

Podem incluir:

- SATA;
- M.2;
- conexões específicas da plataforma.

Um conector M.2 não garante, por si só, que qualquer SSD M.2 seja compatível. O formato físico pode aceitar diferentes interfaces e protocolos.

### Conectores de alimentação

Os principais incluem:

- conector principal da placa-mãe;
- alimentação dedicada ao processador;
- conectores auxiliares em determinadas plataformas.

Um erro frequente é conectar apenas a alimentação principal e esquecer o conector destinado à CPU. Nesse caso, ventoinhas podem girar, mas o sistema pode não completar a inicialização.

### Chipset

O chipset auxilia no gerenciamento de diversas interfaces e recursos da plataforma.

Dependendo da arquitetura, participa da comunicação com:

- portas USB;
- armazenamento;
- rede;
- pistas PCI Express adicionais;
- áudio;
- dispositivos integrados.

Seu papel mudou ao longo das gerações, pois muitas funções antes externas foram incorporadas ao próprio processador.

### VRM

O Voltage Regulator Module, ou módulo regulador de tensão, converte e controla a energia entregue aos componentes, especialmente ao processador. 

O processador não recebe diretamente a tensão bruta fornecida pela fonte. O VRM ajusta essa energia para níveis adequados e estáveis.

Ele pode incluir:

- controladores;
- MOSFETs;
- indutores;
- capacitores;
- dissipadores.

Um VRM inadequado, superaquecido ou danificado pode causar:

- instabilidade;
- reinicializações;
- redução de desempenho;
- falhas sob carga;
- ausência de inicialização;
- desligamentos.

## Dentro da Caixa

Vamos analisar uma ficha técnica simplificada:

### Placa-mãe B650

- Socket................AM5
- Memória...............DDR5
- Slots de memória......4
- Capacidade máxima.....192 GB
- PCI Express principal.4.0 x16
- Armazenamento.........2 × M.2 NVMe
                       4 × SATA
- Rede..................2,5 GbE
- Firmware..............UEFI
- Diagnóstico...........LEDs CPU, DRAM, VGA e BOOT

Agora vamos interpretar.

#### Socket AM5

Define a família física e elétrica de processadores suportados. Porém, compartilhar o mesmo socket não garante automaticamente que qualquer processador funcionará.

Também precisamos verificar:

- chipset;
- versão do firmware;
- lista de compatibilidade;
- capacidade elétrica;
- suporte fornecido pelo fabricante.

#### Memória DDR5

A placa foi projetada para DDR5.  
Um módulo DDR4 não deve ser instalado.
A incompatibilidade não é apenas de configuração. A posição do encaixe e a arquitetura são diferentes.

#### LEDs CPU, DRAM, VGA e BOOT

Esses indicadores ajudam a identificar a etapa em que o POST encontrou dificuldade.

De forma geral:

- CPU: problema relacionado à inicialização do processador;
- DRAM: memória não reconhecida ou falha no treinamento;
- VGA: vídeo não inicializado;
- BOOT: dispositivo de inicialização não encontrado.

Esses LEDs não fornecem um diagnóstico definitivo. Eles indicam uma área prioritária para investigação.

#### O treinamento da memória

Em plataformas modernas, especialmente após mudanças de hardware ou configurações, a placa-mãe pode realizar um processo de treinamento da memória.  

Durante esse procedimento, o sistema ajusta parâmetros para encontrar uma configuração funcional e estável.

Isso pode fazer com que:

- a primeira inicialização demore;
- o computador reinicie algumas vezes;
- o LED de memória permaneça aceso temporariamente.

Desligar o computador imediatamente por acreditar que ele travou pode interromper esse processo. Entretanto, uma espera excessivamente longa ou repetitiva exige investigação.

#### Compatibilidade: encaixar não significa funcionar

Um componente pode caber fisicamente e ainda assim não ser compatível.

Precisamos considerar:

- socket;
- geração;
- chipset;
- firmware;
- tipo de memória;
- capacidade;
- perfil elétrico;
- quantidade de pistas;
- protocolo;
- limites térmicos;
- lista de suporte do fabricante.
##### Exemplo

Um processador novo utiliza o mesmo socket de modelos anteriores. A placa-mãe o aceita fisicamente.  

No entanto, ela possui um firmware antigo que não reconhece o processador.

O resultado pode ser:

- ventoinhas girando;
- ausência de vídeo;
- LED de CPU aceso;
- impossibilidade de acessar o firmware.

A placa pode precisar de atualização compatível. Alguns modelos permitem atualizar o firmware sem processador funcional; outros não.

## Diagnóstico sem vídeo

Quando o computador não apresenta imagem, ainda não podemos utilizar ferramentas como HWiNFO ou CPU-Z.

O sistema operacional nem sequer foi carregado.

Nesse cenário, as evidências vêm de outras fontes:

- LEDs de diagnóstico;
- códigos sonoros;
- display numérico;
- comportamento das ventoinhas;
- ciclos de reinicialização;
- temperatura anormal;
- inspeção visual;
- configuração mínima;
- manual da placa-mãe.

Isso mostra uma limitação importante:  

**Software só ajuda quando o sistema consegue avançar o suficiente para executá-lo.**

## Laboratório: ferramentas de diagnóstico da placa-mãe
### LEDs de diagnóstico

Algumas placas possuem indicadores específicos para CPU, DRAM, VGA e BOOT. São simples, rápidos e úteis para orientar a primeira hipótese.

### Códigos sonoros

Quando existe um pequeno alto-falante conectado, a placa pode emitir sequências de sons. O significado depende do firmware e do fabricante. Não existe uma tabela universal válida para todas as placas. O manual deve ser consultado.

### Display de códigos

Placas mais completas podem exibir códigos numéricos ou alfanuméricos. Esses códigos representam estágios da inicialização ou erros encontrados.
Novamente, a interpretação depende da documentação do modelo.

### Placa de diagnóstico

Existem placas que exibem códigos do POST por meio de interfaces de expansão.

Elas podem ajudar em algumas plataformas, mas não substituem:

- conhecimento técnico;
- documentação;
- medições elétricas;
- análise da sequência de inicialização.

### Multímetro

Profissionais podem utilizar um multímetro para investigar:

- presença de tensões;
- continuidade;
- curtos;
- alimentação em conectores;
- circuitos específicos.

O uso inadequado pode causar danos ou choque elétrico. Medições em placas energizadas exigem treinamento, procedimento seguro e conhecimento dos pontos corretos.

### Osciloscópio

Laboratórios de eletrônica podem analisar sinais e comportamento elétrico com maior profundidade.  
Isso permite observar fenômenos que um software ou multímetro comum não demonstra adequadamente. Não é uma ferramenta necessária para o aluno iniciante, mas é importante compreender que diagnósticos avançados podem exigir equipamentos especializados.   

### Inspeção visual

Antes de substituir componentes, o investigador pode observar:

- conectores parcialmente encaixados;
- sinais de oxidação;
- componentes queimados;
- trilhas danificadas;
- parafusos em locais inadequados;
- objetos metálicos soltos;
- pasta térmica em contatos;
- pinos deformados;
- capacitores danificados;
- marcas de líquido;
- poeira excessiva;
- cabos pressionados.

A inspeção deve ser feita com o equipamento desligado, desconectado e seguindo cuidados contra eletricidade estática.

### Configuração mínima

Uma técnica importante consiste em reduzir o sistema ao conjunto mínimo necessário para iniciar.

Normalmente, isso envolve:

- placa-mãe;
- processador;
- sistema de refrigeração;
- um módulo de memória;
- fonte;
- vídeo integrado ou placa de vídeo, quando necessário.

Dispositivos não essenciais são removidos temporariamente.
O objetivo é diminuir o número de variáveis.  

Sistema completo com falha  
          ↓  
Remoção de componentes não essenciais  
          ↓  
Teste em configuração mínima  
          ↓  
Reintrodução controlada dos componentes   

Essa técnica não consiste em remover tudo aleatoriamente. Cada alteração deve ser registrada.

### Limpeza do CMOS

Limpar o CMOS pode restaurar configurações do firmware para valores padrão. Isso pode ajudar quando o problema foi causado por:

- perfil de memória instável;
- overclock;
- configuração incorreta;
- parâmetro incompatível;
- falha após alteração no firmware.

O procedimento varia entre placas e pode envolver:

- jumper;
- botão dedicado;
- remoção temporária da bateria;
- opção específica no painel traseiro.

O manual deve orientar o método correto. A limpeza do CMOS não atualiza o firmware e não corrige defeitos físicos.

### Atualização de firmware

Atualizar o firmware pode:

- adicionar suporte a processadores;
- corrigir falhas;
- melhorar compatibilidade;
- ajustar treinamento de memória;
- resolver problemas de segurança;
- alterar comportamentos da plataforma.

Mas também envolve riscos.  

Uma interrupção durante o processo pode impedir a inicialização, especialmente em placas sem mecanismo de recuperação.

Antes de atualizar, devemos verificar:

- modelo exato da placa;
- revisão do hardware;
- versão instalada;
- motivo da atualização;
- instruções oficiais;
- estabilidade da energia;
- arquivo correto.

**Atualizar “por atualizar” não é uma metodologia investigativa.**

## Estudo de caso 1 — LED DRAM aceso

Um computador recém-montado apresenta:

- ventoinhas funcionando;
- ausência de vídeo;
- LED DRAM continuamente aceso;
- dois módulos de memória instalados;
- perfil de alto desempenho habilitado.

### Hipóteses
- módulo mal encaixado;
- slot inadequado;
- perfil instável;
- memória incompatível;
- módulo defeituoso;
- problema no controlador de memória;
- socket com contato inadequado;
- firmware incompatível.

### Investigação inicial
1. desligar e desconectar o equipamento; 
2. consultar o manual sobre o slot recomendado;
3. reinstalar um único módulo;
4. restaurar configurações padrão;
5. testar individualmente os módulos;
6. observar o tempo de treinamento;
7. verificar a lista de compatibilidade;
8. inspecionar socket e contatos, quando necessário.

O LED orienta a investigação, mas não prova que o módulo de RAM seja o único responsável.

## Estudo de Caso 2 — LED VGA aceso

O sistema apresenta:

- LED VGA;
- placa de vídeo dedicada instalada;
- monitor sem imagem;
- cabo conectado à saída da placa-mãe;
- processador sem gráficos integrados.

Neste caso, a primeira evidência importante é o local em que o monitor foi conectado. Se o processador não possui vídeo integrado, as saídas da placa-mãe não produzirão imagem.  
O cabo deve ser conectado à placa de vídeo dedicada.  
Esse é um exemplo de falha de instalação, não de componente defeituoso.

## Estudo de Caso 3 — Computador reinicia sob carga

Durante tarefas leves, o computador funciona normalmente.Ao executar renderização, ele reinicia. As temperaturas aparentam normais.

Hipóteses possíveis:

- fonte insuficiente ou defeituosa;
- conexão de alimentação da CPU;
- VRM superaquecendo;
- memória instável;
- firmware;
- overclock;
- curto intermitente;
- placa-mãe defeituosa.

A reinicialização não autoriza concluir imediatamente que a placa-mãe está com defeito.

Precisamos correlacionar:

- carga;
- temperatura;
- energia;
- registros;
- configurações;
- comportamento com componentes de referência.

## Mito ou Evidência?
### “Se as ventoinhas giram, a placa-mãe está funcionando”  

Mito. O recebimento de energia não prova que o POST foi concluído.

### “LED DRAM significa obrigatoriamente memória queimada”

Mito. Ele indica falha na etapa relacionada à memória, mas a causa pode envolver módulos, slots, processador, firmware, socket ou configuração.

### “Atualizar a BIOS sempre melhora o computador”

Mito. A atualização deve ter objetivo claro e seguir documentação correta.

### “Uma placa-mãe pode impedir o desempenho máximo do processador”

Evidência. Limitações elétricas, térmicas, de firmware ou configuração podem influenciar o comportamento da CPU.

### “O manual da placa-mãe faz parte das ferramentas de diagnóstico”

Evidência. Ele contém informações específicas que não podem ser substituídas por tabelas genéricas encontradas na Internet.

## O que um perito observaria?
- O sistema recebe energia?
- Qual etapa do POST foi alcançada?
- Existe LED, código sonoro ou display?
- O problema surgiu após alguma alteração?
- O firmware suporta o processador?
- A memória está nos slots recomendados?
- Há sinais de líquido, corrosão ou impacto?
- Existem pinos deformados?
- Os conectores de energia estão corretamente instalados?
- A falha ocorre em configuração mínima?
- O comportamento muda com componentes de referência?
- As alterações foram documentadas?
- Há risco de destruir evidências ao limpar ou atualizar o sistema?

## Laboratório guiado — mapa investigativo da placa-mãe

Utilize o manual de uma placa-mãe disponível para consulta.

Não é necessário desmontar o computador.

### Etapa 1 — Identificação

Registre:

- fabricante;
- modelo;
- revisão;
- socket;
- chipset;
- tipo de memória;
- versão de firmware, quando disponível.

### Etapa 2 — Localização

Identifique no diagrama:

- socket;
- slots de RAM;
- conectores de energia;
- slots PCI Express;
- conectores SATA;
- slots M.2;
- bateria;
- jumper de CMOS;
- LEDs de diagnóstico;
- conectores de ventoinhas;
- painel frontal.

### Etapa 3 — Compatibilidade

Escolha um processador e um módulo de memória e verifique:

- suporte oficial;
- versão mínima de firmware;
- capacidade aceita;
- frequência suportada;
- slot recomendado.

### Etapa 4 — Hipótese

Crie um cenário:

```text
O computador recebe energia, mas o LED de CPU permanece aceso após a troca do processador.
```

Liste pelo menos quatro hipóteses antes de propor qualquer substituição.

### Etapa 5 — Registro

Adicione ao Dossiê:

- evidências;
- hipóteses;
- testes possíveis;
- riscos;
- conclusão provisória.

