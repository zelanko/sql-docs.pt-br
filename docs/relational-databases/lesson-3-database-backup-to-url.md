---
title: "Lição 3: Backup de banco de dados em uma URL | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: a9ae1501-b614-49d3-b975-6569da8350b2
caps.latest.revision: "16"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f63e84d8c22b5c88214cc4d85a6bebf572c41430
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="lesson-3-database-backup-to-url"></a>Lição 3: Backup de banco de dados em URL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Nesta lição, você aprenderá a fazer backup do banco de dados AdventureWorks2014 da instância local do SQL Server 2016 no contêiner do Azure criado na [Lição 1: Criar uma política de acesso armazenado e uma assinatura de acesso compartilhado em um contêiner do Azure](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md).  
  
> [!NOTE]  
> Se quiser fazer backup de um banco de dados SQL Server 2012 SP1 CU2 ou posterior ou SQL Server 2014 nesse contêiner do Azure, você poderá usar a sintaxe preterida documentada [aqui](https://technet.microsoft.com/en-US/library/dn435916(v=sql.120).aspx) para fazer backup na URL usando a sintaxe WITH CREDENTIAL.  
  
Para fazer backup de um banco de dados no armazenamento de Blobs, siga estas etapas:  
  
1.  Conecte-se ao SQL Server Management Studio.  
  
2.  Abra uma nova janela de consulta e conecte-se à instância do SQL Server 2016 do mecanismo de banco de dados na máquina virtual do Azure.  
  
3.  Copie e cole o script Transact-SQL a seguir na janela de consulta. Modifique a URL de forma adequada para o nome de sua conta de armazenamento e o contêiner especificado na Lição 1 e execute este script.  
  
    ```  
  
    -- To permit log backups, before the full database backup, modify the database to use the full recovery model.  
    USE master;  
    ALTER DATABASE AdventureWorks2014  
       SET RECOVERY FULL;  
  
    -- Back up the full AdventureWorks2014 database to the container that you created in Lesson 1  
    BACKUP DATABASE AdventureWorks2014   
       TO URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_onprem.bak'  
  
    ```  
  
4.  Abra o Pesquisador de Objetos e conecte-se ao armazenamento do Azure usando sua conta de armazenamento e a chave de conta.  
  
5.  Expanda Contêineres, expanda o contêiner criado na Lição 1 e verifique se o backup da etapa 3 acima é exibido nesse contêiner.  
  
    ![O arquivo de backup local aparece como um blob no contêiner do Azure](../relational-databases/media/0d060e51-012f-4c61-ab8d-16d461d0ffad.JPG "O arquivo de backup local aparece como um blob no contêiner do Azure")  
  
**Próxima lição:**  
  
[Lição 4: Restaurar o banco de dados na máquina virtual por meio da URL](../relational-databases/lesson-4-restore-database-to-virtual-machine-from-url.md)  
  
