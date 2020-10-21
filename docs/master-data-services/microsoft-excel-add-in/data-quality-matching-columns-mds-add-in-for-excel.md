---
description: Colunas de correspondência de qualidade de dados (Suplemento do MDS para Excel)
title: Colunas de correspondência de qualidade de dados
ms.custom: microsoft-excel-add-in
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: f683fdc6-0d4c-4793-8143-567616cb2094
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: d55d071bac84fee4d97175fc7d4da502feaaebb5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "92257946"
---
# <a name="data-quality-matching-columns-mds-add-in-for-excel"></a>Colunas de correspondência de qualidade de dados (Suplemento do MDS para Excel)

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], após a correspondência de dados, no grupo **Qualidade de Dados** na faixa de opções, você pode clicar em **Mostrar Detalhes** para exibir colunas que fornecem detalhes correspondentes.  
  
 A tabela a seguir mostra as colunas que são exibidas durante a correspondência de dados.  
  
|Nome|Descrição|  
|----------|-----------------|  
|**CLUSTER_ID**|Um identificador exclusivo usado para agrupar registros semelhantes. Todas as linhas semelhantes têm a mesma **CLUSTER_ID**. Se nenhum **CLUSTER_ID** é exibido para uma linha, nenhum registro semelhante foi encontrado.|  
|**RECORD_ID**|Um identificador exclusivo usado para identificar registros. Semelhante ao valor de Código armazenado no repositório do MDS é um valor usado para identificar um registro. É gerado automaticamente a cada correspondência de hora.|  
|**PIVOT_MARK**|Um registro arbitrário com o qual outros registros são comparados; não tem um valor de pontuação.|  
|**PLACAR**|Representa o grau de similaridade dos registros no grupo com o registro dinâmico. Essa pontuação é determinada pelo DQS. Se nenhuma pontuação for exibida, o registro será dinâmico para outros registros ou nenhuma correspondência será encontrada.|  
  
## <a name="see-also"></a>Consulte Também  
 [Correspondência de qualidade de dados no Suplemento MDS para Excel](../../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)   
 [Corresponder dados semelhantes &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/match-similar-data-mds-add-in-for-excel.md)   
 [Correspondência de dados](../../data-quality-services/data-matching.md)  
  
  
