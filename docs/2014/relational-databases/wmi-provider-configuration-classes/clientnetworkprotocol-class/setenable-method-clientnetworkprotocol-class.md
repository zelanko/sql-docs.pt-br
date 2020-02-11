---
title: Método SetEnable (classe ClientNetworkProtocol) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetEnable Method (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetEnable method
ms.assetid: a66c756a-1311-4f4a-8088-818f8ed90056
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 1aa192f2dc78a424b1d4c8792044caac0934173a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62826716"
---
# <a name="setenable-method-clientnetworkprotocol-class"></a>Método SetEnable (classe ClientNetworkProtocol)
  Habilita o protocolo de rede do cliente que é especificado pelo [Configurar protocolos de cliente](https://technet.microsoft.com/library/ms181035.aspx).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.SetEnableMethod()  
  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 Um objeto da [classe ClientNetworkProtocol](clientnetworkprotocol-class.md) que representa o protocolo de rede usado [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pelo cliente.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor `uint32`, que é 0 se o serviço tiver sido modificado com êxito, 1 se a solicitação não tiver suporte e qualquer outro número para indicar um erro.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte Também  
 [Configurando protocolos de cliente de servidor e bibliotecas de rede](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
