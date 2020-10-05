---
description: Método Cancel (RDS)
title: Método Cancel (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Cancel method [RDS]
ms.assetid: 560b5b3d-fba9-4275-8920-9c3e186134f7
author: rothja
ms.author: jroth
ms.openlocfilehash: 24f72c16e1c27d070bcc52fc29c6599cc11c737e
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91722687"
---
# <a name="cancel-method-rds"></a>Método Cancel (RDS)
Cancela a execução de uma chamada de método pendente e assíncrona.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](/dotnet/framework/wcf/).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RDS.DataControl.Cancel  
```  
  
## <a name="remarks"></a>Comentários  
 Quando você chama **Cancel**, [ReadyState](./readystate-property-rds.md) é definido automaticamente como **AdcReadyStateLoaded**e o [conjunto de registros](../ado-api/recordset-object-ado.md) estará vazio.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto DataControl (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método Cancel (VBScript)](./cancel-method-example-vbscript.md)   
 [Método Cancel (ADO)](../ado-api/cancel-method-ado.md)   
 [Método CancelBatch (ADO)](../ado-api/cancelbatch-method-ado.md)   
 [Método CancelUpdate (ADO)](../ado-api/cancelupdate-method-ado.md)   
 [Método CancelUpdate (RDS)](./cancelupdate-method-rds.md)   
 [Propriedade ExecuteOptions (RDS)](./executeoptions-property-rds.md)