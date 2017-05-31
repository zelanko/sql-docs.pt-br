---
title: Copiar bancos de dados para outros servidores | Microsoft Docs
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
- servers [SQL Server], copying databases between
- bulk exporting [SQL Server], between servers
- database copying [SQL Server]
- migrating databases [SQL Server]
- moving databases
- copying databases
- bulk importing [SQL Server], between servers
ms.assetid: 978406d6-a3c8-4902-b1f4-4ced75234be5
caps.latest.revision: 42
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5079ed05c18a1a2647ea085e89f26ac7187101e3
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="copy-databases-to-other-servers"></a>Copiar bancos de dados em outros servidores
  Às vezes é útil copiar um banco de dados de um computador em outro, seja para testar, verificar a consistência, desenvolver software, executar relatórios, criar um banco de dados espelho, ou, possivelmente, para tornar o banco de dados disponível para operações da ramificação remota.  
  
 Há vários modos de copiar um banco de dados:  
  
-   Usando o Assistente para Copiar Banco de Dados  
  
     Você pode usar o Assistente para Copiar Banco de Dados para copiar ou mover bancos de dados entre servidores ou para atualizar um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para uma versão posterior. Para obter mais informações, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
-   Restaurando um backup de banco de dados  
  
     Para copiar um banco de dados inteiro, você pode usar as instruções BACKUP e RESTORE [!INCLUDE[tsql](../../includes/tsql-md.md)] . Normalmente, a restauração de um backup completo de um banco de dados é usada para copiar o banco de dados de um computador para outro por uma variedade de razões. Para obter informações sobre como usar o backup e a restauração para copiar um banco de dados, veja [Copiar bancos de dados com backup e restauração](../../relational-databases/databases/copy-databases-with-backup-and-restore.md).  
  
    > [!NOTE]  
    >  Para definir um banco de dados espelho para espelhamento de banco de dados, é necessário restaurar o banco de dados sobre o servidor espelho por meio de RESTORE DATABASE *<database_name>* WITH NORECOVERY. Para obter mais informações, consulte [Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md).  
  
-   Usando o Assistente para Gerar Scripts para publicar bancos de dados  
  
     Você pode usar o Assistente para Gerar Scripts para transferir um banco de dados de um computador local para um provedor de hospedagem na Web. Para obter mais informações, veja [Assistente para Gerar e Publicar Scripts](../../relational-databases/scripting/generate-and-publish-scripts-wizard.md).  
  
  
