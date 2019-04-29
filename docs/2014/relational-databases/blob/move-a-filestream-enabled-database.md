---
title: Mover um banco de dados habilitado para FILESTREAM | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], moving a FILESTREAM-enabled database
ms.assetid: dd4d270d-9283-431a-aa6b-e571fced1893
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1e0638477dd826f2023c3728bedb2a6f846ef305
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62920663"
---
# <a name="move-a-filestream-enabled-database"></a>Mover um banco de dados habilitado para FILESTREAM
  Este tópico mostra como mover um banco de dados habilitado para FILESTREAM.  
  
> [!NOTE]  
>  Os exemplos neste tópico requerem o banco de dados Archive que foi criado em [Criar um banco de dados habilitado para FILESTREAM](create-a-filestream-enabled-database.md).  
  
### <a name="to-move-a-filestream-enabled-database"></a>Para mover um banco de dados habilitado para FILESTREAM  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], clique em **Nova Consulta** para abrir o Editor de Consultas.  
  
2.  Copie o script [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir no Editor de Consulta e clique em **Executar**. Este script exibe o local dos arquivos físicos usados pelo banco de dados FILESTREAM.  
  
    ```sql  
    USE Archive  
    GO  
    SELECT type_desc, name, physical_name from sys.database_files  
    ```  
  
3.  Copie o script [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir no Editor de Consulta e clique em **Executar**. Este código torna o banco de dados `Archive` offline.  
  
    ```sql  
    USE master  
    EXEC sp_detach_db Archive  
    GO  
    ```  
  
4.  Crie a pasta `C:\moved_location`e, em seguida, mova os arquivos e pastas listadas na etapa para ela.  
  
5.  Copie o script [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir no Editor de Consulta e clique em **Executar**. Este script define o banco de dados `Archive` como online.  
  
    ```sql  
    CREATE DATABASE Archive ON  
    PRIMARY ( NAME = Arch1,  
        FILENAME = 'c:\moved_location\archdat1.mdf'),  
    FILEGROUP FileStreamGroup1 CONTAINS FILESTREAM( NAME = Arch3,  
        FILENAME = 'c:\moved_location\filestream1')  
    LOG ON  ( NAME = Archlog1,  
        FILENAME = 'c:\moved_location\archlog1.ldf')  
    FOR ATTACH  
    GO  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [sp_detach_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-detach-db-transact-sql)  
  
  
