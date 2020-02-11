---
title: Adicionando uma exibição da fonte de dados com tabelas aninhadas (tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a14cd7f1-7a10-4ec6-af6a-f5f0676a0308
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 648b9d561ae340b67ed5e2d1aa878969e5a3bc47
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62822769"
---
# <a name="adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial"></a>Adicionando uma exibição da fonte de dados com tabelas aninhadas (Tutorial de mineração de dados intermediário)
  Para criar um modelo de cesta de compras, você deve usar uma exibição da fonte de dados que dá suporte a dados associativos. Essa fonte de dados também será usada para o cenário de clustering de sequências.  
  
 Essa exibição da fonte de dados é diferente de outras com as quais você pode ter trabalhado porque contém uma *tabela aninhada*. Uma *tabela aninhada* é uma tabela que contém várias linhas de informações sobre uma única linha na tabela de casos. Por exemplo, se o seu modelo analisasse o comportamento de compra de clientes, normalmente você usaria uma tabela com uma linha exclusiva para cada cliente como a tabela de casos. No entanto, cada cliente pode fazer várias compras e talvez você queira analisar a sequência de compras ou os produtos comprados juntos com frequência. Para representar logicamente essas compras no modelo, adicione outra tabela à exibição da fonte de dados que lista as compras para cada cliente.  
  
 Essa tabela de compras aninhada está relacionada à tabela de clientes uma relação muitos para um. A tabela aninhada pode conter várias linhas para cada cliente, cada linha com um único produto comprado, talvez com informações adicionais sobre o pedido em que as compras foram feitas, o preço no momento do pedido ou qualquer promoção aplicável. É possível usar as informações da tabela aninhada como entradas para o modelo ou como o atributo previsível.  
  
 Nesta lição, você executa as seguintes tarefas:  
  
-   Você adiciona uma exibição da fonte de dados [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] à fonte de dados.  
  
-   Você adiciona as tabelas de casos e aninhada a essa exibição.  
  
-   Você especifica a relação muitos para um entre as tabelas de casos e aninhada.  
  
    > [!NOTE]  
    >  . É importante seguir o procedimento descrito com exatidão para especificar corretamente a relação entre a tabela de casos e a tabela aninhada e evitar erros durante o processamento do modelo.  
  
-   Você define como as colunas de dados são usadas no modelo.  
  
 Para obter mais informações sobre como trabalhar com tabelas de casos e aninhadas e como escolher uma chave de tabela aninhada, consulte [tabelas aninhadas &#40;Analysis Services&#41;de mineração de dados ](../../2014/analysis-services/data-mining/nested-tables-analysis-services-data-mining.md).  
  
### <a name="to-add-a-data-source-view"></a>Para adicionar uma exibição da fonte de dados  
  
1.  Em Gerenciador de Soluções, clique com o botão direito do mouse em **exibições da fonte de dados**e selecione **nova exibição da fonte de dados**.  
  
     O Assistente de Exibição da Fonte de Dados é exibido.  
  
2.  Na página **Bem-vindo ao Assistente de Exibição da Fonte de Dados**, clique em **Próximo**.  
  
3.  Na página **selecionar uma fonte de dados** , em **fontes de dados relacionais**, selecione [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] a fonte de dados que você criou no tutorial de mineração de dados básico. Clique em **Próximo**.  
  
4.  Na página **selecionar tabelas e exibições** , selecione as tabelas a seguir e clique na seta para a direita para incluí-las na nova exibição da fonte de dados:  
  
    -   `vAssocSeqOrders`  
  
    -   `vAssocSeqLineItems`  
  
5.  Clique em **Próximo**.  
  
6.  Na página **concluindo o assistente** , por padrão, a exibição da fonte de [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]dados é denominada. Altere o nome para `Orders`e clique em **concluir**.  
  
     O designer de exibição da fonte de `Orders` dados é aberto e a exibição da fonte de dados é exibida.  
  
### <a name="to-create-a-relationship-between-tables"></a>Para criar uma relação entre tabelas  
  
1.  No Designer da Exibição da Fonte de Dados, posicione as duas tabelas para que elas se alinhem horizontalmente, com a tabela vAssocSeqLineItems no lado esquerdo e a tabela vAssocSeqOrders no lado direito.  
  
2.  Selecione a coluna **OrderNumber** na tabela vAssocSeqLineItems.  
  
3.  Arraste a coluna para a tabela vAssocSeqOrders e coloque-a na coluna **OrderNumber** .  
  
    > [!IMPORTANT]  
    >  Certifique-se de arrastar a coluna **OrderNumber** da tabela aninhada vAssocSeqLineItems, que representa o lado muitos da junção, para a tabela de casos vAssocSeqOrders, que representa o lado um da junção.  
  
     Uma nova *relação muitos para um* agora existe entre as tabelas VAssocSeqLineItems e vAssocSeqOrders. Se você uniu as tabelas corretamente, a exibição da fonte de dados deverá ser parecida com esta:  
  
     ![esperada junção muitos-para-um em tabelas aninhadas e de caso](../../2014/tutorials/media/dsv-nestedjoin-illustration.gif "esperada junção muitos-para-um em tabelas aninhadas e de caso")  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Criando uma estrutura de cesta de mercado e um modelo &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/creating-a-market-basket-structure-and-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Tutorial de mineração de dados intermediário &#40;Analysis Services de mineração de dados&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [Estruturas de mineração &#40;Analysis Services de mineração de dados&#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Modelos de mineração &#40;Analysis Services de mineração de dados&#41;](../../2014/analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
  
