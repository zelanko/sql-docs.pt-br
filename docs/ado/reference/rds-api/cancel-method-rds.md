---
description: Método Cancel (RDS)
title: Método Cancel (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: 9f4e902888285f758975ffce0381a08b813152ba
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88768805"
---
# <a name="cancel-method-rds"></a>Método Cancel (RDS)
Cancela a execução de uma chamada de método pendente e assíncrona.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
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