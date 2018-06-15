---
title: Propriedade ConnectionString (classe SqlServerAlias) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ConnectionString Property (SqlServerAlias Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
helpviewer_keywords:
- ConnectionString property
ms.assetid: 8a3692b9-3a34-42e2-b0b9-28e6bd3a7aba
caps.latest.revision: 30
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 25240fa3845c3e14cd49165c91e27355a78734c9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33006923"
---
# <a name="connectionstring-property-sqlserveralias-class"></a>Propriedade ConnectionString (classe SqlServerAlias)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Obtém a cadeia de conexão que é usada para estabelecer a conexão para o alias de conexão do servidor.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.ConnectionString [= value]  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 Um objeto da [classe SqlServerAlias](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md) que representa um alias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Uma cadeia de caracteres que especifica a cadeia de conexão usada para estabelecer a conexão para o alias de conexão do servidor.  
  
## <a name="remarks"></a>Remarks  
  
