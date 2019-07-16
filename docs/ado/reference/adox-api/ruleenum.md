---
title: RuleEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RuleEnum
helpviewer_keywords:
- RuleEnum enumeration [ADOX]
ms.assetid: 738fd3ff-3daf-483d-a0b9-88bef1be54c1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 87c61baa93cb1dbca58bbe86ffc254a92d2b9d5b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67965241"
---
# <a name="ruleenum"></a>RuleEnum
Especifica a regra para seguir quando um [chave](../../../ado/reference/adox-api/key-object-adox.md) é excluído.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adRICascade**|1|Alterações em cascata.|  
|**adRINone**|0|Padrão. Nenhuma ação é tomada.|  
|**adRISetDefault**|3|Valor de chave estrangeira é definida como o padrão.|  
|**adRISetNull**|2|Valor de chave estrangeira é definida como null.|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Propriedade DeleteRule (ADOX)](../../../ado/reference/adox-api/deleterule-property-adox.md)
