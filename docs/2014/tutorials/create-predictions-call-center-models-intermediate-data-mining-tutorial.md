---
title: Criando previsões para os modelos do Call Center (tutorial de mineração de dados intermediário) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63217882"
---
# <a name="creating-predictions-for-the-call-center-models-intermediate-data-mining-tutorial"></a>Criando previsões para modelos de call center (Tutorial de mineração de dados intermediário)
  Agora que aprendeu um pouco sobre as interações entre turnos, o número de operadores, as chamadas e a classificação do serviço, você está pronto para criar algumas consultas de previsão que podem ser usadas na análise e no planejamento empresarial. Primeiro, você criará algumas previsões com base no modelo exploratório para testar algumas suposições. Em seguida, você criará previsões em massa usando o modelo de regressão logística.  
  
 Esta lição pressupõe que você já esteja familiarizado com o conceito de consultas de previsão.  
  
## <a name="creating-predictions-using-the-neural-network-model"></a>Criando previsões usando o modelo de rede neural  
 O exemplo a seguir demonstra como fazer uma previsão singleton usando o modelo de rede neural criado para exploração. As previsões singleton constituem um bom método para testar valores diferentes para visualizar o efeito no modelo. Neste cenário, você fará uma previsão da classificação do serviço para o turno da meia-noite (sem dia da semana especificado), se houver seis operadores experientes em serviço.  
  
#### <a name="to-create-a-singleton-query-by-using-the-neural-network-model"></a>Para criar uma consulta singleton usando-se o modelo de rede neural  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra a solução que contém o modelo que deseja usar.  
  
2.  No designer de mineração de dados, clique na guia **previsão do modelo de mineração** .  
  
3.  No painel **modelo de mineração** , clique em **selecionar modelo**.  
  
4.  A caixa de diálogo **selecionar modelo de mineração** mostra uma lista de estruturas de mineração. Expanda a estrutura de mineração para exibir uma lista dos modelos de mineração associados a essa estrutura.  
  
5.  Expanda a estrutura de mineração Padrão de Call Center e selecione o modelo de rede neural, Call Center - LR.  
  
6.  No menu **Modelo de Mineração** , selecione **Consulta Singleton**.  
  
     A caixa de diálogo **entrada de consulta singleton** é exibida, com colunas mapeadas para as colunas no modelo de mineração.  
  
7.  Na caixa de diálogo **entrada de consulta singleton** , clique na linha para Shift e, em seguida, selecione *meia-noite*.  
  
8.  Clique na linha de lvl 2 Operators e digite `6`.  
  
9. Na metade inferior da guia **previsão do modelo de mineração** , clique na primeira linha da grade.  
  
10. Na coluna **origem** , clique na seta para baixo e selecione **função de previsão**. Na coluna **campo** , selecione **PredictHistogram**.  
  
     Uma lista de argumentos que você pode usar com essa função de previsão aparece automaticamente na caixa **critérios/argumentos** .  
  
11. Arraste a coluna ServiceGrade da lista de colunas no painel **modelo de mineração** até a caixa **critérios/argumentos** .  
  
     O nome da coluna é inserido automaticamente como o argumento. É possível escolher qualquer coluna de atributo previsível a ser arrastada para essa caixa de texto.  
  
12. Clique no botão **alternar para a exibição de resultados da consulta**, no canto superior do construtor de consultas de previsão.  
  
 Os resultados esperados contêm os valores previstos possíveis para cada classificação de serviço que recebeu essas entradas, junto com os valores de suporte e probabilidade para cada previsão. É possível retornar para a exibição design a qualquer momento e alterar as entradas ou adicionar mais entradas.  
  
## <a name="creating-predictions-by-using-a-logistic-regression-model"></a>Criando previsões usando-se um modelo de regressão logística  
 Se você já souber os atributos pertinentes ao problema empresarial, poderá usar um modelo de regressão logística para prever o efeito de fazer alterações em alguns atributos. Regressão logística é um método estatístico que é geralmente usado para fazer previsões com base em alterações em variáveis independentes: por exemplo, é usado em contagem financeira, para prever comportamento de clientes com base em demografia de clientes.  
  
 Nesta tarefa, você irá aprender a criar uma fonte de dados a ser usada para previsões e, em seguida, fazer previsões para ajudar a responder várias perguntas comerciais.  
  
### <a name="generating-data-used-for-bulk-prediction"></a>Gerando dados usados para previsão em massa  
 Há muitas maneiras de fornecer dados de entrada: por exemplo, você poderia importar níveis de equipe de uma planilha e executar esses dados pelo modelo para prever a qualidade de serviço durante o próximo mês.  
  
 Nesta lição, você usará o designer de Exibição da Fonte de Dados para criar uma consulta nomeada. Essa consulta nomeada é uma instrução Transact-SQL personalizada que, para cada turno da agenda, calcula o número máximo de operadores na equipe, o mínimo de chamadas recebidas ou o número médio de problemas gerados. Depois, você unirá esses dados em um modelo de mineração para fazer previsões sobre uma série de datas futuras.  
  
##### <a name="to-generate-input-data-for-a-bulk-prediction-query"></a>Para gerar dados de entrada para uma consulta de previsão em massa  
  
1.  Em Gerenciador de Soluções, clique com o botão direito do mouse em **exibições da fonte de dados**e selecione **nova exibição da fonte de dados**.  
  
2.  No assistente de exibição da fonte de dados [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] , selecione como a fonte de dados e clique em **Avançar**.  
  
3.  Na página **selecionar tabelas e exibições** , clique em **Avançar** sem selecionar nenhuma tabela.  
  
4.  Na página **concluindo o assistente** , digite o nome, `Shifts`.  
  
     Esse nome será exibido no Gerenciador de Soluções como o nome da exibição da fonte de dados.  
  
5.  Clique com o botão direito do mouse no painel Design vazio e selecione **nova consulta nomeada**.  
  
6.  Na caixa de diálogo **criar consulta nomeada** , em **nome**, digite `Shifts for Call Center`.  
  
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
  
8.  No painel Design, clique com o botão direito do mouse na tabela, mude para o Call Center e selecione **explorar dados** para visualizar os dados conforme retornados pela consulta T-SQL.  
  
9. Clique com o botão direito do mouse na guia, **Shifts. dsv (Design)** e clique em **salvar** para salvar a nova definição da exibição da fonte de dados.  
  
### <a name="predicting-service-metrics-for-each-shift"></a>Prevendo a métrica de serviço para cada turno  
 Agora que alguns valores foram gerados para cada turno, você usará esses valores como entrada para o modelo de regressão logística que criará, para gerar algumas previsões que podem ser usadas no planejamento dos negócios.  
  
##### <a name="to-use-the-new-dsv-as-input-to-a-prediction-query"></a>Para usar o novo DSV como entrada para uma consulta de previsão  
  
1.  No designer de mineração de dados, clique na guia **previsão do modelo de mineração** .  
  
2.  No painel **modelo de mineração** , clique em **selecionar modelo**e escolha Call Center-LR na lista de modelos disponíveis.  
  
3.  No menu **modelo de mineração** , desmarque a opção, **consulta singleton**. Um aviso informa que as entradas de consulta singleton serão perdidas. Clique em **OK**.  
  
     A caixa de diálogo **entrada de consulta singleton** é substituída pela caixa de diálogo **selecionar tabela (s) de entrada** .  
  
4.  Clique em **Selecionar Tabela de Casos**.  
  
5.  Na caixa de diálogo **selecionar tabela** , selectShifts na lista de fontes de dados. Na lista **nome da tabela/exibição** , selecione turnos para o Call Center (pode ser selecionado automaticamente) e clique em **OK.**  
  
     A superfície de design de **previsão do modelo de mineração** é atualizada para mostrar mapeamentos criados com base nos nomes e tipos de dados de colunas nos dados de entrada e no modelo.  
  
6.  Clique com o botão direito do mouse em uma das linhas de junção e selecione **Modificar Conexões**.  
  
     Nessa caixa de diálogo, é possível ver exatamente quais colunas são mapeadas e quais não são. O modelo de mineração contém as colunas Calls, Orders, IssuesRaised e LvlTwoOperators, que você pode mapear para quaisquer agregações criadas com base nessas colunas na fonte de dados. Nesse cenário, o mapeamento será realizado para as médias.  
  
7.  Clique na célula vazia ao lado de LevelTwoOperators e selecione **turnos para Call Center. AvgOperators**.  
  
8.  Clique na célula vazia ao lado de chamadas, selecione **turnos para Call Center. AvgCalls**. e clique em **OK**.  
  
##### <a name="to-create-the-predictions-for-each-shift"></a>Para criar as previsões para cada turno  
  
1.  Na grade na metade inferior da **Construtor de consultas de previsão**, clique na célula vazia em **origem** e selecione turnos para o Call Center.  
  
2.  Na célula vazia em **campo**, selecione Shift.  
  
3.  Clique na próxima linha vazia na grade e repita o procedimento descrito acima para adicionar outra linha a WageType.  
  
4.  Clique na próxima linha vazia na grade. Na coluna **origem** , selecione **função de previsão**. Na coluna **campo** , selecione **prever**.  
  
5.  Arraste a coluna ServiceGrade do painel **modelo de mineração** para baixo até a grade e para a célula **critérios/argumento** . No campo **alias** , digite a **classificação de serviço prevista**.  
  
6.  Clique na próxima linha vazia na grade. Na coluna **origem** , selecione **função de previsão**. Na coluna **campo** , selecione **PredictProbability**.  
  
7.  Arraste a coluna ServiceGrade do painel **modelo de mineração** para baixo até a grade e para a célula **critérios/argumento** . No campo **alias** , digite **probabilidade**.  
  
8.  Clique em **alternar para a exibição de resultado da consulta** para exibir as previsões.  
  
 A tabela a seguir mostra exemplos de resultados para cada turno.  
  
|Shift|WageType|Classificação de Serviço Prevista|Probabilidade|  
|-----------|--------------|-----------------------------|-----------------|  
|AM|feriado|0,165|0,377520666|  
|meia-noite|feriado|0,105|0,364105573|  
|PM1|feriado|0,165|0,40056055|  
|PM2|feriado|0,165|0,338532973|  
|AM|weekday|0,165|0,370847617|  
|meia-noite|weekday|0.08|0,352999173|  
|PM1|weekday|0,165|0,317419177|  
|PM2|weekday|0,105|0,311672027|  
  
### <a name="predicting-the-effect-of-reduced-response-time-on-service-grade"></a>Prevendo o efeito do tempo de reposta reduzido na classificação de serviço  
 Você gerou alguns valores de média para cada turno e usou esses valores como entrada para o modelo de regressão logística. No entanto, como o objetivo comercial é manter a taxa de abandono na faixa de 0,00-0,05, os resultados não são encorajadores.  
  
 Por isso, com base no modelo original, que mostrava uma forte influência do tempo de resposta na classificação do serviço, a equipe de Operações opta por executar algumas previsões para avaliar se a redução do tempo médio de resposta para chamadas poderia melhorar a qualidade do serviço. Por exemplo, se você diminuísse o tempo de resposta da chamada para 90 ou até mesmo 80 por cento do tempo atual, o que aconteceria com os valores de classificação de serviço?  
  
 É fácil criar uma exibição de fonte de dados (DSV) que calcule os tempos médios de resposta para cada turno e adicionar colunas para calcular 80% ou 90% do tempo médio de resposta. Assim, você pode usar a DSV como entrada para o modelo.  
  
 Embora as etapas exatas não sejam mostradas aqui, a tabela a seguir compara os efeitos na classificação de serviço quando você reduz os tempos de resposta para 80% ou 90% dos tempos de resposta atuais.  
  
 Destes resultados, você poderia concluir que nos turnos alvo você deve reduzir o tempo de resposta em 90 por cento da taxa atual para melhorar a qualidade de serviço.  
  
|Turno, salário e dia|Qualidade de serviço prevista como o tempo médio de resposta atual|Qualidade de serviço prevista com redução de 90% no tempo de resposta|Qualidade de serviço prevista como a redução de 80 por cento no tempo de resposta|  
|--------------------------|------------------------------------------------------------------|--------------------------------------------------------------------------|--------------------------------------------------------------------------|  
|Feriado AM|0,165|0,05|0,05|  
|Feriado PM1|0,05|0,05|0,05|  
|Feriado à meia-noite|0,165|0,05|0,05|  
  
 Há várias consultas de previsão que podem ser criadas com base nesse modelo. Por exemplo, você pode prever quantos operadores são obrigatórios para atender a um determinado nível de serviço ou um certo número de chamadas de entrada. Como é possível incluir várias saídas em um modelo de regressão logística, é fácil testar variáveis independentes diferentes e resultados, sem a necessidade de criar muitos modelos separados.  
  
## <a name="remarks"></a>Comentários  
 Os Suplementos de Mineração de Dados para Excel 2007 fornecem assistentes de regressão logística que facilitam a resposta de perguntas complexas, como quantos Operadores de Nível Dois seriam obrigatórios para melhorar a classificação do serviço visando um nível de destino para um turno específico. Os suplementos de mineração de dados são um download gratuito e incluem assistentes baseados nos algoritmos de rede neural ou regressão logística. Para obter mais informações, consulte os links a seguir:  
  
-   [Suplementos de mineração de dados do SQL Server 2005 para Office 2007](https://www.microsoft.com/sql/technologies/dm/addins.mspx): meta Seek e análise de cenário de What If  
  
-   [SQL Server de suplementos de mineração de dados do 2008 para Office 2007](https://go.microsoft.com/fwlink/?LinkID=117790): análise do cenário de busca de meta, análise de cenário de What If e cálculo de previsão  
  
## <a name="conclusion"></a>Conclusão  
 Você aprendeu a criar, personalizar e interpretar modelos de mineração baseados nos algoritmos Rede Neural da Microsoft e Regressão Logística da Microsoft. Esses tipos de modelos são sofisticados e permitem uma variedade quase infinita em análise e, portanto, podem ser complexos e difíceis de dominar.  
  
 Porém, esses algoritmos podem iterar por muitas combinações de fatores e identificar automaticamente as correlações mais fortes, fornecendo suporte estatístico para dados que seriam muito difíceis de descobrir por exploração manual de dados usando o Transact-SQL ou até mesmo o PowerPivot.  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplos de consulta de modelo de regressão logística](../../2014/analysis-services/data-mining/logistic-regression-model-query-examples.md)   
 [Algoritmo de regressão logística da Microsoft](../../2014/analysis-services/data-mining/microsoft-logistic-regression-algorithm.md)   
 [Algoritmo rede neural da Microsoft](../../2014/analysis-services/data-mining/microsoft-neural-network-algorithm.md)   
 [Neural Network Model Query Examples](../../2014/analysis-services/data-mining/neural-network-model-query-examples.md)  
  
  
