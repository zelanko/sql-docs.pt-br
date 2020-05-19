---
title: AllowNullsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- AllowNullsEnum
helpviewer_keywords:
- AllowNullsEnum enumeration [ADOX]
ms.assetid: 6acf3689-1a7f-4379-9d7f-df452ccbac27
author: rothja
ms.author: jroth
ms.openlocfilehash: 74bb82433d17bd47df71d3a9f8574d72ce39a265
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764077"
---
# <a name="allownullsenum"></a>AllowNullsEnum
Especifica se os registros com valores nulos são indexados.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adIndexNullsAllow**|0|O índice permite entradas em que as colunas de chave são nulas. Se um valor nulo for inserido em uma coluna de chave, a entrada será inserida no índice.|  
|**adIndexNullsDisallow**|1|Padrão. O índice não permite entradas em que as colunas de chave são nulas. Se um valor nulo for inserido em uma coluna de chave, ocorrerá um erro.|  
|**adIndexNullsIgnore**|2|O índice não insere entradas que contenham chaves nulas. Se um valor nulo for inserido em uma coluna de chave, a entrada será ignorada e nenhum erro ocorrerá.|  
|**adIndexNullsIgnoreAny**|4|O índice não insere entradas em que alguma coluna de chave tem um valor nulo. Para um índice com uma chave de várias colunas, se um valor nulo for inserido em alguma coluna, a entrada será ignorada e nenhum erro ocorrerá.|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Propriedade IndexNulls (ADOX)](../../../ado/reference/adox-api/indexnulls-property-adox.md)
