---
title: Método SetCurrentCertificate (classe SecurityCertificate) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- SetCurrentCertificate Method (SecurityCertificate Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetCurrentCertificate method
ms.assetid: 04b1a76a-932d-4824-8506-e346afe7554e
caps.latest.revision: 33
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: faae2dafe6204d35c48df57b1b9816582f96d7ed
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="setcurrentcertificate-method-securitycertificate-class"></a>Método SetCurrentCertificate (classe SecurityCertificate)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Define o certificado de segurança atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.SetCurrentCertificate(SHA , SQLInstance)  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 Um objeto da [classe SecurityCertificate](../../../relational-databases/wmi-provider-configuration-classes/securitycertificate-class/securitycertificate-class.md) que representa um certificado de segurança.  
  
#### <a name="parameters"></a>Parâmetros  
  
|Parâmetro|Description|  
|---------------|-----------------|  
|*SHA*|Um valor da cadeia de caracteres que especifica a impressão digital de SHA (algoritmo de hash seguro) para o certificado de segurança necessário.|  
|*SQLInstance*|Um valor da cadeia de caracteres que especifica a instância para a qual o certificado é necessário.|  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor uint32, que é 0 se o serviço tiver sido modificado com êxito, 1 se a solicitação não tiver suporte e qualquer outro número para indicar um erro.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Configurando protocolos de rede do servidor e bibliotecas de rede](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
