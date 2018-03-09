---
title: Monitorando os Logs de erro | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logs [SQL Server]
- database performance [SQL Server], errors
- Windows application logs [SQL Server]
- monitoring performance [SQL Server], errors
- server performance [SQL Server], errors
- comparing error and application log output
- errors [SQL Server], logs
- tuning databases [SQL Server], errors
- database monitoring [SQL Server], errors
- SQL Server error log
- logs [SQL Server], SQL Server error logs
- error logs [SQL Server]
- logs [SQL Server], Windows application logs
ms.assetid: e250336b-0695-44f6-a42f-23222f94e377
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: af83c65a76d5dc190ca8833f247d3bc5e3138505
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="monitoring-the-error-logs"></a>Monitorando os logs de erros
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registra determinados eventos de sistema e eventos definidos pelo usuário no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e no log do aplicativo do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Ambos os logs registram automaticamente todos os eventos com carimbos de hora. Use as informações do log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para solucionar problemas relacionados ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O log do aplicativo do Windows fornece um panorama dos eventos que ocorrem no sistema operacional Windows, bem como dos eventos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Use o Visualizador de Eventos do Windows para exibir o log do aplicativo e para filtrar as informações. Por exemplo, você pode filtrar eventos, como informações, advertência, erro, auditoria com êxito ou sem êxito.  
  
## <a name="comparing-error-and-application-log-output"></a>comparando a saída do log de erros e do aplicativo  
 Você pode usar o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o log do aplicativo do Windows para identificar a causa dos problemas. Por exemplo, enquanto monitora o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , você pode encontrar mensagens de erro que não contêm as informações do ocorrido. Comparando as datas e as horas dos eventos entre esses logs, você pode reduzir a lista de causas prováveis. O Visualizador do Arquivo de Log do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] permite integrar os logs do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e do Windows à uma única lista, simplificando a compreensão dos eventos relativos ao servidor e aos eventos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte o tópico "Visualizador do Arquivo de Log" nos Manuais Online do SQL Server.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Exibindo o Log de erros do SQL Server](../../tools/configuration-manager/viewing-the-sql-server-error-log.md)|Contém informações sobre o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e como exibi-lo.|  
|[Exibindo o Log de aplicativo do Windows](../../tools/configuration-manager/viewing-the-windows-application-log.md)|Contém informações sobre o log do aplicativo do Windows e como exibi-lo.|  
  
  
