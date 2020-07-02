---
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1adda63135bc85ae2d8a84a8e8744b04144781de
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85662116"
---
# <a name="startmode-property-sqlservice-class"></a>Propriedade StartMode (classe SqlService)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  Obtém o modo de início do serviço.  
  
## <a name="syntax"></a>Syntax  
  
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
  
 Automático  
 Valor = 2. Serviço a ser iniciado automaticamente pelo gerenciador de controle de serviço durante a inicialização do sistema.  
  
 Manual  
 Valor = 3. Serviço a ser iniciado pelo Gerenciador de computadores quando um processo chama o método **StartService** .  
  
 Desabilitado  
 Valor = 4. Serviço não pode ser iniciado.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciando e parando serviços](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
