---
title: ActionEnum | Microsoft Docs
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
- ActionEnum
helpviewer_keywords:
- ActionEnum enumeration [ADOX]
ms.assetid: f948febd-c885-4621-823b-421e116fec4e
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7a38f635c03567d224559382979717c9098ddc9c
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="actionenum"></a>ActionEnum
Especifica o tipo de ação a ser executada quando [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md) é chamado.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adAccessDeny**|3|O grupo ou usuário terá as permissões especificadas.|  
|**adAccessGrant**|1|O grupo ou usuário terá pelo menos as permissões solicitadas.|  
|**adAccessRevoke**|4|Nenhum direito de acesso explícito do grupo ou usuário será revogado.|  
|**adAccessSet**|2|O grupo ou usuário terá exatamente as permissões solicitadas.|
