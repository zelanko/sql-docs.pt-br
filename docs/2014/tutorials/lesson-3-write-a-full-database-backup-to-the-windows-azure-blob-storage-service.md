---
title: 'Lição 3: Gravar um Backup de banco de dados completo para o serviço de armazenamento de BLOBs do Azure do Windows | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 454c8296-64e9-46ed-b141-5ebfbc8a4fe2
caps.latest.revision: 9
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 4a28465f0175be0bfc12e5c9d51a267ae6597ec6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37236076"
---
# <a name="lesson-3-write-a-full-database-backup-to-the-windows-azure-blob-storage-service"></a>Lição 3: Gravar um backup de banco de dados completo no serviço de armazenamento de Blob do Windows Azure
  Esta lição demonstra o uso da instrução tsql para executar um backup completo de banco de dados no serviço de armazenamento de Blob do Windows Azure.  
  
## <a name="perform-a-full-database-backup-to-the-windows-azure-blob-storage-service"></a>Execute um backup completo de banco de dados no serviço de armazenamento de Blob do Windows Azure  
 Para criar um backup de banco de dados completo, execute as seguintes etapas:  
  
1.  Conectar-se ao [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
2.  No **Pesquisador de objetos**, conecte-se à instância do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
3.  Na barra de menus Padrão, clique em **Nova Consulta**.  
  
4.  Copie e cole o exemplo a seguir na janela de consulta, modifique conforme necessário e clique em **Executar**.  
  
    ```  
    BACKUP DATABASE[AdventureWorks2012]   
    TO URL = 'https://mystorageaccount.blob.core.windows.net/privatecontainertest/AdventureWorks2012.bak'   
    /* URL includes the endpoint for the BLOB service, followed by the container name, and the name of the backup file*/   
    WITH CREDENTIAL = 'mycredential';  
    /* name of the credential you created in the previous step */   
    GO  
  
    ```  
  
5.  No Pesquisador de Objetos, conecte-se ao armazenamento do Azure. Procurar o contêiner e os arquivos de backup recém-criados.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 4: Executar uma restauração de um Backup de banco de dados completo](../../2014/tutorials/lesson-4-perform-a-restore-from-a-full-database-backup.md).  
  
  
