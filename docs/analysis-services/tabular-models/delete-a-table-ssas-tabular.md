---
title: Excluir uma tabela (SSAS Tabular) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: be4ed45f-fde3-466c-9869-49bd3ddb505e
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1d3437449a05b5e1f60083135e020171b3d1e916
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="delete-a-table-ssas-tabular"></a>Excluir uma tabela (SSAS tabular)
  No designer de modelo, você pode excluir tabelas em seu banco de dados de espaço de trabalho modelo que você não precisa mais. A exclusão de uma tabela não afeta os dados de origem originais, somente os dados que você importou e com os quais estava trabalhando. Não é possível desfazer a exclusão de uma tabela.  
  
### <a name="to-delete-a-table"></a>Para excluir uma tabela  
  
-   Clique com o botão direito do mouse na guia, na parte inferior do designer de modelo para a tabela que você deseja excluir, e clique em **Excluir**.  
  
## <a name="considerations-when-deleting-tables"></a>Considerações ao excluir tabelas  
  
-   Quando você excluir uma tabela, a guia inteira na qual a tabela se encontra será excluída.  
  
-   Se houver uma medida associada a essa tabela, a definição da medida também será excluída.  
  
-   Se você criou qualquer coluna calculada usando essa tabela, as colunas dessa tabela também serão excluídas; as colunas calculadas de outras tabelas que usam colunas da tabela excluída exibirão um erro.  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas e colunas &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)  
  
  
