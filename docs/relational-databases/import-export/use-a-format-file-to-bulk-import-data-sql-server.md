---
title: Usar um arquivo de formato para importação em massa de dados
description: No SQL Server, você pode usar um arquivo de formato em operações de importação em massa. Um arquivo de formato mapeia os campos do arquivo de dados para as colunas da tabela.
ms.date: 09/20/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], format files
- format files [SQL Server], importing data using
ms.assetid: 2956df78-833f-45fa-8a10-41d6522562b9
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: b893b6dc0c3ad11225d1144f757f206fcf5500d5
ms.sourcegitcommit: 22e97435c8b692f7612c4a6d3fe9e9baeaecbb94
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2020
ms.locfileid: "92678973"
---
# <a name="use-a-format-file-to-bulk-import-data-sql-server"></a>Usar um arquivo de formato para importação em massa de dados (SQL Server)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Este tópico ilustra o uso de um arquivo de formato operações de importação em massa.  Um arquivo de formato mapeia os campos do arquivo de dados para as colunas da tabela.  Examine [Criar um arquivo de formato (SQL Server)](../../relational-databases/import-export/create-a-format-file-sql-server.md) para obter mais informações.
  
## <a name="before-you-begin"></a>Antes de começar
* Para um arquivo de formato funcionar com um arquivo de dados de caractere Unicode, todos os campos de entrada devem ser cadeias de caracteres de texto Unicode (isto é, cadeias de caracteres Unicode de tamanho fixo ou terminadas por caractere).
* Para exportar ou importar dados [SQLXML](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md) em massa, use um dos tipos de dados a seguir em seu arquivo de formato:
  * SQLCHAR ou SQLVARCHAR (os dados são enviados na página de código do cliente ou na página de código implícita na ordenação)
  * SQLNCHAR ou SQLNVARCHAR (os dados são enviados como Unicode)
  * SQLBINARY ou SQLVARBIN (os dados são enviados sem nenhuma conversão).
* O Banco de Dados SQL do Azure e o Azure Synapse Analytics dão suporte somente a [bcp](../../tools/bcp-utility.md).  Para obter informações adicionais, consulte:
  * [Carregar dados no Azure Synapse Analytics](/azure/synapse-analytics/sql-data-warehouse/design-elt-data-loading)
  * [Carregar dados do SQL Server no Azure Synapse Analytics (arquivos simples)](/azure/synapse-analytics/sql-data-warehouse/design-elt-data-loading)
  * [Migrar seus dados](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-overview-develop)

## <a name="example-test-conditions"></a>Condições de teste de exemplo
Os exemplos de arquivos de formato neste tópico baseiam-se na tabela e no arquivo de dados definidos abaixo.

### <a name="sample-table"></a>Tabela de exemplo
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

### <a name="sample-data-file"></a>Arquivo de dados de exemplo
Usando o Bloco de Notas, crie um arquivo vazio `D:\BCP\myFirstImport.bcp` e insira os seguintes dados:
```
1,Anthony,Grosse,1980-02-23
2,Alica,Fatnowna,1963-11-14
3,Stella,Rosenhain,1992-03-02
```

Como alternativa, você pode executar o seguinte script do PowerShell para criar e preencher o arquivo de dados:
```powershell
Clear-Host
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
Notepad.exe $bcpfile;
```

## <a name="creating-the-format-files"></a>Criar os arquivos de formato
O SQL Server dá suporte a dois tipos de arquivo de formato: XML e não XML.  O formato não XML é o formato original com suporte em versões anteriores do SQL Server.

### <a name="creating-a-non-xml-format-file"></a>Criando um arquivo de formato não XML
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

### <a name="creating-an-xml-format-file"></a>Criando um arquivo de formato XML
Examine [Arquivos de formato XML (SQL Server)](../../relational-databases/import-export/xml-format-files-sql-server.md) para obter informações detalhadas.  O comando a seguir usará o [utilitário bcp](../../tools/bcp-utility.md) para criar um arquivo de formato XML, `myFirstImport.xml`, com base no esquema de `myFirstImport`. Para usar um comando bcp para criar um arquivo de formato, especifique o argumento **format** e use **nul** em vez de um caminho de arquivo de dados.  A opção format sempre exige a opção **-f** e, para criar um arquivo de formato XML, é necessário especificar também a opção **-x** .  Além disso, neste exemplo, o qualificador **c** é usado para especificar dados de caractere, **t** é usado para especificar uma vírgula como um [terminador de campo](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)e **T** é usado para especificar uma conexão confiável usando a segurança integrada.  No prompt de comando, digite o seguinte comando:
```cmd
bcp TestDatabase.dbo.myFirstImport format nul -c -x -f D:\BCP\myFirstImport.xml -t, -T

REM Review file
Notepad D:\BCP\myFirstImport.xml
```

Seu arquivo de formato XML, `D:\BCP\myFirstImport.xml` , deve se assemelhar ao seguinte:
```xml
<?xml version="1.0"?>
<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <RECORD>
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="30" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="11"/>
 </RECORD>
 <ROW>
  <COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>
  <COLUMN SOURCE="2" NAME="FirstName" xsi:type="SQLVARCHAR"/>
  <COLUMN SOURCE="3" NAME="LastName" xsi:type="SQLVARCHAR"/>
  <COLUMN SOURCE="4" NAME="BirthDate" xsi:type="SQLDATE"/>
 </ROW>
</BCPFORMAT>
```

## <a name="using-a-format-file-to-bulk-import-data"></a>Usar um arquivo de formato para importar dados em massa
Os exemplos abaixo usam o banco de dados, o arquivo de dados e os arquivos de formato criados acima.

### <a name="using-bcp-and-non-xml-format-file"></a>Usando o [bcp](../../tools/bcp-utility.md) e um [arquivo de formato não XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)
No prompt de comando, digite o seguinte comando:
```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.MyFirstImport;"

REM Import data
bcp TestDatabase.dbo.myFirstImport IN D:\BCP\myFirstImport.bcp -f D:\BCP\myFirstImport.fmt -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.MyFirstImport"
```


### <a name="using-bcp-and-xml-format-file"></a>Usar [bcp](../../tools/bcp-utility.md) e um [arquivo de formato XML](../../relational-databases/import-export/xml-format-files-sql-server.md)
No prompt de comando, digite o seguinte comando:
```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.MyFirstImport;"

REM Import data
bcp TestDatabase.dbo.myFirstImport IN D:\BCP\myFirstImport.bcp -f D:\BCP\myFirstImport.xml -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.MyFirstImport;"
```


### <a name="using-bulk-insert-and-non-xml-format-file"></a>Usando [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) e um [arquivo de formato não XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)
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

### <a name="using-bulk-insert-and-xml-format-file"></a>Usando [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) e um [arquivo de formato XML](../../relational-databases/import-export/xml-format-files-sql-server.md)
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

### <a name="using-openrowsetbulk-and-non-xml-format-file"></a>Usando [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) e um [arquivo de formato não XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)    
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

### <a name="using-openrowsetbulk-and-xml-format-file"></a>Usando [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) e um [arquivo de formato XML](../../relational-databases/import-export/xml-format-files-sql-server.md)
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
  
## <a name="more-examples"></a>Mais exemplos
 [Criar um arquivo de formato &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)  
 [Usar um arquivo de formato para ignorar uma coluna de tabela &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
 [Usar um arquivo de formato para ignorar um campo de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
 [Usar um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>Confira também  
 [Utilitário bcp](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Arquivos de formato não XML &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md)   
 [Arquivos de formato XML &#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md)  
  [Arquivos de formato para importação ou exportação de dados (SQL Server)](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)
