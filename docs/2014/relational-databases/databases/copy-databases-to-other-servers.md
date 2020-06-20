---
title: Copiar bancos de dados para outros servidores | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: bcde6185f25129596b4be7a150d4ee230c54c1a0
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84952080"
---
# <a name="copy-databases-to-other-servers"></a>Copiar bancos de dados em outros servidores
  Às vezes é útil copiar um banco de dados de um computador em outro, seja para testar, verificar a consistência, desenvolver software, executar relatórios, criar um banco de dados espelho, ou, possivelmente, para tornar o banco de dados disponível para operações da ramificação remota.  
  
 Há vários modos de copiar um banco de dados:  
  
-   Usando o Assistente para Copiar Banco de Dados  
  
     Você pode usar o Assistente para Copiar Banco de Dados para copiar ou mover bancos de dados entre servidores ou para atualizar um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para uma versão posterior. Para obter mais informações, consulte [Use the Copy Database Wizard](use-the-copy-database-wizard.md).  
  
-   Restaurando um backup de banco de dados  
  
     Para copiar um banco de dados inteiro, você pode usar as instruções BACKUP e RESTORE [!INCLUDE[tsql](../../includes/tsql-md.md)] . Normalmente, a restauração de um backup completo de um banco de dados é usada para copiar o banco de dados de um computador para outro por uma variedade de razões. Para obter informações sobre como usar o backup e a restauração para copiar um banco de dados, veja [Copiar bancos de dados com backup e restauração](copy-databases-with-backup-and-restore.md).  
  
    > [!NOTE]  
    >  Para definir um banco de dados espelho para espelhamento de banco de dados, é necessário restaurar o banco de dados sobre o servidor espelho por meio de RESTORE DATABASE *<database_name>* WITH NORECOVERY. Para obter mais informações, veja [Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md).  
  
-   Usando o Assistente para Gerar Scripts para publicar bancos de dados  
  
     Você pode usar o Assistente para Gerar Scripts para transferir um banco de dados de um computador local para um provedor de hospedagem na Web. Para obter mais informações, veja [Assistente para Gerar e Publicar Scripts](../scripting/generate-and-publish-scripts-wizard.md).  
  
  
