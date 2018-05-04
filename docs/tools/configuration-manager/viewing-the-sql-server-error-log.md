---
title: Exibindo o Log de erros do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- cycling SQL Server error log
- viewing SQL Server error log
- errors [SQL Server], logs
- SQL Server error log
- displaying SQL Server error log
- logs [SQL Server], SQL Server error logs
ms.assetid: 6908c21a-65e3-458f-a272-fee256d86448
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 15708cb149ce4baa8068f298aa5478fd221d4331
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="viewing-the-sql-server-error-log"></a>Exibindo o log de erros do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  Exiba o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para garantir que os processos tenham sido concluídos com êxito (por exemplo, operações de backup e restauração, comandos em lotes ou outros scripts e processos). Isso poderá ajudar a detectar áreas com problemas atuais ou em potencial, inclusive mensagens de recuperação automática, principalmente se tiver ocorrido parada e reinicialização de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , mensagens do kernel ou outras mensagens de erro do servidor.  
  
 Exiba o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou qualquer editor de texto. Para obter mais informações sobre como exibir o log de erros, consulte [Open Log File Viewer](../../relational-databases/logs/open-log-file-viewer.md). Por padrão, o log de erros está localizado nos arquivos `Program Files\Microsoft SQL Server\MSSQL.`*n*`\MSSQL\LOG\ERRORLOG` e `ERRORLOG.`*n* .  
  
 Um novo log de erros é criado sempre que uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciada, embora o procedimento armazenado do sistema, [sp_cycle_errorlog](../../relational-databases/system-stored-procedures/sp-cycle-errorlog-transact-sql.md) , possa ser usado no ciclo de arquivos de log de erros sem a necessidade de reiniciar a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Em geral, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retém backups dos seis logs anteriores e fornece ao backup de log mais recente a extensão .1, ao segundo mais recente a extensão .2 e assim por diante. O log de erros atual não tem extensão.  
  
 Também é possível exibir o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] log de erros em instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que estejam offline ou que não seja possível inicializar. Para obter mais informações, veja [Exibir arquivos de log offline](../../relational-databases/logs/view-offline-log-files.md).  
  
  
