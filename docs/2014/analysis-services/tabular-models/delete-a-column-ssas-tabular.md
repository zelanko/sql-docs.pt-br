---
title: Excluir uma coluna (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 703db83b-e554-450e-813e-23ad08c1cdad
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f0a95e8580aa30ce34ada1c77e198eb40d767304
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66067268"
---
# <a name="delete-a-column-ssas-tabular"></a>Excluir uma coluna (SSAS tabular)
  Este tópico descreve como excluir uma coluna de uma tabela de modelo de tabela.  
  
## <a name="delete-a-model-table-column"></a>Excluir uma coluna de tabela modelo  
  
> [!NOTE]  
>  A exclusão de uma coluna de uma tabela modelo não exclui a coluna de uma definição de consulta de partição. Se a coluna que você está excluindo fizer parte de uma partição, exclua a coluna manualmente da definição de consulta de partição. A falha ao excluir a coluna da definição de consulta de partição causará a consulta da coluna e o retorno dos dados, mas não a população da tabela modelo, durante operações de processamento. Para obter mais informações, consulte [Partições &#40;SSAS de Tabela&#41;](partitions-ssas-tabular.md).  
  
#### <a name="to-delete-a-model-table-column"></a>Para excluir uma coluna de tabela modelo  
  
-   No designer de modelo, na tabela que contém a coluna a ser excluída, clique com o botão direito do mouse na coluna e, depois, clique em **Excluir**.  
  
#### <a name="to-delete-a-model-table-column-by-using-the-table-properties-dialog-box"></a>Para excluir uma coluna de tabela modelo usando a caixa de diálogo Propriedades da Tabela  
  
1.  No designer de modelo, clique na tabela que contém a coluna a ser excluída, clique no menu **Tabela** e em  **Propriedades da Tabela**.  
  
2.  Em **Nomes das coluna de**, selecione **Modelo** (*para usar nomes de coluna de tabela modelo, se for diferente da origem*).  
  
3.  Na caixa de diálogo **Editar Propriedades da Tabela** , na janela de visualização de tabela, desmarque a coluna a ser excluída e clique em **OK**.  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar colunas a uma tabela &#40;SSAS tabular&#41;](add-columns-to-a-table-ssas-tabular.md)   
 [Partições &#40;SSAS de Tabela&#41;](partitions-ssas-tabular.md)  
  
  
