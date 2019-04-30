---
title: 'Lição 4: Executar uma restauração de um Backup de banco de dados completo | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 580f76e6-9802-4abc-9043-db6de592c733
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 077fb708f09db0182bc5f1510f0264b139beab13
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63312067"
---
# <a name="lesson-4-perform-a-restore-from-a-full-database-backup"></a>Lição 4: Executar uma restauração de um backup de banco de dados completo
  Esta lição demonstra o uso de uma instrução tsql para executar uma restauração a partir de um backup de banco de dados completo criado na lição anterior.  
  
## <a name="perform-a-restore-of-a-database-backup"></a>Executar uma restauração a partir de um backup de banco de dados  
 Para restaurar um backup de banco de dados completo, execute as seguintes etapas:  
  
1.  Conecte-se ao [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
2.  No **Pesquisador de Objetos**, conecte-se à instância do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
3.  Na barra de menus Padrão, clique em **Nova Consulta**.  
  
4.  Copie e cole o exemplo a seguir na janela de consulta, e modifique conforme necessário.  
  
    ```  
    RESTORE DATABASE AdventureWorks2012   
    FROM URL = 'https://mystorageaccount.blob.core.windows.net/privatecontainertest/AdventureWorks2012.bak'   
    WITH CREDENTIAL = 'mycredential';  
    , STATS = 5 - use this to see monitor the progress  
    GO  
  
    ```  
  
5.  Verifique se a instrução T-SQL e clique em **Execute**  
  
### <a name="return-to-tutorials-portal"></a>Retorne ao portal Tutoriais  
 [Tutorial: Serviço de armazenamento de BLOBs do SQL Server Backup e restauração para o Windows Azure](../relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md).  
  
  
