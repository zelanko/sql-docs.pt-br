---
title: onReadyStateChange evento (RDS) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords: onReadyStateChange event [ADO]
ms.assetid: bf2ae3ac-bfe4-4709-b50a-ea7c282c3164
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6bfb7ee92573f1e21ecb70f34b73346a0c0303ce
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="onreadystatechange-event-rds"></a>onReadyStateChange evento (RDS)
O **onReadyStateChange** evento é chamado sempre que o valor da [estado de prontidão é](../../../ado/reference/rds-api/readystate-property-rds.md) alterações de propriedade.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
onReadyStateChange  
```  
  
#### <a name="parameters"></a>Parâmetros  
 Nenhum.  
  
## <a name="remarks"></a>Remarks  
 O **estado de prontidão é** propriedade reflete o progresso de uma [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto como assincronamente recupera dados em seu [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto. Use o **onReadyStateChange** evento para monitorar as alterações no **estado de prontidão é** propriedade sempre que ocorrerem. Isso é mais eficiente do que a verificação periodicamente o valor da propriedade.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de modelo de eventos do ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)


