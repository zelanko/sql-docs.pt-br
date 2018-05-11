---
title: Excluir uma coluna | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3bf20ec7c225bbac1f11f0ccccdc4feb81ee7f98
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="delete-a-column"></a>Excluir uma coluna 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Este artigo descreve como excluir uma coluna de uma tabela de modelo de tabela.  
  
## <a name="delete-a-model-table-column"></a>Excluir uma coluna de tabela modelo  
  
> [!NOTE]  
>  A exclusão de uma coluna de uma tabela modelo não exclui a coluna de uma definição de consulta de partição. Se a coluna que você está excluindo fizer parte de uma partição, exclua a coluna manualmente da definição de consulta de partição. A falha ao excluir a coluna da definição de consulta de partição causará a consulta da coluna e o retorno dos dados, mas não a população da tabela modelo, durante operações de processamento. Para obter mais informações, consulte [partições](../../analysis-services/tabular-models/partitions-ssas-tabular.md).  
  
#### <a name="to-delete-a-model-table-column"></a>Para excluir uma coluna de tabela modelo  
  
-   No designer de modelo, na tabela que contém a coluna a ser excluída, clique com o botão direito do mouse na coluna e, depois, clique em **Excluir**.  
  
#### <a name="to-delete-a-model-table-column-by-using-the-table-properties-dialog-box"></a>Para excluir uma coluna de tabela modelo usando a caixa de diálogo Propriedades da Tabela  
  
1.  No designer de modelo, clique na tabela que contém a coluna a ser excluída, clique no menu **Tabela** e em  **Propriedades da Tabela**.  
  
2.  Em **Nomes das coluna de**, selecione **Modelo** (*para usar nomes de coluna de tabela modelo, se for diferente da origem*).  
  
3.  Na caixa de diálogo **Editar Propriedades da Tabela** , na janela de visualização de tabela, desmarque a coluna a ser excluída e clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar colunas a uma tabela](../../analysis-services/tabular-models/add-columns-to-a-table-ssas-tabular.md)   
 [Partições](../../analysis-services/tabular-models/partitions-ssas-tabular.md)  
  
  
