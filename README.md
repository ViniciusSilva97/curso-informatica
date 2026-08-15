<div align="center">
  <img src="docs/assets/brand/smart-eletro-vini-logo.png" alt="Smart Eletro Vini" width="160">

# Curso Gratuito de Informática

**Informática para entender, investigar e resolver.**

Do primeiro contato com o computador ao raciocínio técnico usado para diagnosticar problemas reais.

[**Comece agora — acesso gratuito**](https://viniciussilva97.github.io/curso-informatica/)

</div>

---

## Conhecimento deve abrir caminhos

A tecnologia está presente no trabalho, nos estudos, nos negócios e nas tarefas mais simples do cotidiano. Mesmo assim, aprender informática com profundidade ainda pode parecer difícil, caro ou distante.

Este projeto nasceu para ajudar a mudar essa realidade.

O **Curso Gratuito de Informática da Smart Eletro Vini** compartilha conhecimento técnico de qualidade em linguagem acessível, sem tratar o estudante como alguém incapaz e sem transformar assuntos importantes em simples memorização.

Queremos que cada pessoa consiga compreender o que acontece dentro e fora do computador, desenvolver autonomia, investigar problemas e transformar curiosidade em habilidade.

> Não ensinamos apenas onde clicar. Ensinamos a pensar sobre o que está acontecendo.

## Nosso compromisso com a educação

Acreditamos que educação tecnológica pode gerar independência, novas oportunidades profissionais e decisões melhores no dia a dia.

Por isso, o curso é construído sobre alguns compromissos:

- **acesso gratuito:** o conteúdo principal pode ser estudado sem cobrança;
- **linguagem acolhedora:** começamos do zero e explicamos os termos antes de usá-los;
- **profundidade técnica:** simplificar a explicação não significa empobrecer o conhecimento;
- **aprendizado progressivo:** cada aula prepara o terreno para a próxima;
- **aplicação prática:** exemplos, diagnósticos e atividades conectam a teoria ao mundo real;
- **responsabilidade:** segurança, limitações e boas práticas fazem parte do aprendizado;
- **evolução contínua:** o material cresce e é revisado conforme o projeto amadurece.

A loja **Smart Eletro Vini** apoia esta iniciativa porque vender tecnologia também significa ajudar as pessoas a entendê-la e utilizá-la melhor.

## O que você encontrará

O curso possui atualmente **2 módulos e 18 aulas publicadas**.

| Módulo | Conteúdo | Situação |
|---|---|---|
| **1 — Fundamentos da informática** | Hardware, software, sistemas operacionais, desempenho, inicialização, dados, internet, sites e arquivos | 11 aulas disponíveis |
| **2 — Investigação computacional I** | Método de diagnóstico, processador, memória RAM, SSDs, HDs, placa-mãe, fontes e refrigeração | 7 aulas disponíveis |

A trilha continuará avançando para temas como sistemas operacionais, redes, segurança da informação, infraestrutura, bancos de dados e desenvolvimento de sistemas.

## Nosso jeito de ensinar

### Explicações que fazem sentido

Conceitos técnicos são apresentados com clareza, exemplos cotidianos e comparações que ajudam a construir entendimento — não apenas decorar nomes.

### Situações reais

As aulas partem de perguntas que surgem na prática:

- Por que um computador fica lento?
- O que acontece quando ele é ligado?
- Como identificar se o problema está na memória, no armazenamento ou na fonte?
- O que realmente acontece quando um arquivo é apagado?
- Como um site chega até a nossa tela?

### Investigação antes da troca de peças

Nosso método incentiva o estudante a observar sintomas, levantar hipóteses, testar com segurança e registrar evidências antes de chegar a uma conclusão.

### Recursos visuais e atividades

Diagramas, ilustrações responsivas, exercícios e pequenos laboratórios ajudam a transformar informação em habilidade aplicável.

## Para quem é este curso?

Este conteúdo foi pensado para:

- quem está começando e acredita que “não entende de computador”;
- estudantes que desejam construir uma base técnica sólida;
- pessoas que se preparam para concursos e avaliações;
- profissionais que utilizam tecnologia, mas querem compreender melhor suas ferramentas;
- futuros técnicos e profissionais de suporte;
- empreendedores que precisam tomar decisões melhores sobre equipamentos e infraestrutura;
- pessoas curiosas que gostam de descobrir como as coisas funcionam.

Você não precisa chegar sabendo. Precisa apenas chegar disposto a aprender.

## Acesse o curso

O conteúdo publicado está disponível em:

### [viniciussilva97.github.io/curso-informatica](https://viniciussilva97.github.io/curso-informatica/)

A sequência recomendada começa na [Aula 1 — O que é informática?](https://viniciussilva97.github.io/curso-informatica/modulo-1/aula-1-o-que-e-informatica/).

## Tecnologias do projeto

A plataforma educacional é construída com:

- [MkDocs](https://www.mkdocs.org/);
- [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/);
- Python e [uv](https://docs.astral.sh/uv/);
- GitHub Pages;
- HTML, CSS e JavaScript para a experiência visual;
- SVGs responsivos produzidos especialmente para as aulas.

## Executando localmente

Com o [uv](https://docs.astral.sh/uv/getting-started/installation/) instalado:

```bash
git clone https://github.com/ViniciusSilva97/curso-informatica.git
cd curso-informatica
uv sync
uv run mkdocs serve
```

Depois, acesse:

```text
http://127.0.0.1:8000
```

## Estrutura principal

```text
docs/
├── assets/          # Identidade visual, diagramas e ilustrações
├── modulo-1/        # Fundamentos da informática
├── modulo-2/        # Investigação computacional
├── stylesheets/     # Estilos da plataforma
├── javascripts/     # Comportamentos complementares
└── index.md         # Página inicial do curso

mkdocs.yml           # Navegação e configuração do site
overrides/           # Personalizações do tema
pyproject.toml       # Dependências do projeto
```

## Como ajudar o projeto

Educação de qualidade também é construída com escuta e revisão.

Você pode colaborar:

- relatando um erro técnico ou de escrita;
- sugerindo uma explicação mais clara;
- informando dificuldade de leitura em celular ou computador;
- propondo exercícios e situações reais;
- apontando problemas de acessibilidade;
- sugerindo temas para aulas futuras.

Antes de enviar uma alteração, abra uma [issue](https://github.com/ViniciusSilva97/curso-informatica/issues) descrevendo a proposta e o benefício educacional.

## Direitos autorais

O acesso ao curso é gratuito, mas gratuidade não significa ausência de autoria.

Até que uma política específica para o código da plataforma e para o conteúdo educacional seja formalizada, os textos, ilustrações, identidade visual e demais materiais permanecem protegidos por direitos autorais.

**© 2026 Vinícius Silva e Smart Eletro Vini. Todos os direitos reservados.**

---

<div align="center">

**Tecnologia, informática e soluções para você montar, aprender e evoluir.**

Feito com dedicação por quem acredita que compartilhar conhecimento também é uma forma de construir o futuro.

</div>
