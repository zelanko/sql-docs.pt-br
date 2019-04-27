---
title: 'Lição 7: Mover os arquivos de dados para o armazenamento do Windows Azure | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 26aa534a-afe7-4a14-b99f-a9184fc699bd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 45004f8544efc0f0cc02292dbe28fdd75d6dc1de
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62743252"
---
# <a name="lesson-7-move-your-data-files-to-windows-azure-storage"></a>Lição 7: Mover seus arquivos de dados para o Armazenamento do Microsoft Azure
  Nesta lição, você aprenderá a mover os arquivos de dados para o Armazenamento do Windows Azure (mas não a instância do SQL Server). Para acompanhar esta lição, você não precisará concluir as lições 4, 5 e 6.  
  
 Para mover os arquivos de dados para o Armazenamento do Windows Azure, você pode usar a instrução `ALTER DATABASE`, pois ela ajuda a alterar o local dos arquivos de dados.  
  
 Esta lição supõe que você já concluiu as seguintes etapas:  
  
-   Você tem uma conta de Armazenamento do Windows Azure.  
  
-   Você criou um contêiner na sua conta de Armazenamento do Windows Azure.  
  
-   Você criou uma política em um contêiner com direitos de leitura, gravação e lista. Você também gerou uma chave de SAS.  
  
-   Você criou uma credencial do SQL Server no computador de origem.  
  
 Em seguida, use as etapas a seguir para mover os arquivos de dados para o Armazenamento do Windows Azure:  
  
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
  
2.  Execute o seguinte código:  
  
    ```sql  
  
    -- In the following statement, modify the path specified in FILENAME to   
    -- the new location of the file in Windows Azure Storage container.   
    ALTER DATABASE TestDB1Alter    
        MODIFY FILE ( NAME = TestDB1Alter,    
                    FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontaineralter/TestDB1AlterData.mdf');   
    GO  
  
    ```  
  
3.  Quando você executar isso, você verá esta mensagem: "O arquivo"TestDB1Alter"foi modificado no catálogo do sistema. O novo caminho será usado na próxima vez que o banco de dados é iniciado."  
  
4.  Em seguida, defina o banco de dados offline.  
  
    ```sql  
  
    ALTER DATABASE TestDB1Alter SET OFFLINE;   
    GO  
  
    ```  
  
5.  Agora, você precisa copiar os arquivos de dados para o armazenamento do Windows Azure usando um dos seguintes métodos: [Ferramenta AzCopy](https://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx), [Put Page](https://msdn.microsoft.com/library/azure/ee691975.aspx), [referência de biblioteca de cliente de armazenamento](https://msdn.microsoft.com/library/azure/dn261237.aspx), ou uma ferramenta de Gerenciador de armazenamento de terceiros.  
  
     **Importante:** Ao usar esse novo aprimoramento, sempre Certifique-se de que você crie um blob de página não é um blob de blocos.  
  
6.  Em seguida, defina o banco de dados online.  
  
    ```sql  
  
    ALTER DATABASE TestDB1Alter SET ONLINE;   
    GO  
  
    ```  
  
 **Próxima lição:**  
  
 [Lição 8. Restaurar um banco de dados para o Armazenamento do Microsoft Azure](lesson-7-restore-a-database-to-a-point-in-time.md)  
  
  
