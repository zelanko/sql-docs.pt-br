---
description: Propriedade StartMode (classe SqlService)
title: Propriedade StartMode (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- StartMode Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- StartMode property
ms.assetid: c0c2c7f8-d4ae-44f2-ad8e-aecfcb7c2878
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f662597bf67837678690928810875f62e5d75e04
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542753"
---
# <a name="startmode-property-sqlservice-class"></a>Propriedade StartMode (classe SqlService)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Obtém o modo de início do serviço.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.StartMode [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) que representa o serviço.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor uint32 que especifica o modo do serviço.  
  
 Pode conter um dos valores a seguir.  
  
 Inicialização  
 Valor = 0. Serviço iniciado pelo carregador do sistema operacional. Esta opção só é válida para serviços de driver.  
  
 Sistema  
 Valor = 1. Serviço iniciado pelo método **IoInitSystem** . Esta opção só é válida para serviços de driver.  
  
 Automática  
 Valor = 2. Serviço a ser iniciado automaticamente pelo gerenciador de controle de serviço durante a inicialização do sistema.  
  
 Manual  
 Valor = 3. Serviço a ser iniciado pelo Gerenciador de computadores quando um processo chama o método **StartService** .  
  
 Desabilitado  
 Valor = 4. Serviço não pode ser iniciado.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciando e parando serviços](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
