---
title: Método SetStartMode (classe SqlService) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- SetStartMode Method (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetStartMode method
ms.assetid: f6f198b4-f9a4-468c-8977-76462ef06e61
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 289317a56c1a48b69b500758fbbb47e57b8a49e6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48112087"
---
# <a name="setstartmode-method-sqlservice-class"></a>Método SetStartMode (classe SqlService)
  Modifica o modo de início da instância do serviço.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.SetStartMode(  
StartMode  
)  
  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe SqlService](sqlservice-class.md) que representa o serviço.  
  
#### <a name="parameters"></a>Parâmetros  
 *StartMode*  
 Um valor `uint32` que especifica o modo de início da instância do serviço.  
  
 Os valores válidos são os seguintes:  
  
 Valor = 0. Inicializar – o driver do dispositivo é iniciado pelo carregador do sistema operacional. Esse valor só é válido para serviços do driver.  
  
 Valor = 1. Sistema - driver de dispositivo iniciado pelo método `IoInitSystem`. Esse valor só é válido para serviços do driver.  
  
 Valor = 2. Automático - serviço a ser iniciado automaticamente pelo gerenciador de controle de serviço durante a inicialização do sistema.  
  
 Valor = 3. Manual - serviço a ser iniciado pelo Gerenciador de Computador quando um processo chamar o método `StartService`.  
  
 Valor = 4. Desabilitado - serviço não pode mais ser iniciado.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor `uint32`, que é 0 se o serviço tiver sido modificado com êxito ou 1 se a solicitação não tiver suporte. Qualquer outro número indica um erro.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Iniciando e parando serviços](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
