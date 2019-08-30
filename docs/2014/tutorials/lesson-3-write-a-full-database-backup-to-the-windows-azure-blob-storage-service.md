---
title: 'Lição 3: Gravar um backup de banco de dados completo no serviço de armazenamento de BLOBs do Azure | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 454c8296-64e9-46ed-b141-5ebfbc8a4fe2
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 1d5a749c61a3bc97de841e1149dd1539cbc990f2
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153471"
---
# <a name="lesson-3-write-a-full-database-backup-to-the-azure-blob-storage-service"></a>Lição 3: Gravar um backup de banco de dados completo no serviço de armazenamento de BLOBs do Azure
  Esta lição demonstra o uso da instrução TSQL para executar um backup de banco de dados completo no serviço de armazenamento de BLOBs do Azure.  
  
## <a name="perform-a-full-database-backup-to-the-azure-blob-storage-service"></a>Executar um backup de banco de dados completo para o serviço de armazenamento de BLOBs do Azure  
 Para criar um backup de banco de dados completo, execute as seguintes etapas:  
  
1.  Conecte-se ao [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
2.  No **Pesquisador de Objetos**, conecte-se à instância do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
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
 [Lição 4: Execute uma restauração de um backup](../../2014/tutorials/lesson-4-perform-a-restore-from-a-full-database-backup.md)de banco de dados completo.  
  
  
