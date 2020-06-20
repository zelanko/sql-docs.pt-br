---
title: 'Tutorial: SQL Server arquivos de dados no serviço de armazenamento do Azure | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: e69be67d-da1c-41ae-8c9a-6b12c8c2fb61
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1b80b6af9b198db61f8cd34360ddbb3e00bc13d7
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85037195"
---
# <a name="tutorial-sql-server-data-files-in-azure-storage-service"></a>Tutorial: Arquivos de dados do SQL Server no serviço de Armazenamento do Microsoft Azure
  Bem-vindo ao tutorial SQL Server arquivos de dados no serviço de armazenamento do Azure. Este tutorial explica como armazenar diretamente os arquivos de dados do SQL Server no serviço de Armazenamento de Blobs do Azure.  
  
 SQL Server suporte à integração para o serviço de armazenamento de BLOBs do Azure é um aprimoramento SQL Server 2014. Para obter uma visão geral da funcionalidade e dos benefícios de usar essa funcionalidade, consulte [SQL Server arquivos de dados no Azure](databases/sql-server-data-files-in-microsoft-azure.md).  
  
## <a name="what-you-will-learn"></a>O que você aprenderá  
 Este tutorial mostra como armazenar SQL Server arquivos de dados no serviço de armazenamento do Azure em várias lições. Cada lição é centrada em uma tarefa específica. Primeiro, você aprenderá a criar uma conta de armazenamento e um contêiner no Azure. Em seguida, você aprenderá a criar uma credencial SQL Server para poder integrar o SQL Server ao armazenamento do Azure. Em seguida, você criará um banco de dados no armazenamento do Azure diretamente. Além disso, o tutorial demonstrará criptografia, migração e os cenários de backup e restauração.  
  
 Este tutorial divide-se em nove lições:  
  
 **[Lição 1: Criar um contêiner e uma conta de Armazenamento do Microsoft Azure](../tutorials/lesson-1-create-windows-azure-storage-account-and-container.md)**  
 Nesta lição, você criará uma conta de armazenamento do Azure e um contêiner.  
  
 **[Lição 2. Criar uma política no contêiner e gerar uma assinatura de acesso compartilhado &#40;chave de&#41; SAS](lesson-1-create-stored-access-policy-and-shared-access-signature.md)**  
 Nesta lição, você criará uma política no contêiner do blob e também gerará uma assinatura de acesso compartilhado.  
  
 **[Lição 3: Criar uma credencial do SQL Server](lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)**  
 Nesta lição, você criará uma credencial para armazenar as informações de segurança usadas para acessar a conta de armazenamento do Azure.  
  
 **[Lição 4: Criar um banco de dados no Armazenamento do Microsoft Azure](../relational-databases/lesson-3-database-backup-to-url.md)**  
 Nesta lição, você criará um banco de dados no armazenamento do Azure usando a opção criar nome de arquivo do banco de dados.  
  
 **[Lição 5. &#40;opcional&#41; criptografar seu banco de dados usando TDE](../relational-databases/lesson-4-restore-database-to-virtual-machine-from-url.md)**  
 Nesta lição, você criptografará o banco de dados usando uma criptografia de dados transparente (TDE) e um certificado de servidor.  
  
 **[Lição 6: Migrar um banco de dados de um computador de origem no local para um computador de destino no Azure](lesson-5-backup-database-using-file-snapshot-backup.md)**  
 Nesta lição, você migra um banco de dados do local para uma máquina virtual no Azure usando a opção criar banco de dados para anexar.  
  
 **[Lição 7: Migrar seus arquivos de dados para o Armazenamento do Microsoft Azure](../relational-databases/lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup.md)**  
 Nesta lição, você move os arquivos de dados para o armazenamento do Azure usando a instrução ALTER DATABASE.  
  
 **[Lição 8. Restaurar um banco de dados no armazenamento do Azure](../relational-databases/lesson-7-restore-a-database-to-a-point-in-time.md)**  
 Nesta lição, você restaura um banco de dados no armazenamento do Azure usando a opção de movimentação do banco de dados de restauração.  
  
 **[Lição 9. Restaurar um banco de dados do armazenamento do Azure](lesson-8-restore-as-new-database-from-log-backup.md)**  
 Nesta lição, você restaura um banco de dados do armazenamento do Azure usando a opção de movimentação do banco de dados de restauração.  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server arquivos de dados no Azure](databases/sql-server-data-files-in-microsoft-azure.md)  
  
  
