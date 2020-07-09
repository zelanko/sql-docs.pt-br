---
title: Manter valores nulos ou padrão durante a importação em massa
description: Para a importação em massa no SQL Server, o bcp e a instrução BULK INSERT carregam valores padrão para substituir valores nulos. Nos dois, você pode optar por manter valores nulos.
ms.date: 09/20/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], null values
- bulk importing [SQL Server], default values
- data formats [SQL Server], null values
- bulk rowset providers [SQL Server]
- bcp utility [SQL Server], null values
- BULK INSERT statement
- default values
- OPENROWSET function, bulk importing
- data formats [SQL Server], default values
ms.assetid: 6b91d762-337b-4345-a159-88abb3e64a81
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: ca3b994cb831e78807b8aeb44c5fe6f8fc454f41
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86001203"
---
# <a name="keep-nulls-or-default-values-during-bulk-import-sql-server"></a>Manter valores nulos ou padrão durante a importação em massa (SQL Server)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Por padrão, quando os dados são importados para uma tabela, o comando [bcp](../../tools/bcp-utility.md) e a instrução [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) observam os padrões definidos para as colunas na tabela.  Por exemplo, se houver um campo nulo em um arquivo de dados, o valor padrão para a coluna será carregado no campo nulo.  O comando [bcp](../../tools/bcp-utility.md) e a instrução [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) permitem que você especifique a retenção de campos nulos.

Em contraste, uma instrução INSERT regular retém o valor nulo em vez de inserir um valor padrão. A instrução INSERT ... SELECT * FROM [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) fornece o mesmo comportamento básico de INSERT regular, mas, além disso, dá suporte a uma [dica de tabela](../../t-sql/queries/hints-transact-sql-table.md) para inserir os valores padrão.

|Contorno|
|---|
|[Manter valores nulos](#keep_nulls)<br />[Usando valores padrão com INSERT... SELECT * FROM OPENROWSET(BULK...)](#keep_default)<br />[Condições de teste de exemplo](#etc)<br />&emsp;&#9679;&emsp;[Tabela de exemplo](#sample_table)<br />&emsp;&#9679;&emsp;[Arquivo de dados de exemplo](#sample_data_file)<br />&emsp;&#9679;&emsp;[Arquivo de formato não XML de exemplo](#nonxml_format_file)<br />[Manter valores nulos ou use os valores padrão durante a importação em massa](#import_data)<br />&emsp;&#9679;&emsp;[Usando bcp e mantendo valores nulos sem um arquivo de formato](#bcp_null)<br />&emsp;&#9679;&emsp;[Usando bcp e mantendo valores nulos com um arquivo de formato não XML](#bcp_null_fmt)<br />&emsp;&#9679;&emsp;[Usando bcp e valores padrão sem um arquivo de formato](#bcp_default)<br />&emsp;&#9679;&emsp;[Usando bcp e valores padrão com um arquivo de formato não XML](#bcp_default_fmt)<br />&emsp;&#9679;&emsp;[Usando BULK INSERT e mantendo valores nulos sem um arquivo de formato](#bulk_null)<br />&emsp;&#9679;&emsp;[Usando BULK INSERT e mantendo valores nulos com um arquivo de formato não XML](#bulk_null_fmt)<br />&emsp;&#9679;&emsp;[Usando BULK INSERT e valores padrão sem um arquivo de formato](#bulk_default)<br />&emsp;&#9679;&emsp;[Usando BULK INSERT e valores padrão com um arquivo de formato não XML](#bulk_default_fmt)<br />&emsp;&#9679;&emsp;[Usando OPENROWSET(BULK...) e mantendo valores nulos com um arquivo de formato não XML](#openrowset__null_fmt)<br />&emsp;&#9679;&emsp;[Usando OPENROWSET(BULK...) e valores padrão com um arquivo de formato não XML](#openrowset__default_fmt)

## <a name="keeping-null-values"></a>Manter valores nulos<a name="keep_nulls"></a>  
Os qualificadores a seguir especificam que um campo vazio no arquivo de dados retém seu valor nulo durante a operação de importação em massa, em vez de herdar um valor padrão (se houver) para as colunas de tabela.  Para [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md), por padrão, toda coluna não especificada na operação de carregamento em massa é definida como NULL.
  
|Comando|Qualificador|Tipo de qualificador|  
|-------------|---------------|--------------------|  
|bcp|-k|Opção|  
|BULK INSERT|KEEPNULLS\*|Argumento|  
|INSERT ... SELECT * FROM OPENROWSET(BULK...)|N/D|N/D|  
  
\* Para [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md), se os valores padrão não estiverem disponíveis, a coluna de tabela deverá ser definida para permitir valores nulos. 
  
> [!NOTE]
> Esses qualificadores desabilitam a verificação de definições DEFAULT em uma tabela por esses comandos de importação em massa.  No entanto, para qualquer instrução INSERT simultânea, são previstas definições DEFAULT.
 
## <a name="using-default-values-with-insert--select--from-openrowsetbulk"></a>Usar valores padrão com INSERT... SELECT * FROM [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md)<a name="keep_default"></a>  
Você pode especificar que para um campo vazio no arquivo de dados, a coluna de tabela correspondente use seu valor padrão (se houver).  Para usar valores padrão, use a dica de tabela [KEEPDEFAULTS](../../t-sql/queries/hints-transact-sql-table.md).
 
> [!NOTE]
>  Para obter mais informações, veja [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md), [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md), [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md) e [Dicas de tabela &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)

## <a name="example-test-conditions"></a>Condições de teste de exemplo<a name="etc"></a>  
Os exemplos neste tópico baseiam-se na tabela, no arquivo de dados e no arquivo de formato definidos abaixo.

### <a name="sample-table"></a>**Tabela de exemplo**<a name="sample_table"></a>
O script abaixo cria um banco de dados de teste e uma tabela chamada `myNulls`.  Observe que a quarta coluna de tabela, `Kids`, tem um valor padrão.  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):

```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.myNulls ( 
   PersonID smallint not null,
   FirstName varchar(25),
   LastName varchar(30),
   Kids varchar(13) DEFAULT 'Default Value',
   BirthDate date
   );
```

### <a name="sample-data-file"></a>**Arquivo de dados de exemplo**<a name="sample_data_file"></a>
Usando o Bloco de Notas, crie um arquivo vazio `D:\BCP\myNulls.bcp` e insira os dados abaixo.  Observe que não há nenhum valor no terceiro registro, na quarta coluna.

```
1,Anthony,Grosse,Yes,1980-02-23
2,Alica,Fatnowna,No,1963-11-14
3,Stella,Rosenhain,,1992-03-02
```

Como alternativa, você pode executar o seguinte script do PowerShell para criar e preencher o arquivo de dados:

```powershell
cls
# revise directory as desired
$dir = 'D:\BCP\';

$bcpFile = $dir + 'MyNulls.bcp';

# Confirm directory exists
IF ((Test-Path -Path $dir) -eq 0)
{
    Write-Host "The path $dir does not exist; please create or modify the directory.";
    RETURN;
};

# clear content, will error if file does not exist, can be ignored
Clear-Content -Path $bcpFile -ErrorAction SilentlyContinue;

# Add data
Add-Content -Path $bcpFile -Value '1,Anthony,Grosse,Yes,1980-02-23';
Add-Content -Path $bcpFile -Value '2,Alica,Fatnowna,No,1963-11-14';
Add-Content -Path $bcpFile -Value '3,Stella,Rosenhain,,1992-03-02';

#Review content
Get-Content -Path $bcpFile;
Invoke-Item $bcpFile;
```
  
### <a name="sample-non-xml-format-file"></a>**Exemplo de arquivo de formato não XML**<a name="nonxml_format_file"></a>
O SQL Server dá suporte a dois tipos de arquivo de formato: XML e não XML.  O formato não XML é o formato original com suporte em versões anteriores do SQL Server.  Examine [Arquivos de formato não XML (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) para obter informações detalhadas.  O comando a seguir usará o [utilitário bcp](../../tools/bcp-utility.md) para gerar um arquivo de formato não XML, `myNulls.fmt`, com base no esquema de `myNulls`.  Para usar um comando [bcp](../../tools/bcp-utility.md) para criar um arquivo de formato, especifique o argumento **format** e use **nul** em vez de um caminho de arquivo de dados.  A opção format também exige a opção **-f** .  Além disso, neste exemplo, o qualificador **c** é usado para especificar dados de caractere, **t** é usado para especificar uma vírgula como um [terminador de campo](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)e **T** é usado para especificar uma conexão confiável usando a segurança integrada.  No prompt de comando, digite o seguinte comando:

```cmd
bcp TestDatabase.dbo.myNulls format nul -c -f D:\BCP\myNulls.fmt -t, -T

REM Review file
Notepad D:\BCP\myNulls.fmt
```

> [!IMPORTANT]
> Verifique se o arquivo de formato não XML termina com um retorno de carro/alimentação de linha.  Caso contrário, você provavelmente receberá a seguinte mensagem de erro:
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`

 Para obter mais informações sobre como criar arquivos de formato, veja [Criar um arquivo de formato &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md).  
  
## <a name="keep-nulls-or-use-default-values-during-bulk-import"></a>Manter valores nulos ou use os valores padrão durante a importação em massa<a name="import_data"></a>
Os exemplos abaixo usam o banco de dados, o arquivo de dados e os arquivos de formato criados acima.

### <a name="using-bcp-and-keeping-null-values-without-a-format-file"></a>**Como usar [bcp](../../tools/bcp-utility.md) e manter valores nulos sem um arquivo de formato**<a name="bcp_null"></a>

Opção **-k** .  No prompt de comando, digite o seguinte comando:

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myNulls;"

REM Import data
bcp TestDatabase.dbo.myNulls IN D:\BCP\myNulls.bcp -c -t, -T -k

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myNulls;"
```
  
### <a name="using-bcp-and-keeping-null-values-with-a-non-xml-format-file"></a>**Como usar [bcp](../../tools/bcp-utility.md) e manter valores nulos com um [arquivo de formato não XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)** <a name="bcp_null_fmt"></a>
Opções **-k** e **-f** . No prompt de comando, digite o seguinte comando:

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myNulls;"

REM Import data
bcp TestDatabase.dbo.myNulls IN D:\BCP\myNulls.bcp -f D:\BCP\myNulls.fmt -T -k

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myNulls;"
```

### <a name="using-bcp-and-using-default-values-without-a-format-file"></a>**Como usar [bcp](../../tools/bcp-utility.md) e valores padrão sem um arquivo de formato**<a name="bcp_default"></a>
No prompt de comando, digite o seguinte comando:

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myNulls;"

REM Import data
bcp TestDatabase.dbo.myNulls IN D:\BCP\myNulls.bcp -c -t, -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myNulls;"
```
  
### <a name="using-bcp-and-using-default-values-with-a-non-xml-format-file"></a>**Como usar [bcp](../../tools/bcp-utility.md) e valores padrão com um [arquivo de formato não XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)** <a name="bcp_default_fmt"></a>
Opção **-f** .  No prompt de comando, digite o seguinte comando:

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myNulls;"

REM Import data
bcp TestDatabase.dbo.myNulls IN D:\BCP\myNulls.bcp -f D:\BCP\myNulls.fmt -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myNulls;"
```

### <a name="using-bulk-insert-and-keeping-null-values-without-a-format-file"></a>**Como usar [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) e manter valores nulos sem um arquivo de formato**<a name="bulk_null"></a>
Argumento**KEEPNULLS** .  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):

```sql
USE TestDatabase;
GO
TRUNCATE TABLE dbo.myNulls; -- for testing
BULK INSERT dbo.myNulls
    FROM 'D:\BCP\myNulls.bcp'
    WITH (
        DATAFILETYPE = 'char',  
        FIELDTERMINATOR = ',',  
        KEEPNULLS
        );

-- review results
SELECT * FROM TestDatabase.dbo.myNulls;
```

### <a name="using-bulk-insert-and-keeping-null-values-with-a-non-xml-format-file"></a>**Como usar [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) e manter valores nulos com um [arquivo de formato não XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)** <a name="bulk_null_fmt"></a>
**KEEPNULLS** e o argumento **FORMATFILE** .  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):

```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myNulls; -- for testing
BULK INSERT dbo.myNulls
   FROM 'D:\BCP\myNulls.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myNulls.fmt',
        KEEPNULLS
        );

-- review results
SELECT * FROM TestDatabase.dbo.myNulls;
```

### <a name="using-bulk-insert-and-using-default-values-without-a-format-file"></a>**Como usar [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) e valores padrão sem um arquivo de formato**<a name="bulk_default"></a>
Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):

```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myNulls;  -- for testing
BULK INSERT dbo.myNulls
   FROM 'D:\BCP\myNulls.bcp'
   WITH (
      DATAFILETYPE = 'char',  
      FIELDTERMINATOR = ','
      );

-- review results
SELECT * FROM TestDatabase.dbo.myNulls;
```

### <a name="using-bulk-insert-and-using-default-values-with-a-non-xml-format-file"></a>**Como usar [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) e valores padrão com um [arquivo de formato não XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)** <a name="bulk_default_fmt"></a>
Argumento**FORMATFILE** .  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):

```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myNulls;  -- for testing
BULK INSERT dbo.myNulls
   FROM 'D:\BCP\myNulls.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myNulls.fmt'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myNulls;
```

### <a name="using-openrowsetbulk-and-keeping-null-values-with-a-non-xml-format-file"></a>**Como usar [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) e manter valores nulos com um [arquivo de formato não XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)** <a name="openrowset__null_fmt"></a>
Argumento**FORMATFILE** .  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):

```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myNulls;  -- for testing
INSERT INTO dbo.myNulls
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myNulls.bcp', 
        FORMATFILE = 'D:\BCP\myNulls.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myNulls;
```

### <a name="using-openrowsetbulk-and-using-default-values-with-a-non-xml-format-file"></a>**Como usar [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) e valores padrão com um [arquivo de formato não XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)** <a name="openrowset__default_fmt"></a>
Dica de tabela**KEEPDEFAULTS** e argumento **FORMATFILE** .  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):

```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myNulls;  -- for testing
INSERT INTO dbo.myNulls
WITH (KEEPDEFAULTS) 
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myNulls.bcp', 
        FORMATFILE = 'D:\BCP\myNulls.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myNulls;
```

  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Manter valores de identidade ao importar dados em massa &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
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
  
-   [Especificar terminadores de campo e linha &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)  
  
-   [Especificar o tamanho de prefixo em arquivos de dados usando bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
-   [Especificar tipo de armazenamento de arquivo usando bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Utilitário bcp](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [Dicas de tabela &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)  
  
  
