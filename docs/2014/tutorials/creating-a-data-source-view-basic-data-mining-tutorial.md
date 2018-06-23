---
title: Criando um tipo de dados da fonte de exibição (Tutorial de mineração de dados básico) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c1e68a88-0f82-415d-becc-78d180d4f845
caps.latest.revision: 38
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 37c1548820bfe40478cdd5a8fd7b7ed051722056
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/21/2018
ms.locfileid: "36311844"
---
# <a name="creating-a-data-source-view-basic-data-mining-tutorial"></a>Criando uma exibição da fonte de dados (Tutorial de mineração de dados básico)
  Uma exibição de fonte de dados é criada em uma fonte de dados e define um subconjunto dos dados, que você pode então usar em suas estruturas de mineração. Você também pode usar a exibição da fonte de dados para adicionar colunas, criar colunas calculadas e agregações, e adicionar exibições nomeadas. Usando as exibições de fonte de dados, você pode selecionar os dados que se relacionam ao seu projeto, estabelecer relações entre as tabelas e modificar a estrutura dos dados sem modificar a fonte de dados original. Para obter mais informações, consulte [Exibições de fontes de dados em modelos multidimensionais](../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md).  
  
### <a name="to-create-a-data-source-view"></a>Para criar uma exibição da fonte de dados  
  
1.  Em **Solution Explorer**, clique com botão direito **exibições da fonte de dados**e selecione **nova exibição da fonte de dados**.  
  
2.  Na página **Bem-vindo ao Assistente de Exibição da Fonte de Dados** , clique em **Avançar**.  
  
3.  Sobre o **selecionar uma fonte de dados** página em **fontes de dados relacionais**, selecione a fonte de dados do Adventure Works DW 2012 que você criou na última tarefa. Clique em **Avançar**.  
  
    > [!NOTE]  
    >  Se você quiser criar uma fonte de dados, clique com botão direito **fontes de dados** e, em seguida, clique em **nova fonte de dados** para iniciar o Assistente de fonte de dados.  
  
4.  Sobre o **selecionar tabelas e exibições** página, selecione os objetos a seguir e, em seguida, clique na seta à direita para incluí-los na nova exibição de fonte de dados:  
  
    -   **ProspectiveBuyer (dbo)** -tabela de potenciais compradores de bicicleta  
  
    -   **vTargetMail (dbo)** -modo de exibição de dados históricos sobre compradores de bicicleta passados  
  
5.  Clique em **Avançar**.  
  
6.  Sobre o **Concluindo o assistente** página, por padrão, o modo de exibição de fonte de dados é denominado Adventure Works DW 2012. Altere o nome para `Targeted Mailing`e, em seguida, clique em **concluir**.  
  
     A nova exibição da fonte de dados é aberto no **mala direta.DSV [Design]** guia.  
  
## <a name="previous-task-in-lesson"></a>Tarefa anterior da lição  
 [Criar uma fonte de dados &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/creating-a-data-source-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 2: Criando uma estrutura de mala direta &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/lesson-2-building-a-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Definindo dados de um exibição da fonte &#40;do Analysis Services&#41;](../analysis-services/multidimensional-models/defining-a-data-source-view-analysis-services.md)  
  
  