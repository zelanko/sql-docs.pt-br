---
title: ActionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ActionEnum
helpviewer_keywords:
- ActionEnum enumeration [ADOX]
ms.assetid: f948febd-c885-4621-823b-421e116fec4e
author: rothja
ms.author: jroth
ms.openlocfilehash: af82b9fbe8f38bcd55e90b5fee979e8c248c3542
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764217"
---
# <a name="actionenum"></a>ActionEnum
Especifica o tipo de ação a ser executada quando [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md) é chamada.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adAccessDeny**|3|O grupo ou usuário terá as permissões especificadas negadas.|  
|**adAccessGrant**|1|O grupo ou usuário terá pelo menos as permissões solicitadas.|  
|**adAccessRevoke**|4|Todos os direitos de acesso explícitos do grupo ou do usuário serão revogados.|  
|**adAccessSet**|2|O grupo ou usuário terá exatamente as permissões solicitadas.|
