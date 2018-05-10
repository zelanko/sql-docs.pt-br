---
title: Colunas de correspondência de qualidade de dados (Suplemento MDS para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.component: microsoft-excel-add-in
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f683fdc6-0d4c-4793-8143-567616cb2094
caps.latest.revision: 9
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 33ea0d3a74f97c9ee4e8701213ecdb6757b0b017
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="data-quality-matching-columns-mds-add-in-for-excel"></a>Colunas de correspondência de qualidade de dados (Suplemento do MDS para Excel)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], após a correspondência de dados, no grupo **Qualidade de Dados** na faixa de opções, você pode clicar em **Mostrar Detalhes** para exibir colunas que fornecem detalhes correspondentes.  
  
 A tabela a seguir mostra as colunas que são exibidas durante a correspondência de dados.  
  
|Nome|Description|  
|----------|-----------------|  
|**CLUSTER_ID**|Um identificador exclusivo usado para agrupar registros semelhantes. Todas as linhas semelhantes têm a mesma **CLUSTER_ID**. Se nenhum **CLUSTER_ID** é exibido para uma linha, nenhum registro semelhante foi encontrado.|  
|**RECORD_ID**|Um identificador exclusivo usado para identificar registros. Semelhante ao valor de Código armazenado no repositório do MDS é um valor usado para identificar um registro. É gerado automaticamente a cada correspondência de hora.|  
|**PIVOT_MARK**|Um registro arbitrário com o qual outros registros são comparados; não tem um valor de pontuação.|  
|**SCORE**|Representa o grau de similaridade dos registros no grupo com o registro dinâmico. Essa pontuação é determinada pelo DQS. Se nenhuma pontuação for exibida, o registro será dinâmico para outros registros ou nenhuma correspondência será encontrada.|  
  
## <a name="see-also"></a>Consulte Também  
 [Correspondência de qualidade de dados no Suplemento do MDS para Excel](../../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)   
 [Corresponder dados semelhantes &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/match-similar-data-mds-add-in-for-excel.md)   
 [Correspondência de dados](../../data-quality-services/data-matching.md)  
  
  
