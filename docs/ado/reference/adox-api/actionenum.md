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
ms.openlocfilehash: 2c9032dfdb3394e582541f60afce7b930751a5c0
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777775"
---
# <a name="actionenum"></a>ActionEnum
Especifica o tipo de ação a ser executada quando [SetPermissions](./setpermissions-method-adox.md) é chamada.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adAccessDeny**|3|O grupo ou usuário terá as permissões especificadas negadas.|  
|**adAccessGrant**|1|O grupo ou usuário terá pelo menos as permissões solicitadas.|  
|**adAccessRevoke**|4|Todos os direitos de acesso explícitos do grupo ou do usuário serão revogados.|  
|**adAccessSet**|2|O grupo ou usuário terá exatamente as permissões solicitadas.|