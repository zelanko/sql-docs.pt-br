---
title: 'Tutorial: backup e restauração do SQL Server para o Serviço de Armazenamento de Blobs do Azure | Microsoft Docs'
ms.custom: ''
ms.date: 04/09/2018
ms.prod: sql
ms.prod_service: database-engine
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology: performance
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016 Preview
ms.assetid: 9e1d94ce-2c93-45d1-ae2a-2a7d1fa094c4
caps.latest.revision: 11
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1c070d081e622982bbead15826914b01a89179e7
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37991889"
---
# <a name="tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service"></a>Tutorial: backup e restauração do SQL Server no serviço de Armazenamento de Blobs do Azure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Este tutorial ajudará você a compreender como gravar backups e executar restaurações no serviço de Armazenamento de Blobs do Azure.  
  
## <a name="what-you-will-learn"></a>O que você aprenderá  
Este tutorial mostra como criar uma conta de armazenamento, um contêiner de blobs, como criar credenciais para acessar a conta de armazenamento, como gravar um backup do serviço Blob e como executar uma restauração simples. Este tutorial é dividido em quatro lições:  
  
[Lição 1: criar objetos de armazenamento do Azure](http://msdn.microsoft.com/library/74edd1fd-ab00-46f7-9e29-7ba3f1a446c5)  
Nesta lição, você criará uma conta de armazenamento do Azure e um contêiner de blobs.  
  
[Lição 2: criar uma credencial do SQL Server](http://msdn.microsoft.com/library/64f8805c-1ddc-4c96-a47c-22917d12e1ab)  
Nesta lição, você criará uma credencial para armazenar as informações de segurança usadas para acessar a conta de armazenamento do Azure.  
  
[Lição 3: gravar um backup de banco de dados completo no serviço de Armazenamento de Blobs do Azure](https://technet.microsoft.com/en-us/library/jj720552\(v=sql.110\).aspx)  
Nesta lição, você gerará uma instrução T-SQL para gravar um backup do banco de dados AdventureWorks2012 no serviço de Armazenamento de Blobs do Azure.  
  
[Lição 4: executar uma restauração de um backup de banco de dados completo](http://msdn.microsoft.com/library/580f76e6-9802-4abc-9043-db6de592c733)  
Nesta lição, você emitirá uma instrução T-SQL para fazer a restauração a partir do backup de banco de dados criado na lição anterior.  
  
### <a name="requirements"></a>Requisitos  
Para concluir este tutorial, você deve estar familiarizado com os conceitos de backup e restauração do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e a sintaxe do T-SQL. Para usar este tutorial, o sistema deve atender aos seguintes requisitos:  
  
-   Uma instância do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], e o banco de dados AdventureWorks2012 instalado.  
  
    A instância do SQL Server pode ser local ou em uma máquina virtual do Azure.  
  
    Você pode usar um banco de dados de usuário no lugar do AdventureWorks2012 e modificar a sintaxe do tsql adequadamente.  
  
-   A conta de usuário usada para emitir os comandos BACKUP ou RESTORE deve estar na função de banco de dados **db_backup operator** com as permissões **Alterar qualquer credencial**.  
  
### <a name="additional-reading"></a>Leitura adicional  
Estas são algumas leituras que podem ajudar a compreender os conceitos e as práticas recomendadas ao usar o serviço de armazenamento de Blobs do Azure para backups do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
1.  [Backup e restauração do SQL Server com o Serviço de Armazenamento de Blobs do Microsoft Azure](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
2.  [Melhores práticas e solução de problemas de backup do SQL Server para URL](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
## <a name="see-also"></a>Confira também  
[Backup e restauração do SQL Server com o Serviço de Armazenamento de Blobs do Microsoft Azure](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)

