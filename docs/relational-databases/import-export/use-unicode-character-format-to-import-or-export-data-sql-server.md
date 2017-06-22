---
title: Usar o formato de caractere Unicode para importar ou exportar dados (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 09/30/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data formats [SQL Server], Unicode character
- Unicode [SQL Server], bulk importing and exporting
ms.assetid: 74342a11-c1c0-4746-b482-7f3537744a70
caps.latest.revision: 37
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 63fb68860ade1e0bd64ce87ca98ec4439bf238fa
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="use-unicode-character-format-to-import-or-export-data-sql-server"></a>Usar o formato de caractere Unicode para importar ou exportar dados (SQL Server)
O formato de caractere Unicode é recomendado para transferir em massa dados entre várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um arquivo de dados com caracteres estendidos DBCS. O formato de dados de caractere Unicode permite exportar dados de um servidor usando uma página de código que difere da página de código usada pelo cliente que está executando a operação. Em tais casos, o uso do formato de caractere Unicode tem as seguintes vantagens:  
  
* Se os dados de origem e destino forem tipos de dados Unicode, o uso do formato de caractere Unicode preservará todos os dados de caractere.  
  
* Se os dados de origem e destino não forem tipos de dados Unicode, o uso do formato de caractere Unicode minimizará a perda de caracteres estendidos nos dados de origem que não podem ser representados no destino.

|Neste tópico:|
|---|
|[Considerações sobre usar o formato de caractere Unicode](#considerations)|
|[Considerações especiais para o formato de caractere Unicode, bcp e um arquivo de formato](#special_considerations)|
|[Opções de comando para formato de caractere Unicode](#command_options)|
|[Condições de teste de exemplo](#etc)<br />&emsp;&#9679;&emsp;[Tabela de exemplo](#sample_table)<br />&emsp;&#9679;&emsp;[Arquivo de formato não XML de exemplo](#nonxml_format_file)|
|[Exemplos](#examples)<br />&emsp;&#9679;&emsp;[Usando bcp e formato de caractere Unicode para exportar dados](#bcp_widechar_export)<br />&emsp;&#9679;&emsp;[Usando bcp e formato de caractere Unicode para importar dados sem um arquivo de formato](#bcp_widechar_import)<br />&emsp;&#9679;&emsp;[Usando bcp e formato de caractere Unicode para importar dados com um arquivo de formato não XML](#bcp_widechar_import_fmt)<br />&emsp;&#9679;&emsp;[Usando BULK INSERT e formato de caractere Unicode sem um arquivo de formato](#bulk_widechar)<br />&emsp;&#9679;&emsp;[Usando BULK INSERT e formato de caractere Unicode com um arquivo de formato não XML](#bulk_widechar_fmt)<br />&emsp;&#9679;&emsp;[Usando OPENROWSET e formato de caractere Unicode com um arquivo de formato não XML](#openrowset_widechar_fmt)|
|[Tarefas relacionadas](#RelatedTasks)<p>                                                                                                                                                                                                                  </p>|
 
## Considerações sobre usar o formato de caractere Unicode<a name="considerations"></a>
Ao usar formato de caractere Unicode, considere o seguinte:  

* Por padrão, o [utilitário bcp](../../tools/bcp-utility.md) separa os campos dos dados de caractere com o caractere de guia e termina os registros com o caractere de nova linha.  Para obter informações sobre como especificar terminadores alternativos, consulte [Especificar terminadores de campo e linha &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).

* Os dados de [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) que são armazenados em um arquivo de dados no formato de caractere Unicode operam da mesma maneira que operam em um arquivo de dados no formato de caractere, com a exceção de que os dados são armazenados como [nchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md) em vez de dados [char](../../t-sql/data-types/char-and-varchar-transact-sql.md). Para obter mais informações sobre formato de caractere, consulte [Suporte a agrupamentos e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md).  

## Considerações especiais para o formato de caractere Unicode, bcp e um arquivo de formato<a name="special_considerations"></a>
Os arquivos de dados em formato de caractere Unicode seguem as convenções para arquivos Unicode.  Os primeiros dois bytes do arquivo são números hexadecimais, 0xFFFE.  Esses bytes servem como marcas de ordem do byte (BOM), especificando se o byte de ordem alta é armazenado em primeiro ou por último no arquivo.  O [utilitário bcp](../../tools/bcp-utility.md) pode interpretar incorretamente o BOM e fazer com que parte de seu processo de importação falhe; você pode receber uma mensagem de erro semelhante da seguinte maneira:
```
Starting copy...
SQLState = 22005, NativeError = 0
Error = [Microsoft][ODBC Driver 13 for SQL Server]Invalid character value for cast specification
```

O BOM pode ser interpretado incorretamente sob as seguintes condições:
* O [utilitário bcp](../../tools/bcp-utility.md) é usado e a opção **-w** é usada para indicar o caractere Unicode

* É usado um arquivo de formato

* O primeiro campo no arquivo de dados é não caractere

Considere se qualquer uma das seguintes alternativas podem estar disponíveis para sua situação *específica* :
* Não use um arquivo de formato.  Um exemplo dessa solução alternativa é fornecido abaixo, consulte [Usando bcp e formato de caractere Unicode para importar dados sem um arquivo de formato](#bcp_widechar_import),

* Use a opção **- c** , em vez de **-w**,

* Exportar novamente os dados usando um formato nativo,

* Use [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) ou [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md).  Exemplos dessas soluções alternativas são fornecidos abaixo, consulte [Usando BULK INSERT e o formato de caractere Unicode com um arquivo de formato não XML](#bulk_widechar_fmt) e [Usando OPENROWSET e o formato de caractere Unicode com um arquivo de formato não XML](#openrowset_widechar_fmt),
 
* Inserir manualmente o primeiro registro na tabela de destino e, em seguida, use a opção **-F 2** para que a importação se inicie no segundo registro,

* Inserir manualmente o primeiro registro fictício no arquivo de dados e, em seguida, use a opção **-F 2** para que a importação se inicie no segundo registro.  Um exemplo dessa solução alternativa é fornecido abaixo, consulte [Usando bcp e formato de caractere Unicode para importar dados com um arquivo de formato não XML](#bcp_widechar_import_fmt),

* Use uma tabela de preparo na qual a primeira coluna é um tipo de dados de caractere, ou

* Exportar os dados novamente e altere a ordem de campo dos dados para que o primeiro campo de dados seja um caractere.  Em seguida, use um arquivo de formato para remapear o campo de dados para a ordem real na tabela.  Por exemplo, consulte [Usar um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md).
  
## Opções de comando para formato de caractere Unicode<a name="command_options"></a>  
Você pode importar dados de formato de caractere Unicode para uma tabela usando [bcp](../../tools/bcp-utility.md), [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) ou [INSERT... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md).  Para um comando [bcp](../../tools/bcp-utility.md) ou uma instrução [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md), você pode especificar o formato de dados na instrução.  Para uma instrução [INSERT... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md), é necessário especificar o formato dos dados em um arquivo de formato.  
  
Formato de caractere Unicode tem suporte nas seguintes opções da linha de comando:  
  
|Comando|Opção|Descrição|  
|-------------|------------|-----------------|  
|bcp|**-w**|Usa o formato de caractere Unicode.|  
|BULK INSERT|DATAFILETYPE **='widechar'**|Usa o formato de caractere Unicode na importação em massa de dados.|  
|OPENROWSET|N/A|Deve usar um arquivo de formato|
  
> [!NOTE]
>  Como alternativa, você pode especificar a formatação por campo, em um arquivo de formato. Para obter mais informações, consulte [Arquivos de formato para importação ou exportação de dados &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).
  
## Condições de teste de exemplo<a name="etc"></a>  
Os exemplos neste tópico baseiam-se na tabela e no arquivo de formato definidos abaixo.

### **Tabela de exemplo**<a name="sample_table"></a>
O script a seguir cria um banco de dados de teste, uma tabela chamada de `myWidechar` e preenche a tabela com alguns valores iniciais.  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```tsql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.myWidechar ( 
    PersonID smallint NOT NULL,
    FirstName nvarchar(25) NOT NULL,
    LastName nvarchar(30) NOT NULL,
    BirthDate date,
    AnnualSalary money
);

-- Populate table
INSERT TestDatabase.dbo.myWidechar
VALUES 
(1, N'ϴAnthony', N'Grosse', '02-23-1980', 65000.00),
(2, N'❤Alica', N'Fatnowna', '11-14-1963', 45000.00),
(3, N'☎Stella', N'Rossenhain', '03-02-1992', 120000.00);

-- Review Data
SELECT * FROM TestDatabase.dbo.myWidechar;
```

### **Exemplo de arquivo de formato não XML**<a name="nonxml_format_file"></a>
O SQL Server dá suporte a dois tipos de arquivo de formato: XML e não XML.  O formato não XML é o formato original com suporte em versões anteriores do SQL Server.  Examine [Arquivos de formato não XML (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) para obter informações detalhadas.  O comando a seguir usará o [utilitário bcp](../../tools/bcp-utility.md) para gerar um arquivo de formato não XML, `myWidechar.fmt`, com base no esquema de `myWidechar`.  Para usar um comando [bcp](../../tools/bcp-utility.md) para criar um arquivo de formato, especifique o argumento **format** e use **nul** em vez de um caminho de arquivo de dados.  A opção format também exige a opção **-f** .  Além disso, neste exemplo, o qualificador **c** é usado para especificar dados de caractere, e **T** é usado para especificar uma conexão confiável usando a segurança integrada.  No prompt de comando, digite os seguintes comandos:

```
bcp TestDatabase.dbo.myWidechar format nul -f D:\BCP\myWidechar.fmt -T -w

REM Review file
Notepad D:\BCP\myWidechar.fmt
```

> [!IMPORTANT]
> Verifique se o arquivo de formato não XML termina com um retorno de carro/alimentação de linha.  Caso contrário, você provavelmente receberá a seguinte mensagem de erro:
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`


## Exemplos<a name="examples"></a>
Os exemplos abaixo usam o banco de dados e os arquivos de formato criados acima.

### **Usando bcp e formato de caractere Unicode para exportar dados**<a name="bcp_widechar_export"></a>
Opção**-w** e comando **OUT** .  Observação: o arquivo de dados criado neste exemplo será usado em todos os exemplos subsequentes.  No prompt de comando, digite os seguintes comandos:
```
bcp TestDatabase.dbo.myWidechar OUT D:\BCP\myWidechar.bcp -T -w

REM Review results
NOTEPAD D:\BCP\myWidechar.bcp
```

### **Usando bcp e formato de caractere Unicode para importar dados sem um arquivo de formato**<a name="bcp_widechar_import"></a>
Opção**-w** e comando **IN** .  No prompt de comando, digite os seguintes comandos:
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myWidechar;"

REM Import data
bcp TestDatabase.dbo.myWidechar IN D:\BCP\myWidechar.bcp -T -w

REM Review results is SSMS
```

### **Usando bcp e formato de caractere Unicode para importar dados com um arquivo de formato não XML**<a name="bcp_widechar_import_fmt"></a>
Opções**-w** e **-f** switches e **IN** comme.  Uma solução alternativa precisará ser usada, já que este exemplo envolve bcp, um arquivo de formato, caractere Unicode, e o primeiro campo de dados no arquivo de dados é não caractere.  Consulte [Considerações especiais para o formato de caractere Unicode, bcp e um arquivo de formato](#special_considerations), acima.  O arquivo de dados `myWidechar.bcp` será alterado adicionando um registro adicional como um registro "fictício", em seguida, será ignorado com a opção `-F 2` .

No prompt de comando, digite os seguintes comandos e siga as etapas de modificação:
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myWidechar;"

REM Open data file
Notepad D:\BCP\myWidechar.bcp
REM Copy first record and then paste as new first record.  This additional record is the "dummy" record.
REM Close file.

REM Import data instructing bcp to skip dummy record with the -F 2 switch.
bcp TestDatabase.dbo.myWidechar IN D:\BCP\myWidechar.bcp -f D:\BCP\myWidechar.fmt -T -F 2

REM Review results is SSMS

REM Return data file to original state for usage in other examples
bcp TestDatabase.dbo.myWidechar OUT D:\BCP\myWidechar.bcp -T -w
```
  
### **Usando BULK INSERT e formato de caractere Unicode sem um arquivo de formato**<a name="bulk_widechar"></a>
Argumento**DATAFILETYPE** .  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```tsql
TRUNCATE TABLE TestDatabase.dbo.myWidechar; -- for testing
BULK INSERT TestDatabase.dbo.myWidechar
    FROM 'D:\BCP\myWidechar.bcp'
    WITH (
        DATAFILETYPE = 'widechar'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myWidechar;
```
  
### **Usando BULK INSERT e formato de caractere Unicode com um arquivo de formato não XML**<a name="bulk_widechar_fmt"></a>
Argumento**FORMATFILE** .  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```tsql
TRUNCATE TABLE TestDatabase.dbo.myWidechar; -- for testing
BULK INSERT TestDatabase.dbo.myWidechar
   FROM 'D:\BCP\myWidechar.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myWidechar.fmt'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myWidechar;
```
  
### **Usando OPENROWSET e formato de caractere Unicode com um arquivo de formato não XML**<a name="openrowset_widechar_fmt"></a>
Argumento**FORMATFILE** .  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```tsql
TRUNCATE TABLE TestDatabase.dbo.myWidechar;  -- for testing
INSERT INTO TestDatabase.dbo.myWidechar
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myWidechar.bcp', 
        FORMATFILE = 'D:\BCP\myWidechar.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myWidechar;
```
 
  
## Tarefas relacionadas<a name="RelatedTasks"></a>
Para usar formatos de dados para importação ou exportação em massa  
-   [Importar dados de formato de caractere e nativo de versões anteriores do SQL Server](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Usar o formato de caractere para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo Unicode para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>Consulte também  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Suporte a agrupamentos e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  

