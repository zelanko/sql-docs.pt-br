---
title: Método SetServiceAccountPassword (classe SqlService) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetServiceAccountPassword Method (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetServiceAccountPassword method
ms.assetid: e577a1ac-985c-4799-bb38-9393efc3def2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 41823ebcbad3f545a8b516b3fad457230d3fdf8e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85067880"
---
# <a name="setserviceaccountpassword-method-sqlservice-class"></a>Método SetServiceAccountPassword (classe SqlService)
  Modifica a senha para a conta com a qual o serviço referenciado é executado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.SetServiceAccountPassword(  
AccountOldPassword , ServiceStartPassword  
)  
  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe SqlService](sqlservice-class.md) que representa o serviço.  
  
#### <a name="parameters"></a>Parâmetros  
 *AccountOldPassword*  
 Um valor da cadeia de caracteres que especifica a senha existente para a conta.  
  
 *ServiceStartPassword*  
 Um valor da cadeia de caracteres que especifica a nova senha existente para a conta.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor `uint32`, que é 0 se o serviço tiver sido modificado com êxito, 1 se a solicitação não tiver suporte e qualquer outro número para indicar um erro.  
  
## <a name="remarks"></a>Comentários  
  
