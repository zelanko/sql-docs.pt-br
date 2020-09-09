---
description: Método SetDisable (classe ClientNetworkProtocol)
title: Método SetDisable (ClientNetworkProtocol)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetDisable Method (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetDisable method
ms.assetid: bce69ab9-ea5b-43fd-8114-08b1b5890755
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 772e6c3eac9a6e6b9434e2cbb9e76f884cc031aa
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537189"
---
# <a name="setdisable-method-clientnetworkprotocol-class"></a>Método SetDisable (classe ClientNetworkProtocol)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Desabilita o protocolo de rede do cliente que é especificado pelo [Configurar protocolos de cliente](https://technet.microsoft.com/library/ms181035.aspx).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.SetDisable()  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 A [classe ClientNetworkProtocol](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) que representa o protocolo de rede usado pelo cliente do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor **uint32** , que é 0 se o serviço tiver sido modificado com êxito, 1 se a solicitação não tiver suporte e qualquer outro número para indicar um erro.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte Também  
 [Configurando protocolos de cliente de servidor e bibliotecas de rede](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
