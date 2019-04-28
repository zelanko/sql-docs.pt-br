---
title: Excluir relações (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: d40e3f05-54e8-4c4b-807a-0b06f446079b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c3be65edb0300b2ab47f22784cb7b109372062e0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62795453"
---
# <a name="delete-relationships-ssas-tabular"></a>Excluir relações (SSAS tabular)
  É possível excluir relações existentes usando o designer de modelos na Exibição de Diagrama ou usando a caixa de diálogos Gerenciar Relações. Para obter informações sobre como as relações são usadas em modelos tabulares, consulte [Relações &#40;SSAS de Tabela&#41;](relationships-ssas-tabular.md).  
  
## <a name="considerations-for-deleting-relationships"></a>Considerações para excluir relações  
 Lembre-se destes problemas quando decidir excluir uma relação:  
  
-   Não há como desfazer a exclusão de uma relação. Você pode recriar a relação, mas essa ação requer um recálculo completo das fórmulas no modelo. Portanto, sempre verifique primeiro antes de excluir uma relação que é usada em fórmulas.  
  
-   A exclusão de uma relação entre duas tabelas pode causar erros em fórmulas que referenciam essas tabelas.  
  
-   A função DAX (Data Analysis Expression) RELATED usa as relações entre tabelas para procurar valores relacionados em outra tabela. Ela retornará resultados diferentes depois que a relação for excluída. Para obter mais informações, consulte a função RELATED (DAX).  
  
-   Além de alterar os resultados de Tabelas Dinâmicas e de fórmulas, a criação e a exclusão de relações causará o recálculo da pasta de trabalho, o que pode demorar um pouco.  
  
## <a name="delete-relationships"></a>Excluir relações  
  
#### <a name="to-delete-a-relationship-by-using-diagram-view"></a>Para excluir uma relação usando a Exibição de Diagrama  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique no menu **Modelo** , aponte para **Exibição de Modelo**e clique em **Exibição de Diagrama**.  
  
2.  Clique com o botão direito do mouse na linha da relação entre as duas tabelas e clique em **Excluir**.  
  
#### <a name="to-delete-a-relationship-by-using-the-manage-relationships-dialog-box"></a>Para excluir uma relação usando a caixa de diálogo Gerenciar Relações  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], clique no menu **Tabela** e clique em **Gerenciar Relações**.  
  
2.  Na caixa de diálogo **Gerenciar Relações** , selecione uma ou mais relações na lista.  
  
     Para selecionar várias relações, mantenha a tecla CTRL pressionada enquanto você clica em cada relação.  
  
3.  Clique em **Excluir Relação**.  
  
4.  Na caixa de diálogo **Gerenciar Relações** , clique em **Fechar**.  
  
## <a name="see-also"></a>Consulte também  
 [Relações &#40;SSAS de Tabela&#41;](relationships-ssas-tabular.md)   
 [Criar uma relação entre duas tabelas &#40;SSAS de Tabela&#41;](create-a-relationship-between-two-tables-ssas-tabular.md)  
  
  
