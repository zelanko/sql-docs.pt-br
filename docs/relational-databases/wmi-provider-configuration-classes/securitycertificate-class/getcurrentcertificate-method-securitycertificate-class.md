---
description: Método GetCurrentCertificate (classe SecurityCertificate)
title: Método GetCurrentCertificate (SecurityCertificate)
ms.custom: seo-lt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- GetCurrentCertificate Method (SecurityCertificate Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- GetCurrentCertificate method
ms.assetid: 987a2671-1801-45c4-93e6-29f883c58720
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1a341dec5f50a798cd2534e102416df2bc21a538
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537148"
---
# <a name="getcurrentcertificate-method-securitycertificate-class"></a>Método GetCurrentCertificate (classe SecurityCertificate)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Obtém o certificado de segurança atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.GetCurrentCertificate(SHA , SQLInstance)  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe SecurityCertificate](../../../relational-databases/wmi-provider-configuration-classes/securitycertificate-class/securitycertificate-class.md) que representa um certificado de segurança.  
  
#### <a name="parameters"></a>Parâmetros  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|*SHA*|Um valor de objeto da cadeia de caracteres (parâmetro de saída) que especifica a impressão digital SHA do certificado de segurança atual depois que o método é concluído.|  
|*SQLInstance*|Um valor da cadeia de caracteres que especifica a instância para a qual o certificado é necessário.|  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor **uint32** , que é 0 se o serviço tiver sido modificado com êxito, 1 se a solicitação não tiver suporte e qualquer outro número para indicar um erro.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte Também  
 [Configurando protocolos de rede de servidor e Net-Libraries](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
