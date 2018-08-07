---
title: Usar o formato nativo para importar ou exportar dados (SQL Server) | Microsoft Docs
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
- native data format [SQL Server]
- data formats [SQL Server], native
ms.assetid: eb279b2f-0f1f-428f-9b8f-2a7fc495b79f
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 7b5b297687860debe57d0624b9498678e86108f5
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39535366"
---
# <a name="use-native-format-to-import-or-export-data-sql-server"></a>Usar o formato nativo para importar ou exportar dados (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
O formato nativo é recomendado quando você transfere dados em massa entre várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um arquivo de dados que não contém nenhum conjunto de caracteres estendidos ou DBCS (Conjunto de caracteres de byte duplo).  

> [!NOTE]
>  Para transferir dados em massa entre várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um arquivo de dados com caracteres estendidos ou DBCS, use o formato nativo Unicode. Para obter mais informações, veja [Usar o formato nativo Unicode para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md).

O formato nativo mantém os tipos de dados nativos de um banco de dados. O formato nativo é planejado para transferência de dados em alta velocidade de dados entre tabelas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se você usar um arquivo de formato, as tabelas de origem e destino não precisarão ser idênticas. A transferência de dados envolve duas etapas:  
  
1.  A exportação de dados em massa de uma tabela de origem para um arquivo de dados  
  
2.  A exportação de dados em massa do arquivo de dados para uma tabela de origem  
  
O uso de formato nativo entre tabelas idênticas evita conversão desnecessária de tipos de dados do e para formato de caractere, economizando tempo e espaço. Porém, para alcançar a taxa de transferência otimizada são executadas algumas verificações referentes à formatação dos dados. Para evitar problemas com os dados carregados, consulte a lista de restrições a seguir.  

|Neste tópico:|
|---|
|[Restrições](#restrictions)|
|[Como o bcp trata dados no formato nativo](#considerations)|
|[Opções de comando para formato nativo](#command_options)|
|[Condições de teste de exemplo](#etc)<br /><br />&emsp;&#9679;&emsp;[Tabela de exemplo](#sample_table)<br />&emsp;&#9679;&emsp;[Arquivo de formato não XML de exemplo](#nonxml_format_file)|
|[Exemplos](#examples)<br />&emsp;&#9679;&emsp;[Usando bcp e formato nativo para exportar dados](#bcp_native_export)<br />&emsp;&#9679;&emsp;[Usando bcp e formato nativo para importar dados sem um arquivo de formato](#bcp_native_import)<br />&emsp;&#9679;&emsp;[Usando bcp e formato nativo para importar dados com um arquivo de formato não XML](#bcp_native_import_fmt)<br />&emsp;&#9679;&emsp;[Usando BULK INSERT e formato nativo sem um arquivo de formato](#bulk_native)<br />&emsp;&#9679;&emsp;[Usando BULK INSERT e formato nativo com um arquivo de formato não XML](#bulk_native_fmt)<br />&emsp;&#9679;&emsp;[Usando OPENROWSET e formato nativo com um arquivo de formato não XML](#openrowset_native_fmt)|
|[Tarefas relacionadas](#RelatedTasks)<p>                                                                                                                                                                                                                  </p>|

## Restrições<a name="restrictions"></a>  
Para importar dados em formato nativo com êxito, garanta que:  
  
-   O arquivo de dados está em formato nativo.  
  
-   A tabela de destino deve ser compatível com o arquivo de dados (com o número correto de colunas, tipo de dados, comprimento, status NULL, e assim sucessivamente) ou você deve usar um arquivo de formato para mapear cada campo para suas colunas correspondentes.  
  
    > [!NOTE]
    >  Se você importar dados de um arquivo que não corresponde à tabela de destino, a operação de importação poderá ter sucesso, mas os valores de dados inseridos na tabela de destino poderão estar incorretos. Isso porque os dados do arquivo são interpretados usando o formato da tabela de destino. Portanto, qualquer resultado divergente resultará na inserção de valores incorretos. Porém, em nenhuma circunstância tal divergência pode causar inconsistências lógicas ou físicas no banco de dados.  
  
     Para obter informações sobre como usar arquivos de formato, veja [Arquivos de formato para importação ou exportação de dados &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).  
  
 Uma importação bem-sucedida não corromperá a tabela de destino.  
  
## Como o bcp trata dados no formato nativo<a name="considerations"></a>
 Esta seção discute considerações especiais sobre como o utilitário **bcp** exporta e importa dados em formato nativo.  
  
-   Dados não caracteres  
  
     O [utilitário bcp](../../tools/bcp-utility.md) usa o formato de dados binário interno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para gravar dados não caracteres de uma tabela para um arquivo de dados.  
  
-   Dados[char](../../t-sql/data-types/char-and-varchar-transact-sql.md) ou [varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md)  
  
     No início de cada campo [char](../../t-sql/data-types/char-and-varchar-transact-sql.md) ou [varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md) , o [bcp](../../tools/bcp-utility.md) adiciona o tamanho do prefixo.  
  
    > [!IMPORTANT]
    >  Quando o modo nativo é usado, por padrão, o [utilitário bcp](../../tools/bcp-utility.md) converte caracteres do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em caracteres OEM antes de copiá-los em um arquivo de dados. O [utilitário bcp](../../tools/bcp-utility.md) converte caracteres de um arquivo de dados em caracteres ANSI antes de importá-los em uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Durante essas conversões, podem ser perdidos dados de caractere estendidos. Para caracteres estendidos, use o formato nativo Unicode ou especifique uma página de código.
  
-   Dados[sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md)  
  
     Se dados [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) forem armazenados como SQLVARIANT em um arquivo de dados do formato nativo, os dados manterão todas as suas características. Os metadados que registram o tipo de dados de cada valor de dado são armazenados com os valores de dados. Esses metadados são usados para recriar o valor de dado com o mesmo tipo de dados em uma coluna [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) de destino.  
  
     Se o tipo de dados da coluna de destino não for [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md), cada valor dos dados será convertido no tipo de dados da coluna de destino, seguindo as regras normais de conversão de dados implícita. Se ocorrer um erro durante a conversão dos dados, o lote atual será revertido. Quaisquer valores [char](../../t-sql/data-types/char-and-varchar-transact-sql.md) e [varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md) transferidos entre colunas [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) podem ter problemas de conversão de página de código.  
  
     Para obter mais informações sobre conversão de dados, consulte [Conversão de tipo de dados &#40;Mecanismo do Banco de Dados &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md).  
  
## Opções de comando para formato nativo<a name="command_options"></a>  
Você pode importar dados de formato nativo para uma tabela usando [bcp](../../tools/bcp-utility.md), [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) ou [INSERT... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md).  Para um comando [bcp](../../tools/bcp-utility.md) ou uma instrução [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md), você pode especificar o formato de dados na instrução.  Para uma instrução [INSERT... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md), é necessário especificar o formato dos dados em um arquivo de formato.  

O formato nativo tem suporte nas seguintes opções de comando:  

|Comando|Opção|Descrição|  
|-------------|------------|-----------------|  
|bcp|**-n**|Faz com que o utilitário bcp use os tipos de dados nativos dos dados.*|  
|BULK INSERT|DATAFILETYPE **='native'**|Usa o tipo de dados nativo ou nativo largo. Observe que DATAFILETYPE não será necessário se um arquivo de formato especificar os tipos de dados.|  
|OPENROWSET|N/A|Deve usar um arquivo de formato|

  
 \*Para carregar dados nativos (**-n**) em um formato compatível com versões anteriores de clientes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , use a opção **-V** . Para obter mais informações, consulte [Importar dados de formato de caractere e nativo de versões anteriores do SQL Server](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md).  
  
> [!NOTE]
>  Como alternativa, você pode especificar a formatação por campo, em um arquivo de formato. Para obter mais informações, consulte [Arquivos de formato para importação ou exportação de dados &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).
  

## Condições de teste de exemplo<a name="etc"></a>  
Os exemplos neste tópico baseiam-se na tabela e no arquivo de formato definidos abaixo.

### **Tabela de exemplo**<a name="sample_table"></a>
O script a seguir cria um banco de dados de teste, uma tabela chamada de `myNative` e preenche a tabela com alguns valores iniciais.  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):

```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.myNative ( 
   PersonID smallint NOT NULL,
   FirstName varchar(25) NOT NULL,
   LastName varchar(30) NOT NULL,
   BirthDate date,
   AnnualSalary money
   );

-- Populate table
INSERT TestDatabase.dbo.myNative
VALUES 
(1, 'Anthony', 'Grosse', '1980-02-23', 65000.00),
(2, 'Alica', 'Fatnowna', '1963-11-14', 45000.00),
(3, 'Stella', 'Rossenhain', '1992-03-02', 120000.00);

-- Review Data
SELECT * FROM TestDatabase.dbo.myNative;
```

### **Exemplo de arquivo de formato não XML**<a name="nonxml_format_file"></a>
O SQL Server dá suporte a dois tipos de arquivo de formato: XML e não XML.  O formato não XML é o formato original com suporte em versões anteriores do SQL Server.  Examine [Arquivos de formato não XML (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) para obter informações detalhadas.  O comando a seguir usará o [utilitário bcp](../../tools/bcp-utility.md) para gerar um arquivo de formato não XML, `myNative.fmt`, com base no esquema de `myNative`.  Para usar um comando [bcp](../../tools/bcp-utility.md) para criar um arquivo de formato, especifique o argumento **format** e use **nul** em vez de um caminho de arquivo de dados.  A opção format também exige a opção **-f** .  Além disso, neste exemplo, o qualificador **c** é usado para especificar dados de caractere, e **T** é usado para especificar uma conexão confiável usando a segurança integrada.  No prompt de comando, digite os seguintes comandos:

```cmd
bcp TestDatabase.dbo.myNative format nul -f D:\BCP\myNative.fmt -T -n 

REM Review file
Notepad D:\BCP\myNative.fmt
```

> [!IMPORTANT]
> Verifique se o arquivo de formato não XML termina com um retorno de carro/alimentação de linha.  Caso contrário, você provavelmente receberá a seguinte mensagem de erro:
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`

## Exemplos<a name="examples"></a>
Os exemplos abaixo usam o banco de dados e os arquivos de formato criados acima.

### **Usando bcp e formato nativo para exportar dados**<a name="bcp_native_export"></a>
Opção **-n** e comando **OUT** .  Observação: o arquivo de dados criado neste exemplo será usado em todos os exemplos subsequentes.  No prompt de comando, digite os seguintes comandos:

```cmd
bcp TestDatabase.dbo.myNative OUT D:\BCP\myNative.bcp -T -n

REM Review results
NOTEPAD D:\BCP\myNative.bcp
```

### **Usando bcp e formato nativo para importar dados sem um arquivo de formato**<a name="bcp_native_import"></a>
Opção **-n** e comando **IN** .  No prompt de comando, digite os seguintes comandos:

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myNative;"

REM Import data
bcp TestDatabase.dbo.myNative IN D:\BCP\myNative.bcp -T -n

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myNative;"
```

### **Usando bcp e formato nativo para importar dados com um arquivo de formato não XML**<a name="bcp_native_import_fmt"></a>
Opções **-n** e **-f** switches e **IN** comme.  No prompt de comando, digite os seguintes comandos:

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myNative;"

REM Import data
bcp TestDatabase.dbo.myNative IN D:\BCP\myNative.bcp -f D:\BCP\myNative.fmt -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myNative;"
```

### **Usando BULK INSERT e formato nativo sem um arquivo de formato**<a name="bulk_native"></a>
Argumento**DATAFILETYPE** .  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):

```sql
TRUNCATE TABLE TestDatabase.dbo.myNative; -- for testing
BULK INSERT TestDatabase.dbo.myNative
    FROM 'D:\BCP\myNative.bcp'
    WITH (
        DATAFILETYPE = 'native'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myNative;
```

### **Usando BULK INSERT e formato nativo com um arquivo de formato não XML**<a name="bulk_native_fmt"></a>
Argumento**FORMATFILE** .  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):

```sql
TRUNCATE TABLE TestDatabase.dbo.myNative; -- for testing
BULK INSERT TestDatabase.dbo.myNative
   FROM 'D:\BCP\myNative.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myNative.fmt'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myNative;
```

### **Usando OPENROWSET e formato nativo com um arquivo de formato não XML**<a name="openrowset_native_fmt"></a>
Argumento**FORMATFILE** .  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):

```sql
TRUNCATE TABLE TestDatabase.dbo.myNative;  -- for testing
INSERT INTO TestDatabase.dbo.myNative
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myNative.bcp', 
        FORMATFILE = 'D:\BCP\myNative.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myNative;
```
  
## Tarefas relacionadas<a name="RelatedTasks"></a>
Para usar formatos de dados para importação ou exportação em massa 
  
-   [Importar dados de formato de caractere e nativo de versões anteriores do SQL Server](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Usar o formato de caractere para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato de caractere Unicode para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo Unicode para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)   
 [Importar dados de formato de caractere e nativo de versões anteriores do SQL Server](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Usar o formato nativo Unicode para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
  
