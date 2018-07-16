---
title: 'Tutorial: SQL Server Backup e restauração para o Windows Azure Blob Storage Service | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 9e1d94ce-2c93-45d1-ae2a-2a7d1fa094c4
caps.latest.revision: 10
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 856ff3ec55236b8216c04fbffeb4f5abed6dbc5d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37188013"
---
# <a name="tutorial-sql-server-backup-and-restore-to-windows-azure-blob-storage-service"></a>Tutorial: Backup e restauração do SQL Server para o serviço de armazenamento de Blob do Windows Azure
  Bem-vindo ao tutorial Introdução ao Backup e à restauração do SQL Server com o serviço de armazenamento de Blob do Windows Azure. Este tutorial ajuda a compreender como gravar backups e executar restaurações no serviço de armazenamento de Blob do Windows Azure.  
  
## <a name="what-you-will-learn"></a>O que você aprenderá  
 Este tutorial mostra como criar uma conta de armazenamento do Windows, um contêiner de blob, criando credenciais para acessar a conta de armazenamento, gravando um backup no serviço de blob e executando uma restauração simples. Este tutorial é dividido em quatro lições:  
  
 [Lição 1: Criar objetos de Armazenamento do Microsoft Azure](../tutorials/lesson-1-create-windows-azure-storage-objects.md)  
 Nesta lição, você criará uma conta de armazenamento do Windows Azure e um contêiner de blob.  
  
 [Lição 2: criar uma credencial do SQL Server](../tutorials/lesson-2-create-a-sql-server-credential.md)  
 Nesta lição, você criará uma credencial para armazenar as informações de segurança usadas para acessar a conta de armazenamento do Windows Azure.  
  
 [Lição 3: Gravar um backup de banco de dados completo no serviço de armazenamento de Blob do Microsoft Azure](../tutorials/lesson-3-write-a-full-database-backup-to-the-windows-azure-blob-storage-service.md)  
 Nesta lição, você emitirá uma instrução T-SQL para gravar um backup do banco de dados AdventureWorks2012 no serviço de armazenamento de Blob do Windows Azure.  
  
 [Lição 4: executar uma restauração de um backup de banco de dados completo](../tutorials/lesson-4-perform-a-restore-from-a-full-database-backup.md)  
 Nesta lição, você emitirá uma instrução T-SQL para fazer a restauração a partir do backup de banco de dados criado na lição anterior.  
  
### <a name="requirements"></a>Requisitos  
 Para concluir este tutorial, você deve estar familiarizado com os conceitos de backup e restauração do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e a sintaxe do T-SQL. Para usar este tutorial, o sistema deve atender aos seguintes requisitos:  
  
-   Uma instância do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], e o banco de dados AdventureWorks2012 instalado.  
  
     A instância do SQL Server pode ser no local ou em uma máquina virtual do Windows Azure.  
  
     Você pode usar um banco de dados de usuário no lugar do AdventureWorks2012 e modificar a sintaxe do tsql adequadamente.  
  
-   A conta de usuário usada para emitir os comandos BACKUP ou RESTORE deve estar na função de banco de dados **operador db_backup** com as permissões **Alterar qualquer credencial** .  
  
### <a name="additional-reading"></a>Leitura adicional  
 Estas são algumas leituras que podem ajudar a compreender os conceitos e as práticas recomendadas no uso do serviço de armazenamento de Blob do Windows Azure para backups do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
1.  [Backup e restauração do SQL Server com o serviço de armazenamento de Blob do Microsoft Azure](backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
2.  [Práticas recomendadas e solução de problemas de backup do SQL Server para URL](backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
  
