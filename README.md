SmartPick - Sistema Inteligente de Organização de Caixas e Cálculo de Rotas

Sistema acadêmico que ajuda empresas de prestação de serviços a organizar caixas dentro de armazéns. Usa grafos para calcular rotas e definir a melhor posição de armazenamento, conforme a distância, o peso da caixa e a necessidade de empilhadeira.

Disciplina: Fabrica de projetos
Curso: Ciência da Computação - UNIMAR
Tecnologia principal: C# (.NET)


1. Visão Geral

O SmartPick combina regras de negócio e algoritmos de grafos para otimizar o armazenamento de caixas. O sistema deve:

- cadastrar caixas e suas características;
- representar a estrutura física do armazém;
- identificar posições disponíveis;
- escolher automaticamente a posição mais adequada;
- calcular a melhor rota para o operador ou para a empilhadeira;
- mostrar a posição e o caminho encontrado.

O objetivo é reduzir deslocamentos desnecessários, melhorar a organização das prateleiras e aumentar a segurança no armazenamento.


2. Problema

Normalmente a organização das caixas depende da experiência do operador. Essa decisão manual pode causar:

- caixas pesadas guardadas de forma inadequada;
- uso desnecessário de empilhadeiras;
- percursos maiores que o necessário;
- dificuldade para achar posições livres;
- desperdício de espaço nas prateleiras;
- risco de danificar caixas leves quando há caixas pesadas acima delas.

O SmartPick automatiza essa decisão com critérios objetivos e algoritmos de menor caminho.


3. Objetivos

Objetivo geral: desenvolver um sistema que determine a melhor posição para guardar uma caixa e calcule a rota mais eficiente dentro do armazém, considerando distância, peso e acessibilidade.

Objetivos específicos:

- representar o armazém com grafos;
- calcular rotas de menor distância;
- diferenciar rotas manuais e rotas para empilhadeira;
- organizar as caixas conforme o peso;
- representar prateleiras por altura, repartição e profundidade;
- mostrar ao usuário a posição recomendada e a rota calculada.


4. Atores do Sistema

- Operador: cadastra a caixa e solicita o armazenamento.
- Administrador: gerencia a estrutura do armazém.
- Sistema SmartPick: calcula posições e rotas.
- Empilhadeira: faz movimentações em áreas específicas.


5. Fluxo Principal

1. Cadastrar a caixa.
2. Informar peso e dimensões.
3. Buscar posições disponíveis.
4. Verificar se a posição exige empilhadeira. Se não exige, usa a rota manual; se exige, usa a rota da empilhadeira.
5. Selecionar a melhor posição.
6. Calcular a menor rota.
7. Mostrar a posição e o caminho.


6. Escopo

Dentro do escopo:
- cadastro de caixas, prateleiras e posições;
- organização por altura e profundidade;
- identificação de posições livres;
- cálculo de rotas, com grafo manual e grafo para empilhadeira;
- escolha automática da posição;
- visualização da rota.

Fora do escopo:
- controle financeiro;
- controle de estoque completo;
- emissão de notas fiscais;
- rastreamento por GPS;
- integração com ERP;
- automação física do armazém.

Evoluções futuras:
- leitura de QR Code;
- integração com código de barras;
- sensores de ocupação;
- histórico de movimentações;
- otimização de várias caixas ao mesmo tempo.


7. Requisitos Funcionais

RF01 - Cadastrar caixas
RF02 - Informar peso e dimensões
RF03 - Cadastrar prateleiras
RF04 - Cadastrar posições do armazém
RF05 - Identificar posições disponíveis
RF06 - Calcular rota manual
RF07 - Calcular rota para empilhadeira
RF08 - Considerar distância no cálculo
RF09 - Considerar o peso da caixa
RF10 - Indicar posição recomendada
RF11 - Exibir a rota calculada
RF12 - Diferenciar acessibilidade manual e empilhadeira
RF13 - Informar quando não existir posição disponível


8. Requisitos Não Funcionais

RNF01 - O cálculo das rotas deve ser rápido
RNF02 - A interface deve ser simples e intuitiva
RNF03 - O sistema deve funcionar em computadores da empresa
RNF04 - O código deve ser modular e de fácil manutenção
RNF05 - As posições sugeridas devem respeitar as regras de segurança


9. Regras de Negócio

RN01 - Peso: caixas pesadas têm prioridade para posições inferiores.
RN02 - Caixas leves: podem ocupar posições superiores quando houver disponibilidade.
RN03 - Empilhadeira: posições elevadas ou restritas exigem empilhadeira.
RN04 - Circulação: a empilhadeira usa apenas corredores autorizados para ela.
RN05 - Rota manual: operadores usam somente corredores classificados como acesso manual.
RN06 - Profundidade: a posição deve informar se a caixa fica na frente ou no fundo da prateleira.
RN07 - Ocupação: posições ocupadas não podem ser sugeridas.


10. Solução Proposta

A decisão do SmartPick acontece em duas etapas.

Etapa 1 - Escolha da posição. O sistema analisa o peso da caixa, a altura da prateleira, a profundidade e a disponibilidade da posição.

Etapa 2 - Cálculo da rota. Com a posição escolhida, o algoritmo calcula o menor caminho considerando distância, tipo de acesso, circulação permitida e necessidade de empilhadeira.

Essa separação evita que uma rota da empilhadeira seja usada por operadores.


11. Arquitetura

O usuário acessa a interface web (front-end), que se comunica com o back-end em C# (.NET). O back-end trata caixas, armazém e o algoritmo de rotas, que usa grafos. Os dados ficam em um banco MySQL.

- Front-end: interação com o usuário
- Back-end: regras de negócio
- Grafos: cálculo das rotas
- Banco: armazenamento dos dados


12. Tecnologias

- Front-end: HTML, CSS e JavaScript
- Back-end: C# (.NET)
- Banco de dados: MySQL
- Algoritmos: grafos
- Versionamento: Git e GitHub
- Planejamento: GitHub Projects
- Prototipação: Figma


13. Representação do Armazém

Cada corredor é um vértice e cada ligação entre corredores é uma aresta.

O sistema usa dois grafos independentes: um para acesso manual e outro para a empilhadeira. Assim, cada tipo de movimentação tem seus próprios corredores permitidos.


14. Principal Desafio Técnico

Calcular rotas considerando ao mesmo tempo distância, peso da caixa, altura da prateleira, profundidade, acessibilidade e circulação da empilhadeira.

Estratégia:
1. Modelar o armazém como grafo.
2. Criar grafos separados para cada tipo de acesso.
3. Aplicar as regras de peso para escolher a posição.
4. Usar um algoritmo de menor caminho para calcular a rota.


15. Planejamento (Sprints)

O desenvolvimento dura 9 semanas, em 3 sprints, com 3 equipes trabalhando ao mesmo tempo:

- Equipe 1: Armazém / Dados
- Equipe 2: Grafos / Rotas
- Equipe 3: Sistema / Interface

Sprint 1 - Estrutura e Protótipo (semanas 1 a 3)
Objetivo: definir a estrutura do armazém, modelar os dados e criar o protótipo inicial.
- Equipe 1: definir estrutura do armazém, das prateleiras, divisões, níveis de altura e posições de profundidade; criar modelo da caixa e da posição.
- Equipe 2: definir a representação do armazém como grafo (entrada e saída, circulação, vértices, conexões e distâncias); criar o primeiro modelo do grafo e o grafo inicial de acesso manual.
- Equipe 3: definir fluxo de utilização e telas; criar protótipos da tela inicial, do cadastro da caixa, da visualização do armazém e da tela de resultado.
Entrega: estrutura inicial do armazém, modelos de caixas e posições, primeiro grafo e protótipo das telas principais.

Sprint 2 - Desenvolvimento do Núcleo (semanas 4 a 6)
Objetivo: desenvolver a lógica principal do sistema.
- Equipe 1: criar modelo da prateleira e o banco de dados; relacionar caixas e posições; registrar posições ocupadas e disponíveis; criar dados de teste; validar a estrutura.
- Equipe 2: criar o grafo da empilhadeira e definir corredores permitidos; implementar o algoritmo de menor caminho; testar rota manual e de empilhadeira; verificar a necessidade de empilhadeira; separar os dois tipos de rota.
- Equipe 3: implementar tela inicial, cadastro da caixa (formulários de peso e dimensões), visualização do armazém, posições disponíveis e tela de resultado.
Entrega: primeiro fluxo funcional (cadastrar caixa, informar características, verificar posição, identificar acesso, calcular rota e apresentar resultado).

Sprint 3 - Integração, Testes e MVP (semanas 7 a 9)
Objetivo: integrar todos os módulos e validar o Produto Mínimo Viável.
- Equipe 1: ajustar a estrutura conforme os testes; validar alturas, profundidades e posições ocupadas; corrigir inconsistências; finalizar o banco de dados.
- Equipe 2: implementar a regra de peso; definir a posição conforme peso, altura e profundidade; integrar o algoritmo ao banco; testar cenários; corrigir problemas; validar o cálculo final.
- Equipe 3: mostrar rota manual, rota da empilhadeira, posição recomendada e tipo de acesso; integrar a interface ao back-end; criar mensagens de erro; testar o fluxo completo; preparar a demonstração.
Entrega: sistema integrado, regras de negócio aplicadas, rotas funcionando e MVP pronto para apresentação.


16. MVP

O SmartPick será considerado funcional quando conseguir:

- cadastrar uma caixa;
- representar as posições do armazém;
- identificar posições disponíveis;
- considerar o peso da caixa;
- identificar quando é necessária uma empilhadeira;
- calcular uma rota manual ou de empilhadeira;
- mostrar visualmente a posição e a rota.


17. Riscos do Projeto

- Complexidade dos grafos (probabilidade alta, impacto alto): desenvolver um protótipo do algoritmo no Sprint 1.
- Integração entre módulos (média, alto): integração contínua entre as equipes.
- Erros no cálculo da rota (média, alto): criar cenários de teste variados.
- Modelagem do armazém (média, médio): validar a estrutura antes de implementar.
- Falta de tempo (média, alto): priorizar as funcionalidades do MVP.


18. Estrutura do Repositório

SmartPick/
  README.txt
  docs/ (arquitetura, prototipo, apresentacao)
  src/ (SmartPick.Core, SmartPick.Data, SmartPick.API, SmartPick.Web)
  database/ (smartpick.sql)
  assets/ (imagens, logo)
  .github/workflows/


19. Equipe

- Integrante 1: Armazém / Banco de Dados
- Integrante 2: Armazém / Modelagem
- Integrante 3: Grafos e Algoritmos
- Integrante 4: Regras de Negócio
- Integrante 5: Interface do Sistema
- Integrante 6: Testes e Integração


20. Status do Projeto

- Planejamento: concluído
- Protótipo: em desenvolvimento
- GitHub Projects: organizado em 3 sprints
- Desenvolvimento em C#: não iniciado
- MVP: previsto para o Sprint 3



