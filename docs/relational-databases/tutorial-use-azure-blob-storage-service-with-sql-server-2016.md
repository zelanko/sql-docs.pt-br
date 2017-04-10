---
title: "Tutorial: Como usar o servi&#231;o de Armazenamento de Blobs do Microsoft Azure com os bancos de dados do SQL Server 2016 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/07/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: e69be67d-da1c-41ae-8c9a-6b12c8c2fb61
caps.latest.revision: 23
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 22
---
# Tutorial: Como usar o servi&#231;o de Armazenamento de Blobs do Microsoft Azure com os bancos de dados do SQL Server 2016
Bem-vindo ao tutorial “Trabalhando com o SQL Server 2016 no serviço de Armazenamento de Blobs do Microsoft Azure”. Este tutorial o ajudará a entender como usar o serviço de armazenamento de Blobs do Microsoft Azure para arquivos de dados e backups do SQL Server.  
  
O suporte da integração do SQL Server no serviço de armazenamento de Blobs do Microsoft Azure começou como uma melhoria do SQL Server 2012 Service Pack 1 CU2 e foi aprimorado ainda mais com o SQL Server 2014 e SQL Server 2016. Para obter uma visão geral da funcionalidade e dos benefícios do uso dessa funcionalidade, consulte [Arquivos de dados do SQL Server no Microsoft Azure](../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md). Para uma demonstração ao vivo, confira [Demonstração da recuperação pontual](https://channel9.msdn.com/Blogs/Windows-Azure/File-Snapshot-Backups-Demo).  
  
||  
|-|  
|**Download**<br /><br />**>>** Para baixar o [!INCLUDE[ssSQL15](../includes/sssql15-md.md)], vá para o **[Centro de Avaliação](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**.<br /><br />**>>** Tem uma conta do Azure?  Então, acesse **[aqui](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016ctp3evaluationwindowsserver2012r2/?wt.mc_id=sqL16_vm)** para executar uma máquina virtual com o [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] já instalado.|  
  
## O que você aprenderá  
Este tutorial mostra como trabalhar com arquivos de dados do SQL Server no serviço de armazenamento de Blobs do Microsoft Azure em várias lições. Cada lição é centrada em uma tarefa específica e as lições devem ser concluídas na sequência. Primeiro, você aprenderá a criar um novo contêiner no armazenamento de Blobs com uma política de acesso armazenado e uma assinatura de acesso compartilhado. Em seguida, você aprenderá a criar uma credencial do SQL Server para integrar o SQL Server com o armazenamento de blobs do Azure. Em seguida, você vai fazer backup de um banco de dados no armazenamento de Blobs e restaurá-lo em uma máquina virtual do Azure. Depois, você vai usar o backup de log de transações de instantâneo de arquivo do SQL Server 2016 para restaurá-lo em um ponto específico e em um novo banco de dados. Por fim, o tutorial demonstrará o uso dos procedimentos armazenados e funções do sistema de metadados para ajudá-lo a entender e trabalhar com backups de instantâneo de arquivo.  
  
Este artigo pressupõe o seguinte:  
  
-   Você tem uma instância local do SQL Server 2016 com uma cópia do AdventureWorks2014 instalado.  
  
-   Você tem uma conta de armazenamento do Azure.  
  
-   Você tem, no mínimo, uma máquina virtual do Azure com o SQL Server 2016 instalado e provisionado, conforme explicado no artigo [Provisionando uma máquina virtual do SQL Server no Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-provision-sql-server/). Como opção, uma segunda máquina virtual pode ser usada para o cenário da [Lição 8: Restaurar como um novo banco de dados por meio do backup de log](../relational-databases/lesson-8-restore-as-new-database-from-log-backup.md).  
  
Este tutorial é dividido em nove lições, que devem ser concluídas na ordem:  
  
**[Lição 1: Criar uma política de acesso armazenado e uma assinatura de acesso compartilhado em um contêiner do Azure](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md)**  
Nesta lição, você aprenderá a criar uma política em um novo contêiner de blobs e também gera uma assinatura de acesso compartilhado para uso na criação de uma credencial do SQL Server.  
  
**[Lição 2: Criar uma credencial do SQL Server usando uma assinatura de acesso compartilhado](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)**  
Nesta lição, você aprenderá a criar uma credencial usando uma chave SAS para armazenar informações de segurança usadas para acessar a conta de armazenamento do Microsoft Azure.  
  
**[Lição 3: Backup de banco de dados em URL](../relational-databases/lesson-3-database-backup-to-url.md)**  
Nesta lição, você aprenderá a fazer backup de um banco de dados local no armazenamento de Blobs do Microsoft Azure.  
  
**[Lição 4: Restaurar o banco de dados na máquina virtual por meio da URL](../relational-databases/lesson-4-restore-database-to-virtual-machine-from-url.md)**  
Nesta lição, você aprenderá a restaurar um banco de dados em uma máquina virtual do Azure por meio do armazenamento de Blobs do Microsoft Azure.  
  
**[Lição 5: Fazer backup do banco de dados usando o backup de instantâneo de arquivo](../relational-databases/lesson-5-backup-database-using-file-snapshot-backup.md)**  
Nesta lição, você aprenderá a fazer backup de um banco de dados usando o backup de instantâneo de arquivo e exibe metadados de instantâneo de arquivo.  
  
**[Lição 6: Gerar log de atividade e de backup usando o backup de instantâneo de arquivo](../relational-databases/lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup.md)**  
Nesta lição, você aprenderá a gerar atividade no banco de dados e executa vários backups de log usando o backup de instantâneo de arquivo e exibe metadados de instantâneo de arquivo.  
  
**[Lição 7: Restaurar um banco de dados em um ponto específico](../relational-databases/lesson-7-restore-a-database-to-a-point-in-time.md)**  
Nesta lição, você aprenderá a restaurar um banco de dados em um ponto específico usando dois backups de log de instantâneo de arquivo.  
  
**[Lição 8: Restaurar como um novo banco de dados por meio do backup de log](../relational-databases/lesson-8-restore-as-new-database-from-log-backup.md)**  
Nesta lição, você aprenderá a restaurar um backup de log de instantâneo de arquivo em um novo banco de dados de outra máquina virtual.  
  
**[Lição 9: Gerenciar conjuntos de backup e backups de instantâneo de arquivo](../relational-databases/lesson-9-manage-backup-sets-and-file-snapshot-backups.md)**  
Nesta lição, você aprenderá a excluir conjuntos de backup desnecessários e aprende a excluir backups de instantâneo de arquivo órfãos (quando necessário).  
  
## Este artigo foi útil para você? Estamos atentos  
Quais são as informações que você está procurando? Você as localizou? Estamos atentos aos seus comentários para aprimorar o conteúdo. Envie seus comentários para [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Tutorial:%20Using%20the%20Microsoft%20Azure%20Blob%20storage%20service%20with%20SQL%20Server%202016%20databases%20page)  
  
## Consulte também  
[Arquivos de dados do SQL Server no Microsoft Azure](../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)  
[Backups de instantâneo de arquivo para arquivos de banco de dados no Azure](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)  
[Backup do SQL Server para URL](../relational-databases/backup-restore/sql-server-backup-to-url.md)  
  
  
  
