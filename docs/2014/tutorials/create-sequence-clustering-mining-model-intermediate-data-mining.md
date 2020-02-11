---
title: Criando uma estrutura de modelo de mineração de clustering de sequências (tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: e9339227-6c2e-4c4b-8be2-8c1960bc4a8d
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b7f4f543952fd86cf6c3c66f9f4b2c51019b1869
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63273475"
---
# <a name="creating-a-sequence-clustering-mining-model-structure-intermediate-data-mining-tutorial"></a>Criando uma estrutura de modelo de mineração de clustering de sequências (Tutorial de mineração de dados intermediário)
  A primeira etapa da criação de um modelo de mineração de clustering de sequências é usar o Assistente de Mineração de Dados para criar uma nova estrutura de mineração e um modelo de mineração baseado no algoritmo Clustering de Sequências da [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
 Você usará a mesma exibição da fonte de dados utilizada para a análise da cesta de compras, mas adicionará uma coluna com o identificador `sequence`. Neste cenário, a sequência significa a ordem em que o cliente adicionou itens à cesta de compras.  
  
 Você também adicionará algumas colunas usadas em um dos modelos para agrupar clientes por dados demográficos.  
  
### <a name="to-create-a-sequence-clustering-structure-and-model"></a>Para criar uma estrutura e um modelo de de clustering de sequências  
  
1.  Em Gerenciador de Soluções no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], clique com o botão direito do mouse em **estruturas de mineração** e selecione **nova estrutura de mineração**.  
  
2.  Na página **Bem-vindo ao Assistente de Mineração de Dados** , clique em **Avançar**.  
  
3.  Na página **selecionar o método de definição** , verifique se a **partir de banco de dados relacional existente ou data warehouse** está selecionada e clique em **Avançar**.  
  
4.  Na página **criar a estrutura de mineração de dados** , verifique se a opção **criar estrutura de mineração com um modelo de mineração** está selecionada. Em seguida, clique na lista suspensa da opção, **que data mining técnica deseja usar?** e selecione **clustering de sequências da Microsoft**. Clique em **Próximo**.  
  
     A página **selecionar exibição da fonte de dados** é exibida. Em **exibições da fonte de dados disponíveis**, selecione `Orders`.  
  
     Pedidos é a mesma exibição da fonte de dados utilizada para a análise do cenário de cesta de compras. Se você não tiver criado essa exibição da fonte de dados, consulte [o tutorial adicionar uma exibição da fonte de dados com tabelas aninhadas &#40;&#41;de mineração de dados intermediários ](../../2014/tutorials/adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial.md).  
  
5.  Clique em **Próximo**.  
  
6.  Na página **especificar tipos de tabela** , marque a caixa de seleção **caso** ao lado da tabela **vAssocSeqOrders** e marque a caixa de seleção **aninhada** ao lado da tabela **vAssocSeqLineItems** . Clique em **Próximo**.  
  
    > [!NOTE]  
    >  Se ocorrer um erro quando você marcar as caixas de seleção **caso** ou **aninhado** , pode ser que a junção na exibição da fonte de dados não esteja correta. A tabela aninhada, **vAssocSeqLineItems**, deve estar conectada à tabela de casos, **vAssocSeqOrders,** por uma junção de muitos para um. Você pode editar a relação clicando com o botão direito do mouse na linha de junção e invertendo a direção da junção. Para obter mais informações, consulte [a caixa de diálogo criar ou editar relação &#40;Analysis Services-&#41;de dados multidimensionais ](../../2014/analysis-services/create-or-edit-relationship-dialog-box-analysis-services-multidimensional-data.md).  
  
7.  Na página **especificar os dados de treinamento** , escolha as colunas a serem usadas no modelo marcando uma caixa de seleção da seguinte maneira:  
  
    -   **Invir** Marque a caixa de seleção **entrada** .  
  
         Essa coluna contém informações interessantes sobre os clientes que poderão ser usadas para clustering. Você a usará no primeiro modelo e vai ignorá-la no segundo.  
  
    -   **OrderNumber** Marque a `Key` caixa de seleção.  
  
         Esse campo será usado como o identificador da tabela de casos, ou `Key`. Em geral, você nunca deve usar o campo de chave da tabela de casos como uma entrada, já que a chave contém valores exclusivos que não são úteis para clustering.  
  
    -   **Região** do Marque a caixa de seleção **entrada** .  
  
         Essa coluna contém informações interessantes sobre os clientes que poderão ser usadas para clustering. Você a usará no primeiro modelo e vai ignorá-la no segundo.  
  
    -   **LineNumber** Marque as `Key` caixas de seleção e de **entrada** .  
  
         O campo **LineNumber** será usado como o identificador para a tabela aninhada ou `Sequence Key`. A chave para uma tabela aninhada sempre deve ser usada como entrada.  
  
    -   **Modelo** Marque as caixas de seleção **entrada** e **previsível** .  
  
     Verifique se as seleções estão corretas e clique em **Avançar**.  
  
8.  Na página **especificar conteúdo e tipo de dados das colunas** , verifique se a grade contém as colunas, os tipos de conteúdo e os tipos de dados mostrados na tabela a seguir e clique em **Avançar**.  
  
    |Tabelas/Colunas|Tipo de conteúdo|Tipo de Dados|  
    |---------------------|------------------|---------------|  
    |IncomeGroup|Discreto|Texto|  
    |OrderNumber|Chave|Texto|  
    |Região|Discreto|Texto|  
    |vAssocSeqLineItems|||  
    |Número da Linha|Key Sequence|long|  
    |Modelo|Discreto|Texto|  
  
9. Na página **criar conjunto de testes** , altere a **porcentagem de dados para teste** para 20 e clique em **Avançar**.  
  
10. Na página **concluindo o assistente** , para o **nome da estrutura**de mineração `Sequence Clustering with Region`, digite.  
  
11. Para o **nome do modelo**de mineração `Sequence Clustering with Region`, digite.  
  
12. Marque a caixa **permitir Drill-through** e clique em **concluir**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Processando o modelo de clustering de sequências](../../2014/tutorials/processing-the-sequence-clustering-model.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Designer de mineração de dados](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Microsoft Sequence Clustering Algorithm](../../2014/analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)  
  
  
