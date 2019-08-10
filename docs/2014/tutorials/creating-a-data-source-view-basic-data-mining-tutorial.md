---
title: Criando uma exibição da fonte de dados (tutorial de mineração de dados básico) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: c1e68a88-0f82-415d-becc-78d180d4f845
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ac7730e8437eaed304ed69c40e45fc93ee9b5531
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68888645"
---
# <a name="creating-a-data-source-view-basic-data-mining-tutorial"></a>Criando uma exibição da fonte de dados (Tutorial de mineração de dados básico)
  Uma exibição de fonte de dados é criada em uma fonte de dados e define um subconjunto dos dados, que você pode então usar em suas estruturas de mineração. Você também pode usar a exibição da fonte de dados para adicionar colunas, criar colunas calculadas e agregações, e adicionar exibições nomeadas. Usando as exibições de fonte de dados, você pode selecionar os dados que se relacionam ao seu projeto, estabelecer relações entre as tabelas e modificar a estrutura dos dados sem modificar a fonte de dados original. Para obter mais informações, consulte [Exibições de fontes de dados em modelos multidimensionais](https://docs.microsoft.com/analysis-services/multidimensional-models/data-source-views-in-multidimensional-models).  
  
### <a name="to-create-a-data-source-view"></a>Para criar uma exibição da fonte de dados  
  
1.  Em **Gerenciador de soluções**, clique com o botão direito do mouse em exibições da **fonte de dados**e selecione **nova exibição da fonte de dados**.  
  
2.  Na página **Bem-vindo ao Assistente de Exibição da Fonte de Dados** , clique em **Avançar**.  
  
3.  Na página **selecionar uma fonte de dados** , em **fontes de dados relacionais**, selecione a fonte de dados Adventure Works DW 2012 que você criou na última tarefa. Clique em **Avançar**.  
  
    > [!NOTE]  
    >  Se você quiser criar uma fonte de dados, clique com o botão direito do mouse em **fontes de dados** e clique em **nova fonte de dados** para iniciar o assistente de fonte de dados.  
  
4.  Na página **selecionar tabelas e exibições** , selecione os seguintes objetos e clique na seta para a direita para incluí-los na nova exibição da fonte de dados:  
  
    -   **ProspectiveBuyer (dbo)** -tabela de compradores de bicicletas potenciais  
  
    -   **vTargetMail (dbo)** -exibição de dados históricos sobre os compradores de bicicletas anteriores  
  
5.  Clique em **Avançar**.  
  
6.  Na página **concluindo o assistente** , por padrão, a exibição da fonte de dados é chamada Adventure Works DW 2012. Altere o nome para `Targeted Mailing`e clique em **concluir**.  
  
     A nova exibição da fonte de dados é aberta na guia **endereçamento direcionado. dsv [Design]** .  
  
## <a name="previous-task-in-lesson"></a>Tarefa anterior da lição  
 [Criando um tutorial de &#40;mineração de dados básico de fonte de dados&#41;](../../2014/tutorials/creating-a-data-source-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 2: Criando um tutorial de mineração de &#40;dados básico de estrutura de endereçamento de destino&#41;](../../2014/tutorials/lesson-2-building-a-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Como definir uma exibição da fonte de dados &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/defining-a-data-source-view-analysis-services)  
  
  
