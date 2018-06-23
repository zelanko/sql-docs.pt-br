---
title: Criando uma estrutura de modelo de mineração (Tutorial de mineração de dados intermediário) msc | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e9339227-6c2e-4c4b-8be2-8c1960bc4a8d
caps.latest.revision: 40
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 09aaac50873d6c4c63b46fdf37dd7ee854000886
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312694"
---
# <a name="creating-a-sequence-clustering-mining-model-structure-intermediate-data-mining-tutorial"></a>Criando uma estrutura de modelo de mineração de clustering de sequências (Tutorial de mineração de dados intermediário)
  A primeira etapa da criação de um modelo de mineração de clustering de sequências é usar o Assistente de Mineração de Dados para criar uma nova estrutura de mineração e um modelo de mineração baseado no algoritmo Clustering de Sequências da [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
 Você usará a mesma exibição da fonte de dados utilizada para a análise da cesta de compras, mas adicionará uma coluna com o identificador `sequence`. Neste cenário, a sequência significa a ordem em que o cliente adicionou itens à cesta de compras.  
  
 Você também adicionará algumas colunas usadas em um dos modelos para agrupar clientes por dados demográficos.  
  
### <a name="to-create-a-sequence-clustering-structure-and-model"></a>Para criar uma estrutura e um modelo de de clustering de sequências  
  
1.  No Gerenciador de soluções no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], clique com botão direito **estruturas de mineração** e selecione **nova estrutura de mineração**.  
  
2.  Na página **Bem-vindo ao Assistente de Mineração de Dados** , clique em **Avançar**.  
  
3.  No **Selecionar método de definição** Verifique **de warehouse existente de dados ou banco de dados relacional** está selecionado e, em seguida, clique em **próximo**.  
  
4.  No **criar a estrutura de mineração de dados** , verifique se que a opção **criar estrutura de mineração com um modelo de mineração** está selecionado. Em seguida, clique na lista suspensa para a opção **qual técnica de mineração de dados você deseja usar?** e selecione **msc**. Clique em **Avançar**.  
  
     O **Selecionar exibição da fonte de dados** página será exibida. Em **modos de exibição de fonte de dados disponíveis**, selecione `Orders`.  
  
     Pedidos é a mesma exibição da fonte de dados utilizada para a análise do cenário de cesta de compras. Se você não tiver criado essa exibição da fonte de dados, consulte [adicionando uma exibição da fonte de dados com tabelas aninhadas &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial.md).  
  
5.  Clique em **Avançar**.  
  
6.  No **especificar tipos de tabela** página, selecione o **caso** caixa de seleção próxima ao **vAssocSeqOrders** de tabela e selecione o **aninhadas** caixa de seleção ao lado de **vAssocSeqLineItems** tabela. Clique em **Avançar**.  
  
    > [!NOTE]  
    >  Se ocorrer um erro quando você seleciona o **caso** ou **aninhadas** caixas de seleção, pode ser que a junção na exibição da fonte de dados não está correta. A tabela aninhada, **vAssocSeqLineItems**, deve estar conectado à tabela de casos, **vAssocSeqOrders** por uma junção de muitos-para-um. Você pode editar a relação clicando com o botão direito do mouse na linha de junção e invertendo a direção da junção. Para obter mais informações, consulte [criar ou caixa de diálogo Editar relação &#40;Analysis Services - dados multidimensionais&#41;](../../2014/analysis-services/create-or-edit-relationship-dialog-box-analysis-services-multidimensional-data.md).  
  
7.  Sobre o **especificar os dados de treinamento** página, escolha as colunas para uso no modelo, selecionando a caixa de seleção da seguinte maneira:  
  
    -   **IncomeGroup** selecionar o **entrada** caixa de seleção.  
  
         Essa coluna contém informações interessantes sobre os clientes que poderão ser usadas para clustering. Você a usará no primeiro modelo e vai ignorá-la no segundo.  
  
    -   **OrderNumber** selecionar o `Key` caixa de seleção.  
  
         Esse campo será usado como o identificador da tabela de casos, ou `Key`. Em geral, você nunca deve usar o campo de chave da tabela de casos como uma entrada, já que a chave contém valores exclusivos que não são úteis para clustering.  
  
    -   **Região** selecionar o **entrada** caixa de seleção.  
  
         Essa coluna contém informações interessantes sobre os clientes que poderão ser usadas para clustering. Você a usará no primeiro modelo e vai ignorá-la no segundo.  
  
    -   **LineNumber** selecionar o `Key` e **entrada** caixas de seleção.  
  
         O **LineNumber** campo será usado como o identificador para a tabela aninhada, ou `Sequence Key`. A chave para uma tabela aninhada sempre deve ser usada como entrada.  
  
    -   **Modelo** selecionar o **entrada** e **previsível** caixas de seleção.  
  
     Verifique se as seleções estão corretas e, em seguida, clique em **próximo**.  
  
8.  Sobre o **colunas especificar conteúdo e tipo de dados** página, verifique se a grade contém as colunas, tipos de conteúdo e tipos de dados mostrados na tabela a seguir e, em seguida, clique em **próximo**.  
  
    |Tabelas/Colunas|Tipo de Conteúdo|Tipo de Dados|  
    |---------------------|------------------|---------------|  
    |IncomeGroup|Discreto|Texto|  
    |OrderNumber|Chave|Texto|  
    |Região|Discreto|Texto|  
    |vAssocSeqLineItems|||  
    |Número da Linha|Key Sequence|Longo|  
    |Modelo|Discreto|Texto|  
  
9. No **criar conjunto de testes** página, altere o **porcentagem de dados de teste** para 20 e depois clique em **próximo**.  
  
10. Sobre o **Concluindo o assistente** página, para o **nome da estrutura de mineração**, tipo `Sequence Clustering with Region`.  
  
11. Para o **nome do modelo de mineração**, tipo `Sequence Clustering with Region`.  
  
12. Verifique o **Permitir drill-through** caixa e, em seguida, clique em **concluir**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Processando o modelo de clustering de sequências](../../2014/tutorials/processing-the-sequence-clustering-model.md)  
  
## <a name="see-also"></a>Consulte também  
 [Designer de mineração de dados](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Algoritmo Microsoft Sequence Clustering](../../2014/analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)  
  
  