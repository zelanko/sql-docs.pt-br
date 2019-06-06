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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 53fadcddd49ebf68949da0a7dca3cb37da0b5d93
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66708608"
---
# <a name="allownullsenum"></a>AllowNullsEnum
Especifica se os registros com valores nulos são indexados.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adIndexNullsAllow**|0|O índice permite entradas em que as colunas de chave são nulas. Se um valor nulo é inserido em uma coluna de chave, a entrada é inserida no índice.|  
|**adIndexNullsDisallow**|1|Padrão. O índice não permite entradas em que as colunas de chave são nulas. Se um valor nulo é inserido em uma coluna de chave, ocorrerá um erro.|  
|**adIndexNullsIgnore**|2|O índice não inserir entradas contendo chaves nulas. Se um valor nulo é inserido em uma coluna de chave, a entrada será ignorada e não ocorre nenhum erro.|  
|**adIndexNullsIgnoreAny**|4|O índice não inserir entradas onde alguma coluna de chave tem um valor nulo. Para um índice tendo uma várias colunas chave, se um valor nulo é inserido em alguma coluna, a entrada será ignorada e não ocorre nenhum erro.|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Propriedade IndexNulls (ADOX)](../../../ado/reference/adox-api/indexnulls-property-adox.md)
