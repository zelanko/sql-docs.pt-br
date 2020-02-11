---
title: 'Lição 7: mover seus arquivos de dados para o armazenamento do Azure | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 26aa534a-afe7-4a14-b99f-a9184fc699bd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 25ae3cee8e08292297449914bfb6e40dfc1b4b3a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "70175458"
---
# <a name="lesson-7-move-your-data-files-to-azure-storage"></a>Lição 7: Mover os arquivos de dados para o Armazenamento do Microsoft Azure
  Nesta lição, você aprenderá a mover seus arquivos de dados para o armazenamento do Azure (mas não sua instância de SQL Server). Para acompanhar esta lição, você não precisará concluir as lições 4, 5 e 6.  
  
 Para mover seus arquivos de dados para o armazenamento do Azure, você `ALTER DATABASE` pode usar a instrução, pois ajuda a alterar o local dos arquivos de dados.  
  
 Esta lição supõe que você já concluiu as seguintes etapas:  
  
-   Você tem uma conta de armazenamento do Azure.  
  
-   Você criou um contêiner em sua conta de armazenamento do Azure.  
  
-   Você criou uma política em um contêiner com direitos de leitura, gravação e lista. Você também gerou uma chave de SAS.  
  
-   Você criou uma credencial do SQL Server no computador de origem.  
  
 Em seguida, use as seguintes etapas para mover seus arquivos de dados para o armazenamento do Azure:  
  
1.  Primeiro, crie um banco de dados de teste no computador de origem e adicione alguns dados a ele.  
  
    ```sql  
  
    USE master;   
    CREATE DATABASE TestDB1Alter;   
    GO   
    USE TestDB1Alter;   
    GO   
    CREATE TABLE Table1 (Col1 int primary key, Col2 varchar(20));   
    GO   
    INSERT INTO Table1 (Col1, Col2) VALUES (1, 'string1'), (2, 'string2');   
    GO  
  
    ```  
  
2.  Execute o código a seguir:  
  
    ```sql  
  
    -- In the following statement, modify the path specified in FILENAME to   
    -- the new location of the file in Azure Storage container.   
    ALTER DATABASE TestDB1Alter    
        MODIFY FILE ( NAME = TestDB1Alter,    
                    FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontaineralter/TestDB1AlterData.mdf');   
    GO  
  
    ```  
  
3.  Quando você executar isso, verá esta mensagem: "o arquivo" TestDB1Alter "foi modificado no catálogo do sistema. O novo caminho será usado na próxima vez que o banco de dados for iniciado. "  
  
4.  Em seguida, defina o banco de dados offline.  
  
    ```sql  
  
    ALTER DATABASE TestDB1Alter SET OFFLINE;   
    GO  
  
    ```  
  
5.  Agora, você precisa copiar os arquivos de dados para o armazenamento do Azure usando um dos seguintes métodos: [ferramenta AzCopy](https://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx), [colocar página](https://msdn.microsoft.com/library/azure/ee691975.aspx), [referência da biblioteca de cliente de armazenamento](https://msdn.microsoft.com/library/azure/dn261237.aspx)ou uma ferramenta de Gerenciador de armazenamento de terceiros.  
  
     **Importante:** Ao usar esse novo aprimoramento, sempre certifique-se de criar um blob de páginas não um blob de blocos.  
  
6.  Em seguida, defina o banco de dados online.  
  
    ```sql  
  
    ALTER DATABASE TestDB1Alter SET ONLINE;   
    GO  
  
    ```  
  
 **Próxima lição:**  
  
 [Lição 8. Restaurar um banco de dados no armazenamento do Azure](lesson-7-restore-a-database-to-a-point-in-time.md)  
  
  
