---
description: AllowNullsEnum
title: AllowNullsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: c2d21b4a7e4de67e45210f11598a7cf3a2a99b9e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985537"
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
 [Propriedade IndexNulls (ADOX)](./indexnulls-property-adox.md)