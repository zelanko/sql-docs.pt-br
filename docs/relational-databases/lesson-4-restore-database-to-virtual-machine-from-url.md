---
title: 'Lição 4: Restaurar o banco de dados na máquina virtual por meio da URL | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: ba793c8f-665a-4c46-b68d-f558a37906b2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 006370ef2f1d40f83c8ea50cfce15c13c4c33fb5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47794942"
---
# <a name="lesson-4-restore-database-to-virtual-machine-from-url"></a>Lição 4: Restaurar o banco de dados na máquina virtual por meio da URL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Nesta lição, você restaurará o banco de dados AdventureWorks2014 na instância do SQL Server 2016 na máquina virtual do Azure.
  
> [!NOTE]  
> Para fins de simplicidade neste tutorial, estamos usando o mesmo contêiner para os arquivos de log e de dados que foram usados para o backup do banco de dados. Em um ambiente de produção, provavelmente, você usará vários contêineres e, com frequência, vários arquivos de dados também. Com o SQL Server 2016, você poderá também considerar a distribuição do backup em vários blobs, a fim de aumentar o desempenho do backup ao fazer backup de um banco de dados grande.  
  
Para restaurar o banco de dados SQL Server 2014 do armazenamento de blobs do Azure na instância do SQL Server 2016 da máquina virtual do Azure, siga estas etapas:  
  
1.  Conecte-se ao SQL Server Management Studio.  
  
2.  Abra uma nova janela de consulta e conecte-se à instância do SQL Server 2016 do mecanismo de banco de dados na máquina virtual do Azure.  
  
3.  Copie e cole o script Transact-SQL a seguir na janela de consulta. Modifique a URL de forma adequada para o nome de sua conta de armazenamento e o contêiner especificado na Lição 1 e execute este script.  
  
    ```  
  
    -- Restore AdventureWorks2014 from URL to SQL Server instance using Azure blob storage for database files  
    RESTORE DATABASE AdventureWorks2014   
       FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_onprem.bak'   
       WITH  
          MOVE 'AdventureWorks2014_data' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_Data.mdf'  
         ,MOVE 'AdventureWorks2014_log' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_Log.ldf'  
    --, REPLACE  
  
    ```  
  
4.  Abra o Pesquisador de Objetos e conecte-se à instância do Azure SQL Server 2016.  
  
5.  No Pesquisador de Objetos, expanda o nó Bancos de Dados e verifique se o banco de dados AdventureWorks2014 foi restaurado (atualize o nó, conforme necessário).  
  
    ![Banco de dados do Adventure Works 2014 restaurado no SQL Server 2016 na máquina virtual](../relational-databases/media/311f69a6-8443-4df5-8f30-3103c2472300.JPG "Banco de dados do Adventure Works 2014 restaurado no SQL Server 2016 na máquina virtual")  
  
6.  No Pesquisador de Objetos, clique com o botão direito do mouse em AdventureWorks2014 e em Propriedades (clique em Cancelar quando terminar).  
  
7.  Clique em Arquivos e verifique se o caminho para os dois arquivos de banco de dados são URLs que apontam para os blobs em seu contêiner de blogs do Azure.  
  
    ![propriedades do banco de dados mostrando o caminho dos arquivos de dados lógicos como uma URL](../relational-databases/media/cfeee576-6319-460e-9fa2-f0922e02ee23.JPG "propriedades do banco de dados mostrando o caminho dos arquivos de dados lógicos como uma URL")  
  
8.  No Pesquisador de Objetos, conecte-se ao armazenamento do Azure.  
  
9. Expanda Contêineres, expanda o contêiner criado na Lição 1 e verifique se AdventureWorks2014_Data.mdf e AdventureWorks2014_Log.ldf da etapa 3 acima são exibidos nesse contêiner, juntamente com o arquivo de backup da Lição 3 (atualize o nó, conforme necessário).  
  
    ![Os arquivos de log e de dados do Adventure Works 2014 aparecem como blobs no contêiner do Azure](../relational-databases/media/156c7d73-44be-4754-9653-04cccb6c3066.JPG "Os arquivos de log e de dados do Adventure Works 2014 aparecem como blobs no contêiner do Azure")  
  
**Próxima lição:**  
  
[Lição 5: Fazer backup do banco de dados usando o backup de instantâneo de arquivo](../relational-databases/lesson-5-backup-database-using-file-snapshot-backup.md)  
  
  
  
