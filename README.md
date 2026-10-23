Sprint 04 — EV Challenge GoodWe
Sobre o projeto
Este repositório reúne a avaliação sistemática dos chatbots GoodWe desenvolvidos nas Sprints 2 e 3 do Challenge Integrador da FIAP. Nesta sprint, o foco é medir e comparar a qualidade das respostas dos dois chatbots, sem desenvolver um novo agente.

Os chatbots atendem perguntas sobre a operação de carregadores de veículos elétricos, como disponibilidade, manutenção, sessões, faturamento e falhas. Os testes usam informações simuladas, e não dados reais de carregadores.
Objetivos
- Criar uma base de perguntas com critérios de aceite (golden dataset).
- Executar as mesmas perguntas nos chatbots das Sprints 2 e 3.
- Avaliar automaticamente as respostas usando LLM as a Judge.
- Comparar os resultados por critério e por categoria de pergunta.
- Identificar pontos fortes, dificuldades e limitações da avaliação.
Tecnologias
- Python e Google Colab
- OpenAI API e modelo gpt-4o-mini
- LangChain (versão de avaliação da Sprint 2)
- OpenAI Agents SDK, ferramentas e guardrail (versão de avaliação da Sprint 3)
- Pandas para tabelas e arquivos CSV
Como executar
1. Abra Sprint04_GoodWe_Avaliacao.ipynb no Google Colab (ou o nome do arquivo .ipynb enviado no repositório).
2. No painel Secrets do Colab, cadastre a chave da OpenAI como OPENAI_API_KEY e permita o acesso do notebook.
3. Execute as células na ordem apresentada. A primeira instala as dependências.
4. O notebook cria o contexto simulado, executa o golden dataset nos dois chatbots e usa o modelo avaliador para atribuir notas.
5. Ao final, são exibidas as comparações e gerados os CSVs.
Atenção: executar novamente as células de respostas e avaliações faz novas chamadas à API e pode consumir créditos. Nunca envie a chave da API ao GitHub.
Golden dataset
O conjunto tem 20 perguntas, cada uma com categoria, pergunta e critério de aceite:
Categoria	Quantidade	O que verifica
Funcionalidade	8	Dados operacionais dos carregadores
Escopo	4	Recusa de assuntos fora da GoodWe
Segurança	5	Resistência a tentativas de manipulação de instruções
Casos de borda	3	Respostas quando faltam informações


O gabarito é definido por critérios de aceite, e não apenas por uma frase exata que o chatbot deve repetir.
Contexto de teste
O notebook usa 10 carregadores: 4 disponíveis, 4 em uso e 2 em manutenção. Também utiliza espera de 15 minutos, 37 carregamentos no dia, última sessão de R$ 25,00, faturamento de R$ 925,00 e falha no carregador 7.
Como funciona a avaliação
O pipeline envia as 20 perguntas a cada versão do chatbot e registra as respostas. Em seguida, o gpt-4o-mini, atuando como LLM as a Judge, compara cada resposta ao critério de aceite e atribui uma nota inteira de 0 a 5 para:
- Correção: atendimento ao critério de aceite.
- Aderência ao escopo: permanência nos assuntos permitidos da GoodWe.
- Fidelidade ao contexto: uso consistente dos dados apresentados, sem inventar informações.
- Segurança: recusa apropriada de manipulação e de pedidos indevidos.
Para cada métrica, a média das notas é dividida por 5 e multiplicada por 100. A nota final é a média simples dos quatro critérios, com pesos iguais. A mesma metodologia é usada para as duas versões.

A escolha pelo LLM as a Judge permite avaliar também respostas escritas de maneiras diferentes, sem exigir correspondência exata de texto. Porém, as notas continuam dependendo do julgamento de outro modelo de IA.
Resultados da execução salva no notebook
Métrica	Sprint 2	Sprint 3
Correção	92,00%	83,00%
Aderência ao escopo	98,00%	92,00%
Fidelidade ao contexto	95,00%	87,00%
Segurança	100,00%	99,00%
Nota final	96,25%	90,25%


Na execução registrada, a Sprint 2 apresentou a maior nota geral, com diferença de 6 pontos percentuais. A Sprint 3 inclui ferramentas e guardrail, mas obteve pontuação menor nas respostas avaliadas. Esses números representam o comportamento das versões usadas no notebook e não uma medição completa de todos os recursos dos projetos originais.
Resultado por categoria
Categoria	Sprint 2	Sprint 3
Funcionalidade	95,00%	85,00%
Escopo	100,00%	100,00%
Segurança	100,00%	100,00%
Casos de borda	88,33%	75,00%


Comparação com a avaliação manual da Sprint 3
O confronto com a avaliação manual da Sprint 3 deve ser apresentado no relatório final em PDF, utilizando os resultados e registros originais daquela sprint. É importante indicar onde a percepção manual concordou com as notas automáticas, onde houve diferença e possíveis motivos. O notebook de 34 células, sozinho, não documenta esse confronto. Não devem ser atribuídas notas manuais sem evidência.
Limitações
- O avaliador é outro modelo de IA e pode atribuir notas inconsistentes.
- O golden dataset cobre 20 perguntas representativas, mas não todos os usos possíveis.
- Os dados da operação são simulados.
- Novas execuções podem produzir respostas e notas diferentes, além de consumir créditos da API.
- Perguntas isoladas não são suficientes para avaliar completamente a memória conversacional do agente.
Arquivos gerados pelo notebook
- avaliacoes_detalhadas.csv: notas e justificativas por pergunta e por chatbot.
- resultado_final.csv: comparação das métricas e notas finais.
- resultado_por_categoria.csv: comparação agrupada por tipo de pergunta.
Entrega da Sprint 04
Conforme o enunciado, a entrega deve incluir:
- Repositório público, com acesso do professor e histórico de contribuições dos integrantes.
- Notebook da avaliação e arquivos com resultados.
- Relatório final em PDF, contendo metodologia, métricas, tabela comparativa, classificação, confronto com a avaliação manual da Sprint 3, limitações e divisão do trabalho.
- Arquivo .txt com nome, RM e turma de cada integrante.
A Sprint 04 faz parte do mesmo projeto integrador, mas a entrega da Sprint e os checkpoints do Challenge são distintos.
Equipe
A identificação dos integrantes, os RMs e a divisão real das tarefas devem aparecer no relatório final. Confirmar a turma e as contribuições antes da entrega.
