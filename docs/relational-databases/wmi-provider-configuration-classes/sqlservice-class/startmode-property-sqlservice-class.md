---
title: Propriedade StartMode (classe SqlService) | Microsoft Docs
ms.custom: ''
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
manager: craigg
ms.openlocfilehash: 79b79347b03eda5540e59b00dd23c26c7c19bd1d
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51214994"
---
# <a name="startmode-property-sqlservice-class"></a>Propriedade StartMode (classe SqlService)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
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
 Valor = 1. Serviço iniciado pelos **IoInitSystem** método. Esta opção só é válida para serviços de driver.  
  
 Automático  
 Valor = 2. Serviço a ser iniciado automaticamente pelo gerenciador de controle de serviço durante a inicialização do sistema.  
  
 Manual  
 Valor = 3. Serviço a ser iniciado pelo Gerenciador de computador quando um processo chamar o **StartService** método.  
  
 Desabilitado  
 Valor = 4. Serviço não pode ser iniciado.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Iniciando e parando serviços](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
