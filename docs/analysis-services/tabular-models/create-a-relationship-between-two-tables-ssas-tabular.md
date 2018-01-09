---
title: "Criar uma relação entre duas tabelas (SSAS Tabular) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: multidimensional-tabular
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.bidtoolset.createrelatdb.f1
- sql13.asvs.bidtoolset.managereldb.f1
ms.assetid: 052d77b7-7922-408a-a200-786016ee4d15
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4278d13d9bbff216a4b5480382de1c8a565278b0
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="create-a-relationship-between-two-tables-ssas-tabular"></a>Criar uma relação entre duas tabelas (SSAS tabular)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Se as tabelas na fonte de dados não tiverem relações existentes ou adicionar novas tabelas, você pode usar as ferramentas no designer de modelo para criar novas relações. Para obter informações sobre como as relações são usadas em modelos tabulares, consulte [Relações &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/relationships-ssas-tabular.md).  
  
## <a name="create-a-relationship-between-two-tables"></a>Criar uma relação entre duas tabelas  
  
#### <a name="to-create-a-relationship-between-two-tables-in-diagram-view-click-and-drag"></a>Para criar uma relação entre duas tabelas na Exibição de Diagrama (clicar e arrastar)  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], clique no menu **Modelo** , clique em **Exibição de Modelo**e clique em **Exibição de Diagrama**.  
  
2.  Clique (e mantenha pressionado) em uma coluna dentro de uma tabela e arraste o cursor para uma coluna de pesquisa relacionada em uma tabela de pesquisa relacionada e, em seguida, solte. A relação será criada na ordem correta automaticamente.  
  
#### <a name="to-create-a-relationship-between-two-tables-in-diagram-view-right-click"></a>Para criar uma relação entre duas tabelas na Exibição de Diagrama (clicar com o botão direito)  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], clique no menu **Modelo** , clique em **Exibição de Modelo**e clique em **Exibição de Diagrama**.  
  
2.  Clique com o botão direito do mouse em um cabeçalho ou coluna de tabela e clique em **Criar Relação**.  
  
3.  Na caixa de diálogo **Criar Relação** , clique na seta para baixo de **Tabela**e selecione uma tabela da lista suspensa.  
  
     Em uma relação "muitos-para-um", essa tabela deve estar no lado "muitos".  
  
4.  Para **Coluna**, selecione a coluna que contém os dados relacionados a **Coluna de Pesquisa Relacionada**. A coluna é selecionada automaticamente se você clicou com o botão direito em uma coluna para criar a relação.  
  
5.  Para **Coluna de Pesquisa Relacionada**, selecione uma tabela que tenha pelo menos uma coluna de dados relacionada à tabela que você acabou de selecionar para **Tabela**.  
  
     Em uma relação "um-para-muitos", essa tabela deve estar no lado "um", o que significa que os valores da coluna selecionada não contêm duplicatas. Se você tentar criar a relação na ordem errada (um para muitos, em vez de muitos para um), um ícone aparecerá ao lado do campo **Coluna de Pesquisa Relacionada** . Inverta a ordem para criar uma relação válida.  
  
6.  Para **Coluna de Pesquisa Relacionada**, selecione uma coluna que tenha valores exclusivos correspondentes aos valores da coluna selecionada para **Coluna**.  
  
7.  Clique em **Criar**.  
  
#### <a name="to-create-a-relationship-between-two-tables-in-data-view"></a>Para criar uma relação entre duas tabelas na Exibição de Dados  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], clique no menu **Tabela** e clique em **Criar Relações**.  
  
2.  Na caixa de diálogo **Criar Relação** , clique na seta para baixo de **Tabela**e selecione uma tabela da lista suspensa.  
  
     Em uma relação "muitos-para-um", essa tabela deve estar no lado "muitos".  
  
3.  Para **Coluna**, selecione a coluna que contém os dados relacionados a **Coluna de Pesquisa Relacionada**.  
  
4.  Para **Coluna de Pesquisa Relacionada**, selecione uma tabela que tenha pelo menos uma coluna de dados relacionada à tabela que você acabou de selecionar para **Tabela**.  
  
     Em uma relação "um-para-muitos", essa tabela deve estar no lado "um", o que significa que os valores da coluna selecionada não contêm duplicatas. Se você tentar criar a relação na ordem errada (um para muitos, em vez de muitos para um), um ícone aparecerá ao lado do campo **Coluna de Pesquisa Relacionada** . Inverta a ordem para criar uma relação válida.  
  
5.  Para **Coluna de Pesquisa Relacionada**, selecione uma coluna que tenha valores exclusivos correspondentes aos valores da coluna selecionada para **Coluna**.  
  
6.  Clique em **Criar**.  
  
## <a name="see-also"></a>Consulte Também  
 [Excluir relações &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/delete-relationships-ssas-tabular.md)   
 [Relações &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/relationships-ssas-tabular.md)  
  
  
