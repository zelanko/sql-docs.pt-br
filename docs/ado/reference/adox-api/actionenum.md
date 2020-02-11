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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fad40c6daed6fd86f93da3f658af6a21c33ca762
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67928629"
---
# <a name="actionenum"></a>ActionEnum
Especifica o tipo de ação a ser executada quando [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md) é chamada.  
  
|Constante|Valor|DESCRIÇÃO|  
|--------------|-----------|-----------------|  
|**adAccessDeny**|3|O grupo ou usuário terá as permissões especificadas negadas.|  
|**adAccessGrant**|1|O grupo ou usuário terá pelo menos as permissões solicitadas.|  
|**adAccessRevoke**|4|Todos os direitos de acesso explícitos do grupo ou do usuário serão revogados.|  
|**adAccessSet**|2|O grupo ou usuário terá exatamente as permissões solicitadas.|
