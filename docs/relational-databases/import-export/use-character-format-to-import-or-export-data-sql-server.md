---
title: Usar o formato de caractere para importar ou exportar dados (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 09/29/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data formats [SQL Server], character
- character formats [SQL Server]
ms.assetid: d925e66a-1a73-43cd-bc06-1cbdf8174a4d
caps.latest.revision: "42"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: d5dd9155a7cc669a5f7a62036bb42410dced9c48
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="use-character-format-to-import-or-export-data-sql-server"></a>Usar o formato de caractere para importar ou exportar dados (SQL Server)
Formato de caractere é recomendado quando você exporta dados em massa para um arquivo de texto que será usado em outro programa ou quando você importa dados em massa de um arquivo de texto que é gerado por outro programa.  

Formato de caractere usa o formato de dados de caractere para todas as colunas. Armazenar informações em formato de caractere é útil quando os dados são usados com outro programa, como uma planilha, ou quando os dados precisam ser copiados em uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de outro fornecedor de banco de dados como Oracle.  
  
> [!NOTE]
>  Quando você transfere dados em massa entre instâncias do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o arquivo de dados contém dados de caractere Unicode mas não caracteres estendidos ou DBCS, use o formato de caractere Unicode. Para obter mais informações, consulte [Usar o formato de caractere Unicode para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md).
  
|Neste tópico:|
|---|
|[Considerações sobre usar o formato de caractere](#considerations)|
|[Opções de comando para formato de caractere](#command_options)|
|[Condições de teste de exemplo](#etc)<br />&emsp;&#9679;&emsp;[Tabela de exemplo](#sample_table)<br />&emsp;&#9679;&emsp;[Arquivo de formato não XML de exemplo](#nonxml_format_file)<br />|
|[Exemplos](#examples)<br />&emsp;&#9679;&emsp;[Usando bcp e formato de caractere para exportar dados](#bcp_char_export)<br />&emsp;&#9679;&emsp;[Usando bcp e formato de caractere para importar dados sem um arquivo de formato](#bcp_char_import)<br />&emsp;&#9679;&emsp;[Usando bcp e formato de caractere para importar dados com um arquivo de formato não XML](#bcp_char_import_fmt)<br />&emsp;&#9679;&emsp;[Usando BULK INSERT e formato de caractere sem um arquivo de formato](#bulk_char)<br />&emsp;&#9679;&emsp;[Usando BULK INSERT e formato de caractere com um arquivo de formato não XML](#bulk_char_fmt)<br />&emsp;&#9679;&emsp;[Usando OPENROWSET e formato de caractere com um arquivo de formato não XML](#openrowset_char_fmt)|
|[Tarefas relacionadas](#RelatedTasks)<p>                                                                                                                                                                                                                  </p>|


  
## Considerações sobre usar o formato de caractere<a name="considerations"></a>
Ao usar formato de caractere, considere o seguinte:  
  
-   Por padrão, o [utilitário bcp](../../tools/bcp-utility.md) separa os campos dos dados de caractere com o caractere de guia e termina os registros com o caractere de nova linha.  Para obter informações sobre como especificar terminadores alternativos, consulte [Especificar terminadores de campo e linha &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).  
  
-   Por padrão, antes da exportação ou importação em massa de dados do modo de caractere, são executadas as conversões seguintes:  
  
    |Direção da operação em massa|Conversão|  
    |---------------------------------|----------------|  
    |Exportar|Converte dados para representação de caractere. Se solicitado explicitamente, os dados são convertidos à página de código solicitada para colunas de caractere. Se nenhuma página de código for especificada, os dados de caractere serão convertidos usando a página de código OEM do computador do cliente.|  
    |Importar|Converte dados de caractere em representação nativa e traduz os dados de caractere da página de código do cliente para a página de código da(s) coluna(s) de destino, quando necessário.|  
  
-   Para evitar a perda de caracteres estendidos durante conversão, use formato de caractere Unicode ou especifique uma página de código.  
  
-   São armazenados quaisquer dados [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) em um arquivo do formato de caractere sem metadados. Cada valor de dados é convertido ao formato [char](../../t-sql/data-types/char-and-varchar-transact-sql.md) , de acordo com as regras de conversão de dados implícita. Quando importado em uma coluna [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) , os dados são importados como [char](../../t-sql/data-types/char-and-varchar-transact-sql.md). Quando importado em uma coluna com um tipo de dados diferente de [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md), os dados são convertidos de [char](../../t-sql/data-types/char-and-varchar-transact-sql.md) usando conversão implícita. Para obter mais informações sobre conversão de dados, consulte [Conversão de tipo de dados &#40;Mecanismo do Banco de Dados &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md).  
  
-   O [utilitário bcp](../../tools/bcp-utility.md) exporta valores [money](../../t-sql/data-types/money-and-smallmoney-transact-sql.md) como arquivos de dados do formato de caractere com quatro dígitos depois do ponto decimal e sem qualquer símbolo de agrupamento de dígito como separadores de vírgula. Por exemplo, uma coluna [money](../../t-sql/data-types/money-and-smallmoney-transact-sql.md) que contém o valor 1,234,567.123456 é exportada em massa para um arquivo de dados como a cadeia de caracteres 1234567.1235.  
  
## Opções de comando para formato de caractere<a name="command_options"></a>  
Você pode importar dados de formato de caractere em uma tabela que usa [bcp](../../tools/bcp-utility.md), [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) ou [INSERT... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md). Para um comando [bcp](../../tools/bcp-utility.md) ou uma instrução [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md), você pode especificar o formato de dados na instrução.  Para uma instrução [INSERT... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md), é necessário especificar o formato dos dados em um arquivo de formato.  
  
Formato de caractere tem suporte nas seguintes opções de comando:  
  
|Comando|Opção|Descrição|  
|-------------|------------|-----------------|  
|bcp|**-c**|Faz com que o utilitário bcp use os dados de caractere.*|  
|BULK INSERT|DATAFILETYPE **='char'**|Use o formato de caractere quando na importação em massa de dados.|  
|OPENROWSET|N/A|Deve usar um arquivo de formato|
  
 \*Para carregar dados de caractere (**-c**) em um formato compatível com versões anteriores de clientes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , use a opção **-V** . Para obter mais informações, consulte [Importar dados de formato de caractere e nativo de versões anteriores do SQL Server](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md).  
   
> [!NOTE]
>  Como alternativa, você pode especificar a formatação por campo, em um arquivo de formato. Para obter mais informações, consulte [Arquivos de formato para importação ou exportação de dados &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).

## Condições de teste de exemplo<a name="etc"></a>  
Os exemplos neste tópico baseiam-se na tabela e no arquivo de formato definidos abaixo.

### **Tabela de exemplo**<a name="sample_table"></a>
O script a seguir cria um banco de dados de teste, uma tabela chamada de `myChar` e preenche a tabela com alguns valores iniciais.  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):

```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.myChar ( 
   PersonID smallint NOT NULL,
   FirstName varchar(25) NOT NULL,
   LastName varchar(30) NOT NULL,
   BirthDate date,
   AnnualSalary money
   );

-- Populate table
INSERT TestDatabase.dbo.myChar
VALUES 
(1, 'Anthony', 'Grosse', '1980-02-23', 65000.00),
(2, 'Alica', 'Fatnowna', '1963-11-14', 45000.00),
(3, 'Stella', 'Rossenhain', '1992-03-02', 120000.00);

-- Review Data
SELECT * FROM TestDatabase.dbo.myChar;
```

### **Exemplo de arquivo de formato não XML**<a name="nonxml_format_file"></a>
O SQL Server dá suporte a dois tipos de arquivo de formato: XML e não XML.  O formato não XML é o formato original com suporte em versões anteriores do SQL Server.  Examine [Arquivos de formato não XML (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) para obter informações detalhadas.  O comando a seguir usará o [utilitário bcp](../../tools/bcp-utility.md) para gerar um arquivo de formato não XML, `myChar.fmt`, com base no esquema de `myChar`.  Para usar um comando [bcp](../../tools/bcp-utility.md) para criar um arquivo de formato, especifique o argumento **format** e use **nul** em vez de um caminho de arquivo de dados.  A opção format também exige a opção **-f** .  Além disso, neste exemplo, o qualificador **c** é usado para especificar dados de caractere, e **T** é usado para especificar uma conexão confiável usando a segurança integrada.  No prompt de comando, digite o seguinte comando:

```cmd
bcp TestDatabase.dbo.myChar format nul -f D:\BCP\myChar.fmt -T -c 

REM Review file
Notepad D:\BCP\myChar.fmt
```

> [!IMPORTANT]
> Verifique se o arquivo de formato não XML termina com um retorno de carro/alimentação de linha.  Caso contrário, você provavelmente receberá a seguinte mensagem de erro:
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`

## Exemplos<a name="examples"></a>
Os exemplos abaixo usam o banco de dados e os arquivos de formato criados acima.

### **Usando bcp e formato de caractere para exportar dados**<a name="bcp_char_export"></a>
Opção**-c** e comando **OUT** .  Observação: o arquivo de dados criado neste exemplo será usado em todos os exemplos subsequentes.  No prompt de comando, digite o seguinte comando:

```cmd
bcp TestDatabase.dbo.myChar OUT D:\BCP\myChar.bcp -T -c

REM Review results
NOTEPAD D:\BCP\myChar.bcp
```

### **Usando bcp e formato de caractere para importar dados sem um arquivo de formato**<a name="bcp_char_import"></a>
Opção**-c** e comando **IN** .  No prompt de comando, digite o seguinte comando:

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myChar;"

REM Import data
bcp TestDatabase.dbo.myChar IN D:\BCP\myChar.bcp -T -c

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myChar;"
```

### **Usando bcp e formato de caractere para importar dados com um arquivo de formato não XML**<a name="bcp_char_import_fmt"></a>
Opções**-c** e **-f** switches e **IN** comme.  No prompt de comando, digite o seguinte comando:

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myChar;"

REM Import data
bcp TestDatabase.dbo.myChar IN D:\BCP\myChar.bcp -f D:\BCP\myChar.fmt -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myChar;"
```

### **Usando BULK INSERT e formato de caractere sem um arquivo de formato**<a name="bulk_char"></a>
Argumento**DATAFILETYPE** .  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):

```sql
TRUNCATE TABLE TestDatabase.dbo.myChar; -- for testing
BULK INSERT TestDatabase.dbo.myChar
    FROM 'D:\BCP\myChar.bcp'
    WITH (
        DATAFILETYPE = 'Char'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myChar;
```

### **Usando BULK INSERT e formato de caractere com um arquivo de formato não XML**<a name="bulk_char_fmt"></a>
Argumento**FORMATFILE** .  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):

```sql
TRUNCATE TABLE TestDatabase.dbo.myChar; -- for testing
BULK INSERT TestDatabase.dbo.myChar
   FROM 'D:\BCP\myChar.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myChar.fmt'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myChar;
```

### **Usando OPENROWSET e formato de caractere com um arquivo de formato não XML**<a name="openrowset_char_fmt"></a>
Argumento**FORMATFILE** .  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):

```sql
TRUNCATE TABLE TestDatabase.dbo.myChar;  -- for testing
INSERT INTO TestDatabase.dbo.myChar
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myChar.bcp', 
        FORMATFILE = 'D:\BCP\myChar.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myChar;
```
  
## Tarefas relacionadas<a name="RelatedTasks"></a>  
Para usar formatos de dados para importação ou exportação em massa 
  
-   [Importar dados de formato de caractere e nativo de versões anteriores do SQL Server](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Usar o formato nativo para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato de caractere Unicode para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo Unicode para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>Consulte também  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Importar dados de formato de caractere e nativo de versões anteriores do SQL Server](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
  
