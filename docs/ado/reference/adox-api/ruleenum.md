---
title: RuleEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RuleEnum
helpviewer_keywords:
- RuleEnum enumeration [ADOX]
ms.assetid: 738fd3ff-3daf-483d-a0b9-88bef1be54c1
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 66a6a38010487345e2b50ae1267bbe291e05407b
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35286881"
---
# <a name="ruleenum"></a>RuleEnum
Especifica a regra para seguir quando um [chave](../../../ado/reference/adox-api/key-object-adox.md) é excluído.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adRICascade**|1|Alterações em cascata.|  
|**adRINone**|0|Padrão. Nenhuma ação é tomada.|  
|**adRISetDefault**|3|Valor de chave estrangeira é definida como o padrão.|  
|**adRISetNull**|2|Valor de chave estrangeira é definida como null.|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Propriedade DeleteRule (ADOX)](../../../ado/reference/adox-api/deleterule-property-adox.md)
