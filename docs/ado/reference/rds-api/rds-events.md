---
description: Eventos RDS
title: Eventos RDS | Microsoft Docs
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
helpviewer_keywords:
- events [ADO], RDS
- RDS events [ADO]
ms.assetid: e03739e0-8169-46d6-9956-556b644a7645
author: rothja
ms.author: jroth
ms.openlocfilehash: be38e4897e942e30af61937c326cd2efa16a1fd8
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724367"
---
# <a name="rds-events"></a>Eventos RDS
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](/dotnet/framework/wcf/).  
  
|Evento|Descrição|  
|-|-|  
|[OnError (RDS)](./onerror-event-rds.md)|Chamado sempre que ocorre um erro durante uma operação.|  
|[onReadyStateChange (RDS)](./onreadystatechange-event-rds.md)|Chamado sempre que o valor da propriedade **ReadyState** é alterado.|