---
title: Monitorando os logs de erros | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5c376340af1674c05ac3a38c88cde202bd35f314
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68211170"
---
# <a name="monitoring-the-error-logs"></a>Monitorando os logs de erros
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registra determinados eventos de sistema e eventos definidos pelo usuário no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e no log do aplicativo do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Ambos os logs registram automaticamente todos os eventos com carimbos de hora. Use as informações do log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para solucionar problemas relacionados ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O log do aplicativo do Windows fornece um panorama dos eventos que ocorrem no sistema operacional Windows, bem como dos eventos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Use o Visualizador de Eventos do Windows para exibir o log do aplicativo e para filtrar as informações. Por exemplo, você pode filtrar eventos, como informações, advertência, erro, auditoria com êxito ou sem êxito.  
  
## <a name="comparing-error-and-application-log-output"></a>comparando a saída do log de erros e do aplicativo  
 Você pode usar o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o log do aplicativo do Windows para identificar a causa dos problemas. Por exemplo, enquanto monitora o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , você pode encontrar mensagens de erro que não contêm as informações do ocorrido. Comparando as datas e as horas dos eventos entre esses logs, você pode reduzir a lista de causas prováveis. O Visualizador do Arquivo de Log do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] permite integrar os logs do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e do Windows à uma única lista, simplificando a compreensão dos eventos relativos ao servidor e aos eventos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte o tópico "Visualizador do Arquivo de Log" nos Manuais Online do SQL Server.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|DESCRIÇÃO|  
|-----------|-----------------|  
|[Exibir o log de erros do SQL Server](../../../2014/tools/configuration-manager/viewing-the-sql-server-error-log.md)|Contém informações sobre o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e como exibi-lo.|  
|[Exibir o log do aplicativo do Windows](viewing-the-windows-application-log.md)|Contém informações sobre o log do aplicativo do Windows e como exibi-lo.|  
  
  
