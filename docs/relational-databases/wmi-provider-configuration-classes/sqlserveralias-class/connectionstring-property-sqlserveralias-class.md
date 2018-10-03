---
title: Propriedade ConnectionString (classe SqlServerAlias) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: reference
apiname:
- ConnectionString Property (SqlServerAlias Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
helpviewer_keywords:
- ConnectionString property
ms.assetid: 8a3692b9-3a34-42e2-b0b9-28e6bd3a7aba
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 7c2bedb961d8a6063c766ae5f6c31b5895e96c8f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47824324"
---
# <a name="connectionstring-property-sqlserveralias-class"></a>Propriedade ConnectionString (classe SqlServerAlias)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Obtém a cadeia de conexão que é usada para estabelecer a conexão para o alias de conexão do servidor.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.ConnectionString [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe SqlServerAlias](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md) que representa um alias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Uma cadeia de caracteres que especifica a cadeia de conexão usada para estabelecer a conexão para o alias de conexão do servidor.  
  
## <a name="remarks"></a>Comentários  
  
