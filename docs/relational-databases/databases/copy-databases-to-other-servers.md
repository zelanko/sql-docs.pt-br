---
title: Copiar bancos de dados para outros servidores | Microsoft Docs
description: Saiba como copiar um banco de dados do SQL Server de um computador a outro para teste, disponibilizando-o para operações de branch remoto ou por outros motivos.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- servers [SQL Server], copying databases between
- bulk exporting [SQL Server], between servers
- database copying [SQL Server]
- migrating databases [SQL Server]
- moving databases
- copying databases
- bulk importing [SQL Server], between servers
ms.assetid: 978406d6-a3c8-4902-b1f4-4ced75234be5
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2a347556196ff6732ef979fd36e93aff06611448
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85763602"
---
# <a name="copy-databases-to-other-servers"></a>Copiar bancos de dados em outros servidores
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Às vezes é útil copiar um banco de dados de um computador em outro, seja para testar, verificar a consistência, desenvolver software, executar relatórios, criar um banco de dados espelho, ou, possivelmente, para tornar o banco de dados disponível para operações da ramificação remota.  
  
 Há vários modos de copiar um banco de dados:  
  
-   Usando o Assistente para Copiar Banco de Dados  
  
     Você pode usar o Assistente para Copiar Banco de Dados para copiar ou mover bancos de dados entre servidores ou para atualizar um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para uma versão posterior. Para obter mais informações, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
-   Restaurando um backup de banco de dados  
  
     Para copiar um banco de dados inteiro, você pode usar as instruções BACKUP e RESTORE [!INCLUDE[tsql](../../includes/tsql-md.md)] . Normalmente, a restauração de um backup completo de um banco de dados é usada para copiar o banco de dados de um computador para outro por uma variedade de razões. Para obter informações sobre como usar o backup e a restauração para copiar um banco de dados, veja [Copiar bancos de dados com backup e restauração](../../relational-databases/databases/copy-databases-with-backup-and-restore.md).  
  
    > [!NOTE]  
    >  Para definir um banco de dados espelho para espelhamento de banco de dados, é necessário restaurar o banco de dados sobre o servidor espelho por meio de RESTORE DATABASE *<database_name>* WITH NORECOVERY. Para obter mais informações, veja [Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md).  
  
-   Usando o Assistente para Gerar Scripts para publicar bancos de dados  
  
     Você pode usar o Assistente para Gerar Scripts para transferir um banco de dados de um computador local para um provedor de hospedagem na Web. Para obter mais informações, veja [Assistente para Gerar e Publicar Scripts](../../relational-databases/scripting/generate-and-publish-scripts-wizard.md).  
  
  
