---
title: Propriedade StartMode (classe SqlService) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 36
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: c3bed01976385885d84768101d8b64c9436fdcea
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37307486"
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
  
 Automático  
 Valor = 2. Serviço a ser iniciado automaticamente pelo gerenciador de controle de serviço durante a inicialização do sistema.  
  
 Manual  
 Valor = 3. Serviço a ser iniciado pelo Gerenciador de Computador quando um processo chamar o método `StartService`.  
  
 Desabilitado  
 Valor = 4. Serviço não pode ser iniciado.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>Consulte também  
 [Iniciando e parando serviços](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
