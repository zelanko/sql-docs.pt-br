---
description: ActionEnum
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
ms.openlocfilehash: 78c931cdbc37d73942baa72b41d8c8071f107c8d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440658"
---
# <a name="actionenum"></a>ActionEnum
Especifica o tipo de ação a ser executada quando [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md) é chamada.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adAccessDeny**|3|O grupo ou usuário terá as permissões especificadas negadas.|  
|**adAccessGrant**|1|O grupo ou usuário terá pelo menos as permissões solicitadas.|  
|**adAccessRevoke**|4|Todos os direitos de acesso explícitos do grupo ou do usuário serão revogados.|  
|**adAccessSet**|2|O grupo ou usuário terá exatamente as permissões solicitadas.|
