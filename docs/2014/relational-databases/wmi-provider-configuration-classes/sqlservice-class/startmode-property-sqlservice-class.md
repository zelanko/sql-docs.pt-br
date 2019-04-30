---
title: Propriedade StartMode (classe SqlService) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- StartMode Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- StartMode property
ms.assetid: c0c2c7f8-d4ae-44f2-ad8e-aecfcb7c2878
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: bf77e36824c05a0f07bc789c380cffbc1518669d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63187832"
---
# <a name="startmode-property-sqlservice-class"></a>Propriedade StartMode (classe SqlService)
  Obtém o modo de início do serviço.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.StartMode [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe SqlService](sqlservice-class.md) que representa o serviço.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor uint32 que especifica o modo do serviço.  
  
 Pode conter um dos valores a seguir.  
  
 Inicialização  
 Valor = 0. Serviço iniciado pelo carregador do sistema operacional. Esta opção só é válida para serviços de driver.  
  
 Sistema  
 Valor = 1. Serviço iniciado pelo método `IoInitSystem`. Esta opção só é válida para serviços de driver.  
  
 Automatic  
 Valor = 2. Serviço a ser iniciado automaticamente pelo gerenciador de controle de serviço durante a inicialização do sistema.  
  
 Manual  
 Valor = 3. Serviço a ser iniciado pelo Gerenciador de Computador quando um processo chamar o método `StartService`.  
  
 Desabilitado  
 Valor = 4. Serviço não pode ser iniciado.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Iniciando e parando serviços](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
