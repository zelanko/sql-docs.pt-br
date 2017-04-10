---
title: "Usar um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "09/19/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-bulk-import-export"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "mapeando colunas para campos durante importação [SQL Server]"
  - "arquivos de formato [SQL Server], mapeando colunas para campos"
ms.assetid: e7ee4f7e-24c4-4eb7-84d2-41e57ccc1ef1
caps.latest.revision: 40
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 40
---
# Usar um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados (SQL Server)
Um arquivo de dados pode conter campos organizados em uma ordem diferente das colunas correspondentes na tabela. Este tópico apresenta arquivos de formato não XML e XML que foram modificados para acomodar um arquivo de dados cujos campos são organizados em uma ordem diferente das colunas da tabela. O arquivo de formato modificado mapeia os campos de dados para as colunas da tabela correspondentes.  Examine [Criar um arquivo de formato (SQL Server)](../../relational-databases/import-export/create-a-format-file-sql-server.md) para obter mais informações.

|Contorno|
|---|
|[Condições de teste de exemplo](#etc)<br />&emsp;&#9679;&emsp;[Tabela de exemplo](#sample_table)<br />&emsp;&#9679;&emsp;[Arquivo de dados de exemplo](#sample_data_file)<br />[Criando os arquivos de formato](#create_format_file)<br />&emsp;&#9679;&emsp;[Criando um arquivo de formato não XML](#nonxml_format_file)<br />&emsp;&#9679;&emsp;[Modificando o arquivo de formato não XML](#modify_nonxml_format_file)<br />&emsp;&#9679;&emsp;[Criando um arquivo de formato XML](#xml_format_file)<br />&emsp;&#9679;&emsp;[Modificando o arquivo de formato XML](#modify_xml_format_file)<br />[Importando dados com um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados](#import_data)<br />&emsp;&#9679;&emsp;[Usando o bcp e um arquivo de formato não XML](#bcp_nonxml)<br />&emsp;&#9679;&emsp;[Usando o bcp e um arquivo de formato XML](#bcp_xml)<br />&emsp;&#9679;&emsp;[Usando BULK INSERT e um arquivo de formato não XML](#bulk_nonxml)<br />&emsp;&#9679;&emsp;[Usando BULK INSERT e um arquivo de formato XML](#bulk_xml)<br />&emsp;&#9679;&emsp;[Usando OPENROWSET(BULK...) e um arquivo de formato não XML](#openrowset_nonxml)<br />&emsp;&#9679;&emsp;[Usando OPENROWSET(BULK...) e um arquivo de formato XML](#openrowset_xml)<p>                                                                                                                                                                                                                  </p>|

> [!NOTE]  
>  Um arquivo de formato XML ou não XML pode ser usado para a importação em massa de um arquivo de dados para a tabela usando um comando do [utilitário bcp](../../tools/bcp-utility.md), uma instrução [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) ou INSERT... Instrução SELECT * FROM [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md). Para obter mais informações, veja [Usar um arquivo de formato para importação de dados em massa &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md).  

## Condições de teste de exemplo<a name="etc"></a>  
Os exemplos de arquivos de formato modificados neste tópico baseiam-se na tabela e no arquivo de dados definidos abaixo.

### Tabela de exemplo<a name="sample_table"></a>
O script abaixo cria um banco de dados de teste e uma tabela chamada `myRemap`.  Execute o seguinte script Transact-SQL no Microsoft SSMS (SQL Server Management Studio):
```tsql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE myRemap
   (
   PersonID smallint,
   FirstName varchar(25),
   LastName varchar(30),
   Gender char(1)
   );
```

### Arquivo de dados de exemplo<a name="sample_data_file"></a>
Os dados abaixo apresentam `FirstName` e `LastName` na ordem inversa como apresentados na tabela `myRemap`.  Usando o Bloco de Notas, crie um arquivo vazio `D:\BCP\myRemap.bcp` e insira os seguintes dados:
```
1,Grosse,Anthony,M
2,Fatnowna,Alica,F
3,Rosenhain,Stella,F
```

## Criando os arquivos de formato<a name="create_format_file"></a>
Para importar em massa dados de `myRemap.bcp` para a tabela `myRemap`, o arquivo de formato deverá fazer o seguinte:
* Mapear o primeiro campo de dados para a primeira coluna, `PersonID`.
* Mapear o segundo campo de dados para a terceira coluna, `LastName`.
* Mapear o terceiro campo de dados para a segunda coluna, `FirstName`.
* Mapear o quarto campo de dados para a quarta coluna, `Gender`.

O método mais simples para criar o arquivo de formato é usando o [utilitário bcp](../../tools/bcp-utility.md).  Primeiro, crie um arquivo de formato base da tabela existente.  Em segundo lugar, modifique o arquivo de formato base para refletir o arquivo de dados real.

### Criando um arquivo de formato não XML<a name="nonxml_format_file"></a>
Examine [Arquivos de formato não XML (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) para obter informações detalhadas. O comando a seguir usará o [utilitário bcp](../../tools/bcp-utility.md) para gerar um arquivo de formato não XML, `myRemap.fmt`, com base no esquema de `myRemap`.  Além disso, o qualificador `c` é usado para especificar dados de caractere, `t,` é usado para especificar uma vírgula como um terminador de campo e `T` é usado para especificar uma conexão confiável usando a segurança integrada.  No prompt de comando, digite o seguinte comando:
```
bcp TestDatabase.dbo.myRemap format nul -c -f D:\BCP\myRemap.fmt -t, -T
```
### Modificando o arquivo de formato não XML <a name="modify_nonxml_format_file"></a>
Consulte [Estrutura de arquivos de formato não XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md#Structure) para obter a terminologia.  Abra `D:\BCP\myRemap.fmt` no Bloco de Notas e realize as seguintes modificações:
1) Reorganize a ordem das linhas do arquivo de formato para que as linhas estejam na mesma ordem que os dados do `myRemap.bcp`.
2) Verifique se os valores de ordem do campo do arquivo de host são sequenciais.
3) Verifique se há um retorno de carro após a última linha do arquivo de formato.

Compare as alterações:     
**Antes de**
```
13.0
4
1       SQLCHAR 0       7       ","      1     PersonID               ""
2       SQLCHAR 0       25      ","      2     FirstName              SQL_Latin1_General_CP1_CI_AS
3       SQLCHAR 0       30      ","      3     LastName               SQL_Latin1_General_CP1_CI_AS
4       SQLCHAR 0       1       "\r\n"   4     Gender                 SQL_Latin1_General_CP1_CI_AS

```
**After (após)**
```
13.0
4
1       SQLCHAR 0       7       ","      1     PersonID               ""
2       SQLCHAR 0       30      ","      3     LastName               SQL_Latin1_General_CP1_CI_AS
3       SQLCHAR 0       25      ","      2     FirstName              SQL_Latin1_General_CP1_CI_AS
4       SQLCHAR 0       1       "\r\n"   4     Gender                 SQL_Latin1_General_CP1_CI_AS

```
O arquivo de formato modificado agora reflete:
* O primeiro campo de dados do `myRemap.bcp` é mapeado para a primeira coluna, ` myRemap.. PersonID`
* O segundo campo de dados do `myRemap.bcp` é mapeado para a terceira coluna, `myRemap.. LastName`
* O terceiro campo de dados do `myRemap.bcp` é mapeado para a segunda coluna, `myRemap.. FirstName`
* O quarto campo de dados do `myRemap.bcp` é mapeado para a quarta coluna, ` myRemap.. Gender`

### Criando um arquivo de formato XML <a name="xml_format_file"></a>  
Examine [Arquivos de formato XML (SQL Server)](../../relational-databases/import-export/xml-format-files-sql-server.md) para obter informações detalhadas.  O comando a seguir usará o [utilitário bcp](../../tools/bcp-utility.md) para criar um arquivo de formato XML, `myRemap.xml`, com base no esquema de `myRemap`.  Além disso, o qualificador `c` é usado para especificar dados de caractere, `t,` é usado para especificar uma vírgula como um terminador de campo e `T` é usado para especificar uma conexão confiável usando a segurança integrada.  O qualificador `x` deve ser usado para gerar um arquivo de formato baseado em XML.  No prompt de comando, digite o seguinte comando:
```
bcp TestDatabase.dbo.myRemap format nul -c -x -f D:\BCP\myRemap.xml -t, -T
```
### Modificando o arquivo de formato XML <a name="modify_xml_format_file"></a>
Consulte [Sintaxe de esquema para arquivos de formato XML](../../relational-databases/import-export/xml-format-files-sql-server.md#StructureOfXmlFFs) para obter a terminologia.  Abra `D:\BCP\myRemap.xml` no Bloco de Notas e realize as seguintes modificações:
1) A ordem na qual os elementos \<FIELD> são declarados no formato de arquivo é a ordem na qual os campos são exibidos no arquivo de dados; portanto, inverta a ordem dos elementos \<FIELD> com os atributos de ID 2 e 3.
2) Verifique se os valores do atributo de ID \<FIELD> são sequenciais.
3) A ordem dos elementos <COLUMN\< no elemento <ROW\< define a ordem em que eles são retornados pela operação em massa.  O arquivo de formato XML atribui a cada elemento \<COLUMN> um nome local que não tem nenhuma relação com a coluna da tabela de destino de uma operação de importação em massa.  A ordem dos elementos \<COLUMN> não depende da ordem dos elementos \<FIELD> em uma definição de \<RECORD>.  Cada elemento \<COLUMN> corresponde a um elemento \<FIELD> (cuja ID é especificada no atributo SOURCE do elemento \<COLUMN>).  Portanto, os valores de \<COLUMN> SOURCE são os únicos atributos que exigem revisão.  Inverta a ordem dos atributos 2 e 3 de \<COLUMN> SOURCE.

Comparar as alterações  
**Antes de**
```
<?xml version="1.0"?>
<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <RECORD>
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="30" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="1" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
 </RECORD>
 <ROW>
  <COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>
  <COLUMN SOURCE="2" NAME="FirstName" xsi:type="SQLVARYCHAR"/>
  <COLUMN SOURCE="3" NAME="LastName" xsi:type="SQLVARYCHAR"/>
  <COLUMN SOURCE="4" NAME="Gender" xsi:type="SQLCHAR"/>
 </ROW>
</BCPFORMAT>
```
**After (após)**
```
<?xml version="1.0"?>
<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <RECORD>
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="30" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="1" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
 </RECORD>
 <ROW>
  <COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>
  <COLUMN SOURCE="3" NAME="FirstName" xsi:type="SQLVARYCHAR"/>
  <COLUMN SOURCE="2" NAME="LastName" xsi:type="SQLVARYCHAR"/>
  <COLUMN SOURCE="4" NAME="Gender" xsi:type="SQLCHAR"/>
 </ROW>
</BCPFORMAT>
```
O arquivo de formato modificado agora reflete:
* FIELD 1, que corresponde à COLUMN 1, é mapeado para a primeira coluna da tabela, `myRemap.. PersonID`
* FIELD 2, que corresponde à COLUMN 2, é mapeado novamente para a terceira coluna da tabela, `myRemap.. LastName`
* FIELD 3, que corresponde à COLUMN 3, é mapeado novamente para a segunda coluna da tabela, `myRemap.. FirstName`
* FIELD 4, que corresponde à COLUMN 4, é mapeado para a quarta coluna da tabela, `myRemap.. Gender`


## Importando dados com um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados<a name="import_data"></a>
Os exemplos abaixo usam o banco de dados, o arquivo de dados e os arquivos de formato criados acima.

### Usando o [bcp](../../tools/bcp-utility.md) e um [arquivo de formato não XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)<a name="bcp_nonxml"></a>
No prompt de comando, digite o seguinte comando:
```
bcp TestDatabase.dbo.myRemap IN D:\BCP\myRemap.bcp -f D:\BCP\myRemap.fmt -T
```

### Usando o [bcp](../../tools/bcp-utility.md) e um [arquivo de formato XML](../../relational-databases/import-export/xml-format-files-sql-server.md)<a name="bcp_xml"></a>
No prompt de comando, digite o seguinte comando:
```
bcp TestDatabase.dbo.myRemap IN D:\BCP\myRemap.bcp -f D:\BCP\myRemap.xml -T
```

### Usando [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) e um [arquivo de formato não XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)<a name="bulk_nonxml"></a>
Execute o seguinte script Transact-SQL no Microsoft SSMS (SQL Server Management Studio):
```tsql
USE TestDatabase;  
GO

TRUNCATE TABLE myRemap;
BULK INSERT dbo.myRemap   
   FROM 'D:\BCP\myRemap.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myRemap.fmt');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myRemap;
```

### Usando [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) e um [arquivo de formato XML](../../relational-databases/import-export/xml-format-files-sql-server.md)<a name="bulk_xml"></a>
Execute o seguinte script Transact-SQL no Microsoft SSMS (SQL Server Management Studio):
```tsql
USE TestDatabase;  
GO

TRUNCATE TABLE myRemap;
BULK INSERT dbo.myRemap   
   FROM 'D:\BCP\myRemap.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myRemap.xml');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myRemap;
```

### Usando [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) e um [arquivo de formato não XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)<a name="openrowset_nonxml"></a> 
Execute o seguinte script Transact-SQL no Microsoft SSMS (SQL Server Management Studio):
```tsql
USE TestDatabase;
GO

TRUNCATE TABLE myRemap;
INSERT INTO dbo.myRemap
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myRemap.bcp',
        FORMATFILE = 'D:\BCP\myRemap.fmt'
        ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myRemap;
```

### Usando [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) e um [arquivo de formato XML](../../relational-databases/import-export/xml-format-files-sql-server.md)<a name="openrowset_xml"></a>
Execute o seguinte script Transact-SQL no Microsoft SSMS (SQL Server Management Studio):
```tsql
USE TestDatabase;  
GO

TRUNCATE TABLE myRemap;
INSERT INTO dbo.myRemap 
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myRemap.bcp',
        FORMATFILE = 'D:\BCP\myRemap.xml'  
       ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myRemap;
```


  
## Consulte também  
[Utilitário bcp](../../tools/bcp-utility.md)   
 [Usar um arquivo de formato para ignorar uma coluna de tabela &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)   
 [Usar um arquivo de formato para ignorar um campo de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
  