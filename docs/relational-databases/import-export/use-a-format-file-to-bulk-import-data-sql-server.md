---
title: "Usar um arquivo de formato para importação em massa de dados (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 09/20/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: import-export
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bulk importing [SQL Server], format files
- format files [SQL Server], importing data using
ms.assetid: 2956df78-833f-45fa-8a10-41d6522562b9
caps.latest.revision: "45"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: dfefe25814ab63e91b4104d89ce823de49061c68
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="use-a-format-file-to-bulk-import-data-sql-server"></a>Usar um arquivo de formato para importação em massa de dados (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Este tópico ilustra o uso de um arquivo de formato operações de importação em massa.  Um arquivo de formato mapeia os campos do arquivo de dados para as colunas da tabela.  Examine [Criar um arquivo de formato (SQL Server)](../../relational-databases/import-export/create-a-format-file-sql-server.md) para obter mais informações.

|Contorno|
|---|
|[Antes de começar](#begin)<br />[Condições de teste de exemplo](#etc)<br />&emsp;&#9679;&emsp;[Tabela de exemplo](#sample_table)<br />&emsp;&#9679;&emsp;[Arquivo de dados de exemplo](#sample_data_file)<br />[Criando os arquivos de formato](#create_format_file)<br />&emsp;&#9679;&emsp;[Criando um arquivo de formato não XML](#nonxml_format_file)<br />&emsp;&#9679;&emsp;[Criando um arquivo de formato XML](#xml_format_file)<br />[Usando um arquivo de formato para importar dados em massa](#import_data)<br />&emsp;&#9679;&emsp;[Usando bcp e um arquivo de formato não XML](#bcp_nonxml)<br />&emsp;&#9679;&emsp;[Usando bcp e um arquivo de formato XML](#bcp_xml)<br />&emsp;&#9679;&emsp;[Usando BULK INSERT e um arquivo de formato não XML](#bulk_nonxml)<br />&emsp;&#9679;&emsp;[Usando BULK INSERT e um arquivo de formato XML](#bulk_xml)<br />&emsp;&#9679;&emsp;[Usando OPENROWSET(BULK...) e um arquivo de formato não XML](#openrowset_nonxml)<br />&emsp;&#9679;&emsp;[Usando OPENROWSET(BULK...) e um arquivo de formato XML](#openrowset_xml)<p>                                                                                                                                                                                                                  </p>|
  
## Antes de começar<a name="begin"></a>
* Para um arquivo de formato funcionar com um arquivo de dados de caractere Unicode, todos os campos de entrada devem ser cadeias de caracteres de texto Unicode (isto é, cadeias de caracteres Unicode de tamanho fixo ou terminadas por caractere).
* Para exportar ou importar dados [SQLXML](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md) em massa, use um dos tipos de dados a seguir em seu arquivo de formato:
  * SQLCHAR ou SQLVARYCHAR (os dados são enviados na página de código do cliente ou na página de código implicada pelo agrupamento)
  * SQLNCHAR ou SQLNVARCHAR (os dados são enviados como Unicode)
  * SQLBINARY ou SQLVARYBIN (os dados são enviados sem nenhuma conversão).
* O Banco de Dados SQL do Azure e o Azure SQL Data Warehouse dão suporte apenas ao [bcp](../../tools/bcp-utility.md).  Para obter informações adicionais, consulte:
  * [Carregar dados no Azure SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-overview-load/)
  * [Carregar dados do SQL Server no Azure SQL Data Warehouse (arquivos simples)](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-load-from-sql-server-with-bcp/)
  * [Migrar seus dados](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-migrate-data/)

## Condições de teste de exemplo<a name="etc"></a>  
Os exemplos de arquivos de formato neste tópico baseiam-se na tabela e no arquivo de dados definidos abaixo.

### **Tabela de exemplo**<a name="sample_table"></a>
O script abaixo cria um banco de dados de teste e uma tabela chamada `myFirstImport`.  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.MyFirstImport (
   PersonID smallint,
   FirstName varchar(25),
   LastName varchar(30),
   BirthDate Date
   );
```

### **Arquivo de dados de exemplo**<a name="sample_data_file"></a>
Usando o Bloco de Notas, crie um arquivo vazio `D:\BCP\myFirstImport.bcp` e insira os seguintes dados:
```
1,Anthony,Grosse,1980-02-23
2,Alica,Fatnowna,1963-11-14
3,Stella,Rosenhain,1992-03-02
```

Como alternativa, você pode executar o seguinte script do PowerShell para criar e preencher o arquivo de dados:
```powershell
cls
# revise directory as desired
$dir = 'D:\BCP\';

$bcpFile = Join-Path -Path $dir -ChildPath 'MyFirstImport.bcp';

# Confirm directory exists
IF ((Test-Path -Path $dir) -eq 0)
{
    Write-Host "The path $dir does not exist; please create or modify the directory.";
    RETURN;
};

# clear content, will error if file does not exist, can be ignored
Clear-Content -Path $bcpFile -ErrorAction SilentlyContinue;

# Add data
Add-Content -Path $bcpFile -Value '1,Anthony,Grosse,1980-02-23';
Add-Content -Path $bcpFile -Value '2,Alica,Fatnowna,1963-11-14';
Add-Content -Path $bcpFile -Value '3,Stella,Rosenhain,1992-03-02';

#Review content
Get-Content -Path $bcpFile;
Invoke-Item $bcpFile;
```

## Criando os arquivos de formato<a name="create_format_file"></a>
O SQL Server dá suporte a dois tipos de arquivo de formato: XML e não XML.  O formato não XML é o formato original com suporte em versões anteriores do SQL Server.

### **Criando um arquivo de formato não XML**<a name="nonxml_format_file"></a>
Examine [Arquivos de formato não XML (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) para obter informações detalhadas.  O comando a seguir usará o [utilitário bcp](../../tools/bcp-utility.md) para gerar um arquivo de formato não XML, `myFirstImport.fmt`, com base no esquema de `myFirstImport`.  Para usar um comando bcp para criar um arquivo de formato, especifique o argumento **format** e use **nul** em vez de um caminho de arquivo de dados.  A opção format também exige a opção **-f** .  Além disso, neste exemplo, o qualificador **c** é usado para especificar dados de caractere, **t** é usado para especificar uma vírgula como um [terminador de campo](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)e **T** é usado para especificar uma conexão confiável usando a segurança integrada.  No prompt de comando, digite o seguinte comando:

```cmd
bcp TestDatabase.dbo.myFirstImport format nul -c -f D:\BCP\myFirstImport.fmt -t, -T

REM Review file
Notepad D:\BCP\myFirstImport.fmt
```

Seu arquivo de formato não XML, `D:\BCP\myFirstImport.fmt` , deve se assemelhar ao seguinte:
```
13.0
4
1       SQLCHAR             0       7       ","      1     PersonID               ""
2       SQLCHAR             0       25      ","      2     FirstName              SQL_Latin1_General_CP1_CI_AS
3       SQLCHAR             0       30      ","      3     LastName               SQL_Latin1_General_CP1_CI_AS
4       SQLCHAR             0       11      "\r\n"   4     BirthDate              ""
```

> [!IMPORTANT]
> Verifique se o arquivo de formato não XML termina com um retorno de carro/alimentação de linha.  Caso contrário, você provavelmente receberá a seguinte mensagem de erro:
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`

### **Criando um arquivo de formato XML**<a name="xml_format_file"></a>  
Examine [Arquivos de formato XML (SQL Server)](../../relational-databases/import-export/xml-format-files-sql-server.md) para obter informações detalhadas.  O comando a seguir usará o [utilitário bcp](../../tools/bcp-utility.md) para criar um arquivo de formato XML, `myFirstImport.xml`, com base no esquema de `myFirstImport`. Para usar um comando bcp para criar um arquivo de formato, especifique o argumento **format** e use **nul** em vez de um caminho de arquivo de dados.  A opção format sempre exige a opção **-f** e, para criar um arquivo de formato XML, é necessário especificar também a opção **-x** .  Além disso, neste exemplo, o qualificador **c** é usado para especificar dados de caractere, **t** é usado para especificar uma vírgula como um [terminador de campo](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)e **T** é usado para especificar uma conexão confiável usando a segurança integrada.  No prompt de comando, digite o seguinte comando:
```cmd
bcp TestDatabase.dbo.myFirstImport format nul -c -x -f D:\BCP\myFirstImport.xml -t, -T

REM Review file
Notepad D:\BCP\myFirstImport.xml
```

Seu arquivo de formato XML, `D:\BCP\myFirstImport.xml` , deve se assemelhar ao seguinte:
```xml
\<?xml version="1.0"?>
\<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <RECORD>
  \<FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>
  \<FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="30" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="11"/>
 </RECORD>
 <ROW>
  \<COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>
  \<COLUMN SOURCE="2" NAME="FirstName" xsi:type="SQLVARYCHAR"/>
  \<COLUMN SOURCE="3" NAME="LastName" xsi:type="SQLVARYCHAR"/>
  \<COLUMN SOURCE="4" NAME="BirthDate" xsi:type="SQLDATE"/>
 </ROW>
</BCPFORMAT>
```

## Usando um arquivo de formato para importar dados em massa<a name="import_data"></a>
Os exemplos abaixo usam o banco de dados, o arquivo de dados e os arquivos de formato criados acima.

### **Usando o [bcp](../../tools/bcp-utility.md) e um [arquivo de formato não XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bcp_nonxml"></a>
No prompt de comando, digite o seguinte comando:
```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.MyFirstImport;"

REM Import data
bcp TestDatabase.dbo.myFirstImport IN D:\BCP\myFirstImport.bcp -f D:\BCP\myFirstImport.fmt -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.MyFirstImport"
```


### **Usando o [bcp](../../tools/bcp-utility.md) e um [arquivo de formato XML](../../relational-databases/import-export/xml-format-files-sql-server.md)**<a name="bcp_xml"></a>
No prompt de comando, digite o seguinte comando:
```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.MyFirstImport;"

REM Import data
bcp TestDatabase.dbo.myFirstImport IN D:\BCP\myFirstImport.bcp -f D:\BCP\myFirstImport.xml -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.MyFirstImport;"
```


### **Usando [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) e um [arquivo de formato não XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bulk_nonxml"></a>
Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myFirstImport; -- (for testing)
BULK INSERT dbo.myFirstImport   
   FROM 'D:\BCP\myFirstImport.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myFirstImport.fmt');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myFirstImport;
```

### **Usando [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) e um [arquivo de formato XML](../../relational-databases/import-export/xml-format-files-sql-server.md)**<a name="bulk_xml"></a>
Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myFirstImport; -- (for testing)
BULK INSERT dbo.myFirstImport   
   FROM 'D:\BCP\myFirstImport.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myFirstImport.xml');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myFirstImport;
```

### **Usando [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) e um [arquivo de formato não XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="openrowset_nonxml"></a>    
Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
USE TestDatabase;
GO

TRUNCATE TABLE myFirstImport; -- (for testing)
INSERT INTO dbo.myFirstImport
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myFirstImport.bcp',
        FORMATFILE = 'D:\BCP\myFirstImport.fmt'
        ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myFirstImport;
```

### **Usando [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) e um [arquivo de formato XML](../../relational-databases/import-export/xml-format-files-sql-server.md)**<a name="openrowset_xml"></a>
Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myFirstImport; -- (for testing)
INSERT INTO dbo.myFirstImport 
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myFirstImport.bcp',
        FORMATFILE = 'D:\BCP\myFirstImport.xml'  
       ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myFirstImport;
```
  
## <a name="more-examples"></a>Mais exemplos:  
 [Criar um arquivo de formato &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)  
 [Usar um arquivo de formato para ignorar uma coluna de tabela &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
 [Usar um arquivo de formato para ignorar um campo de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
 [Usar um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>Consulte também  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Arquivos de formato não XML &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md)   
 [Arquivos de formato XML &#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md)  
  [Arquivos de formato para importação ou exportação de dados (SQL Server)](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)
  
