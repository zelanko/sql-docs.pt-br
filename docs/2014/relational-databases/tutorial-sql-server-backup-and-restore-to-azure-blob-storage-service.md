---
title: 'Tutorial: Backup e restauração do SQL Server para o Serviço de Armazenamento de Blobs do Azure | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 9e1d94ce-2c93-45d1-ae2a-2a7d1fa094c4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b166930b5d077e7294fcdbc13449d40cab309425
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176119"
---
# <a name="tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service"></a>Tutorial: Backup e restauração do SQL Server no serviço de Armazenamento de Blobs do Azure
  Bem-vindo ao tutorial de Introdução com SQL Server Backup e restauração com o serviço de armazenamento de BLOBs do Azure. Este tutorial ajudará você a compreender como gravar backups e executar restaurações no serviço de Armazenamento de Blobs do Azure.  
  
## <a name="what-you-will-learn"></a>O que você aprenderá  
 Este tutorial mostra como criar uma conta de armazenamento do Windows, um contêiner de blob, criando credenciais para acessar a conta de armazenamento, gravando um backup no serviço de blob e executando uma restauração simples. Este tutorial é dividido em quatro lições:  
  
 [Lição 1: Criar objetos de armazenamento do Azure](../tutorials/lesson-1-create-windows-azure-storage-objects.md)  
 Nesta lição, você criará uma conta de armazenamento do Azure e um contêiner de blobs.  
  
 [Lição 2: Criar uma credencial de SQL Server](../tutorials/lesson-2-create-a-sql-server-credential.md)  
 Nesta lição, você criará uma credencial para armazenar as informações de segurança usadas para acessar a conta de armazenamento do Azure.  
  
 [Lição 3: Gravar um backup de banco de dados completo no serviço de armazenamento de BLOBs do Azure](../tutorials/lesson-3-write-a-full-database-backup-to-the-windows-azure-blob-storage-service.md)  
 Nesta lição, você gerará uma instrução T-SQL para gravar um backup do banco de dados AdventureWorks2012 no serviço de Armazenamento de Blobs do Azure.  
  
 [Lição 4: Executar uma restauração de um backup de banco de dados completo](../tutorials/lesson-4-perform-a-restore-from-a-full-database-backup.md)  
 Nesta lição, você emitirá uma instrução T-SQL para fazer a restauração a partir do backup de banco de dados criado na lição anterior.  
  
### <a name="requirements"></a>Requisitos  
 Para concluir este tutorial, você deve estar familiarizado com os conceitos de backup e restauração do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e a sintaxe do T-SQL. Para usar este tutorial, o sistema deve atender aos seguintes requisitos:  
  
-   Uma instância do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], e o banco de dados AdventureWorks2012 instalado.  
  
     A instância do SQL Server pode ser local ou em uma máquina virtual do Azure.  
  
     Você pode usar um banco de dados de usuário no lugar do AdventureWorks2012 e modificar a sintaxe do tsql adequadamente.  
  
-   A conta de usuário usada para emitir os comandos BACKUP ou RESTORE deve estar na função de banco de dados **operador db_backup** com as permissões **Alterar qualquer credencial** .  
  
### <a name="additional-reading"></a>Leitura adicional  
 Estas são algumas leituras que podem ajudar a compreender os conceitos e as práticas recomendadas ao usar o serviço de armazenamento de Blobs do Azure para backups do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
1.  [SQL Server Backup e restauração com o serviço de armazenamento de BLOBs do Azure](backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
2.  [Práticas recomendadas e solução de problemas de backup do SQL Server para URL](backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
  
