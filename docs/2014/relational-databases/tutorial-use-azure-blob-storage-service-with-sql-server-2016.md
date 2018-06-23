---
title: 'Tutorial: Arquivos de dados do SQL Server no serviço de armazenamento do Windows Azure | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e69be67d-da1c-41ae-8c9a-6b12c8c2fb61
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: cd793aad219d8e65a787dd3d872046df00cca414
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121661"
---
# <a name="tutorial-sql-server-data-files-in-windows-azure-storage-service"></a>Tutorial: arquivos de dados do SQL Server no serviço de armazenamento do Windows Azure
  Bem-vindo ao tutorial de arquivos de dados do SQL Server no serviço de armazenamento do Windows Azure. Este tutorial explica como armazenar diretamente os arquivos de dados do SQL Server no serviço de armazenamento de Blob do Windows Azure.  
  
 O suporte à integração do SQL Server no serviço de armazenamento de blob do Windows Azure é um aprimoramento do SQL Server 2014. Para obter uma visão geral das funcionalidades e benefícios de usar essa funcionalidade, consulte [arquivos de dados do SQL Server no Windows Azure](databases/sql-server-data-files-in-microsoft-azure.md).  
  
## <a name="what-you-will-learn"></a>O que você aprenderá  
 Este tutorial mostra como armazenar os arquivos de dados do SQL Server no serviço de Armazenamento do Windows Azure em várias lições. Cada lição é centrada em uma tarefa específica. Primeiro, você aprenderá a criar uma conta de armazenamento e um contêiner no Windows Azure. Em seguida, você aprenderá a criar uma credencial do SQL Server para poder integrar o SQL Server com o Armazenamento do Windows Azure. Em seguida, você criará um banco de dados no Armazenamento do Windows Azure diretamente. Além disso, o tutorial demonstrará criptografia, migração e os cenários de backup e restauração.  
  
 Este tutorial divide-se em nove lições:  
  
 **[Lição 1: Criar o contêiner e a conta de armazenamento do Azure do Windows](../tutorials/lesson-1-create-windows-azure-storage-account-and-container.md)**  
 Nesta lição, você criará uma conta de Armazenamento do Windows Azure e um contêiner.  
  
 **[Lição 2. Criar uma política no contêiner e gerar uma assinatura de acesso compartilhado &#40;SAS&#41; chave](lesson-1-create-stored-access-policy-and-shared-access-signature.md)**  
 Nesta lição, você criará uma política no contêiner do blob e também gerará uma assinatura de acesso compartilhado.  
  
 **[Lição 3: Criar uma credencial do SQL Server](lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)**  
 Nesta lição, você criará uma credencial para armazenar as informações de segurança usadas para acessar a conta de armazenamento do Windows Azure.  
  
 **[Lição 4: Criar um banco de dados no armazenamento do Windows Azure](../relational-databases/lesson-3-database-backup-to-url.md)**  
 Nesta lição, você criará um banco de dados no Armazenamento do Windows Azure usando a opção CREATE Database FILENAME.  
  
 **[Lição 5. &#40;Opcional&#41; criptografar o banco de dados usando TDE](../relational-databases/lesson-4-restore-database-to-virtual-machine-from-url.md)**  
 Nesta lição, você criptografará o banco de dados usando uma criptografia de dados transparente (TDE) e um certificado de servidor.  
  
 **[Lição 6: Migrar um banco de dados de uma fonte de máquina local para um computador de destino no Windows Azure](lesson-5-backup-database-using-file-snapshot-backup.md)**  
 Nesta lição, você migrará um banco de dados local para uma máquina virtual no Windows Azure usando a opção CREATE DATABASE FOR ATTACH.  
  
 **[Lição 7: Mover os arquivos de dados para o armazenamento do Windows Azure](../relational-databases/lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup.md)**  
 Nesta lição, você moverá os arquivos de dados para o Armazenamento do Windows Azure usando a instrução ALTER DATABASE.  
  
 **[Lição 8. Restaurar um banco de dados para o armazenamento do Windows Azure](../relational-databases/lesson-7-restore-a-database-to-a-point-in-time.md)**  
 Nesta lição, você restaurará um banco de dados para o Armazenamento do Windows Azure usando a opção RESTORE Database MOVE.  
  
 **[Lição 9. Restaurar um banco de dados de armazenamento do Windows Azure](lesson-8-restore-as-new-database-from-log-backup.md)**  
 Nesta lição, você restaurará um banco de dados do Armazenamento do Windows Azure usando a opção RESTORE Database MOVE.  
  
## <a name="see-also"></a>Consulte também  
 [Arquivos de dados do SQL Server no Microsoft Azure](databases/sql-server-data-files-in-microsoft-azure.md)  
  
  