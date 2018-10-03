---
title: Adicionando dados de um fonte de exibição com tabelas aninhadas (Tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: a14cd7f1-7a10-4ec6-af6a-f5f0676a0308
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 70db9a9ff6ed8aa5c9a960ae40009369341b99b4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48068036"
---
# <a name="adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial"></a>Adicionando uma exibição da fonte de dados com tabelas aninhadas (Tutorial de mineração de dados intermediário)
  Para criar um modelo de cesta de compras, você deve usar uma exibição da fonte de dados que dá suporte a dados associativos. Essa fonte de dados também será usada para o cenário de clustering de sequências.  
  
 Essa exibição da fonte de dados é diferente de outras pessoas que você talvez tenha trabalhado porque contém um *tabela aninhada*. Um *tabela aninhada* é uma tabela que contém várias linhas de informações sobre uma única linha na tabela de casos. Por exemplo, se o seu modelo analisasse o comportamento de compra de clientes, normalmente você usaria uma tabela com uma linha exclusiva para cada cliente como a tabela de casos. No entanto, cada cliente pode fazer várias compras e talvez você queira analisar a sequência de compras ou os produtos comprados juntos com frequência. Para representar logicamente essas compras no modelo, adicione outra tabela à exibição da fonte de dados que lista as compras para cada cliente.  
  
 Essa tabela de compras aninhada está relacionada à tabela de clientes uma relação muitos para um. A tabela aninhada pode conter várias linhas para cada cliente, cada linha com um único produto comprado, talvez com informações adicionais sobre o pedido em que as compras foram feitas, o preço no momento do pedido ou qualquer promoção aplicável. É possível usar as informações da tabela aninhada como entradas para o modelo ou como o atributo previsível.  
  
 Nesta lição, você deve fazer as seguintes tarefas:  
  
-   Você adiciona uma exibição da fonte de dados para o [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] fonte de dados.  
  
-   Você adiciona as tabelas de casos e aninhada a essa exibição.  
  
-   Você especifica a relação muitos para um entre as tabelas de casos e aninhada.  
  
    > [!NOTE]  
    >  para obter informações sobre a ferramenta de configuração e recursos adicionais. É importante seguir o procedimento descrito com exatidão para especificar corretamente a relação entre a tabela de casos e a tabela aninhada e evitar erros durante o processamento do modelo.  
  
-   Você define como as colunas de dados são usadas no modelo.  
  
 Para obter mais informações sobre como trabalhar com o caso e tabelas aninhadas e como escolher uma chave de tabela aninhada, consulte [tabelas aninhadas &#40;Analysis Services - mineração de dados&#41;](../../2014/analysis-services/data-mining/nested-tables-analysis-services-data-mining.md).  
  
### <a name="to-add-a-data-source-view"></a>Para adicionar uma exibição da fonte de dados  
  
1.  No Gerenciador de soluções, clique com botão direito **exibições da fonte de dados**e, em seguida, selecione **nova exibição da fonte de dados**.  
  
     O Assistente de Exibição da Fonte de Dados é exibido.  
  
2.  Na página **Bem-vindo ao Assistente de Exibição da Fonte de Dados** , clique em **Avançar**.  
  
3.  Sobre o **selecionar uma fonte de dados** página em **fontes de dados relacionais**, selecione o [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] fonte de dados que você criou no Tutorial de mineração de dados básico. Clique em **Avançar**.  
  
4.  Sobre o **selecionar tabelas e exibições** página, selecione as tabelas a seguir e, em seguida, clique na seta à direita para incluí-los na nova exibição de fonte de dados:  
  
    -   `vAssocSeqOrders`  
  
    -   `vAssocSeqLineItems`  
  
5.  Clique em **Avançar**.  
  
6.  Sobre o **Concluindo o assistente** página, por padrão, a exibição da fonte de dados é denominada [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]. Altere o nome para `Orders`e, em seguida, clique em **concluir**.  
  
     Designer de exibição de fonte de dados é aberta e o `Orders` exibição da fonte de dados é exibida.  
  
### <a name="to-create-a-relationship-between-tables"></a>Para criar uma relação entre tabelas  
  
1.  No Designer da Exibição da Fonte de Dados, posicione as duas tabelas para que elas se alinhem horizontalmente, com a tabela vAssocSeqLineItems no lado esquerdo e a tabela vAssocSeqOrders no lado direito.  
  
2.  Selecione o **OrderNumber** coluna na tabela vAssocSeqLineItems.  
  
3.  Arraste a coluna para a tabela vAssocSeqOrders e coloque-a o **OrderNumber** coluna.  
  
    > [!IMPORTANT]  
    >  Certifique-se de arrastar o **OrderNumber** coluna da tabela aninhada vAssocSeqLineItems, que representa os vários lados da junção, para a tabela de casos vAssocSeqOrders, que representa um lado da junção.  
  
     Uma nova *relação muitos-para-um* agora existe entre as tabelas vAssocSeqLineItems e vAssocSeqOrders. Se você uniu as tabelas corretamente, a exibição da fonte de dados deverá ser parecida com esta:  
  
     ![relação muitos-para-um esperado na tabela de casos e aninhada](../../2014/tutorials/media/dsv-nestedjoin-illustration.gif "relação muitos-para-um esperado na tabela de casos e aninhada")  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Criando uma estrutura de cesta de compras e o modelo &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/creating-a-market-basket-structure-and-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Tutorial de mineração de dados intermediário &#40;Analysis Services - mineração de dados&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [Estruturas de mineração &#40;Analysis Services - mineração de dados&#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Modelos de mineração &#40;Analysis Services - mineração de dados&#41;](../../2014/analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
  
