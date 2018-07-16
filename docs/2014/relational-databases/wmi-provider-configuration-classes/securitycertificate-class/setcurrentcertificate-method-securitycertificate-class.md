---
title: Método SetCurrentCertificate (classe SecurityCertificate) | Microsoft Docs
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
- SetCurrentCertificate Method (SecurityCertificate Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetCurrentCertificate method
ms.assetid: 04b1a76a-932d-4824-8506-e346afe7554e
caps.latest.revision: 34
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: b406ecc02bcdf0466903beb71de9e633cc2d985c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37191766"
---
# <a name="setcurrentcertificate-method-securitycertificate-class"></a>Método SetCurrentCertificate (classe SecurityCertificate)
  Define o certificado de segurança atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.SetCurrentCertificate(  
SHA , SQLInstance  
)  
  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um [classe SecurityCertificate] securitycertificate-class.md) o objeto que representa um certificado de segurança.  
  
#### <a name="parameters"></a>Parâmetros  
  
|Parâmetro|Description|  
|---------------|-----------------|  
|*SHA*|Um valor da cadeia de caracteres que especifica a impressão digital de SHA (algoritmo de hash seguro) para o certificado de segurança necessário.|  
|*SQLInstance*|Um valor da cadeia de caracteres que especifica a instância para a qual o certificado é necessário.|  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor uint32, que é 0 se o serviço tiver sido modificado com êxito, 1 se a solicitação não tiver suporte e qualquer outro número para indicar um erro.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>Consulte também  
 [Configurando protocolos de rede do servidor e bibliotecas de rede](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
