---
title: "Armazenamento do Gerenciamento Baseado em Pol&#237;ticas | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Gerenciamento Baseado em Políticas, armazenamento"
ms.assetid: d0cbf214-fc2e-4917-8d31-1d71c9ffa61d
caps.latest.revision: 11
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 11
---
# Armazenamento do Gerenciamento Baseado em Pol&#237;ticas
  As políticas são armazenadas no banco de dados msdb. Após a alteração de uma política ou condição, deve ser feito backup do msdb. Para obter mais informações, consulte [Fazer backup e restaurar bancos de dados do sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md).  
  
## Armazenando políticas  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] inclui políticas que podem ser usadas para monitorar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por padrão, essas políticas não são instaladas no [!INCLUDE[ssDE](../../includes/ssde-md.md)]; no entanto, elas podem ser importadas do local de instalação padrão C:\Arquivos de Programas\Microsoft SQL Server\130\Tools\Policies\DatabaseEngine\1033.  
  
 Você pode criar políticas diretamente usando o menu **Arquivo/Novo** e salvá-las em um arquivo. Isso permite criar políticas quando você não estiver conectado a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 O histórico de políticas avaliadas na instância atual do [!INCLUDE[ssDE](../../includes/ssde-md.md)] é mantido em tabelas do sistema de msdb. O histórico de políticas aplicadas a outras instâncias do [!INCLUDE[ssDE](../../includes/ssde-md.md)] ou aplicadas ao [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou ao [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não é retido.  
  
  