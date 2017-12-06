---
title: Exibindo o Log de erros do SQL Server | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cycling SQL Server error log
- viewing SQL Server error log
- errors [SQL Server], logs
- SQL Server error log
- displaying SQL Server error log
- logs [SQL Server], SQL Server error logs
ms.assetid: 6908c21a-65e3-458f-a272-fee256d86448
caps.latest.revision: "24"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f25d82815803d6003d5b9196c4f38caf012beaeb
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="viewing-the-sql-server-error-log"></a>Exibindo o log de erros do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Exibição de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] log de erros para garantir que os processos sejam concluídas com êxito (por exemplo, operações de backup e restauração, comandos em lotes ou outros scripts e processos). Isso poderá ajudar a detectar áreas com problemas atuais ou em potencial, inclusive mensagens de recuperação automática, principalmente se tiver ocorrido parada e reinicialização de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , mensagens do kernel ou outras mensagens de erro do servidor.  
  
 Exiba o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou qualquer editor de texto. Para obter mais informações sobre como exibir o log de erros, consulte [Open Log File Viewer](../../relational-databases/logs/open-log-file-viewer.md). Por padrão, o log de erros está localizado nos arquivos `Program Files\Microsoft SQL Server\MSSQL.`*n*`\MSSQL\LOG\ERRORLOG` e `ERRORLOG.`*n* .  
  
 Um novo log de erros é criado sempre que uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciada, embora o procedimento armazenado do sistema, [sp_cycle_errorlog](../../relational-databases/system-stored-procedures/sp-cycle-errorlog-transact-sql.md) , possa ser usado no ciclo de arquivos de log de erros sem a necessidade de reiniciar a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Em geral, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retém backups dos seis logs anteriores e fornece ao backup de log mais recente a extensão .1, ao segundo mais recente a extensão .2 e assim por diante. O log de erros atual não tem extensão.  
  
 Também é possível exibir o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] log de erros em instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que estejam offline ou que não seja possível inicializar. Para obter mais informações, veja [Exibir arquivos de log offline](../../relational-databases/logs/view-offline-log-files.md).  
  
  
