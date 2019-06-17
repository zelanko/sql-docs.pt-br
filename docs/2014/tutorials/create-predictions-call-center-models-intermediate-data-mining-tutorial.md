---
title: Criando previsões para modelos de Call Center (Tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5be0cec7-f639-4eeb-835e-e3204ae619e9
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 30f24ab457669f572189d2eb13deca3f672f5e18
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63217882"
---
# <a name="creating-predictions-for-the-call-center-models-intermediate-data-mining-tutorial"></a>Criando previsões para modelos de call center (Tutorial de mineração de dados intermediário)
  Agora que aprendeu um pouco sobre as interações entre turnos, o número de operadores, as chamadas e a classificação do serviço, você está pronto para criar algumas consultas de previsão que podem ser usadas na análise e no planejamento empresarial. Primeiro, você criará algumas previsões com base no modelo exploratório para testar algumas suposições. Em seguida, você criará previsões em massa usando o modelo de regressão logística.  
  
 Esta lição pressupõe que você já esteja familiarizado com o conceito de consultas de previsão.  
  
## <a name="creating-predictions-using-the-neural-network-model"></a>Criando previsões usando o modelo de rede neural  
 O exemplo a seguir demonstra como fazer uma previsão singleton usando o modelo de rede neural criado para exploração. As previsões singleton constituem um bom método para testar valores diferentes para visualizar o efeito no modelo. Neste cenário, você fará uma previsão da classificação do serviço para o turno da meia-noite (sem dia da semana especificado), se houver seis operadores experientes em serviço.  
  
#### <a name="to-create-a-singleton-query-by-using-the-neural-network-model"></a>Para criar uma consulta singleton usando-se o modelo de rede neural  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra a solução que contém o modelo que deseja usar.  
  
2.  No Designer de mineração de dados, clique o **previsão de modelo de mineração** guia.  
  
3.  No **modelo de mineração** painel, clique em **Selecionar modelo**.  
  
4.  O **Selecionar modelo de mineração** caixa de diálogo mostra uma lista de estruturas de mineração. Expanda a estrutura de mineração para exibir uma lista dos modelos de mineração associados a essa estrutura.  
  
5.  Expanda a estrutura de mineração Padrão de Call Center e selecione o modelo de rede neural, Call Center - LR.  
  
6.  No menu **Modelo de Mineração** , selecione **Consulta Singleton**.  
  
     O **entrada de consulta Singleton** caixa de diálogo é exibida, com colunas mapeadas para as colunas no modelo de mineração.  
  
7.  No **entrada de consulta Singleton** caixa de diálogo, clique na linha para turno e, em seguida, selecione *meia-noite*.  
  
8.  Clique na linha de Lvl 2 Operators e digite `6`.  
  
9. Na parte inferior metade dos **previsão de modelo de mineração** guia, clique na primeira linha na grade.  
  
10. No **fonte** coluna, clique na seta para baixo e selecione **função de previsão**. No **campo** coluna, selecione **PredictHistogram**.  
  
     Será exibida uma lista de argumentos que você pode usar com essa função de previsão automaticamente na **critérios/argumentos** caixa.  
  
11. Arraste a coluna ServiceGrade da lista de colunas na **modelo de mineração** painel para o **critérios/argumentos** caixa.  
  
     O nome da coluna é inserido automaticamente como o argumento. É possível escolher qualquer coluna de atributo previsível a ser arrastada para essa caixa de texto.  
  
12. Clique no botão **alternar para a consulta resulta exibição**, na parte superior do construtor de consultas de previsão.  
  
 Os resultados esperados contêm os valores previstos possíveis para cada classificação de serviço que recebeu essas entradas, junto com os valores de suporte e probabilidade para cada previsão. É possível retornar para a exibição design a qualquer momento e alterar as entradas ou adicionar mais entradas.  
  
## <a name="creating-predictions-by-using-a-logistic-regression-model"></a>Criando previsões usando-se um modelo de regressão logística  
 Se você já souber os atributos pertinentes ao problema empresarial, poderá usar um modelo de regressão logística para prever o efeito de fazer alterações em alguns atributos. Regressão logística é um método estatístico que é geralmente usado para fazer previsões com base em alterações em variáveis independentes: por exemplo, é usado em contagem financeira, para prever comportamento de clientes com base em demografia de clientes.  
  
 Nesta tarefa, você irá aprender a criar uma fonte de dados a ser usada para previsões e, em seguida, fazer previsões para ajudar a responder várias perguntas comerciais.  
  
### <a name="generating-data-used-for-bulk-prediction"></a>Gerando dados usados para previsão em massa  
 Há muitas maneiras de fornecer dados de entrada: por exemplo, você poderia importar níveis de equipe de uma planilha e executar esses dados pelo modelo para prever a qualidade de serviço durante o próximo mês.  
  
 Nesta lição, você usará o designer de Exibição da Fonte de Dados para criar uma consulta nomeada. Essa consulta nomeada é uma instrução Transact-SQL personalizada que, para cada turno da agenda, calcula o número máximo de operadores na equipe, o mínimo de chamadas recebidas ou o número médio de problemas gerados. Depois, você unirá esses dados em um modelo de mineração para fazer previsões sobre uma série de datas futuras.  
  
##### <a name="to-generate-input-data-for-a-bulk-prediction-query"></a>Para gerar dados de entrada para uma consulta de previsão em massa  
  
1.  No Gerenciador de soluções, clique com botão direito **exibições da fonte de dados**e, em seguida, selecione **nova exibição da fonte de dados**.  
  
2.  No Assistente de exibição da fonte de dados, selecione [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] como a fonte de dados e clique **próxima**.  
  
3.  Sobre o **selecionar tabelas e exibições** , clique em **próxima** sem selecionar nenhuma tabela.  
  
4.  Sobre o **Concluindo o assistente** página, digite o nome, `Shifts`.  
  
     Esse nome será exibido no Gerenciador de Soluções como o nome da exibição da fonte de dados.  
  
5.  O painel de design vazia com o botão direito e selecione **nova consulta nomeada**.  
  
6.  No **criar consulta nomeada** caixa de diálogo, para **nome**, tipo `Shifts for Call Center`.  
  
     Esse nome aparecerá no designer da Exibição da Fonte de Dados somente como o nome da consulta nomeada.  
  
7.  Cole a instrução de consulta a seguir no painel de texto SQL na metade inferior da caixa de diálogo.  
  
    ```  
    SELECT DISTINCT WageType, Shift,   
    AVG(Orders) as AvgOrders, MIN(Orders) as MinOrders, MAX(Orders) as MaxOrders,  
    AVG(Calls) as AvgCalls, MIN(Calls) as MinCalls, MAX(Calls) as MaxCalls,  
    AVG(LevelTwoOperators) as AvgOperators, MIN(LevelTwoOperators) as MinOperators, MAX(LevelTwoOperators) as MaxOperators,  
    AVG(IssuesRaised) as AvgIssues, MIN(IssuesRaised) as MinIssues, MAX(IssuesRaised) as MaxIssues  
    FROM dbo.FactCallCenter  
    GROUP BY Shift, WageType  
    ```  
  
8.  No painel de design, clique na tabela, Shifts for Call Center e selecione **explorar dados** para visualizar os dados conforme retornados pela consulta T-SQL.  
  
9. Clique com botão direito na guia **Shifts (Design),** e, em seguida, clique em **salvar** para salvar a nova definição de exibição de fonte de dados.  
  
### <a name="predicting-service-metrics-for-each-shift"></a>Prevendo a métrica de serviço para cada turno  
 Agora que alguns valores foram gerados para cada turno, você usará esses valores como entrada para o modelo de regressão logística que criará, para gerar algumas previsões que podem ser usadas no planejamento dos negócios.  
  
##### <a name="to-use-the-new-dsv-as-input-to-a-prediction-query"></a>Para usar o novo DSV como entrada para uma consulta de previsão  
  
1.  No Designer de mineração de dados, clique o **previsão de modelo de mineração** guia.  
  
2.  No **modelo de mineração** painel, clique em **Selecionar modelo**e escolha Call Center - LR na lista de modelos disponíveis.  
  
3.  Dos **modelo de mineração** menu, desmarque a opção **consulta Singleton**. Um aviso informa que as entradas de consulta singleton serão perdidas. Clique em **OK**.  
  
     O **entrada de consulta Singleton** caixa de diálogo é substituída com o **Selecionar tabela (s) de entrada** caixa de diálogo.  
  
4.  Clique em **Selecionar Tabela de Casos**.  
  
5.  No **Selecionar tabela** caixa de diálogo, selectShifts da lista de fontes de dados. No **nome da tabela/exibição** , selecione turnos por Call Center (ele pode ser selecionado automaticamente) e depois clique em **Okey.**  
  
     O **previsão de modelo de mineração** superfície de design é atualizada para Mostrar mapeamentos criados com base no que os tipos de dados e nomes de colunas nos dados de entrada e no modelo.  
  
6.  Uma das linhas de junção e, em seguida, selecione **modificar conexões**.  
  
     Nessa caixa de diálogo, é possível ver exatamente quais colunas são mapeadas e quais não são. O modelo de mineração contém as colunas Calls, Orders, IssuesRaised e LvlTwoOperators, que você pode mapear para quaisquer agregações criadas com base nessas colunas na fonte de dados. Nesse cenário, o mapeamento será realizado para as médias.  
  
7.  Clique na célula vazia leveltwooperators e selecione **turnos por Call avgoperators**.  
  
8.  Clique na célula vazia próxima de Calls, selecione **turnos por Call avgcalls**. e, em seguida, clique em **Okey**.  
  
##### <a name="to-create-the-predictions-for-each-shift"></a>Para criar as previsões para cada turno  
  
1.  Na grade, na parte inferior metade da **construtor de consultas de previsão**, clique na célula vazia sob **origem,** e, em seguida, selecione turnos por Call Center.  
  
2.  Na célula vazia sob **campo**, selecione turno.  
  
3.  Clique na próxima linha vazia na grade e repita o procedimento descrito acima para adicionar outra linha a WageType.  
  
4.  Clique na próxima linha vazia na grade. No **fonte** coluna, selecione **função de previsão**. No **campo** coluna, selecione **Predict**.  
  
5.  Arraste a coluna ServiceGrade do **modelo de mineração** painel para baixo na grade e para o **critérios/argumento** célula. No **Alias** , digite **Predicted Service Grade**.  
  
6.  Clique na próxima linha vazia na grade. No **fonte** coluna, selecione **função de previsão**. No **campo** coluna, selecione **PredictProbability**.  
  
7.  Arraste a coluna ServiceGrade do **modelo de mineração** painel para baixo na grade e para o **critérios/argumento** célula. No **Alias** , digite **probabilidade**.  
  
8.  Clique em **alternar para a exibição de resultado de consulta** para exibir as previsões.  
  
 A tabela a seguir mostra exemplos de resultados para cada turno.  
  
|Turno|WageType|Classificação de Serviço Prevista|Probabilidade|  
|-----------|--------------|-----------------------------|-----------------|  
|AM|feriado|0.165|0.377520666|  
|meia-noite|feriado|0.105|0.364105573|  
|PM1|feriado|0.165|0.40056055|  
|PM2|feriado|0.165|0.338532973|  
|AM|weekday|0.165|0.370847617|  
|meia-noite|weekday|0.08|0.352999173|  
|PM1|weekday|0.165|0.317419177|  
|PM2|weekday|0.105|0.311672027|  
  
### <a name="predicting-the-effect-of-reduced-response-time-on-service-grade"></a>Prevendo o efeito do tempo de reposta reduzido na classificação de serviço  
 Você gerou alguns valores de média para cada turno e usou esses valores como entrada para o modelo de regressão logística. No entanto, como o objetivo comercial é manter a taxa de abandono na faixa de 0,00-0,05, os resultados não são encorajadores.  
  
 Por isso, com base no modelo original, que mostrava uma forte influência do tempo de resposta na classificação do serviço, a equipe de Operações opta por executar algumas previsões para avaliar se a redução do tempo médio de resposta para chamadas poderia melhorar a qualidade do serviço. Por exemplo, se você diminuísse o tempo de resposta da chamada para 90 ou até mesmo 80 por cento do tempo atual, o que aconteceria com os valores de classificação de serviço?  
  
 É fácil criar uma exibição de fonte de dados (DSV) que calcule os tempos médios de resposta para cada turno e adicionar colunas para calcular 80% ou 90% do tempo médio de resposta. Assim, você pode usar a DSV como entrada para o modelo.  
  
 Embora as etapas exatas não sejam mostradas aqui, a tabela a seguir compara os efeitos na classificação de serviço quando você reduz os tempos de resposta para 80% ou 90% dos tempos de resposta atuais.  
  
 Destes resultados, você poderia concluir que nos turnos alvo você deve reduzir o tempo de resposta em 90 por cento da taxa atual para melhorar a qualidade de serviço.  
  
|Turno, salário e dia|Qualidade de serviço prevista como o tempo médio de resposta atual|Qualidade de serviço com a redução de 90% no tempo de resposta prevista|Qualidade de serviço prevista como a redução de 80 por cento no tempo de resposta|  
|--------------------------|------------------------------------------------------------------|--------------------------------------------------------------------------|--------------------------------------------------------------------------|  
|Feriado AM|0.165|0,05|0,05|  
|Feriado PM1|0,05|0,05|0,05|  
|Feriado à meia-noite|0.165|0,05|0,05|  
  
 Há várias consultas de previsão que podem ser criadas com base nesse modelo. Por exemplo, você pode prever quantos operadores são obrigatórios para atender a um determinado nível de serviço ou um certo número de chamadas de entrada. Como é possível incluir várias saídas em um modelo de regressão logística, é fácil testar variáveis independentes diferentes e resultados, sem a necessidade de criar muitos modelos separados.  
  
## <a name="remarks"></a>Comentários  
 Os Suplementos de Mineração de Dados para Excel 2007 fornecem assistentes de regressão logística que facilitam a resposta de perguntas complexas, como quantos Operadores de Nível Dois seriam obrigatórios para melhorar a classificação do serviço visando um nível de destino para um turno específico. Os suplementos de mineração de dados são um download gratuito e incluem assistentes baseados nos algoritmos de rede neural ou regressão logística. Para obter mais informações, consulte os seguintes links:  
  
-   [SQL Server 2005 Data Mining Add-Ins para Office 2007](https://www.microsoft.com/sql/technologies/dm/addins.mspx): Meta a atingir e e se a análise de cenário  
  
-   [SQL Server 2008 Data Mining Add-Ins para Office 2007](https://go.microsoft.com/fwlink/?LinkID=117790): Meta a atingir análise do cenário, e se a análise de cenário e cálculo de previsão  
  
## <a name="conclusion"></a>Conclusão  
 Você aprendeu a criar, personalizar e interpretar modelos de mineração baseados nos algoritmos Rede Neural da Microsoft e Regressão Logística da Microsoft. Esses tipos de modelos são sofisticados e permitem uma variedade quase infinita em análise e, portanto, podem ser complexos e difíceis de dominar.  
  
 Porém, esses algoritmos podem iterar por muitas combinações de fatores e identificar automaticamente as correlações mais fortes, fornecendo suporte estatístico para dados que seriam muito difíceis de descobrir por exploração manual de dados usando o Transact-SQL ou até mesmo o PowerPivot.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplos de consulta de modelo de regressão logística](../../2014/analysis-services/data-mining/logistic-regression-model-query-examples.md)   
 [Algoritmo Regressão Logística da Microsoft](../../2014/analysis-services/data-mining/microsoft-logistic-regression-algorithm.md)   
 [Microsoft Neural Network Algorithm](../../2014/analysis-services/data-mining/microsoft-neural-network-algorithm.md)   
 [Exemplos de consulta de modelos de rede neural](../../2014/analysis-services/data-mining/neural-network-model-query-examples.md)  
  
  
