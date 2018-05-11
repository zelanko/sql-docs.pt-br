---
title: Excluir uma tabela | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1d3176baca80333c8167d45e6fb3a20e85e4f19d
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="delete-a-table"></a>Excluir uma tabela
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  No designer de modelo, você pode excluir tabelas em seu banco de dados de espaço de trabalho modelo que você não precisa mais. A exclusão de uma tabela não afeta os dados de origem originais, somente os dados que você importou e com os quais estava trabalhando. Não é possível desfazer a exclusão de uma tabela.  
  
### <a name="to-delete-a-table"></a>Para excluir uma tabela  
  
-   Clique com o botão direito do mouse na guia, na parte inferior do designer de modelo para a tabela que você deseja excluir, e clique em **Excluir**.  
  
## <a name="considerations-when-deleting-tables"></a>Considerações ao excluir tabelas  
  
-   Quando você excluir uma tabela, a guia inteira na qual a tabela se encontra será excluída.  
  
-   Se houver uma medida associada a essa tabela, a definição da medida também será excluída.  
  
-   Se você criou qualquer coluna calculada usando essa tabela, as colunas dessa tabela também serão excluídas; as colunas calculadas de outras tabelas que usam colunas da tabela excluída exibirão um erro.  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas e colunas](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)  
  
  
