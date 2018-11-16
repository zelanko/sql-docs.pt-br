---
title: Evento onReadyStateChange (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- onReadyStateChange event [ADO]
ms.assetid: bf2ae3ac-bfe4-4709-b50a-ea7c282c3164
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e544c3f373f5e85254d40915e6b6f241a6b70379
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51606026"
---
# <a name="onreadystatechange-event-rds"></a>Evento onReadyStateChange (RDS)
O **onReadyStateChange** evento é chamado sempre que o valor da [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md) alterações de propriedade.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
onReadyStateChange  
```  
  
#### <a name="parameters"></a>Parâmetros  
 Nenhum.  
  
## <a name="remarks"></a>Comentários  
 O **ReadyState** propriedade reflete o progresso de um [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) do objeto conforme ele recupera de maneira assíncrona dados em seu [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto. Use o **onReadyStateChange** evento para monitorar as alterações na **ReadyState** propriedade sempre que eles ocorrerem. Isso é mais eficiente do que periodicamente para verificar o valor da propriedade.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de modelo de eventos ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)


