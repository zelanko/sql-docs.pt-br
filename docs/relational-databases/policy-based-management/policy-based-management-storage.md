---
title: "Armazenamento do gerenciamento baseado em políticas | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Policy-Based Management, storage
ms.assetid: d0cbf214-fc2e-4917-8d31-1d71c9ffa61d
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0426d583d1ada35c7ad3e36d4fe1a621e9754360
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="policy-based-management-storage"></a>Armazenamento do Gerenciamento Baseado em Políticas
  As políticas são armazenadas no banco de dados msdb. Após a alteração de uma política ou condição, deve ser feito backup do msdb. Para obter mais informações, consulte [Fazer backup e restaurar bancos de dados do sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md).  
  
## <a name="storing-policies"></a>Armazenando políticas  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] inclui políticas que podem ser usadas para monitorar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por padrão, essas políticas não são instaladas no [!INCLUDE[ssDE](../../includes/ssde-md.md)]; no entanto, elas podem ser importadas do local de instalação padrão C:\Arquivos de Programas\Microsoft SQL Server\130\Tools\Policies\DatabaseEngine\1033.  
  
 Você pode criar políticas diretamente usando o menu **Arquivo/Novo** e salvá-las em um arquivo. Isso permite criar políticas quando você não estiver conectado a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 O histórico de políticas avaliadas na instância atual do [!INCLUDE[ssDE](../../includes/ssde-md.md)] é mantido em tabelas do sistema de msdb. O histórico de políticas aplicadas a outras instâncias do [!INCLUDE[ssDE](../../includes/ssde-md.md)] ou aplicadas ao [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou ao [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não é retido.  
  
  
