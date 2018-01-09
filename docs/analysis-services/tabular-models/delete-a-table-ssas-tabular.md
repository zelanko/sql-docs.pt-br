---
title: Excluir uma tabela (SSAS Tabular) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: be4ed45f-fde3-466c-9869-49bd3ddb505e
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b3d1ec8c0c56a7fd1fb83f2b0401907eb0c0302c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="delete-a-table-ssas-tabular"></a>Excluir uma tabela (SSAS tabular)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]No designer de modelo, você pode excluir tabelas em seu banco de dados de espaço de trabalho de modelo que você não precisa mais. A exclusão de uma tabela não afeta os dados de origem originais, somente os dados que você importou e com os quais estava trabalhando. Não é possível desfazer a exclusão de uma tabela.  
  
### <a name="to-delete-a-table"></a>Para excluir uma tabela  
  
-   Clique com o botão direito do mouse na guia, na parte inferior do designer de modelo para a tabela que você deseja excluir, e clique em **Excluir**.  
  
## <a name="considerations-when-deleting-tables"></a>Considerações ao excluir tabelas  
  
-   Quando você excluir uma tabela, a guia inteira na qual a tabela se encontra será excluída.  
  
-   Se houver uma medida associada a essa tabela, a definição da medida também será excluída.  
  
-   Se você criou qualquer coluna calculada usando essa tabela, as colunas dessa tabela também serão excluídas; as colunas calculadas de outras tabelas que usam colunas da tabela excluída exibirão um erro.  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas e colunas &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)  
  
  
