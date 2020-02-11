---
title: Criando uma estrutura e um modelo de cesta de compras (tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 659b7a4e-f687-44d9-a60a-86490ccbf90f
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 207d82f740b7b5ff174e220e647d67d5bac7f9ea
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63190836"
---
# <a name="creating-a-market-basket-structure-and-model-intermediate-data-mining-tutorial"></a>Criando uma estrutura e um modelo de cesta de compras (Tutorial de mineração de dados intermediário)
  Agora que você criou uma exibição da fonte de dados, usará o Assistente de Mineração de Dados para criar uma nova estrutura de mineração. Nesta tarefa, você criará uma estrutura de mineração e um modelo de mineração baseado no algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Association.  
  
> [!NOTE]  
>  Se você encontrar um erro indicando que vAssocSeqLineItems não pode ser usado como uma tabela aninhada, volte para a tarefa anterior da lição e crie a junção muitos para um, arrastando da tabela vAssocSeqLineItems (o lado muitos) para a tabela vAssocSeqOrders (o lado um). Você também pode editar a relação entre as tabelas, clicando com o botão direito em a linha de junção.  
  
### <a name="to-create-an-association-mining-structure"></a>Para criar uma estrutura de mineração de associação  
  
1.  Em Gerenciador de Soluções no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], clique com o botão direito do mouse em **estruturas de mineração** e selecione **nova estrutura de mineração** para abrir o assistente de mineração de dados.  
  
2.  Na página **Bem-vindo ao Assistente de Mineração de Dados** , clique em **Avançar**.  
  
3.  Na página **selecionar o método de definição** , verifique se a **partir de banco de dados relacional existente ou data warehouse** está selecionada e clique em **Avançar**.  
  
4.  Na página **criar a estrutura de mineração de dados** , sob a **qual data mining técnica você deseja usar?**, selecione **regras de associação da Microsoft** na lista e clique em **Avançar**. A página **selecionar exibição da fonte de dados** é exibida.  
  
5.  Selecione **pedidos**em **exibições da fonte de dados disponíveis**e clique em **Avançar**.  
  
6.  Na página **especificar tipos de tabela** , na linha da tabela vAssocSeqLineItems, marque a caixa de seleção **aninhada** e, na linha da tabela aninhada vAssocSeqOrders, marque a caixa de seleção **caso** . Clique em **Próximo**.  
  
7.  Na página **especificar os dados de treinamento** , desmarque as caixas que podem estar marcadas. Defina a chave para a tabela de casos, vAssocSeqOrders, selecionando a caixa de seleção **chave** ao lado de OrderNumber.  
  
     Como a finalidade da análise de cesta de mercado é determinar quais produtos estão incluídos em uma única transação, você não precisa usar o campo **CustomerKey** .  
  
8.  Defina a chave para a tabela aninhada, vAssocSeqLineItems, selecionando a caixa de seleção **chave** ao lado de modelo. A caixa de seleção de **entrada** também é selecionada automaticamente quando você faz isso. Marque a caixa de `Model` seleção **previsível** também.  
  
     Em um modelo de cesta de compras, você não se preocupa com a seqüência de produtos na cesta de compra e, portanto, não deve incluir **LineNumber** como uma chave para a tabela aninhada. Você usaria **LineNumber** como uma chave somente em um modelo em que a sequência é importante. Você criará um modelo que use o algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Sequence Clustering na Lição 4.  
  
9. Marque a caixa de seleção à esquerda de IncomeGroup e de Região, mas não faça outras seleções. Verificar a coluna mais à esquerda adiciona as colunas à estrutura para referência futura, mas as colunas não serão usadas no modelo. As suas seleções deverão ficar assim:  
  
     ![como a caixa de diálogo deve parecer](../../2014/tutorials/media/tutorial-configassocmodel.gif "como a caixa de diálogo deve parecer")  
  
10. Clique em **Próximo**.  
  
11. Na página **especificar conteúdo e tipo de dados das colunas**, examine as seleções, que devem ser conforme mostrado na tabela a seguir e clique em **Avançar**.  
  
    |Colunas|Tipo de conteúdo|Tipo de Dados|  
    |-------------|------------------|---------------|  
    |IncomeGroup|Discreto|Texto|  
    |Número do pedido|Chave|Texto|  
    |Região|Discreto|Texto|  
    |vAssocSeqLineItems|||  
    |Modelo|Chave|Texto|  
  
12. Na página **criar conjunto de testes** , o valor padrão para a **porcentagem de opção de dados para teste** é de 30%. Altere isso para **0**. Clique em **Próximo**.  
  
    > [!NOTE]  
    >  O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] fornece gráficos diferentes para medir a exatidão do modelo. No entanto, alguns tipos de gráfico de precisão, como o gráfico de comparação de precisão e o relatório de validação cruzada, foram criados para classificação e estimativa. Eles não são suportados para previsão associativa.  
  
13. Na página **concluindo o assistente** , em **nome da estrutura**de mineração `Association`, digite.  
  
14. Em **nome do modelo**de mineração `Association`, digite.  
  
15. Selecione a opção **permitir Drill-through**e clique em **concluir**.  
  
     O designer de mineração de dados é `Association` aberto para exibir a estrutura de mineração que você acabou de criar.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Modificando e processando o modelo de cesta de mercado &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/modify-process-market-basket-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Algoritmo de associação da Microsoft](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md)   
 [Tipos de conteúdo &#40;mineração de dados&#41;](../../2014/analysis-services/data-mining/content-types-data-mining.md)  
  
  
