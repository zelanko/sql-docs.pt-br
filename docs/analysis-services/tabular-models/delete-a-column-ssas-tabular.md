---
title: Excluir uma coluna | Microsoft Docs
ms.custom: ''
ms.date: 02/22/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 703db83b-e554-450e-813e-23ad08c1cdad
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: baa5527f9c7eef1a2c6099dfb423347117a1f41d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
  
  
