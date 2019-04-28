---
title: Método SetNumericalValue (classe ServerNetworkProtocolProperty) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetNumericalValue Method (ServerNetworkProtocolProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetNumericalValue method
ms.assetid: b3b4bce8-9d9e-4ccb-a223-0454281353b0
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: e2b3318b9aae0412e827875af35cbdf0477e059f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62736276"
---
# <a name="setnumericalvalue-method-servernetworkprotocolproperty-class"></a>Método SetNumericalValue (classe ServerNetworkProtocolProperty)
  Define o valor numérico da propriedade referenciada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.SetNumericalValue(  
NumValue  
)  
  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um [classe ServerNetworkProtocolProperty] servernetworkprotocolproperty-class.md) que representa um atributo do protocolo de rede na instância do objeto [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
#### <a name="parameters"></a>Parâmetros  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|*NumValue*|Um valor `uint32` que especifica o novo valor da propriedade atual.|  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor `uint32`, que é 0 se o serviço tiver sido modificado com êxito, 1 se a solicitação não tiver suporte e qualquer outro número para indicar um erro.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Configurando protocolos de rede do servidor e bibliotecas de rede](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
