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
author: rothja
ms.author: jroth
ms.openlocfilehash: c04bbd079de68891cf271ff2ea668696e29a4394
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762797"
---
# <a name="ruleenum"></a>RuleEnum
Especifica a regra a ser seguida quando uma [chave](../../../ado/reference/adox-api/key-object-adox.md) é excluída.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adRICascade**|1|Alterações em cascata.|  
|**adRINone**|0|Padrão. Nenhuma ação é tomada.|  
|**adRISetDefault**|3|O valor da chave estrangeira está definido como o padrão.|  
|**adRISetNull**|2|O valor da chave estrangeira está definido como nulo.|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Propriedade DeleteRule (ADOX)](../../../ado/reference/adox-api/deleterule-property-adox.md)
