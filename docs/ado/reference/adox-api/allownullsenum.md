---
title: AllowNullsEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: AllowNullsEnum
helpviewer_keywords: AllowNullsEnum enumeration [ADOX]
ms.assetid: 6acf3689-1a7f-4379-9d7f-df452ccbac27
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d8dd42fbac84831c2b31247ee5b5279c97ba2ba5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="allownullsenum"></a>AllowNullsEnum
Especifica se os registros com valores nulos são indexados.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adIndexNullsAllow**|0|O índice permite entradas em que as colunas de chave são nulas. Se um valor nulo é inserido em uma coluna de chave, a entrada será inserida no índice.|  
|**adIndexNullsDisallow**|1|Padrão. O índice não permite entradas em que as colunas de chave são nulas. Se um valor nulo é inserido em uma coluna de chave, ocorrerá um erro.|  
|**adIndexNullsIgnore**|2|O índice não insere entradas que contém chaves nulas. Se um valor nulo é inserido em uma coluna de chave, a entrada será ignorada e não ocorre nenhum erro.|  
|**adIndexNullsIgnoreAny**|4|O índice não insere entradas onde algumas colunas de chave tem um valor nulo. Para um índice com uma multi-coluna de chave, se um valor nulo é inserido em alguma coluna, a entrada será ignorada e não ocorre nenhum erro.|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Propriedade IndexNulls (ADOX)](../../../ado/reference/adox-api/indexnulls-property-adox.md)
