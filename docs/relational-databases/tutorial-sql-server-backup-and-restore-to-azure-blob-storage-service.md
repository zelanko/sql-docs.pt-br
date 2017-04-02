---
title: "Tutorial: Backup e restaura&#231;&#227;o do SQL Server para o servi&#231;o de armazenamento de Blob do Windows Azure | Microsoft Docs"
ms.custom: ""
ms.date: "02/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-query-tuning"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016 Preview"
ms.assetid: 9e1d94ce-2c93-45d1-ae2a-2a7d1fa094c4
caps.latest.revision: 11
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 9
---
# Tutorial: Backup e restaura&#231;&#227;o do SQL Server para o servi&#231;o de armazenamento de Blob do Windows Azure
Bem-vindo ao tutorial Introdução ao Backup e à restauração do SQL Server com o serviço de armazenamento de Blob do Windows Azure. Este tutorial ajuda a compreender como gravar backups e executar restaurações no serviço de armazenamento de Blob do Windows Azure.  
  
## O que você aprenderá  
Este tutorial mostra como criar uma conta de armazenamento do Windows, um contêiner de blob, criando credenciais para acessar a conta de armazenamento, gravando um backup no serviço de blob e executando uma restauração simples. Este tutorial é dividido em quatro lições:  
  
[Lição 1: Criar objetos de armazenamento do Windows Azure](../Topic/Lesson%201:%20Create%20Windows%20Azure%20Storage%20Objects.md)  
Nesta lição, você criará uma conta de armazenamento do Windows Azure e um contêiner de blob.  
  
[Lesson 2: Create a SQL Server Credential](../Topic/Lesson%202:%20Create%20a%20SQL%20Server%20Credential.md)  
Nesta lição, você criará uma credencial para armazenar as informações de segurança usadas para acessar a conta de armazenamento do Windows Azure.  
  
[Lição 3: Gravar um backup de banco de dados completo no serviço de armazenamento de Blob do Windows Azure](../Topic/Lesson%203:%20Write%20a%20Full%20Database%20Backup%20to%20the%20Windows%20Azure%20Blob%20Storage%20Service.md)  
Nesta lição, você emitirá uma instrução T-SQL para gravar um backup do banco de dados AdventureWorks2012 no serviço de armazenamento de Blob do Windows Azure.  
  
[Lição 4: Executar uma restauração a partir de um backup de banco de dados completo](../Topic/Lesson%204:%20Perform%20a%20Restore%20From%20a%20Full%20Database%20Backup.md)  
Nesta lição, você emitirá uma instrução T-SQL para fazer a restauração a partir do backup de banco de dados criado na lição anterior.  
  
### Requisitos  
Para concluir este tutorial, você deve estar familiarizado com [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de backup e restauração conceitos e a sintaxe do T-SQL. Para usar este tutorial, o sistema deve atender aos seguintes requisitos:  
  
-   Uma instância do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], e o banco de dados AdventureWorks2012 instalado.  
  
    A instância do SQL Server pode ser no local ou em uma máquina virtual do Windows Azure.  
  
    Você pode usar um banco de dados de usuário no lugar do AdventureWorks2012 e modificar a sintaxe do tsql adequadamente.  
  
-   A conta de usuário usada para emitir os comandos BACKUP ou RESTORE deve estar na função de banco de dados **operador db_backup** com as permissões **Alterar qualquer credencial**.  
  
### Leitura adicional  
Estas são algumas leituras que podem ajudar a compreender os conceitos e as práticas recomendadas no uso do serviço de armazenamento de Blob do Windows Azure para backups do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
1.  [Backup e restauração do SQL Server com o Serviço de Armazenamento de Blobs do Microsoft Azure](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
2.  [Práticas recomendadas e solução de problemas de backup do SQL Server para URL](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
## Consulte também  
[Fazendo backup do banco de dados e do log](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md#databaselog)  
[Criando um backup de arquivo completo do grupo de arquivos primário](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md#filegroups)  
[Restaurando um banco de dados e movendo arquivos](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md#restoredbwithmove)  
  
