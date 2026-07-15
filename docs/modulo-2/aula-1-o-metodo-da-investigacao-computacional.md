# O método da investigação computacional
```text
    "Todo computador deixa pistas. A diferença entre um usuário e um especialista está na capacidade de interpretá-la.
```

## Uma história para começar
Imagine que você trabalha como consultor de tecnologia. Uma empresa liga para você, o responsável pelo setor financeiro diz apenas uma frase:

```text
Nosso computador não funciona.
```

Essa informação é suficiente para descobrir o problema?   
Claro que não!

O que significa "não funciona"?.  
O computador não liga?  
Liga, mas não mostra imagem?  
Liga normalmente, mas trava?  
Está lento?  
Faz barulho?  
Desliga sozinho?  
Superaquece?  
A internet não funciona?  
A impressora não imprime?  
Um bom profissional nunca começa trocando peças, ele começa fazendo perguntas.  

## O erro que quase todo iniciante comete

Quem está começando normalmente pensa assim:
```text
 Computador travando?
```

Troca a memória.
```text
 Continua travando?
```

Troca o SSD.
```text
 Continua?
```

Troca a placa-mãe.
```text
 Continua
```

Troca processador.

Esse método recebe um nome bastante conhecido na manutenção: **Tentativa e erro**.

Além de caro, ele desperdiça tempo e frequentemente não resolve o problema. Profissionais experientes trabalham de outra maneira.

**Eles investigam.**

## O método científico aplicado à tecnologia

Curiosamente, o mesmo método utilizado por cientistas, médicos e engenheiros também funciona perfeitamente na informática. Sempre seguimos uma sequência lógica.

```text
Sintoma -> Observação -> Coleta de evidências -> Hipóteses -> Testes -> Conclusão -> Correção -> Validação
```
Percebe que a troca de componentes aparece apenas depois da investigação? Nunca antes!

## O primeiro princípio da Academy
Existe um princípio que acompanhará você durante toda a formação.

```text
Toda tecnologia foi criada para resolver um problema.
```

Existe outro.
```text
Todo problema deixa evidências.
```

Nossa missão será aprender a interpretar essas evidências.

## O que é uma evidência?
Na computação, uma evidência é qualquer informação que ajude a compreender o que realmente está acontecendo.
Por exemplo:  
Um computador apresenta lentidão.
As evidências podem ser:

- temperatura elevada;
- SSD quase cheio;
- memória RAM totalmente ocupada;
- uso excessivo do processador;
- mensagens de erro;
- registro do sistema(logs);
- ruídos incomuns no hardware;
- LEDs de diagnóstico na placa-mãe.

Nenhuma dessas informações confirmam o problema sozinho. Mas, quando analisadas em conjunto, elas ajudam a construir uma hipótese.

## Um investigador nunca começa pela resposta
Imagine dois técnicos.

### Técnico A
Chega ao computador.  
Troca a memória.  
Não resolveu! 
Troca o SSD.
Não resolveu!
Troca a fonte.
Agora resolveu!  

**Ele resolveu? Sim.**

Mas não sabe exatamente qual era a causa.

### Técnico B
Observa o problema.  
Coleta informações.  
Analisa temperaturas.  
Executa testes.  
Consulta os registros do sistema.  
Descobre que a fonte apresentava quedas de tensão sob carga.  
Substitui apenas a fonte.  
Resolve o problema.  
Além de resolver, ele compreendeu a causa, é isso que diferencia um profissional.  

## Laboratório

Durante todo este módulo conheceremos ferramentas utilizadas por técnicos e consultores.

|Ferramenta|Finalidade|
|----------|----------|
|HWiNFO|Monitorar sensores do computador|
|CPU-Z|Identificar processador, placa-mãe e memória|
|GPU-Z|Identificar características da placa de vídeo|
|CrystalDiskInfo|Verificar a saúde dos dispositivos de armazenamento|

Ainda não vamos aprender a utilizá-las. Primeiro precisamos entender o que estamos investigando.  
Depois aprenderemos como coletar e interpretar essa informações.

## Curiosidade técnica
Nas áreas de perícia digital e resposta a incidentes, alterar um sistema antes de coletar evidências pode comprometer completamente uma investigação. Por esse motivo, profissionais especializados seguem procedimentos rigorosos para preservar informações e documentar cada etapa do processo. Embora nosso foco neste módulo seja diagnóstico de hardware, adotaremos a mesma filosofia: **observar antes de modificar**.