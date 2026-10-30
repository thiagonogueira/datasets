# Trabalho final — Arquiteturas de atendimento automatizado da Quantum Commerce

**Disciplina:** Orquestração e Integração de Sistemas Multiagentes  
**Curso:** MBA AI Leadership  
**Grupo:** 2 a 5 alunos  
**Entrega:** 06/12/2026

## Objetivo

Construir e comparar duas arquiteturas multiagentes para atendimento ao cliente, recomendar uma delas com base nos resultados e reavaliar a escolha após uma mudança nas regras de atendimento.

## Contexto e desafios

A Quantum Commerce recebe cerca de **100.000 chamados por dia** sobre entregas, devoluções, produtos divergentes ou com defeito, fraudes de vendedores, cobranças indevidas, suspeitas de falsificação e artigos proibidos.

O primeiro nível de atendimento segue sete procedimentos escritos. Os chamados sem procedimento específico são classificados como “Outros”, sem execução de ações. Reembolsos acima do limite de autonomia do atendimento dependem da aprovação de um supervisor humano.

A operação enfrenta três problemas:

- Nas semanas de campanha, a espera pela aprovação dos supervisores ultrapassa dois dias, atrasando os reembolsos.
- Chamados semelhantes recebem tratamentos diferentes, e a auditoria identifica ações realizadas fora da sequência prevista nos procedimentos.
- O custo por chamado aumentou, sem melhora nos dois problemas anteriores.

A diretora de operações decidiu automatizar o primeiro nível de atendimento com agentes de IA, mantendo a aprovação humana nos casos exigidos pelas regras. Duas arquiteturas foram propostas.

**Arquitetura A — Esteira por função**

Todos os chamados passam por três agentes em sequência: um levanta os fatos, outro aplica o procedimento e define as ações, e o terceiro redige a resposta ao cliente.

A área de tecnologia defende que essa organização pode facilitar a auditoria, concentrar a manutenção das regras de decisão e reduzir o consumo de recursos.

**Arquitetura B — Coordenação com especialistas**

Um agente coordenador identifica a natureza do chamado e o encaminha a um especialista responsável pelo procedimento correspondente.

A área de operações defende que essa organização pode preservar a responsabilidade de cada área e facilitar mudanças em procedimentos específicos.

A diretora pediu ao seu grupo que construa as duas arquiteturas, compare seus resultados sobre os mesmos chamados e recomende uma delas. Os argumentos apresentados pelas áreas deverão ser avaliados a partir das evidências obtidas.

## Parte A — Construção e comparação inicial

### Materiais fornecidos

Todos os arquivos do trabalho, incluindo os da Parte B, estão na pasta [trabalho-final](https://github.com/thiagonogueira/datasets/tree/main/mba-ai-leadership/orquestracao-multiagentes/trabalho-final) do repositório da disciplina e no pacote `trabalho-final.zip` disponibilizado no portal.

| Arquivo | Conteúdo | Download |
|---|---|---|
| `regras-v1.md` | Sete procedimentos de atendimento e regras de aprovação de reembolsos. | [link](https://raw.githubusercontent.com/thiagonogueira/datasets/main/mba-ai-leadership/orquestracao-multiagentes/trabalho-final/regras-v1.md) |
| `chamados.md` | Seis chamados, com o relato do cliente e os fatos disponíveis sobre o pedido. | [link](https://raw.githubusercontent.com/thiagonogueira/datasets/main/mba-ai-leadership/orquestracao-multiagentes/trabalho-final/chamados.md) |
| `formato-de-saida.md` | Estrutura obrigatória da saída de cada automação. | [link](https://raw.githubusercontent.com/thiagonogueira/datasets/main/mba-ai-leadership/orquestracao-multiagentes/trabalho-final/formato-de-saida.md) |
| `tabela-de-medicao.xlsx` | Planilha para registrar e avaliar as execuções. | [link](https://raw.githubusercontent.com/thiagonogueira/datasets/main/mba-ai-leadership/orquestracao-multiagentes/trabalho-final/tabela-de-medicao.xlsx) |

Na versão 1, reembolsos de até **R$ 150, inclusive**, podem ser emitidos pelo atendimento. Acima desse valor, a emissão depende da aprovação de um **supervisor humano**.

### Construção

Implemente cada arquitetura como uma automação própria no **CrewAI Studio**.

- **Arquitetura A:** configure três agentes em sequência, responsáveis pelo levantamento dos fatos, pela aplicação do procedimento e definição das ações, e pela redação da resposta. O agente de decisão deverá receber os sete procedimentos em suas instruções.
- **Arquitetura B:** configure um agente coordenador e um especialista por procedimento. Cada especialista deverá receber apenas o procedimento de sua área. O coordenador deverá ter as informações necessárias para encaminhar os chamados.

As duas automações devem seguir o formato definido em `formato-de-saida.md`, contendo:

- Natureza do chamado.
- Ações previstas, na ordem em que seriam executadas.
- Necessidade de aprovação do supervisor humano, com justificativa.
- Resposta ao cliente.

As ações são simuladas: a automação deve informar o que faria, sem realizar reembolsos, alterar pedidos ou enviar mensagens reais a clientes.

Utilize o mesmo modelo de linguagem e configurações equivalentes nas duas arquiteturas. Registre as configurações adotadas e justifique eventuais diferenças necessárias.

### Execução e medição

Após os testes de montagem, publique as duas automações.

Execute cada um dos seis chamados uma vez em cada automação publicada, totalizando **12 execuções medidas na Parte A**. Utilize o mesmo conteúdo de entrada nas duas arquiteturas.

Para cada execução, registre na planilha a saída produzida, os tokens de entrada, o custo estimado e o tempo total de execução apresentados pelo CrewAI Studio. Informe também a moeda utilizada no registro do custo.

Avalie os resultados segundo três critérios:

| Critério | O que verificar |
|---|---|
| Procedimento | A automação escolheu o procedimento correto, incluiu as ações exigidas e respeitou sua ordem, sem propor ações proibidas? |
| Aprovação humana | A automação solicitou aprovação nos casos exigidos pelas regras e apenas nesses casos? |
| Custo e tempo | Qual foi o custo estimado e quanto tempo a automação levou para processar o chamado? |

Descreva as diferenças entre o resultado esperado pelas regras e a saída obtida. Separe os testes de montagem das execuções utilizadas na comparação e registre eventuais repetições e seus motivos.

### Projeção para a operação

A distribuição dos chamados da Quantum Commerce é apresentada a seguir:

| Assunto | Participação no volume de chamados |
|---|---:|
| Entrega e rastreamento | 45% |
| Devolução por arrependimento | 20% |
| Produto divergente | 12% |
| Produto com defeito | 10% |
| Fraude do vendedor | 5% |
| Cobrança indevida | 4% |
| Suspeita de produto falsificado | 3% |
| Artigo proibido | 1% |
| **Total** | **100%** |

Com base nessa distribuição e nos custos e tempos de execução apresentados pelo CrewAI Studio, projete o custo e o desempenho das duas arquiteturas para a operação da Quantum Commerce. Apresente as premissas adotadas e utilize as projeções para fundamentar sua recomendação.

Para as categorias não contempladas nos casos de teste, estime os valores a partir dos resultados das categorias estudadas, justificando as aproximações utilizadas.

### Recomendação inicial

Recomende uma das arquiteturas com base nas execuções e nas projeções. Apresente os resultados que sustentam a escolha, as limitações observadas e os riscos que ainda precisariam ser investigados antes da adoção em produção.

Considere os limites da avaliação: os seis chamados permitem comparar os casos fornecidos, mas não demonstram o desempenho da solução em toda a operação.

Conclua e preserve essa recomendação antes de iniciar a Parte B. Ela deverá permanecer no relatório, mesmo que o grupo mude de decisão posteriormente.

## Parte B — Mudança de política

Semanas após a recomendação inicial, a diretoria aprova três mudanças:

- O limite de reembolso sem aprovação humana passa de R$ 150 para **R$ 300, inclusive**.
- O prazo de devolução por arrependimento passa a **30 dias para clientes do Clube Q+** e permanece em **7 dias para os demais**.
- É criado um procedimento para **cobrança indevida**, com estorno sujeito ao limite de aprovação. Na versão anterior, esses chamados eram classificados como “Outros”, sem execução de ações, e voltavam como retrabalho.

### Materiais fornecidos

| Arquivo | Conteúdo | Download |
|---|---|---|
| `mudanca-de-politica.md` | Memorando com as mudanças aprovadas pela diretoria. | [link](https://raw.githubusercontent.com/thiagonogueira/datasets/main/mba-ai-leadership/orquestracao-multiagentes/trabalho-final/mudanca-de-politica.md) |
| `regras-v2.md` | Versão atualizada dos procedimentos. | [link](https://raw.githubusercontent.com/thiagonogueira/datasets/main/mba-ai-leadership/orquestracao-multiagentes/trabalho-final/regras-v2.md) |

### Previsão

Leia os novos materiais e, **antes de alterar as automações**, registre:

- Quais dos seis chamados devem ter resultados diferentes e o que deve mudar.
- Quais devem permanecer com o mesmo resultado.
- Quais alterações serão necessárias em cada arquitetura.

Preserve essa previsão para compará-la com o que ocorrer durante a atualização e as execuções.

### Atualização e medição

Aplique as mudanças nas duas automações e registre o que foi alterado em cada uma.

Publique as versões atualizadas e execute novamente os seis chamados em cada arquitetura, totalizando **12 execuções medidas na Parte B**.

Utilize o mesmo formato de saída, a mesma planilha e os mesmos critérios de avaliação da Parte A. Mantenha o modelo e as demais configurações para permitir a comparação entre as versões.

### Comparação e decisão final

Compare os resultados com sua previsão e com as medições da Parte A. Analise a correção das saídas, as alterações necessárias em cada arquitetura e as diferenças de custo e tempo.

Atualize as projeções para a operação, mantendo o volume e a distribuição dos chamados, e considere os resultados na decisão final.

Informe se o grupo mantém ou altera a recomendação inicial. Explique o que a mudança de política revelou sobre as arquiteturas que a avaliação da Parte A não havia mostrado.

Manter ou rever a escolha tem o mesmo valor para a avaliação. O que será considerado é a coerência entre a previsão, as evidências e a decisão.

## Entrega

O grupo deverá entregar:

1. **Relatório**, contendo a recomendação original da Parte A e a análise da Parte B, incluindo previsão, alterações realizadas, comparação dos resultados, projeções e decisão final.
2. **Planilha de medição preenchida**, com as 24 execuções medidas e a identificação de eventuais repetições.
3. **Pacote exportado de cada arquitetura na versão final da Parte B**, gerado pela opção de download do Studio.
4. **Endereço de publicação e token de acesso de cada automação**, pelo canal de entrega da disciplina, para reprodução das execuções durante a correção.

### Planejamento das execuções

O trabalho exige **24 execuções medidas**, além dos testes necessários à montagem das automações.

O plano gratuito do Studio permite cinquenta execuções por mês por organização, e as execuções feitas no editor também contam. Antes de iniciar, confira a cota disponível na organização utilizada e planeje os testes para concluir as duas etapas dentro desse limite. A contagem zera na virada do mês.

## Critérios de avaliação

| Componente | Peso |
|---|---:|
| Construção e medição da Parte A | 20% |
| Recomendação da Parte A | 25% |
| Previsão, atualização e medição da Parte B | 20% |
| Comparação e decisão final | 35% |

As projeções serão consideradas na avaliação das recomendações e da comparação entre as arquiteturas.

Boa sorte!

prof. Thiago Nascimento Nogueira  
e-mail: [profthiago.nogueira@fiap.com.br](mailto:profthiago.nogueira@fiap.com.br)  
linkedIn: [https://www.linkedin.com/in/thnogueira/](https://www.linkedin.com/in/thnogueira/)