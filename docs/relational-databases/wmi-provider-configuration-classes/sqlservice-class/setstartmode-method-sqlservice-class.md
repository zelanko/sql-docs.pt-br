---
title: Método setstart (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetStartMode Method (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetStartMode method
ms.assetid: f6f198b4-f9a4-468c-8977-76462ef06e61
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 15cfa1eddcd9a32b51984d3833c288fc006d395b
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85888350"
---
# <a name="setstartmode-method-sqlservice-class"></a>Método SetStartMode (classe SqlService)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Modifica o modo de início da instância do serviço.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
object.SetStartMode(StartMode)  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) que representa o serviço.  
  
#### <a name="parameters"></a>Parâmetros  
 *StartMode*  
 Um valor **uint32** que especifica o modo de início da instância do serviço.  
  
 Os valores válidos são os seguintes:  
  
 Valor = 0. Inicializar – o driver do dispositivo é iniciado pelo carregador do sistema operacional. Esse valor só é válido para serviços do driver.  
  
 Valor = 1. Sistema - driver de dispositivo iniciado pelo método **IoInitSystem** . Esse valor só é válido para serviços do driver.  
  
 Valor = 2. Automático - serviço a ser iniciado automaticamente pelo gerenciador de controle de serviço durante a inicialização do sistema.  
  
 Valor = 3. Manual - serviço a ser iniciado pelo Gerenciador de Computador quando um processo chamar o método **StartService** .  
  
 Valor = 4. Desabilitado - serviço não pode mais ser iniciado.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor **uint32** , que é 0 se o serviço tiver sido modificado com êxito ou 1 se a solicitação não tiver suporte. Qualquer outro número indica um erro.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciando e parando serviços](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
