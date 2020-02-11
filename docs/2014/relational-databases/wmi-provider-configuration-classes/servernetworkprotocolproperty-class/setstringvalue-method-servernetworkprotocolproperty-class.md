---
title: Método SetStringValue (classe ServerNetworkProtocolProperty) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetStringValue Method (ServerNetworkProtocolProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetStringValue method
ms.assetid: 0911df30-55f7-4fca-a1fb-01d2c91c1467
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 5736b6e4e88d103c29d0d027327a9f3f46d0cfdf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62736246"
---
# <a name="setstringvalue-method-servernetworkprotocolproperty-class"></a>Método SetStringValue (classe ServerNetworkProtocolProperty)
  Define o valor da cadeia de caracteres da propriedade referenciada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.SetStringValue(  
StrValue  
)  
  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 A [classe ServerNetworkProtocolProperty](servernetworkprotocolproperty-class.md) que representa um atributo do protocolo de rede na instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
#### <a name="parameters"></a>parâmetros  
  
|Parâmetro|DESCRIÇÃO|  
|---------------|-----------------|  
|*StrValue*|Um valor da cadeia de caracteres que especifica o novo valor da propriedade atual.|  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor `uint32`, que é 0 se o serviço tiver sido modificado com êxito, 1 se a solicitação não tiver suporte e qualquer outro número para indicar um erro.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte Também  
 [Configurando protocolos de rede de servidor e Net-Libraries](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
