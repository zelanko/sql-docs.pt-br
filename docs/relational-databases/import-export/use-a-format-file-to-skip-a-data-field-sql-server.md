---
title: Usar um arquivo de formato para ignorar um campo de dados
ms.date: 09/19/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- format files [SQL Server], skipping data fields
- skipping data fields when importing
ms.assetid: 6a76517e-983b-47a1-8f02-661b99859a8b
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: 88d9e3805891c62998afb131ddee7fb202f18b75
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "74056326"
---
# <a name="use-a-format-file-to-skip-a-data-field-sql-server"></a>Usar um arquivo de formato para ignorar um campo de dados (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Um arquivo de dados pode conter mais campos do que o número de colunas na tabela. Este tópico descreve como modificar arquivos de formato XML e não XML para acomodar um arquivo de dados com mais campos, mapeando as colunas de tabela para os campos de dados correspondentes e ignorando os campos extras.  Examine [Criar um arquivo de formato (SQL Server)](../../relational-databases/import-export/create-a-format-file-sql-server.md) para obter mais informações.

|Contorno|
|---|
|[Condições de teste de exemplo](#etc)<br />&emsp;&#9679;&emsp;[Tabela de exemplo](#sample_table)<br />&emsp;&#9679;&emsp;[Arquivo de dados de exemplo](#sample_data_file)<br />[Criando os arquivos de formato](#create_format_file)<br />&emsp;&#9679;&emsp;[Criando um arquivo de formato não XML](#nonxml_format_file)<br />&emsp;&#9679;&emsp;[Modificando um arquivo de formato não XML](#modify_nonxml_format_file)<br />&emsp;&#9679;&emsp;[Criando um arquivo de formato XML](#xml_format_file)<br />&emsp;&#9679;&emsp;[Modificando um arquivo de formato XML](#modify_xml_format_file)<br />[Importando dados com um arquivo de formato para ignorar um campo de dados](#import_data)<br />&emsp;&#9679;&emsp;[Usando bcp e um arquivo de formato não XML](#bcp_nonxml)<br />&emsp;&#9679;&emsp;[Usando bcp e um arquivo de formato XML](#bcp_xml)<br />&emsp;&#9679;&emsp;[Usando BULK INSERT e um arquivo de formato não XML](#bulk_nonxml)<br />&emsp;&#9679;&emsp;[Usando BULK INSERT e um arquivo de formato XML](#bulk_xml)<br />&emsp;&#9679;&emsp;[Usando OPENROWSET(BULK...) e um arquivo de formato não XML](#openrowset_nonxml)<br />&emsp;&#9679;&emsp;[Usando OPENROWSET(BULK...) e um arquivo de formato XML](#openrowset_xml)<p>                                                                                                                                                                                                                  </p>|
  
> [!NOTE]
>  Um arquivo de formato XML ou não XML pode ser usado para a importação em massa de um arquivo de dados para a tabela usando um comando do [utilitário bcp](../../tools/bcp-utility.md), uma instrução [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) ou INSERT... Instrução SELECT * FROM [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md). Para obter mais informações, veja [Usar um arquivo de formato para importação de dados em massa &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md).

## Condições de teste de exemplo<a name="etc"></a>  
Os exemplos de arquivos de formato modificados neste tópico baseiam-se na tabela e no arquivo de dados definidos abaixo.
  
### Tabela de exemplo<a name="sample_table"></a>
O script abaixo cria um banco de dados de teste e uma tabela chamada `myTestSkipField`.  Execute o seguinte script Transact-SQL no Microsoft SSMS (SQL Server Management Studio):
 
```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE myTestSkipField
   (
   PersonID smallint,
   FirstName varchar(25),
   LastName varchar(30)
   );
```
  
### Arquivo de dados de exemplo<a name="sample_data_file"></a>
Crie um arquivo vazio `D:\BCP\myTestSkipField.bcp` e insira os seguintes dados: 
```
1,SkipMe,Anthony,Grosse
2,SkipMe,Alica,Fatnowna
3,SkipMe,Stella,Rosenhain
```
  
## Criando os arquivos de formato<a name="create_format_file"></a>
Para importar em massa dados de `myTestSkipField.bcp` para a tabela `myTestSkipField` , o arquivo de formato deverá fazer o seguinte:
* Mapear o primeiro campo de dados para a primeira coluna, `PersonID`.
* Ignorar o segundo campo de dados.
* Mapear o terceiro campo de dados para a segunda coluna, `FirstName`.
* Mapear o quarto campo de dados para a terceira coluna, `LastName`.  

O método mais simples para criar o arquivo de formato é usando o [utilitário bcp](../../tools/bcp-utility.md).  Primeiro, crie um arquivo de formato base da tabela existente.  Em segundo lugar, modifique o arquivo de formato base para refletir o arquivo de dados real.
  
### <a name="nonxml_format_file"></a>Criando um arquivo de formato não XML 
Examine [Arquivos de formato não XML (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) para obter informações detalhadas. O comando a seguir usará o [utilitário bcp](../../tools/bcp-utility.md) para gerar um arquivo de formato não XML, `myTestSkipField.fmt`, com base no esquema de `myTestSkipField`.  Além disso, o qualificador `c` é usado para especificar dados de caractere, `t,` é usado para especificar uma vírgula como um terminador de campo e `T` é usado para especificar uma conexão confiável usando a segurança integrada.  No prompt de comando, digite o seguinte comando:

```
bcp TestDatabase.dbo.myTestSkipField format nul -c -f D:\BCP\myTestSkipField.fmt -t, -T
```

### Modificando o arquivo de formato não XML <a name="modify_nonxml_format_file"></a>
Consulte [Estrutura de arquivos de formato não XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md#Structure) para obter a terminologia. Abra `D:\BCP\myTestSkipField.fmt` no Bloco de Notas e realize as seguintes modificações:
1) Copie a linha inteira de arquivo de formato em `FirstName` e cole-a diretamente após `FirstName` na próxima linha.
2) Aumente o valor de ordem do campo de arquivo de host em um para a nova linha e todas as próximas linhas.
3) Aumente o valor do número de colunas para que ele reflita o número real de campos no arquivo de dados.
3) Modifique a ordem das colunas do servidor de `2` para `0` na segunda linha do arquivo de formato. 

Compare as alterações feitas:  
**Antes**
```
13.0
3
1       SQLCHAR 0       7       ","      1     PersonID     ""
2       SQLCHAR 0       25      ","      2     FirstName    SQL_Latin1_General_CP1_CI_AS
3       SQLCHAR 0       30      "\r\n"   3     LastName     SQL_Latin1_General_CP1_CI_AS
```
**Depois**
```
13.0
4
1       SQLCHAR 0       7       ","      1     PersonID     ""
2       SQLCHAR 0       25      ","      0     FirstName    SQL_Latin1_General_CP1_CI_AS
3       SQLCHAR 0       25      ","      2     FirstName    SQL_Latin1_General_CP1_CI_AS
4       SQLCHAR 0       50      "\r\n"   3     LastName     SQL_Latin1_General_CP1_CI_AS

```

O arquivo de formato modificado agora reflete:
* 4 campos de dados
* O primeiro campo de dados do `myTestSkipField.bcp` é mapeado para a primeira coluna, `myTestSkipField.. PersonID`
* O segundo campo de dados do `myTestSkipField.bcp` não é mapeado para nenhuma coluna.
* O terceiro campo de dados do `myTestSkipField.bcp` é mapeado para a segunda coluna, `myTestSkipField.. FirstName`
* O quarto campo de dados do `myTestSkipField.bcp` é mapeado para a terceira coluna, `myTestSkipField.. LastName`

### Criando um arquivo de formato XML <a name="xml_format_file"></a>  
Examine [Arquivos de formato XML (SQL Server)](../../relational-databases/import-export/xml-format-files-sql-server.md) para obter informações detalhadas.  O comando a seguir usará o [utilitário bcp](../../tools/bcp-utility.md) para criar um arquivo de formato XML, `myTestSkipField.xml`, com base no esquema de `myTestSkipField`.  Além disso, o qualificador `c` é usado para especificar dados de caractere, `t,` é usado para especificar uma vírgula como um terminador de campo e `T` é usado para especificar uma conexão confiável usando a segurança integrada.  O qualificador `x` deve ser usado para gerar um arquivo de formato baseado em XML.  No prompt de comando, digite o seguinte comando:

```
bcp TestDatabase.dbo.myTestSkipField format nul -c -x -f D:\BCP\myTestSkipField.xml -t, -T
```

### Modificando o arquivo de formato XML <a name="modify_xml_format_file"></a>
Consulte [Sintaxe de esquema para arquivos de formato XML](../../relational-databases/import-export/xml-format-files-sql-server.md#StructureOfXmlFFs) para obter a terminologia.  Abra `D:\BCP\myTestSkipField.xml` no Bloco de Notas e realize as seguintes modificações:
1) Copie todo o segundo campo e cole-o diretamente após o segundo campo na próxima linha.
2) Aumente o valor de “FIELD ID” em 1 para o novo FIELD e para cada campo posterior.
3) Aumente o valor de “COLUMN SOURCE” em 1 para `FirstName`e `LastName` para que eles reflitam o mapeamento revisado.

Compare as alterações feitas:  
**Antes**
```
\<?xml version="1.0"?>
\<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <RECORD>
  \<FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>
  \<FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="3" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="30" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
 </RECORD>
 <ROW>
  \<COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>
  \<COLUMN SOURCE="2" NAME="FirstName" xsi:type="SQLVARYCHAR"/>
  \<COLUMN SOURCE="3" NAME="LastName" xsi:type="SQLVARYCHAR"/>
 </ROW>
</BCPFORMAT>
```

**Depois**
```
\<?xml version="1.0"?>
\<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <RECORD>
  \<FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>
  \<FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="30" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
 </RECORD>
 <ROW>
  \<COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>
  \<COLUMN SOURCE="3" NAME="FirstName" xsi:type="SQLVARYCHAR"/>
  \<COLUMN SOURCE="4" NAME="LastName" xsi:type="SQLVARYCHAR"/>
 </ROW>
</BCPFORMAT>
```

O arquivo de formato modificado agora reflete:
* 4 campos de dados
* FIELD 1, que corresponde à COLUMN 1, é mapeado para a primeira coluna da tabela, `myTestSkipField.. PersonID`
* FIELD 2 não corresponde a nenhuma COLUMN e, portanto, não está mapeado para nenhuma coluna da tabela.
* FIELD 3 que corresponde à COLUMN 3 é mapeado para a segunda coluna da tabela, `myTestSkipField.. FirstName`
* FIELD 4 que corresponde à COLUMN 4 é mapeado para a terceira coluna da tabela, `myTestSkipField.. LastName`

## Importando dados com um arquivo de formato para ignorar um campo de dados<a name="import_data"></a>
Os exemplos abaixo usam o banco de dados, o arquivo de dados e os arquivos de formato criados acima.

### Usando o [bcp](../../tools/bcp-utility.md) e um [arquivo de formato não XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)<a name="bcp_nonxml"></a>
No prompt de comando, digite o seguinte comando:
```
bcp TestDatabase.dbo.myTestSkipField IN D:\BCP\myTestSkipField.bcp -f D:\BCP\myTestSkipField.fmt -T
```

### Usando o [bcp](../../tools/bcp-utility.md) e um [arquivo de formato XML](../../relational-databases/import-export/xml-format-files-sql-server.md)<a name="bcp_xml"></a>
No prompt de comando, digite o seguinte comando:
```
bcp TestDatabase.dbo.myTestSkipField IN D:\BCP\myTestSkipField.bcp -f D:\BCP\myTestSkipField.xml -T
```

### Usando [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) e um [arquivo de formato não XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)<a name="bulk_nonxml"></a>
Execute o seguinte script Transact-SQL no Microsoft SSMS (SQL Server Management Studio):
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myTestSkipField;
BULK INSERT dbo.myTestSkipField   
   FROM 'D:\BCP\myTestSkipField.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myTestSkipField.fmt');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myTestSkipField;
```

### Usando [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) e um [arquivo de formato XML](../../relational-databases/import-export/xml-format-files-sql-server.md)<a name="bulk_xml"></a>
Execute o seguinte script Transact-SQL no Microsoft SSMS (SQL Server Management Studio):
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myTestSkipField;
BULK INSERT dbo.myTestSkipField   
   FROM 'D:\BCP\myTestSkipField.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myTestSkipField.xml');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myTestSkipField;
```

### Usando [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) e um [arquivo de formato não XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)<a name="openrowset_nonxml"></a>    
Execute o seguinte script Transact-SQL no Microsoft SSMS (SQL Server Management Studio):
```sql
USE TestDatabase;
GO

TRUNCATE TABLE myTestSkipField;
INSERT INTO dbo.myTestSkipField
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myTestSkipField.bcp',
        FORMATFILE = 'D:\BCP\myTestSkipField.fmt'
        ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myTestSkipField;
```

### Usando [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) e um [arquivo de formato XML](../../relational-databases/import-export/xml-format-files-sql-server.md)<a name="openrowset_xml"></a>
Execute o seguinte script Transact-SQL no Microsoft SSMS (SQL Server Management Studio):
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myTestSkipField;
INSERT INTO dbo.myTestSkipField 
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myTestSkipField.bcp',
        FORMATFILE = 'D:\BCP\myTestSkipField.xml'  
       ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myTestSkipField;
```

  
## <a name="see-also"></a>Consulte Também  
 [Utilitário bcp](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Usar um arquivo de formato para ignorar uma coluna de tabela &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)   
 [Usar um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
  
