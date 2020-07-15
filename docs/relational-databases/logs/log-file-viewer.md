---
title: Visualizador do Arquivo de Log | Microsoft Docs
description: Use o Visualizador do Arquivo de Log no SQL Server Management Studio para acessar informações sobre erros e eventos capturados em arquivos de log.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Log File Viewer
ms.assetid: a4ea7fc8-1cb2-4c98-bc86-8991c5e748b2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7425bb2175b9a2e7b813f63e7d78aec7e73ef5ec
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85668124"
---
# <a name="log-file-viewer"></a>Visualizador do Arquivo de Log
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  O Visualizador do Arquivo de Log no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] é usado para acessar informações sobre erros e eventos capturados em arquivos de log.  
  
## <a name="benefits-of-using-log-file-viewer"></a>Benefícios do uso do Visualizador do Arquivo de Log  
 Você pode exibir arquivos de log do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de uma instância local ou remota do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando a instância de destino estiver offline ou não iniciar. Você pode acessar os arquivos de log offline de Servidores Registrados, ou programaticamente por WMI e o WQL (Linguagem WQL) consulta. Para obter mais informações, veja [Exibir arquivos de log offline](../../relational-databases/logs/view-offline-log-files.md). Estes são tipos de arquivos de log que você pode acessar usando o Visualizador do Arquivo de Log:  
  
-   Coleta de Auditoria  
  
-   Coleta de dados  
  
-   Database Mail  
  
-   Histórico de Trabalhos  
  
-   Planos de manutenção  
  
-   Planos de Manutenção Remotos  
  
-   SQL Server  
  
-   SQL Server Agent  
  
-   Windows NT (eventos do Windows que também podem ser acessados a partir do Visualizador de Eventos)  
  
## <a name="log-file-viewer-tasks"></a>Tarefas do Visualizador do Arquivo de Log  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Descreve como abrir o Visualizador do Arquivo de Log, dependendo das informações que você deseja exibir.|[Abrir o Visualizador do Arquivo de Log](../../relational-databases/logs/open-log-file-viewer.md)|  
|Descreve como exibir arquivos de log offline através de servidores registrados e como verificar permissões de WMI.|[Exibir arquivos de log offline](../../relational-databases/logs/view-offline-log-files.md)|  
|Oferece ajuda F1 do Visualizador de Arquivo de Log.|[Ajuda F1 do Visualizador do Arquivo de Log](../../relational-databases/logs/log-file-viewer-f1-help.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)   
 [Log de erros do SQL Server Agent](../../ssms/agent/sql-server-agent-error-log.md)  
  
  
