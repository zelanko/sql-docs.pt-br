---
title: Manter valores de identidade ao importar dados em massa (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 09/21/2016
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
- identity values [SQL Server], bulk imports
- data formats [SQL Server], identity values
- bulk importing [SQL Server], identity values
ms.assetid: 45894a3f-2d8a-4edd-9568-afa7d0d3061f
caps.latest.revision: "22"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 483471ce594ba3ae2c2b731e197290d2059af049
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="keep-identity-values-when-bulk-importing-data-sql-server"></a>Manter valores de identidade ao importar dados em massa (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Os dados de arquivo que contêm valores de identidade podem ser importados em massa para uma instância do Microsoft SQL Server.  Por padrão, os valores da coluna de identidade do arquivo de dados que é importado são ignorados e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atribui valores exclusivos automaticamente.  Os valores exclusivos são baseados nos valores de semente e incremento que são especificados durante a criação da tabela.

Se o arquivo de dados não contiver valores para a coluna de identificador na tabela, use um arquivo de formato para especificar que a coluna de identificador na tabela deve ser ignorada durante a importação dos dados.  Consulte [Usar um arquivo de formato para ignorar uma coluna de tabela (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md) para obter mais informações.

|Contorno|
|---|
|[Manter valores de identidade](#keep_identity)<br />[Condições de teste de exemplo](#etc)<br />&emsp;&#9679;&emsp;[Tabela de exemplo](#sample_table)<br />&emsp;&#9679;&emsp;[Arquivo de dados de exemplo](#sample_data_file)<br />&emsp;&#9679;&emsp;[Arquivo de formato não XML de exemplo](#nonxml_format_file)<br />[Exemplos](#examples)<br />&emsp;&#9679;&emsp;[Usando bcp e mantendo valores de identidade sem um arquivo de formato](#bcp_identity)<br />&emsp;&#9679;&emsp;[Usando bcp e mantendo valores de identidade com um arquivo de formato não XML](#bcp_identity_fmt)<br />&emsp;&#9679;&emsp;[Usando bcp e valores de identidade gerados sem um arquivo de formato](#bcp_default)<br />&emsp;&#9679;&emsp;[Usando bcp e valores de identidade gerados com um arquivo de formato não XML](#bcp_default_fmt)<br />&emsp;&#9679;&emsp;[Usando BULK INSERT e mantendo valores de identidade sem um arquivo de formato](#bulk_identity)<br />&emsp;&#9679;&emsp;[Usando BULK INSERT e mantendo valores de identidade com um arquivo de formato não XML](#bulk_identity_fmt)<br />&emsp;&#9679;&emsp;[Usando BULK INSERT e valores de identidade gerados sem um arquivo de formato](#bulk_default)<br />&emsp;&#9679;&emsp;[Usando BULK INSERT e valores de identidade gerados com um arquivo de formato não XML](#bulk_default_fmt)<br />&emsp;&#9679;&emsp;[Usando OPENROWSET e mantendo valores de identidade com um arquivo de formato não XML](#openrowset_identity_fmt)<br />&emsp;&#9679;&emsp;[Usando OPENROWSET e valores de identidade gerados com um arquivo de formato não XML](#openrowset_default_fmt)<br /><p>                                                                                                                                                                                                                  </p>|

## Manter valores de identidade <a name="keep_identity"></a>  
Para impedir [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a atribuição de valores de identidade durante a importação em massa de linhas de dados, use o qualificador de comando manter identidade apropriado.  Quando você especificar um qualificador de manter identidade, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa os valores de identidade no arquivo de dados.  Estes qualificadores são os seguintes:

|Comando|Qualificador manter identidade|Tipo de qualificador|  
|-------------|------------------------------|--------------------|  
|bcp|-E|Opção|  
|BULK INSERT|KEEPIDENTITY|Argumento|  
|INSERT ... SELECT * FROM OPENROWSET(BULK...)|KEEPIDENTITY|Dica de tabela|  
   
 Para obter mais informações, consulte [Utilitário bcp](../../tools/bcp-utility.md), [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md), [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md), [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md), [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md) e [Dicas de tabela &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  

> [!NOTE]
>  Para criar um número incrementado automaticamente, que possa ser usado em várias tabelas ou ser chamado de aplicativos, sem referenciar tabelas, consulte [Números de Sequência](../../relational-databases/sequence-numbers/sequence-numbers.md).
 
## Condições de teste de exemplo<a name="etc"></a>  
Os exemplos neste tópico baseiam-se na tabela, no arquivo de dados e no arquivo de formato definidos abaixo.

### **Tabela de exemplo**<a name="sample_table"></a>
O script abaixo cria um banco de dados de teste e uma tabela chamada `myIdentity`.  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.myIdentity ( 
   PersonID smallint IDENTITY(1,1) NOT NULL,
   FirstName varchar(25) NOT NULL,
   LastName varchar(30) NOT NULL,
   BirthDate date
   );
```
 
### **Arquivo de Dados de Exemplo**<a name="sample_data_file"></a>
Usando o Bloco de Notas, crie um arquivo vazio `D:\BCP\myIdentity.bcp` e insira os dados abaixo.  
```
3,Anthony,Grosse,1980-02-23
2,Alica,Fatnowna,1963-11-14
1,Stella,Rosenhain,1992-03-02
4,Miller,Dylan,1954-01-05
```
  
Como alternativa, você pode executar o seguinte script do PowerShell para criar e preencher o arquivo de dados:
```powershell
cls
# revise directory as desired
$dir = 'D:\BCP\';

$bcpFile = $dir + 'myIdentity.bcp';

# Confirm directory exists
IF ((Test-Path -Path $dir) -eq 0)
{
    Write-Host "The path $dir does not exist; please create or modify the directory.";
    RETURN;
};

# clear content, will error if file does not exist, can be ignored
Clear-Content -Path $bcpFile -ErrorAction SilentlyContinue;

# Add data
Add-Content -Path $bcpFile -Value '3,Anthony,Grosse,1980-02-23';
Add-Content -Path $bcpFile -Value '2,Alica,Fatnowna,1963-11-14';
Add-Content -Path $bcpFile -Value '1,Stella,Rosenhain,1992-03-02';
Add-Content -Path $bcpFile -Value '4,Miller,Dylan,1954-01-05';

#Review content
Get-Content -Path $bcpFile;
Invoke-Item $bcpFile;
```

### **Exemplo de arquivo de formato não XML**<a name="nonxml_format_file"></a>
O SQL Server dá suporte a dois tipos de arquivo de formato: XML e não XML.  O formato não XML é o formato original com suporte em versões anteriores do SQL Server.  Examine [Arquivos de formato não XML (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) para obter informações detalhadas.  O comando a seguir usará o [utilitário bcp](../../tools/bcp-utility.md) para gerar um arquivo de formato não XML, `myIdentity.fmt`, com base no esquema de `myIdentity`.  Para usar um comando [bcp](../../tools/bcp-utility.md) para criar um arquivo de formato, especifique o argumento **format** e use **nul** em vez de um caminho de arquivo de dados.  A opção format também exige a opção **-f** .  Além disso, neste exemplo, o qualificador **c** é usado para especificar dados de caractere, **t** é usado para especificar uma vírgula como um [terminador de campo](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)e **T** é usado para especificar uma conexão confiável usando a segurança integrada.  No prompt de comando, digite o seguinte comando:
  
```
bcp TestDatabase.dbo.myIdentity format nul -c -f D:\BCP\myIdentity.fmt -t, -T

REM Review file
Notepad D:\BCP\myIdentity.fmt
```
 
> [!IMPORTANT]
> Verifique se o arquivo de formato não XML termina com um retorno de carro/alimentação de linha.  Caso contrário, você provavelmente receberá a seguinte mensagem de erro:
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`

## Exemplos<a name="examples"></a>
Os exemplos abaixo usam o banco de dados, o arquivo de dados e os arquivos de formato criados acima.
  
### **Como usar [bcp](../../tools/bcp-utility.md) e manter valores de identidade sem um arquivo de formato**<a name="bcp_identity"></a>
Opção**-E** .  No prompt de comando, digite o seguinte comando:
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myIdentity;"

REM Import data
bcp TestDatabase.dbo.myIdentity IN D:\BCP\myIdentity.bcp -T -c -t, -E

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myIdentity;"
```

### **Como usar [bcp](../../tools/bcp-utility.md) e manter valores de identidade com um [arquivo de formato não XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bcp_identity_fmt"></a>
Opções**-E** e **-f** .  No prompt de comando, digite o seguinte comando:
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myIdentity;"

REM Import data
bcp TestDatabase.dbo.myIdentity IN D:\BCP\myIdentity.bcp -f D:\BCP\myIdentity.fmt -T -E

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myIdentity;"
```
 
### **Como usar [bcp](../../tools/bcp-utility.md) e valores de identidade gerados sem um arquivo de formato**<a name="bcp_default"></a>
Usando padrões.  No prompt de comando, digite o seguinte comando:
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myIdentity;"

REM Import data
bcp TestDatabase.dbo.myIdentity IN D:\BCP\myIdentity.bcp -T -c -t,

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myIdentity;"
```
  
### **Como usar [bcp](../../tools/bcp-utility.md) e valores de identidade gerados com um [arquivo de formato não XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bcp_default_fmt"></a>
Usando padrões e a opção **-f** .  No prompt de comando, digite o seguinte comando:
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myIdentity;"

REM Import data
bcp TestDatabase.dbo.myIdentity IN D:\BCP\myIdentity.bcp -f D:\BCP\myIdentity.fmt -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myIdentity;"
```
  
### **Como usar [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) e manter valores de identidade sem um arquivo de formato**<a name="bulk_identity"></a>
Argumento**KEEPIDENTITY** .  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myIdentity; -- for testing
BULK INSERT dbo.myIdentity
    FROM 'D:\BCP\myIdentity.bcp'
    WITH (
        DATAFILETYPE = 'char',  
        FIELDTERMINATOR = ',',  
        KEEPIDENTITY
        );

-- review results
SELECT * FROM TestDatabase.dbo.myIdentity;
```
  
### **Como usar [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) e manter valores de identidade com um [arquivo de formato não XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bulk_identity_fmt"></a>
**KEEPIDENTITY** e o argumento **FORMATFILE** .  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myIdentity; -- for testing
BULK INSERT dbo.myIdentity
   FROM 'D:\BCP\myIdentity.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myIdentity.fmt',
        KEEPIDENTITY
        );

-- review results
SELECT * FROM TestDatabase.dbo.myIdentity;
```
  
### **Como usar [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) e valores de identidade gerados sem um arquivo de formato**<a name="bulk_default"></a>
Usando padrões.  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myIdentity;  -- for testing
BULK INSERT dbo.myIdentity
   FROM 'D:\BCP\myIdentity.bcp'
   WITH (
      DATAFILETYPE = 'char',  
      FIELDTERMINATOR = ','
      );

-- review results
SELECT * FROM TestDatabase.dbo.myIdentity;
```
  
### **Como usar [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) e valores de identidade gerados com um [arquivo de formato não XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bulk_default_fmt"></a>
Usando os padrões e o argumento **FORMATFILE** .  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myIdentity;  -- for testing
BULK INSERT dbo.myIdentity
   FROM 'D:\BCP\myIdentity.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myIdentity.fmt'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myIdentity;
```
  
### **Como usar [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) e manter valores de identidade com um [arquivo de formato não XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="openrowset_identity_fmt"></a>
Dica de tabela**KEEPIDENTITY** e argumento **FORMATFILE** .  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myIdentity;  -- for testing
INSERT INTO dbo.myIdentity
WITH (KEEPIDENTITY) 
(PersonID, FirstName, LastName, BirthDate)
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myIdentity.bcp', 
        FORMATFILE = 'D:\BCP\myIdentity.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myIdentity;
```
 
### **Como usar [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) e valores de identidade gerados com um [arquivo de formato não XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="openrowset_default_fmt"></a>
Usando os padrões e o argumento **FORMATFILE** .  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myIdentity;  -- for testing
INSERT INTO dbo.myIdentity
(FirstName, LastName, BirthDate)
    SELECT FirstName, LastName, BirthDate
    FROM OPENROWSET (
        BULK 'D:\BCP\myIdentity.bcp', 
        FORMATFILE = 'D:\BCP\myIdentity.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myIdentity;
```
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Manter valores nulos ou use os valores padrão durante a importação em massa &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [Preparar dados para exportar ou importar em massa &#40;SQL Server&#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)  
  
 **Para usar um arquivo de formato**  
  
-   [Criar um arquivo de formato &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)  
  
-   [Usar um arquivo de formato para importação em massa de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Usar um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
-   [Usar um arquivo de formato para ignorar um campo de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [Usar um arquivo de formato para ignorar uma coluna de tabela &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
 **Para usar formatos de dados para importação ou exportação em massa**  
  
-   [Importar dados de formato de caractere e nativo de versões anteriores do SQL Server](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Usar o formato de caractere para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato de caractere Unicode para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo Unicode para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
 **Para especificar formatos de dados para compatibilidade usando bcp**  
  
1.  [Especificar terminadores de campo e linha &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)  
  
2.  [Especificar o tamanho de prefixo em arquivos de dados usando bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
3.  [Especificar tipo de armazenamento de arquivo usando bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Utilitário bcp](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Dicas de tabela &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)  
[Arquivos de formato para importação ou exportação de dados (SQL Server)](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)  
  
