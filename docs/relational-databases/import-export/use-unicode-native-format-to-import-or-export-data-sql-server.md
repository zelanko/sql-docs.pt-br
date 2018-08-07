---
title: Usar o formato nativo Unicode para importar ou exportar dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 09/30/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: import-export
ms.reviewer: ''
ms.suite: sql
ms.technology: data-movement
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Unicode [SQL Server], bulk importing and exporting
- data formats [SQL Server], Unicode native
ms.assetid: a6213308-f3d5-406e-9029-19d8bb3367f3
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: f2f0f79a6bd68c362382144b5f3185df9540678d
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39556996"
---
# <a name="use-unicode-native-format-to-import-or-export-data-sql-server"></a>Usar o formato nativo Unicode para importar ou exportar dados (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
O formato nativo Unicode é útil quando as informações devem ser copiadas de uma instalação [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a outra. O uso de formato nativo para dados do tipo não caractere economiza tempo, eliminando a conversão desnecessária de tipos de dados de e para o formato de caractere. O uso de formato de caractere Unicode para obter todos os dados de caractere impede a perda de qualquer caractere estendido durante a transferência de dados em massa entre servidores que usam páginas de código diferentes. Um arquivo de dados em formato nativo Unicode pode ser lido por qualquer método de importação em massa.  
  
 O formato nativo Unicode é recomendado para transferir em massa dados entre várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um arquivo de dados com caracteres estendidos DBCS. Para obter dados do tipo não caractere, o formato nativo Unicode usa tipos de dados nativos (banco de dados). Para dados de caracteres, tal como [char](../../t-sql/data-types/char-and-varchar-transact-sql.md), [nchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md), [varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md), [nvarchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md), [text](../../t-sql/data-types/ntext-text-and-image-transact-sql.md), [varchar(max)](../../t-sql/data-types/char-and-varchar-transact-sql.md), [nvarchar(max)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)e [ntext](../../t-sql/data-types/ntext-text-and-image-transact-sql.md), o formato nativo Unicode usa o formato de dados de caractere Unicode.  
  
 Os dados [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) armazenados como um SQLVARIANT em um arquivo de dados do formato nativo Unicode operam da mesma maneira como em um arquivo de dados do formato nativo, exceto pelos valores [char](../../t-sql/data-types/char-and-varchar-transact-sql.md) e [varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md) , que são convertidos para [nchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md) e [nvarchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md), os quais dobram a quantidade de espaço de armazenamento necessária para as colunas afetadas. Os metadados originais são preservados e os valores são reconvertidos aos seus tipos de dados originais [char](../../t-sql/data-types/char-and-varchar-transact-sql.md) e [varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md) quando importados em massa em uma coluna de tabela.  
 
 |Neste tópico:|
|---|
|[Opções de comando para formato nativo Unicode](#command_options)|
|[Condições de teste de exemplo](#etc)<br />&emsp;&#9679;&emsp;[Tabela de exemplo](#sample_table)<br />&emsp;&#9679;&emsp;[Arquivo de formato não XML de exemplo](#nonxml_format_file)|
|[Exemplos](#examples)<br />&emsp;&#9679;&emsp;[Usando bcp e formato nativo Unicode para exportar dados](#bcp_widenative_export)<br />&emsp;&#9679;&emsp;[Usando bcp e formato nativo Unicode para importar dados sem um arquivo de formato](#bcp_widenative_import)<br />&emsp;&#9679;&emsp;[Usando bcp e formato nativo Unicode para importar dados com um arquivo de formato não XML](#bcp_widenative_import_fmt)<br />&emsp;&#9679;&emsp;[Usando BULK INSERT e formato nativo Unicode sem um arquivo de formato](#bulk_widenative)<br />&emsp;&#9679;&emsp;[Usando BULK INSERT e formato nativo Unicode com um arquivo de formato não XML](#bulk_widenative_fmt)<br />&emsp;&#9679;&emsp;[Usando OPENROWSET e formato nativo Unicode com um arquivo de formato não XML](#openrowset_widenative_fmt)|
|[Tarefas relacionadas](#RelatedTasks)<p>                                                                                                                                                                                                                  </p>|
  
## Opções de comando para formato nativo Unicode<a name="command_options"></a>  
Você pode importar dados de formato nativo Unicode para uma tabela usando [bcp](../../tools/bcp-utility.md), [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) ou [INSERT... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md).  Para um comando [bcp](../../tools/bcp-utility.md) ou uma instrução [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md), você pode especificar o formato de dados na instrução.  Para uma instrução [INSERT... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md), é necessário especificar o formato dos dados em um arquivo de formato.  
  
O formato nativo Unicode tem suporte nas seguintes opções de comando:  
  
|Comando|Opção|Descrição|  
|-------------|------------|-----------------|  
|bcp|**-N**|Faz com que o utilitário **bcp** use o formato nativo Unicode que usa tipos de dados nativos (banco de dados) para todos os dados do tipo não caractere e formato de dados de caractere Unicode para obter todos os dados de caracteres (**char**, **nchar**, **varchar**, **nvarchar**, **text**e **ntext**).|  
|BULK INSERT|DATAFILETYPE **='widenative'**|Usa o formato nativo Unicode na importação de dados em massa.|  
|OPENROWSET|N/A|Deve usar um arquivo de formato|
    
> [!NOTE]
>  Como alternativa, você pode especificar a formatação por campo, em um arquivo de formato. Para obter mais informações, consulte [Arquivos de formato para importação ou exportação de dados &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).
  
## Condições de teste de exemplo<a name="etc"></a>  
Os exemplos neste tópico baseiam-se na tabela e no arquivo de formato definidos abaixo.

### **Tabela de exemplo**<a name="sample_table"></a>
O script a seguir cria um banco de dados de teste, uma tabela chamada de `myWidenative` e preenche a tabela com alguns valores iniciais.  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.myWidenative ( 
    PersonID smallint NOT NULL,
    FirstName nvarchar(25) NOT NULL,
    LastName nvarchar(30) NOT NULL,
    BirthDate date,
    AnnualSalary money
);

-- Populate table
INSERT TestDatabase.dbo.myWidenative
VALUES 
(1, N'ϴAnthony', N'Grosse', '02-23-1980', 65000.00),
(2, N'❤Alica', N'Fatnowna', '11-14-1963', 45000.00),
(3, N'☎Stella', N'Rossenhain', '03-02-1992', 120000.00);

-- Review Data
SELECT * FROM TestDatabase.dbo.myWidenative;
```

### **Exemplo de arquivo de formato não XML**<a name="nonxml_format_file"></a>
O SQL Server dá suporte a dois tipos de arquivo de formato: XML e não XML.  O formato não XML é o formato original com suporte em versões anteriores do SQL Server.  Examine [Arquivos de formato não XML (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) para obter informações detalhadas.  O comando a seguir usará o [utilitário bcp](../../tools/bcp-utility.md) para gerar um arquivo de formato não XML, `myWidenative.fmt`, com base no esquema de `myWidenative`.  Para usar um comando [bcp](../../tools/bcp-utility.md) para criar um arquivo de formato, especifique o argumento **format** e use **nul** em vez de um caminho de arquivo de dados.  A opção format também exige a opção **-f** .  Além disso, neste exemplo, o qualificador **c** é usado para especificar dados de caractere, e **T** é usado para especificar uma conexão confiável usando a segurança integrada.  No prompt de comando, digite os seguintes comandos:

```
bcp TestDatabase.dbo.myWidenative format nul -f D:\BCP\myWidenative.fmt -T -N

REM Review file
Notepad D:\BCP\myWidenative.fmt
```

> [!IMPORTANT]
> Verifique se o arquivo de formato não XML termina com um retorno de carro/alimentação de linha.  Caso contrário, você provavelmente receberá a seguinte mensagem de erro:
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`

## Exemplos<a name="examples"></a>
Os exemplos abaixo usam o banco de dados e os arquivos de formato criados acima.

### **Usando bcp e formato nativo Unicode para exportar dados**<a name="bcp_widenative_export"></a>
Opção **-N** e comando **OUT** .  Observação: o arquivo de dados criado neste exemplo será usado em todos os exemplos subsequentes.  No prompt de comando, digite os seguintes comandos:
```
bcp TestDatabase.dbo.myWidenative OUT D:\BCP\myWidenative.bcp -T -N

REM Review results
NOTEPAD D:\BCP\myWidenative.bcp
```

### **Usando bcp e formato nativo Unicode para importar dados sem um arquivo de formato**<a name="bcp_widenative_import"></a>
Opção **-N** e comando **IN** .  No prompt de comando, digite os seguintes comandos:
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myWidenative;"

REM Import data
bcp TestDatabase.dbo.myWidenative IN D:\BCP\myWidenative.bcp -T -N

REM Review results is SSMS
```

### **Usando bcp e formato nativo Unicode para importar dados com um arquivo de formato não XML**<a name="bcp_widenative_import_fmt"></a>
Opções **-N** e **-f** switches e **IN** comme.  No prompt de comando, digite os seguintes comandos:
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myWidenative;"

REM Import data
bcp TestDatabase.dbo.myWidenative IN D:\BCP\myWidenative.bcp -f D:\BCP\myWidenative.fmt -T

REM Review results is SSMS
```

### **Usando BULK INSERT e formato nativo Unicode sem um arquivo de formato**<a name="bulk_widenative"></a>
Argumento**DATAFILETYPE** .  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
TRUNCATE TABLE TestDatabase.dbo.myWidenative; -- for testing
BULK INSERT TestDatabase.dbo.myWidenative
    FROM 'D:\BCP\myWidenative.bcp'
    WITH (
        DATAFILETYPE = 'widenative'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myWidenative;
```

### **Usando BULK INSERT e formato nativo Unicode com um arquivo de formato não XML**<a name="bulk_widenative_fmt"></a>
Argumento**FORMATFILE** .  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
TRUNCATE TABLE TestDatabase.dbo.myWidenative; -- for testing
BULK INSERT TestDatabase.dbo.myWidenative
   FROM 'D:\BCP\myWidenative.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myWidenative.fmt'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myWidenative;
```

### **Usando OPENROWSET e formato nativo Unicode com um arquivo de formato não XML**<a name="openrowset_widenative_fmt"></a>
Argumento**FORMATFILE** .  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
TRUNCATE TABLE TestDatabase.dbo.myWidenative;  -- for testing
INSERT INTO TestDatabase.dbo.myWidenative
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myWidenative.bcp', 
        FORMATFILE = 'D:\BCP\myWidenative.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myWidenative;
```

## Tarefas relacionadas<a name="RelatedTasks"></a>
Para usar formatos de dados para importação ou exportação em massa  
-   [Importar dados de formato de caractere e nativo de versões anteriores do SQL Server](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Usar o formato de caractere para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato de caractere Unicode para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
  
  
