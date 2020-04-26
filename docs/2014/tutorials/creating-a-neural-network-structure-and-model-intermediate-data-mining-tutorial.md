---
title: Criando uma estrutura de rede neural e um modelo (tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- discretization [Analysis Services]
- DISCRETIZED column
- DiscretizationBuckets property
- DiscretizationMethod property
- EQUAL_AREAS method
ms.assetid: 3f16215c-531e-4ecf-a11f-ee7c6a764463
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6787db165770f944838a312ecd3e0386d161da38
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62856328"
---
# <a name="creating-a-neural-network-structure-and-model-intermediate-data-mining-tutorial"></a>Criando uma estrutura e um modelo de rede neural (Tutorial de mineração de dados intermediário)
  Para criar um modelo de mineração de dados, primeiro você deve usar o Assistente de Mineração de Dados para criar uma nova estrutura de mineração com base na nova exibição da fonte de dados. Nessa tarefa, você usará o assistente para criar uma estrutura de mineração e, ao mesmo tempo, um modelo de mineração associado baseado no algoritmo Rede Neural da [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
 Como as redes neurais são extremamente flexíveis e podem analisar muitas combinações de entradas e saídas, você deve testar várias maneiras de processar os dados para obter os melhores resultados. Por exemplo, talvez você queira personalizar a forma como o destino numérico para a qualidade do serviço é *compartimentalizados*ou agrupado para atender a requisitos de negócios específicos. Para fazer isso, você adicionará uma nova coluna à estrutura de mineração que agrupa dados numéricos de uma maneira diferente e, em seguida, criará um modelo que usa a nova coluna. Você usará esses modelos de mineração para fazer alguma exploração.  
  
 Finalmente, quando você souber, com base no modelo de rede neural, quais fatores têm impacto maior para sua questão comercial, construirá um modelo separado para previsão e marcação. Você usará o algoritmo Regressão Logística da [!INCLUDE[msCoName](../includes/msconame-md.md)], que é baseado no modelo de redes neurais, mas é otimizado para localizar uma solução baseada em entradas específicas.  
  
 **Etapas**  
  
 [Criar a estrutura de mineração padrão e modelo](#bkmk_defaul)  
  
 [Use a diferenciação guardar a coluna previsível](#bkmk_ColumnCopy)  
  
 [Copiar a coluna e alterar o método de diferenciação para um modelo diferente](#bkmk_Alias)  
  
 [Criar um alias para a coluna previsível de modo que você possa comparar modelos](#bkmk_Alias2)  
  
 [Processar todos os modelos](#bkmk_SeedProcess)  
  
## <a name="create-the-default-call-center-structure"></a>Criar a estrutura padrão do Call Center<a name="bkmk_defaul"></a>  
  
1.  Em Gerenciador de Soluções no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], clique com o botão direito do mouse em **estruturas de mineração** e selecione **nova estrutura de mineração**.  
  
2.  Na página **Bem-vindo ao Assistente de Mineração de Dados** , clique em **Avançar**.  
  
3.  Na página **selecionar o método de definição** , verifique se a **partir de banco de dados relacional existente ou data warehouse** está selecionada e clique em **Avançar**.  
  
4.  Na página **criar a estrutura de mineração de dados** , verifique se a opção **criar estrutura de mineração com um modelo de mineração** está selecionada.  
  
5.  Clique na lista suspensa da opção **que data mining técnica deseja usar?** e, em seguida, selecione **redes neurais da Microsoft**.  
  
     Como os modelos de regressão logística se baseiam em redes neurais, você pode reutilizar a mesma estrutura e adicionar um novo modelo de mineração.  
  
6.  Clique em **Avançar**.  
  
     A página **selecionar exibição da fonte de dados** é exibida.  
  
7.  Em **exibições da fonte de dados disponíveis**, selecione `Call Center`e clique em **Avançar**.  
  
8.  Na página **especificar tipos de tabela** , marque a caixa de seleção **caso** ao lado da tabela **FactCallCenter** . Não selecione nada para **DimDate**. Clique em **Avançar**.  
  
9. Na página **especificar os dados de treinamento** , selecione a **chave** ao lado da coluna **FactCallCenterID.**  
  
10. Marque as `Predict` caixas de seleção e de **entrada** .  
  
11. Selecione a **chave**, a **entrada**e `Predict` as caixas de seleção, conforme mostrado na tabela a seguir:  
  
    |Tabelas/Colunas|Chave/Entrada/Prever|  
    |---------------------|-------------------------|  
    |AutomaticResponses|Entrada|  
    |AverageTimePerIssue|Entrada/Prever|  
    |Chamadas|Entrada|  
    |DateKey|Não usar|  
    |DayOfWeek|Entrada|  
    |FactCallCenterID|Chave|  
    |IssuesRaised|Entrada|  
    |LevelOneOperators|Entrada/Prever|  
    |LevelTwoOperators|Entrada|  
    |Orders|Entrada/Prever|  
    |ServiceGrade|Entrada/Prever|  
    |Turno|Entrada|  
    |TotalOperators|Não usar|  
    |WageType|Entrada|  
  
     Observe que várias colunas previsíveis foram selecionadas. Um dos pontos fortes do algoritmo de rede neural é que ele pode analisar todas as combinações possíveis de atributos de entrada e saída. Você não desejaria fazer isso para um grande conjunto de dados, pois ele poderia aumentar exponencialmente o tempo de processamento..  
  
12. Na página **especificar conteúdo e tipo de dados das colunas** , verifique se a grade contém as colunas, os tipos de conteúdo e os tipos de dados, conforme mostrado na tabela a seguir, e clique em **Avançar**.  
  
    |Colunas|Tipo de conteúdo|Tipos de Dados|  
    |-------------|------------------|----------------|  
    |AutomaticResponses|Contínuo|long|  
    |AverageTimePerIssue|Contínuo|long|  
    |Chamadas|Contínuo|long|  
    |DayOfWeek|Discreto|Texto|  
    |FactCallCenterID|Chave|long|  
    |IssuesRaised|Contínuo|long|  
    |LevelOneOperators|Contínuo|long|  
    |LevelTwoOperators|Contínuo|long|  
    |Orders|Contínuo|long|  
    |ServiceGrade|Contínuo|Double|  
    |Turno|Discreto|Texto|  
    |WageType|Discreto|Texto|  
  
13. Na página **criar conjunto de testes** , desmarque a caixa de texto da opção, **porcentagem de dados para teste**. Clique em **Avançar**.  
  
14. Na página **concluindo o assistente** , para o **nome da estrutura**de mineração `Call Center`, digite.  
  
15. Para o **nome do modelo**de mineração `Call Center Default NN`, digite e clique em **concluir**.  
  
     A caixa **permitir Drill-through** está desabilitada porque não é possível detalhar os dados com modelos de rede neural.  
  
16. Em Gerenciador de Soluções, clique com o botão direito do mouse no nome da estrutura de Data Mining que você acabou de criar e selecione **processar**.  
  
## <a name="use-discretization-to-bin-the-target-column"></a>Use a diferenciação guardar a coluna de destino  
 Por padrão, quando você cria um modelo de rede neural que tem um atributo previsível numérico, o algoritmo Rede Neural da Microsoft trata o atributo como um número contínuo. Por exemplo, o atributo ServiceGrade é um número que teoricamente varia de 0.00 (todas as chamadas são atendidas) a 1.00 (todos os chamadores desligam). Neste conjunto de dados, os valores têm a seguinte distribuição:  
  
 ![distribuição de valores de classificação de serviço](../../2014/tutorials/media/skt-service-grade-valuesc.gif "distribuição de valores de classificação de serviço")  
  
 Em virtude disso, quando você processa o modelo, as saídas podem ser agrupadas de modo diferente do esperado. Por exemplo, se você usar clustering para identificar os melhores grupos de valores, o algoritmo dividirá os valores em ServiceGrade em intervalos como este: 0, 748051948-0.09716216215. Embora esse agrupamento seja matematicamente preciso, esse tipo de intervalo pode não ser significativo para usuários empresariais.  
  
 Nesta etapa, para tornar o resultado mais intuitivo, você agrupará os valores numéricos de forma diferente, criando cópias da coluna de dados numéricas.  
  
### <a name="how-discretization-works"></a>Como funciona a diferenciação  
 O Analysis Services fornece vários métodos para guardar ou processar dados numéricos. A tabela a seguir ilustra as diferenças entre os resultados quando o atributo de saída ServiceGrade foi processado de três maneiras diferentes:  
  
-   Tratando-o como um número contínuo.  
  
-   Fazendo o algoritmo usar o clustering para identificar a melhor disposição dos valores.  
  
-   Especificando que os números são guardados pelo método Áreas Iguais.  
  
 Modelo padrão (contínuo)  
  
|VALUE|SUPPORT|  
|-----------|-------------|  
|Ausente|0|  
|0, 9875|120|  
  
 Guardado por clustering  
  
|VALUE|SUPPORT|  
|-----------|-------------|  
|\<0, 748051948|34|  
|0, 748051948-0.09716216215|27|  
|0.09716216215 - 0.13297297295|39|  
|0.13297297295 - 0.167499999975|10|  
|>= 0.167499999975|10|  
  
 Guardado por áreas iguais  
  
|VALUE|SUPPORT|  
|-----------|-------------|  
|\<0, 7|26|  
|0, 7-0, 0|22|  
|0, 9-0,11|36|  
|>= 0,12|36|  
  
> [!NOTE]  
>  É possível obter essas estatísticas do nó de estatísticas marginais do modelo, depois do processamento de todos os dados. Para obter mais informações sobre o nó de estatísticas marginal, consulte [conteúdo do modelo de mineração para modelos de rede neural &#40;&#41;de mineração de dados Analysis Services ](../../2014/analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md).  
  
 Nesta tabela, a coluna VALUE mostra para você como o número de ServiceGrade foi tratado. A coluna SUPPORT mostra para você quantos casos tiveram esse valor ou caíram nesse intervalo.  
  
-   **Usar números contínuos (padrão)**  
  
     Se você usasse o método padrão, o algoritmo computaria os resultados para 120 valores distintos, o valor médio seria 0,09875. Você também pode ver o número de valores ausentes.  
  
-   **Guardar por clustering**  
  
     Se você deixasse o algoritmo Clustering da Microsoft determinar o agrupamento opcional dos valores, o algoritmo agruparia os valores para ServiceGrade em cinco (5) intervalos. O número de casos em cada intervalo não é distribuído uniformemente, como você pode ver na coluna de suporte.  
  
-   **Guardar por áreas iguais**  
  
     Quando você escolhe este método, o algoritmo força os valores em buckets de tamanhos iguais, que por sua vez altera os limites superiores e inferiores de cada intervalo. Você pode especificar o número de buckets, mas você quer evitar ter dois valores pequenos em qualquer bucket.  
  
 Para obter mais informações sobre as opções de compartimentalização, consulte [métodos de discretização &#40;mineração de dados&#41;](../../2014/analysis-services/data-mining/discretization-methods-data-mining.md).  
  
 Como alternativa, em vez de usar os valores numéricos, você pode adicionar uma coluna derivada separada que classifica as notas de serviço em intervalos de destino **Best** predefinidos \<, como melhor (ServiceGrade = 0, 5), **aceitável** (0,10 > ServiceGrade > 0, 5) e **ruim** (ServiceGrade >= 0,10).  
  
###  <a name="create-a-copy-of-a-column-and-change-the-discretization-method"></a><a name="bkmk_newColumn"></a>Criar uma cópia de uma coluna e alterar o método discretização  
 Você fará uma cópia da coluna de mineração que contém o atributo de destino, ServiceGrade e alterará a forma como os números são agrupados. É possível criar várias cópias de qualquer coluna em uma estrutura de mineração, inclusive do atributo previsível.  
  
 Para este tutorial, você usará o método de Áreas Iguais de diferenciação e especificará quatro buckets. Os agrupamentos resultantes desse método são razoavelmente próximos dos valores de destino de interesse de seus usuários empresariais.  
  
####  <a name="to-create-a-customized-copy-of-a-column-in-the-mining-structure"></a><a name="bkmk_ColumnCopy"></a>Para criar uma cópia personalizada de uma coluna na estrutura de mineração  
  
1.  No Gerenciador de Soluções, clique duas vezes na estrutura de mineração que você acabou de criar.  
  
2.  Na guia estrutura de mineração, clique em **Adicionar uma coluna de estrutura de mineração**.  
  
3.  Na caixa de diálogo **Selecionar coluna** , selecione ServiceGrade na lista na **coluna origem**e clique em **OK**.  
  
     Uma nova coluna é adicionada à lista de colunas da estrutura de mineração. Por padrão, a nova coluna de mineração tem o mesmo nome que a coluna existente, com uma pós-fixação numérica: por exemplo, ServiceGrade 1. É possível alterar o nome dessa coluna para que seja mais descritivo.  
  
     Você também especificará o método de diferenciação.  
  
4.  Clique com o botão direito do mouse em ServiceGrade 1 e selecione **Propriedades**.  
  
5.  Na janela **Propriedades** , localize a propriedade **nome** e altere o nome para compartimentalizados de **nível de serviço** .  
  
6.  Uma caixa de diálogo é exibida perguntando se você deseja fazer a mesma alteração no nome de todas as colunas do modelo de mineração relacionado. Clique em **Não**.  
  
7.  Na janela **Propriedades** , localize o tipo de **dados** da seção e expanda-o, se necessário.  
  
8.  Altere o valor da propriedade `Content` de `Continuous` para `Discretized`.  
  
     As propriedades a seguir estão disponíveis agora: Altere os valores das propriedades como mostrado na tabela seguinte:  
  
    |Propriedade|Valor padrão|Novo valor|  
    |--------------|-------------------|---------------|  
    |`DiscretizationMethod`|`Continuous`|`EqualAreas`|  
    |`DiscretizationBucketCount`|Sem valor|4|  
  
    > [!NOTE]  
    >  O valor padrão de <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> é de fato 0, o que significa que o algoritmo determina o número ideal de buckets automaticamente. Portanto, se você quiser redefinir o valor dessa propriedade como seu padrão, digite 0.  
  
9. No designer de mineração de dados, clique na guia **modelos de mineração** .  
  
     Observe que quando você adiciona uma cópia de uma coluna da estrutura de mineração, o sinalizador de uso da cópia é definido automaticamente como `Ignore`. Normalmente, quando você adiciona uma cópia de uma coluna a uma estrutura de mineração, você não usa a cópia para análise junto com a coluna original ou o algoritmo localizará uma correlação forte entre as duas colunas que pode obscurecer outras relações.  
  
##  <a name="add-a-new-mining-model-to-the-mining-structure"></a><a name="bkmk_NewModel"></a>Adicionar um novo modelo de mineração à estrutura de mineração  
 Agora que criou um novo agrupamento para o atributo de destino, você precisa adicionar um novo modelo de mineração que use a coluna de dados discretos. Ao concluir, a estrutura de mineração de CallCenter terá dois modelos de mineração:  
  
-   O modelo de mineração MN Padrão do Call Center trata os valores de ServiceGrade valores como um intervalo contínuo.  
  
-   Você criará um novo modelo de mineração, o Call Center compartimentalizados NN, que usa como seu destino nos origina os valores da coluna ServiceGrade, distribuídos em quatro buckets de tamanho igual.  
  
#### <a name="to-add-a-mining-model-based-on-the-new-discretized-column"></a>Para adicionar um modelo de mineração baseado na nova coluna de dados discretos  
  
1.  No Gerenciador de Soluções, clique com o botão direito do mouse na estrutura de mineração que você acabou de criar e selecione **abrir**.  
  
2.  Clique na guia **Modelos de Mineração** .  
  
3.  Clique em **criar um modelo de mineração relacionado**.  
  
4.  Na caixa de diálogo **novo modelo de mineração** , para **nome**do modelo `Call Center Binned NN`, digite. Na lista suspensa **nome do algoritmo** , selecione **rede neural da Microsoft**.  
  
5.  Na lista de colunas contidas no novo modelo de mineração, localize ServiceGrade e altere o uso de `Predict` para `Ignore`.  
  
6.  De maneira semelhante, localize ServiceGrade Guardado e altere o uso de `Ignore` para `Predict`.  
  
##  <a name="create-an-alias-for-the-target-column"></a><a name="bkmk_Alias2"></a>Criar um alias para a coluna de destino  
 Ordinariamente você não pode comparar modelos de mineração que usam atributos previsíveis diferentes. No entanto, é possível criar um alias para uma coluna do modelo de mineração. Ou seja, você pode renomear a coluna, ServiceGrade compartimentalizados, no modelo de mineração para que ela tenha o mesmo nome que a coluna original. Em seguida, é possível comparar diretamente esses dois modelos em um gráfico de exatidão, embora os dados sejam diferenciados de maneira diferente.  
  
###  <a name="to-add-an-alias-for-a-mining-structure-column-in-a-mining-model"></a><a name="bkmk_Alias"></a>Para adicionar um alias para uma coluna de estrutura de mineração em um modelo de mineração  
  
1.  Na guia **modelos de mineração** , em **estrutura**, selecione ServiceGrade compartimentalizados.  
  
     Observe que a janela **Propriedades** exibe as propriedades do objeto, ScalarMiningStructure coluna.  
  
2.  Na coluna do modelo de mineração, NM Guardado do ServiceGrade, clique na célula que corresponde à coluna ServiceGrade Guardado.  
  
     Observe que agora a janela **Propriedades** exibe as propriedades do objeto, MiningModelColumn.  
  
3.  Localize a propriedade **Name** e altere o valor para `ServiceGrade`.  
  
4.  Localize a propriedade **Descrição** e digite **alias de coluna temporária**.  
  
     A janela **Propriedades** deve conter as seguintes informações:  
  
    |Propriedade|Valor|  
    |--------------|-----------|  
    |**Descrição**|Alias temporário da coluna|  
    |**ID**|ServiceGrade compartimentalizados|  
    |**Sinalizadores de modelagem**||  
    |**Nome**|Nível de serviço|  
    |**ID da SourceColumn**|Nível de serviço 1|  
    |**Uso**|Predict|  
  
5.  Clique em qualquer lugar na guia **modelo de mineração** .  
  
     A grade é atualizada para mostrar o novo alias de coluna temporário `ServiceGrade`, ao lado do uso da coluna. A grade que contém a estrutura de mineração e dois modelos de mineração devem ser parecidas com o seguinte:  
  
    |Estrutura|NM Padrão do Center|NM Guardado do Call Center|  
    |---------------|----------------------------|---------------------------|  
    ||Rede Neural da Microsoft|Rede Neural da Microsoft|  
    |AutomaticResponses|Entrada|Entrada|  
    |AverageTimePerIssue|Predict|Predict|  
    |Chamadas|Entrada|Entrada|  
    |DayOfWeek|Entrada|Entrada|  
    |FactCallCenterID|Chave|Chave|  
    |IssuesRaised|Entrada|Entrada|  
    |LevelOneOperators|Entrada|Entrada|  
    |LevelTwoOperators|Entrada|Entrada|  
    |Orders|Entrada|Entrada|  
    |ServiceGrade Guardado|Ignorar|Prever (ServiceGrade)|  
    |ServiceGrade|Predict|Ignorar|  
    |Turno|Entrada|Entrada|  
    |Total de Operadores|Entrada|Entrada|  
    |WageType|Entrada|Entrada|  
  
## <a name="process-all-models"></a>Processar todos os modelos  
 Finalmente, para garantir que os modelos criados possam ser comparados facilmente, você definirá o parâmetro de semente para os dois modelos padrão e guardado. A definição de um valor de semente garante que cada modelo inicia o processamento dos dados no mesmo ponto.  
  
> [!NOTE]  
>  Se você não especificar um valor numérico para o parâmetro de semente, o SQL Server Analysis Services gerará uma semente com base no nome do modelo. Como os modelos sempre têm nomes diferentes, defina um valor de semente para garantir que eles processem os dados na mesma ordem.  
  
###  <a name="to-specify-the-seed-and-process-the-models"></a><a name="bkmk_SeedProcess"></a>Para especificar a semente e processar os modelos  
  
1.  Na guia **modelo de mineração** , clique com o botão direito do mouse na coluna do modelo chamado Call Center-LR e selecione **definir parâmetros de algoritmo**.  
  
2.  Na linha do parâmetro HOLDOUT_SEED, clique na célula vazia em **valor**e digite `1`. Clique em **OK**. Repita essa etapa para cada modelo associado à estrutura.  
  
    > [!NOTE]  
    >  O valor escolhido como semente não importa, desde que você use a mesma semente para todos os modelos relacionados.  
  
3.  No menu **modelos de mineração** , selecione **processar estrutura de mineração e todos os modelos**. Clique em **Sim** para implantar o projeto de Data Mining atualizado no servidor.  
  
4.  Na caixa de diálogo **modelo de mineração de processo** , clique em **executar**.  
  
5.  Clique em **fechar** para fechar a caixa de diálogo **progresso do processo** e clique em **fechar** novamente na caixa de diálogo **processar modelo de mineração** .  
  
 Agora que criou os dois modelos de mineração relacionados, você explorará os dados para descobrir relações nos dados.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Explorando o modelo do Call Center &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/exploring-the-call-center-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Estruturas de Mineração &#40;Analysis Services – Data Mining&#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)  
  
  
