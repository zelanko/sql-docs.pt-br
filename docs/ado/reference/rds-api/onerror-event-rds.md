---
description: Evento onError (RDS)
title: Evento OnError (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- onError event [ADO]
ms.assetid: b01cbc62-fbd7-4068-b16c-8b0f80a05887
author: rothja
ms.author: jroth
ms.openlocfilehash: fb9ab9b7b97875ee62fe96a39ff8d34591810560
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88767945"
---
# <a name="onerror-event-rds"></a>Evento onError (RDS)
O evento **OnError** é chamado sempre que ocorrer um erro durante uma operação.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
onError SCode, Description, Source, CancelDisplay  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *SCode*  
 Um inteiro que indica o código de status do erro.  
  
 *Descrição*  
 Uma **cadeia de caracteres** que indica uma descrição do erro.  
  
 *Origem*  
 Uma **cadeia de caracteres** que indica a consulta ou o comando que causou o erro.  
  
 *CancelDisplay*  
 Um valor **booliano** , que se definido como **true**, que impede que o erro seja exibido em uma caixa de diálogo.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto DataControl (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do modelo de eventos ADO (VC + +)](../ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../guide/data/ado-event-handler-summary.md)