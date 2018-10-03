---
title: Nome de caminho (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- PathName_TSQL
- PathName
dev_langs:
- TSQL
helpviewer_keywords:
- PathName FILESTREAM [SQL Server]
ms.assetid: 6b95ad90-6c82-4a23-9294-a2adb74934a3
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: fe641df85802baab70efa514179f5abbeaea8951
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47852014"
---
# <a name="pathname-transact-sql"></a>PathName (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o caminho de um objeto binário grande FILESTREAM (BLOB). A API OpenSqlFilestream usa esse caminho para retornar um identificador que um aplicativo pode usar para trabalhar com os dados de BLOB usando as APIs do Win32. PathName é somente leitura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
column_name.PathName ( @option [ , use_replica_computer_name ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *column_name*  
 É o nome da coluna de uma **varbinary (max)** coluna FILESTREAM. *column_name* deve ser um nome de coluna. Não pode ser uma expressão nem o resultado de uma instrução CAST ou CONVERT.  
  
 Solicitação de PathName para uma coluna de qualquer outro tipo de dados ou para um **varbinary (max)** columnthat não tem o será de atributo de armazenamento FILESTREAM causará um erro de tempo de compilação de consulta.  
  
 *@option*  
 Um inteiro [expressão](../../t-sql/language-elements/expressions-transact-sql.md) que define como o componente de servidor do caminho deve ser formatado. *@option* pode ser um dos valores a seguir. O padrão é 0.  
  
|Valor|Description|  
|-----------|-----------------|  
|0|Retorna o nome do servidor convertido no formato de BIOS, por exemplo: `\\SERVERNAME\MSSQLSERVER\v1\Archive\dbo\Records\Chart\A73F19F7-38EA-4AB0-BB89-E6C545DBD3F9`|  
|1|Retorna o nome do servidor sem conversão, por exemplo: `\\ServerName\MSSQLSERVER\v1\Archive\dbo\Records\Chart\A73F1`|  
|2|Retorna o caminho completo do servidor, por exemplo: `\\ServerName.MyDomain.com\MSSQLSERVER\v1\Archive\dbo\Records\Chart\A73F19F7-38EA-4AB0-BB89-E6C545DBD3F9`|  
  
 *use_replica_computer_name*  
 Um valor de bit que define como o nome do servidor deve ser retornado em um grupo de disponibilidade Always On.  
  
 Quando o banco de dados não pertence a um grupo de disponibilidade Always On, o valor desse argumento será ignorado. O nome do computador sempre é usado no caminho.  
  
 Quando o banco de dados pertence a um de disponibilidade Always On do grupo, em seguida, o valor de *use_replica_computer_name* tem o seguinte efeito na saída da **PathName** função:  
  
|Valor|Description|  
|-----------|-----------------|  
|Não especificado.|A função retorna o VNN (nome de rede virtual) no caminho.|  
|0|A função retorna o VNN (nome de rede virtual) no caminho.|  
|1|A função retorna o nome do computador no caminho.|  
  
## <a name="return-type"></a>Tipo de retorno  
 **nvarchar(max)**  
  
## <a name="return-value"></a>Valor retornado  
 O valor retornado é o caminho lógico qualificado global ou NETBIOS do BLOB. PathName não retorna um endereço IP. NULL é retornado quando o FILESTREAM BLOB não foi criado.  
  
## <a name="remarks"></a>Comentários  
 A coluna ROWGUID deve estar visível em qualquer consulta que chama PathName.  
  
 Um FILESTREAM BLOB só pode ser criado usando [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-reading-the-path-for-a-filestream-blob"></a>A. Lendo o caminho para um FILESTREAM BLOB  
 O exemplo a seguir atribui `PathName` a uma variável `nvarchar(max)`.  
  
```sql  
DECLARE @PathName nvarchar(max);  
SET @PathName = (  
    SELECT TOP 1 photo.PathName()  
    FROM dbo.Customer  
    WHERE LastName = 'CustomerName'  
    );  
```  
  
### <a name="b-displaying-the-paths-for-filestream-blobs-in-a-table"></a>B. Exibindo os caminhos de FILESTREAM BLOBs em uma tabela  
 O exemplo a seguir cria e exibe os caminhos para três FILESTREAM BLOBs.  
  
```sql  
-- Create a FILESTREAM-enabled database.  
-- The c:\data directory must exist.  
CREATE DATABASE PathNameDB  
ON  
PRIMARY ( NAME = ArchX1,  
    FILENAME = 'c:\data\archdatP1.mdf'),  
FILEGROUP FileStreamGroup1 CONTAINS FILESTREAM( NAME = ArchX3,  
    FILENAME = 'c:\data\filestreamP1')  
LOG ON  ( NAME = ArchlogX1,  
    FILENAME = 'c:\data\archlogP1.ldf');  
GO  
  
USE PathNameDB;  
GO  
  
-- Create a table, add some records, and  
-- create the associated FILESTREAM  
-- BLOB files.  
  
CREATE TABLE TABLE1  
    (  
        ID int,  
        RowGuidColumn UNIQUEIDENTIFIER  
                      NOT NULL UNIQUE ROWGUIDCOL,  
        FILESTREAMColumn varbinary(MAX) FILESTREAM  
    );  
GO  
  
INSERT INTO TABLE1 VALUES  
 (1, NEWID(), 0x00)  
,(2, NEWID(), 0x00)  
,(3, NEWID(), 0x00);  
GO  
  
SELECT FILESTREAMColumn.PathName() AS 'PathName' FROM TABLE1;  
  
--Results  
--PathName  
------------------------------------------------------------------------------------------------------------  
--\\SERVER\MSSQLSERVER\v1\PathNameExampleDB\dbo\TABLE1\FILESTREAMColumn\DD67C792-916E-4A76-8C8A-4A85DC5DB908  
--\\SERVER\MSSQLSERVER\v1\PathNameExampleDB\dbo\TABLE1\FILESTREAMColumn\2907122B-2560-4CB9-86DC-FBE7ABA1843B  
--\\SERVER\MSSQLSERVER\v1\PathNameExampleDB\dbo\TABLE1\FILESTREAMColumn\922BE0E0-CAB9-4403-90BF-945BD258E4BC  
--  
--(3 row(s) affected)  
GO  
  
--Drop the database to clean up.  
USE master;  
GO  
DROP DATABASE PathNameDB;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Objeto binário grande &#40;Blob&#41; Dados &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)   
 [GET_FILESTREAM_TRANSACTION_CONTEXT &#40;Transact-SQL&#41;](../../t-sql/functions/get-filestream-transaction-context-transact-sql.md)   
 [Acessar dados do FILESTREAM com OpenSqlFilestream](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)  
  
  
