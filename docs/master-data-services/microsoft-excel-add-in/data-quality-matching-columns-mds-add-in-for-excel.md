---
title: Qualidade de dados correspondem a colunas (suplemento MDS para Excel) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f683fdc6-0d4c-4793-8143-567616cb2094
caps.latest.revision: 9
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4ce8ddcdbf8c29663640025ad40b4e01e44d99c1
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="data-quality-matching-columns-mds-add-in-for-excel"></a>Colunas de correspondência de qualidade de dados (Suplemento do MDS para Excel)
  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], após a correspondência de dados, no **de qualidade de dados** grupo na faixa de opções, você pode clicar em **Mostrar detalhes** para exibir as colunas que fornecem detalhes correspondentes.  
  
 A tabela a seguir mostra as colunas que são exibidas durante a correspondência de dados.  
  
|Nome|Description|  
|----------|-----------------|  
|**CLUSTER_ID**|Um identificador exclusivo usado para agrupar registros semelhantes. Todas as linhas semelhantes têm a mesma **CLUSTER_ID**. Se nenhum **CLUSTER_ID** é exibido para uma linha, nenhum registro semelhante foi encontrado.|  
|**RECORD_ID**|Um identificador exclusivo usado para identificar registros. Semelhante ao valor de Código armazenado no repositório do MDS é um valor usado para identificar um registro. É gerado automaticamente a cada correspondência de hora.|  
|**PIVOT_MARK**|Um registro arbitrário com o qual outros registros são comparados; não tem um valor de pontuação.|  
|**SCORE**|Representa o grau de similaridade dos registros no grupo com o registro dinâmico. Essa pontuação é determinada pelo DQS. Se nenhuma pontuação for exibida, o registro será dinâmico para outros registros ou nenhuma correspondência será encontrada.|  
  
## <a name="see-also"></a>Consulte também  
 [Qualidade de dados correspondente no suplemento MDS para Excel](../../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)   
 [Corresponder semelhantes de dados &#40; Suplemento do MDS para Excel &#41;](../../master-data-services/microsoft-excel-add-in/match-similar-data-mds-add-in-for-excel.md)   
 [Correspondência de dados](../../data-quality-services/data-matching.md)  
  
  
