---
title: Usar um formato nativo para importar e exportar dados
description: Na importação ou na exportação do SQL Server, o formato nativo mantém os tipos de dados nativos de um banco de dados para transferência de dados de alta velocidade entre as tabelas do SQL Server.
ms.date: 09/30/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- native data format [SQL Server]
- data formats [SQL Server], native
ms.assetid: eb279b2f-0f1f-428f-9b8f-2a7fc495b79f
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: 4a1802cc2bcd64141c35dcc1e15f4609848e7c79
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465547"
---
# <a name="use-native-format-to-import-or-export-data-sql-server"></a>Usar um formato nativo para importar ou exportar dados (SQL Server)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
O formato nativo é recomendado quando você transfere dados em massa entre várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um arquivo de dados que não contém nenhum conjunto de caracteres estendidos ou DBCS (Conjunto de caracteres de byte duplo).  

> [!NOTE]
>  Para transferir dados em massa entre várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um arquivo de dados com caracteres estendidos ou DBCS, use o formato nativo Unicode. Para obter mais informações, veja [Usar o formato nativo Unicode para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md).

O formato nativo mantém os tipos de dados nativos de um banco de dados. O formato nativo é planejado para transferência de dados em alta velocidade de dados entre tabelas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se você usar um arquivo de formato, as tabelas de origem e destino não precisarão ser idênticas. A transferência de dados envolve duas etapas:  
  
1.  A exportação de dados em massa de uma tabela de origem para um arquivo de dados  
  
2.  A exportação de dados em massa do arquivo de dados para uma tabela de origem  

O uso de formato nativo entre tabelas idênticas evita conversão desnecessária de tipos de dados do e para formato de caractere, economizando tempo e espaço. Porém, para alcançar a taxa de transferência otimizada são executadas algumas verificações referentes à formatação dos dados. Para evitar problemas com os dados carregados, consulte a lista de restrições a seguir.  


## <a name="restrictions"></a>Restrições
Para importar dados em formato nativo com êxito, garanta que:  
  
-   O arquivo de dados está em formato nativo.  
  
-   A tabela de destino deve ser compatível com o arquivo de dados (com o número correto de colunas, tipo de dados, comprimento, status NULL, e assim sucessivamente) ou você deve usar um arquivo de formato para mapear cada campo para suas colunas correspondentes.  
  
    > [!NOTE]
    >  Se você importar dados de um arquivo que não corresponde à tabela de destino, a operação de importação poderá ter sucesso, mas os valores de dados inseridos na tabela de destino poderão estar incorretos. Isso porque os dados do arquivo são interpretados usando o formato da tabela de destino. Portanto, qualquer resultado divergente resultará na inserção de valores incorretos. Porém, em nenhuma circunstância tal divergência pode causar inconsistências lógicas ou físicas no banco de dados.  
  
     Para obter informações sobre como usar arquivos de formato, veja [Arquivos de formato para importação ou exportação de dados &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).  
  
 Uma importação bem-sucedida não corromperá a tabela de destino.  
  
## <a name="how-bcp-handles-data-in-native-format"></a>Como o bcp manipula dados no formato nativo
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
  
## <a name="command-options-for-native-format"></a>Opções de comando para formato nativo
Você pode importar dados de formato nativo para uma tabela usando [bcp](../../tools/bcp-utility.md), [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) ou [INSERT... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md).  Para um comando [bcp](../../tools/bcp-utility.md) ou uma instrução [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md), você pode especificar o formato de dados na instrução.  Para uma instrução [INSERT... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md), é necessário especificar o formato dos dados em um arquivo de formato.  

O formato nativo tem suporte nas seguintes opções de comando:  

|Comando|Opção|Descrição|  
|-------------|------------|-----------------|  
|bcp|**-n**|Faz com que o utilitário bcp use os tipos de dados nativos dos dados.*|  
|BULK INSERT|DATAFILETYPE **='native'**|Usa o tipo de dados nativo ou nativo largo. Observe que DATAFILETYPE não será necessário se um arquivo de formato especificar os tipos de dados.|  
|OPENROWSET|N/D|Deve usar um arquivo de formato|

  
 \*Para carregar dados nativos ( **-n**) em um formato compatível com versões anteriores de clientes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , use a opção **-V** . Para obter mais informações, consulte [Importar dados de formato de caractere e nativo de versões anteriores do SQL Server](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md).  
  
> [!NOTE]
>  Como alternativa, você pode especificar a formatação por campo, em um arquivo de formato. Para obter mais informações, consulte [Arquivos de formato para importação ou exportação de dados &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).
  

## <a name="example-test-conditions"></a>Condições de teste de exemplo
Os exemplos neste tópico baseiam-se na tabela e no arquivo de formato definidos abaixo.

### <a name="sample-table"></a>Tabela de exemplo
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

### <a name="sample-non-xml-format-file"></a>Arquivo de formato não XML de exemplo
O SQL Server dá suporte a dois tipos de arquivo de formato: XML e não XML.  O formato não XML é o formato original com suporte em versões anteriores do SQL Server.  Examine [Arquivos de formato não XML (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) para obter informações detalhadas.  O comando a seguir usará o [utilitário bcp](../../tools/bcp-utility.md) para gerar um arquivo de formato não XML, `myNative.fmt`, com base no esquema de `myNative`.  Para usar um comando [bcp](../../tools/bcp-utility.md) para criar um arquivo de formato, especifique o argumento **format** e use **nul** em vez de um caminho de arquivo de dados.  A opção format também exige a opção **-f** .  Além disso, neste exemplo, o qualificador **c** é usado para especificar dados de caractere, e **T** é usado para especificar uma conexão confiável usando a segurança integrada.  No prompt de comando, digite os seguintes comandos:

```cmd
bcp TestDatabase.dbo.myNative format nul -f D:\BCP\myNative.fmt -T 

REM Review file
Notepad D:\BCP\myNative.fmt
```

> [!IMPORTANT]
> Verifique se o arquivo de formato não XML termina com um retorno de carro/alimentação de linha.  Caso contrário, você provavelmente receberá a seguinte mensagem de erro:
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`

## <a name="examples"></a>Exemplos
Os exemplos abaixo usam o banco de dados e os arquivos de formato criados acima.

### <a name="using-bcp-and-native-format-to-export-data"></a>Usar bcp e formato nativo para exportar dados
Opção **-n** e comando **OUT** .  Observação: o arquivo de dados criado neste exemplo será usado em todos os exemplos subsequentes.  No prompt de comando, digite os seguintes comandos:

```cmd
bcp TestDatabase.dbo.myNative OUT D:\BCP\myNative.bcp -T -n

REM Review results
NOTEPAD D:\BCP\myNative.bcp
```

### <a name="using-bcp-and-native-format-to-import-data-without-a-format-file"></a>Usar bcp e formato nativo para importar dados sem um arquivo de formato
Opção **-n** e comando **IN** .  No prompt de comando, digite os seguintes comandos:

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myNative;"

REM Import data
bcp TestDatabase.dbo.myNative IN D:\BCP\myNative.bcp -T -n

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myNative;"
```

### <a name="using-bcp-and-native-format-to-import-data-with-a-non-xml-format-file"></a>Usar bcp e formato nativo para importar dados com um arquivo de formato não XML
Opções **-n** e **-f** switches e **IN** comme.  No prompt de comando, digite os seguintes comandos:

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myNative;"

REM Import data
bcp TestDatabase.dbo.myNative IN D:\BCP\myNative.bcp -f D:\BCP\myNative.fmt -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myNative;"
```

### <a name="using-bulk-insert-and-native-format-without-a-format-file"></a>Usar BULK INSERT e formato nativo sem um arquivo de formato
Argumento **DATAFILETYPE** .  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):

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

### <a name="using-bulk-insert-and-native-format-with-a-non-xml-format-file"></a>Usar BULK INSERT e formato nativo com um arquivo de formato não XML
Argumento **FORMATFILE** .  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):

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

### <a name="using-openrowset-and-native-format-with-a-non-xml-format-file"></a>Usar OPENROWSET e formato nativo com um arquivo de formato não XML
Argumento **FORMATFILE** .  Execute o seguinte comando Transact-SQL no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):

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
  
## <a name="related-tasks"></a>Tarefas relacionadas
Para usar formatos de dados para importação ou exportação em massa 
  
-   [Importar dados de formato de caractere e nativo de versões anteriores do SQL Server](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Usar o formato de caractere para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato de caractere Unicode para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo Unicode para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>Confira também  
 [Utilitário bcp](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)   
 [Importar dados de formato de caractere e nativo de versões anteriores do SQL Server](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Usar o formato nativo Unicode para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
  
