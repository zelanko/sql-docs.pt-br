---
title: AllowNullsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- AllowNullsEnum
helpviewer_keywords:
- AllowNullsEnum enumeration [ADOX]
ms.assetid: 6acf3689-1a7f-4379-9d7f-df452ccbac27
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3b321045efcf77e3e0a5922638b8437903a69bef
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="allownullsenum"></a>AllowNullsEnum
Especifica se os registros com valores nulos são indexados.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adIndexNullsAllow**|0|O índice permite entradas em que as colunas de chave são nulas. Se um valor nulo é inserido em uma coluna de chave, a entrada será inserida no índice.|  
|**adIndexNullsDisallow**|1|Padrão. O índice não permite entradas em que as colunas de chave são nulas. Se um valor nulo é inserido em uma coluna de chave, ocorrerá um erro.|  
|**adIndexNullsIgnore**|2|O índice não insere entradas que contém chaves nulas. Se um valor nulo é inserido em uma coluna de chave, a entrada será ignorada e não ocorre nenhum erro.|  
|**adIndexNullsIgnoreAny**|4|O índice não insere entradas onde algumas colunas de chave tem um valor nulo. Para um índice com uma multi-coluna de chave, se um valor nulo é inserido em alguma coluna, a entrada será ignorada e não ocorre nenhum erro.|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Propriedade IndexNulls (ADOX)](../../../ado/reference/adox-api/indexnulls-property-adox.md)
