---
title: Excluir relações | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 115d72bd0b833d1f392b2349d3ed4e4970f58453
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37999175"
---
# <a name="delete-relationships"></a>Excluir relações 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  É possível excluir relações existentes usando o designer de modelos na Exibição de Diagrama ou usando a caixa de diálogos Gerenciar Relações. Para obter informações sobre como as relações são usadas em modelos de tabela, consulte [relações](../../analysis-services/tabular-models/relationships-ssas-tabular.md).  
  
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
 [Relações](../../analysis-services/tabular-models/relationships-ssas-tabular.md)   
 [Criar uma relação](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md)  
  
  
