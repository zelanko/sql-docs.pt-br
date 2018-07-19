---
title: BULK INSERT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/09/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- BULK_TSQL
- BULK INSERT
- BULK_INSERT_TSQL
- BULK
dev_langs:
- TSQL
helpviewer_keywords:
- tables [SQL Server], importing data into
- inserting files
- views [SQL Server], importing data into
- BULK INSERT statement
- views [SQL Server], exporting data from
- importing data, bulk import
- bulk importing [SQL Server], BULK INSERT statement
- file importing [SQL Server]
ms.assetid: be3984e1-5ab3-4226-a539-a9f58e1e01e2
caps.latest.revision: 153
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 91e2501a500df7e6536f48f3ac3f17a12aad3b67
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37782667"
---
# <a name="bulk-insert-transact-sql"></a>BULK INSERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Importa um arquivo de dados para uma tabela ou exibição de banco de dados em um formato especificado pelo usuário no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
BULK INSERT   
   [ database_name . [ schema_name ] . | schema_name . ] [ table_name | view_name ]   
      FROM 'data_file'   
     [ WITH   
    (   
   [ [ , ] BATCHSIZE = batch_size ]   
   [ [ , ] CHECK_CONSTRAINTS ]   
   [ [ , ] CODEPAGE = { 'ACP' | 'OEM' | 'RAW' | 'code_page' } ]   
   [ [ , ] DATAFILETYPE =   
      { 'char' | 'native'| 'widechar' | 'widenative' } ]   
   [ [ , ] DATASOURCE = 'data_source_name' ]
   [ [ , ] ERRORFILE = 'file_name' ]
   [ [ , ] ERRORFILE_DATA_SOURCE = 'data_source_name' ]   
   [ [ , ] FIRSTROW = first_row ]   
   [ [ , ] FIRE_TRIGGERS ]   
   [ [ , ] FORMATFILE_DATASOURCE = 'data_source_name' ]
   [ [ , ] KEEPIDENTITY ]   
   [ [ , ] KEEPNULLS ]   
   [ [ , ] KILOBYTES_PER_BATCH = kilobytes_per_batch ]   
   [ [ , ] LASTROW = last_row ]   
   [ [ , ] MAXERRORS = max_errors ]   
   [ [ , ] ORDER ( { column [ ASC | DESC ] } [ ,...n ] ) ]   
   [ [ , ] ROWS_PER_BATCH = rows_per_batch ]   
   [ [ , ] ROWTERMINATOR = 'row_terminator' ]   
   [ [ , ] TABLOCK ]   

   -- input file format options
   [ [ , ] FORMAT = 'CSV' ]
   [ [ , ] FIELDQUOTE = 'quote_characters']
   [ [ , ] FORMATFILE = 'format_file_path' ]   
   [ [ , ] FIELDTERMINATOR = 'field_terminator' ]   
   [ [ , ] ROWTERMINATOR = 'row_terminator' ]   
    )]   
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 É o nome do banco de dados no qual a tabela ou a exibição especificada reside. Se não for especificado, ele será o banco de dados atual.  
  
 *schema_name*  
 É o nome do esquema da tabela ou exibição. *schema_name* será opcional se o esquema padrão do usuário que está executando a operação de importação em massa for o esquema da tabela ou exibição especificada. Se *schema* não for especificado e o esquema padrão do usuário que está executando a operação de importação em massa for diferente da tabela ou exibição especificada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará uma mensagem de erro e a operação de importação em massa será cancelada.  
  
 *table_name*  
 É o nome da tabela ou exibição para a qual os dados serão importados em massa. Só podem ser usadas exibições nas quais todas as colunas se referem à mesma tabela base. Para obter mais informações sobre as restrições para carregar dados em exibições, veja [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md).  
  
 **'** *data_file* **'**  
 É o caminho completo do arquivo de dados que contém dados a serem importados na tabela ou exibição especificada. BULK INSERT pode importar dados de um disco (inclusive rede, disco flexível, disco rígido e assim por diante).   
 
 *data_file* deve especificar um caminho válido do servidor no qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executado. Se *data_file* for um arquivo remoto, especifique o nome UNC. Um nome UNC tem a forma \\\\*Systemname*\\*ShareName*\\*Path*\\*FileName*. Por exemplo, `\\SystemX\DiskZ\Sales\update.txt`.   
**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Começando com o [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP1.1, o data_file pode estar localizado no Armazenamento de Blobs do Azure.

**'** *data_source_name* **'**   
**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
É uma fonte de dados externa nomeada apontando para o local de Armazenamento de Blobs do Azure do arquivo que será importado. A fonte de dados externa deve ser criada usando a opção `TYPE = BLOB_STORAGE` adicionada no [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1. Para obter mais informações, consulte [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).    
  
 BATCHSIZE **=***batch_size*  
 Especifica o número de linhas em um lote. Cada lote é copiado para o servidor como uma transação. Em caso de falha, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] confirmará ou reverterá a transação para cada lote. Por padrão, todos os dados no arquivo de dados especificado são um lote. Para obter informações sobre considerações de desempenho, consulte “Comentários”, posteriormente neste tópico.  
  
 CHECK_CONSTRAINTS  
 Especifica que todas as restrições na tabela ou exibição de destino devem ser verificadas durante a operação de importação em massa. Sem a opção CHECK_CONSTRAINTS, quaisquer restrições CHECK e FOREIGN KEY são ignoradas e, depois da operação, a restrição na tabela é marcada como não confiável.  
  
> [!NOTE]  
>  As restrições UNIQUE e PRIMARY KEY são sempre impostas. Durante a importação para uma coluna de caracteres que é definida com uma restrição NOT NULL, BULK INSERT insere uma cadeia de caracteres em branco quando não há um valor no arquivo de texto.  
  
 Em algum momento, você deve examinar as restrições na tabela inteira. Se a tabela não estiver vazia antes da operação de importação em massa, o custo de revalidação da restrição poderá exceder o custo da aplicação de restrições CHECK aos dados incrementais.  
  
 Uma situação na qual talvez você queira desabilitar as restrições (o comportamento padrão) é quando os dados de entrada contiverem linhas que violam as restrições. Com as restrições CHECK desabilitadas, é possível importar os dados e usar instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] para remover os dados inválidos.  
  
> [!NOTE]  
>  A opção de MAXERRORS não se aplica à verificação de restrição.  
  
 CODEPAGE **=** { **'** ACP **'** | **'** OEM **'** | **'** RAW **'** | **'***code_page***'** }  
 Especifica a página de código dos dados no arquivo de dados. CODEPAGE só será relevante se os dados contiverem colunas **char**, **varchar** ou **text** com valores de caractere maiores que **127** ou menores que **32**.  

> [!IMPORTANT]
> CODEPAGE não é uma opção compatível com o Linux.

> [!NOTE]  
>  A [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que você especifique um nome de agrupamento para cada coluna em um [arquivo de formato](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md).  
  
|Valor de CODEPAGE|Descrição|  
|--------------------|-----------------|  
|ACP|Colunas do tipo de dados **char**, **varchar** ou **text** são convertidas da página de código do Windows [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]/[!INCLUDE[msCoName](../../includes/msconame-md.md)] (ISO 1252) na página de código do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|OEM (padrão)|Colunas do tipo de dados **char**, **varchar** ou **text** são convertidas da página de código de OEM do sistema para a página de código [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|RAW|Nenhuma conversão de uma página de código em outra ocorre; essa opção é a mais rápida.|  
|*code_page*|Especifique o número da página de código, por exemplo, 850.<br /><br /> **\*\* Importante \*\*** As versões anteriores à [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] não dão suporte à página de código 65001 (codificação UTF-8).|  
  
 DATAFILETYPE **=** { **'char'** | **'native'** | **'widechar'** | **'widenative'** }  
 Especifica que BULK INSERT executa a operação de importação usando o valor de tipo de arquivo de dados especificado.  
  
|Valor DATAFILETYPE|Todos os dados representados em:|  
|------------------------|------------------------------|  
|**char** (padrão)|Formato de caractere.<br /><br /> Para obter mais informações, veja [Usar o formato de caractere para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md).|  
|**native**|Tipos de dados (banco de dados) nativo. Crie o arquivo de dados nativo importando dados em massa do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o utilitário **bcp**.<br /><br /> O valor nativo oferece uma alternativa de alto desempenho ao valor char.<br /><br /> Para obter mais informações, veja [Usar o formato nativo para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md).|  
|**widechar**|Caracteres unicode.<br /><br /> Para obter mais informações, consulte [Usar o formato de caractere Unicode para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md).|  
|**widenative**|Tipos de dados nativos (banco de dados), exceto nas colunas **char**, **varchar** e **text** colunas, em que os dados são armazenados como Unicode. Crie o arquivo de dados **widenative** importando dados em massa do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o utilitário **bcp**.<br /><br /> O valor **widenative** oferece uma alternativa de alto desempenho para **widechar**. Se o arquivo de dados contiver caracteres [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)] estendidos, especifique **widenative**.<br /><br /> Para obter mais informações, veja [Usar o formato nativo Unicode para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md).|  
  
  ERRORFILE **='***file_name***'**  
 Especifica o arquivo usado para coletar linhas com erros de formatação e que não podem ser convertidas em um conjunto de linhas OLE DB. Essas linhas são copiadas do arquivo de dados para esse arquivo de erro "no estado em que se encontram".  
  
 O arquivo de erro é criado quando o comando é executado. Ocorrerá um erro se o arquivo já existir. Além disso, é criado um arquivo de controle com a extensão .ERROR.txt. Ele faz referência a cada linha do arquivo de erro e fornece um diagnóstico de erros. Assim que os erros forem corrigidos, os dados poderão ser carregados.   
**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
Começando pelo [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)], o `error_file_path` pode estar no Armazenamento de Blobs do Azure.

'errorfile_data_source_name'   
**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
É uma fonte de dados externa nomeada que aponta para o local de Armazenamento de Blobs do Azure do arquivo de erro que conterá os erros encontrados durante a importação. A fonte de dados externa deve ser criada usando a opção `TYPE = BLOB_STORAGE` adicionada no [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1. Para obter mais informações, consulte [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).
 
 FIRSTROW **=***first_row*  
 Especifica o número da primeira linha a carregar. O padrão é a primeira linha no arquivo de dados especificado. FIRSTROW tem base 1.  
  
> [!NOTE]  
>  O atributo FIRSTROW não tem o objetivo de ignorar cabeçalhos de coluna. Não há suporte para ignorar cabeçalhos por parte da instrução BULK INSERT. Ao ignorar linhas, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] examina somente os terminadores de campo e não valida os dados nos campos das linhas ignoradas.  
  
 FIRE_TRIGGERS  
 Especifica que qualquer gatilho de inserção definido na tabela de destino seja executado durante a operação de importação em massa. Se os gatilhos forem definidos para operações INSERT na tabela de destino, eles serão disparados para cada lote concluído.  
  
 Se FIRE_TRIGGERS não for especificado, nenhum gatilho de inserção será executado.  

FORMATFILE_DATASOURCE **=** 'data_source_name'   
**Aplica-se a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 1.1.   
É uma fonte de dados externa nomeada que está apontando para o local de Armazenamento de Blobs do Azure do formato de arquivo que define o esquema de dados importados. A fonte de dados externa deve ser criada usando a opção `TYPE = BLOB_STORAGE` adicionada no [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1. Para obter mais informações, consulte [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).
  
 KEEPIDENTITY  
 Especifica que o valor, ou valores, de identidade no arquivo de dados importado deve ser usado para a coluna de identidade. Se KEEPIDENTITY não for especificado, os valores de identidade dessa coluna serão verificados, mas não importados e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atribuirá valores exclusivos automaticamente com base nos valores de semente e de incremento especificados durante a criação da tabela. Se o arquivo de dados não contiver valores para a coluna de identidade na tabela ou exibição, use um arquivo de formato para especificar que a coluna de identidade na tabela ou exibição deve ser ignorada ao importar dados. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atribui valores exclusivos para a coluna automaticamente. Para obter mais informações, veja [DBCC CHECKIDENT &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md).  
  
 Para obter mais informações, veja como manter identificar valores, em [Manter valores de identidade ao importar dados em massa &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md).  
  
 KEEPNULLS  
 Especifica que colunas vazias devem reter um valor nulo durante a operação de importação em massa, em vez de ter qualquer valor padrão para as colunas inseridas. Para obter mais informações, veja [Manter valores nulos ou usar os valores padrão durante a importação em massa &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md).  
  
 KILOBYTES_PER_BATCH **=** *kilobytes_per_batch*  
 Especifica o número aproximado de KB (kilobytes) de dados por lote como *kilobytes_per_batch*. Por padrão, KILOBYTES_PER_BATCH é desconhecido. Para obter informações sobre considerações de desempenho, consulte “Comentários”, posteriormente neste tópico.  
  
 LASTROW**=***last_row*  
 Especifica o número da última linha a ser carregada. O padrão é 0, que indica a última fila no arquivo de dados especificado.  
  
 MAXERRORS **=** *max_errors*  
 Especifica o número máximo de erros de sintaxe permitido nos dados antes que a operação de importação em massa seja cancelada. Cada linha que não pode ser importada pela operação de importação em massa é ignorada e contada como um erro. Se *max_errors* não for especificado, o padrão será 10.  
  
> [!NOTE]  
>  A opção MAX_ERRORS não se aplica a verificações de restrição ou à conversão dos tipos de dados **money** e **bigint**.  
  
 ORDER ( { *column* [ ASC | DESC ] } [ **,**... *n* ] )  
 Especifica como os dados no arquivo de dados são classificados. O desempenho da importação em massa será melhorado se os dados importados forem armazenados de acordo com o índice clusterizado na tabela, se houver. Se o arquivo de dados for classificado em outra ordem, ou seja, diferente da ordem de uma chave de índice clusterizado, ou se não houver nenhum índice clusterizado na tabela, a cláusula ORDER será ignorada. Os nomes das colunas fornecidos devem ser nomes de colunas válidas na tabela de destino. Por padrão, a operação de inserção em massa supõe que o arquivo de dados não esteja ordenado. Para obter uma importação em massa otimizada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também valida que os dados importados sejam classificados.  
  
 *n*  
 É um espaço reservado que indica que várias colunas podem ser especificadas.  
  
 ROWS_PER_BATCH **=***rows_per_batch*  
 Indica o número aproximado de linhas de dados no arquivo de dados.  
  
 Por padrão, todos os dados de arquivo são enviados ao servidor como uma única transação, e o número de linhas no lote é desconhecido para o otimizador de consulta. Se você especificar ROWS_PER_BATCH (com um valor > 0), o servidor usará esse valor para otimizar a operação da importação em massa. O valor especificado para ROWS_PER_BATCH deve ser aproximadamente igual ao número real de linhas. Para obter informações sobre considerações de desempenho, consulte “Comentários”, posteriormente neste tópico.  
  
 
 TABLOCK  
 Especifica que um bloqueio no nível de tabela é adquirido durante a operação de importação em massa. Uma tabela pode ser carregada simultaneamente através de vários clientes se não tiver nenhum índice e TABLOCK for especificado. Por padrão, o comportamento de bloqueio é determinado pela opção de tabela **bloqueio de tabela em carregamento em massa**. Manter um bloqueio durante a operação de importação em massa reduz a contenção de bloqueio na tabela e em alguns casos pode melhorar significativamente o desempenho. Para obter informações sobre considerações de desempenho, consulte “Comentários”, posteriormente neste tópico.  
  
 Para o índice columnstore. o comportamento de bloqueio é diferente porque ele é dividido internamente em vários conjuntos de linhas.  Cada thread carrega dados exclusivamente em cada conjunto de linhas pegando um bloqueio X no conjunto de linhas, permitindo carregamento de dados em paralelo com sessões de carregamento de dados simultâneas. O uso da opção TABLOCK fará com que o thread pegue um bloqueio X na tabela (diferente do bloqueio BU para conjuntos de linhas tradicionais), o que impedirá que outros threads simultâneos carreguem dados simultaneamente.  

### <a name="input-file-format-options"></a>Opções de formato de arquivo de entrada
  
FORMAT **=** 'CSV'   
**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Especifica um arquivo de valores separados por vírgula em conformidade com o padrão [RFC 4180](https://tools.ietf.org/html/rfc4180).

FIELDQUOTE **=** 'field_quote'   
**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Especifica um caractere que será usado como o caractere de aspas no arquivo CSV. Se não for especificado, o caractere de aspas (") será usado como o caractere de aspas, conforme definido no padrão [RFC 4180](https://tools.ietf.org/html/rfc4180).
  
 FORMATFILE **='***format_file_path***'**  
 Especifica o caminho completo de um arquivo de formato. Um arquivo de formato descreve o arquivo de dados que contém as respostas armazenadas criadas usando o utilitário **bcp** na mesma tabela ou exibição. O arquivo de formato deverá ser usado se:  
  
-   O arquivo de dados contiver colunas maiores ou menos colunas que a tabela ou exibição.  
  
-   As colunas estiverem em uma ordem diferente.  
  
-   Os delimitadores de coluna variarem.  
  
-   Houver outras alterações no formato de dados. Os arquivos de formato em geral são criados por meio do utilitário **bcp** e modificados com um editor de texto conforme necessário. Para obter mais informações, consulte [bcp Utility](../../tools/bcp-utility.md).  

**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Começando com o [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1, o format_file_path pode estar localizado no Armazenamento de Blobs do Azure.

 FIELDTERMINATOR **='***field_terminator***'**  
 Especifica o terminador de campo a ser usado para os arquivos de dados **char** e **widechar**. O terminador de campo padrão é \t (caractere de tabulação). Para obter mais informações, veja [Especificar terminadores de campo e linha &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).  

 ROWTERMINATOR **='***row_terminator***'**  
 Especifica o terminador de linha a ser usado para os arquivos de dados **char** e **widechar**. O terminador de linha padrão é **\r\n** (caractere de nova linha).  Para obter mais informações, veja [Especificar terminadores de campo e linha &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).  

  
## <a name="compatibility"></a>Compatibilidade  
 O BULK INSERT impõe validação estrita de dados e verificações de dados lidos de um arquivo que podem provocar falha nos scripts existentes quando executadas com dados inválidos. Por exemplo, BULK INSERT verifica se:  
  
-   As representações nativa dos tipos de dados **float** ou **real** são válidas.  
  
-   Dados Unicode têm um comprimento regular de byte.  
  
## <a name="data-types"></a>Tipos de dados  
  
### <a name="string-to-decimal-data-type-conversions"></a>Conversões do tipo de dados de cadeia de caracteres em decimal  
 As conversões do tipo de dados de cadeia de caracteres em decimal usada em BULK INSERT seguem as mesmas regras que a função [!INCLUDE[tsql](../../includes/tsql-md.md)] [CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md), que rejeita cadeias de caracteres que representam valores numéricos que usam notação científica. Portanto, BULK INSERT trata essas cadeias de caracteres como valores inválidos e relata erros de conversão.  
  
 Como solução alternativa para esse comportamento, use um arquivo de formato para importar em massa dados **float** de notação científica em uma coluna decimal. No arquivo de formato, descreva explicitamente a coluna como de dados **reais** ou **float**. Para obter mais informações sobre esses tipos de dados, veja [float e real &#40;Transact-SQL&#41;](../../t-sql/data-types/float-and-real-transact-sql.md).  
  
> [!NOTE]  
>  Arquivos de formato representam dados **real** como o **SQLFLT4** tipo de dados e dados **float** como o tipo de dados **SQLFLT8**. Para obter informações sobre arquivos de formato não XML, veja [Especificar o tipo de armazenamento de arquivos usando bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md).  
  
#### <a name="example-of-importing-a-numeric-value-that-uses-scientific-notation"></a>Exemplo de importação de um valor numérico que usa notação científica  
 Este exemplo usa a seguinte tabela:  
  
```  
CREATE TABLE t_float(c1 float, c2 decimal (5,4));  
```  
  
 O usuário quer importar dados em massa para a tabela `t_float`. O arquivo de dados, C:\t_float-c.dat, contém dados **float** de notação científica, por exemplo:  
  
```  
8.0000000000000002E-28.0000000000000002E-2  
```  
  
 Entretanto, BULK INSERT não pode importar esses dados diretamente em `t_float`, porque sua segunda coluna, `c2`, usa o tipo de dados `decimal`. Portanto, um arquivo de formato é necessário. O arquivo de formato deve mapear os dados **float** de notação científica para o formato decimal de coluna `c2`.  
  
 O arquivo de formato a seguir usa o tipo de dados `SQLFLT8` para mapear o segundo campo de dados para a segunda coluna:  
  
 ```
 <?xml version="1.0"?> 
 <BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"> 
 <RECORD> 
 <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="\t" MAX_LENGTH="30"/> 
 <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="30"/>  </RECORD>  <ROW> 
 <COLUMN SOURCE="1" NAME="c1" xsi:type="SQLFLT8"/> 
 <COLUMN SOURCE="2" NAME="c2" xsi:type="SQLFLT8"/>  </ROW> </BCPFORMAT> 
 ```
  
 Para usar esse arquivo de formato (usando o nome de arquivo `C:\t_floatformat-c-xml.xml`) ao importar os dados de teste para a tabela de teste, emita a seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
```  
BULK INSERT bulktest..t_float  
FROM 'C:\t_float-c.dat' WITH (FORMATFILE='C:\t_floatformat-c-xml.xml');  
GO  
```  
  
### <a name="data-types-for-bulk-exporting-or-importing-sqlxml-documents"></a>Tipos de dados para exportação ou importação em massa de documentos SQLXML  
 Para exportar ou importar dados SQLXML em massa, use um dos tipos de dados a seguir em seu arquivo de formato:  
  
|Tipo de dados|Efeito|  
|---------------|------------|  
|SQLCHAR ou SQLVARCHAR|Os dados são enviados na página de código do cliente ou na página de código implicada pelo agrupamento. O efeito é o mesmo que especificar DATAFILETYPE **='char'** sem especificar um arquivo de formato.|  
|SQLNCHAR ou SQLNVARCHAR|Os dados são enviados como Unicode. O efeito é o mesmo que especificar DATAFILETYPE **= 'widechar'** sem especificar um arquivo de formato.|  
|SQLBINARY ou SQLVARBIN|Os dados são enviados sem qualquer conversão.|  
  
## <a name="general-remarks"></a>Comentários gerais  
 Para obter uma comparação da instrução BULK INSERT, da instrução INSERT ... Instrução SELECT \* FROM OPENROWSET(BULK...) e o comando **bcp**, veja [Importação e exportação em massa de dados &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md).  
  
 Para obter informações sobre como preparar dados para importação em massa, veja [Preparar dados para exportação ou importação em massa &#40;SQL Server&#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).  
  
 A instrução BULK INSERT pode ser executada dentro de uma transação definida pelo usuário para importar dados em uma tabela ou exibição. Opcionalmente, para usar várias correspondências para obter dados de importação em massa, uma transação pode especificar a cláusula BATCHSIZE na instrução de BULK INSERT. Se uma transação de vários lotes for revertida, todo o lote enviado pela transação ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será revertido.  
  
## <a name="interoperability"></a>Interoperabilidade  
  
### <a name="importing-data-from-a-csv-file"></a>Importando dados de um arquivo CSV  
Começando com o [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1, BULK INSERT é compatível com o formato CSV.  
Antes do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1, arquivos CSV (valores separados por vírgula) não eram compatíveis com operações de importação em massa do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No entanto, em alguns casos, um arquivo CSV pode ser usado como o arquivo de dados para uma importação em massa de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter informações sobre os requisitos para importar dados de um arquivo de dados CSV, veja [Preparar dados para exportação ou importação em massa &#40;SQL Server&#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).  
  
## <a name="logging-behavior"></a>Comportamento de log  
 Para obter informações sobre quando as operações de inserção de linhas executadas por importações em massa são registradas no log de transações, veja [Pré-requisitos para log mínimo em importação em massa](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
##  <a name="Limitations"></a> Restrições  
 Ao usar um arquivo de formato com BULK INSERT, você pode especificar até somente 1024 campos. Isso é o mesmo que o número máximo de colunas permitido em uma tabela. Se você usar BULK INSERT com um arquivo de dados que contém mais de 1024 campos, o BULK INSERT gerará o erro 4822. O [utilitário bcp](../../tools/bcp-utility.md) não tem esta limitação, portanto, para arquivos de dados que contêm mais de 1024 campos, use o comando **bcp**.  
  
## <a name="performance-considerations"></a>Considerações sobre desempenho  
 Se o número de páginas a ser liberado em um único lote exceder um limite interno, poderá ocorrer um exame completo do pool de buffers para identificar quais páginas devem ser liberadas quando o lote for confirmado. Esse exame completo pode prejudicar o desempenho da importação em massa. Um caso provável de exceder o limite interno ocorre quando um pool de buffers grande é combinado com um subsistema de E/S lento. Para evitar estouros de buffer em máquinas grandes, não use a dica TABLOCK (que removerá as otimizações em massa) ou use um tamanho de lote menor (que preserva as otimizações em massa).  
  
 Como os computadores variam, é recomendável testar vários tamanhos de lote com seu carregamento de dados para descobrir o que funciona melhor para você.  
  
## <a name="security"></a>Segurança  
  
### <a name="security-account-delegation-impersonation"></a>Delegação de conta de segurança (representação)  
 Se um usuário usar um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o perfil de segurança da conta de processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será usado. Um logon que usa a autenticação do SQL Server não pode ser autenticado fora do Mecanismo de Banco de Dados. Assim, quando um comando BULK INSERT é iniciado por um logon que usa a autenticação do SQL Server, a conexão aos dados é feita por meio do contexto de segurança da conta de processo do SQL Server (a conta usada pelo serviço de Mecanismo de Banco de Dados do SQL Server). Para ler a fonte de dados com êxito, você deve dar à conta usada pelo Mecanismo de Banco de Dados do SQL Server acesso ao banco de dados. Em contrapartida, se um usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fizer logon por meio da Autenticação do Windows, ele poderá acessar, no modo somente leitura, aqueles arquivos que podem ser acessados pela conta do usuário, a despeito do perfil de segurança do processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Durante a execução da instrução BULK INSERT usando **sqlcmd** ou **osql**, de um computador, durante a inserção de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um segundo computador e durante a especificação de um *data_file* em um terceiro computador por meio de um caminho UNC, você poderá receber um erro 4861.  
  
 Para resolver esse erro, use a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e especifique um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que use o perfil de segurança da conta de processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ou configure o Windows para habilitar a delegação de conta de segurança. Para obter informações sobre como habilitar uma conta de usuário que seja confiável para a delegação, consulte a Ajuda do Windows.  
  
 Para obter mais informações sobre estas e outras considerações de segurança para usar BULK INSERT, veja [Importação de dados em massa usando BULK INSERT ou OPENROWSET&#40;BULK...&#41; &#40;SQL Server&#41;](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).  
  
### <a name="permissions"></a>Permissões  
 Requer as permissões INSERT e ADMINISTER BULK OPERATIONS. No Banco de Dados SQL do Azure, são necessárias permissões de INSERT e ADMINISTER DATABASE BULK OPERATIONS. Além disso, a permissão ALTER TABLE será necessária se uma ou mais das seguintes afirmações for verdadeira:  
  
-   Existem restrições e a opção CHECK_CONSTRAINTS não foi especificada.  
  
    > [!NOTE]  
    >  Desabilitar restrições é o comportamento padrão. Para verificar as restrições explicitamente, use a opção CHECK_CONSTRAINTS.  
  
-   Existem gatilhos e a opção FIRE_TRIGGER não foi especificada.  
  
    > [!NOTE]  
    >  Por padrão, os gatilhos não são disparados. Para disparar gatilhos explicitamente, use a opção FIRE_TRIGGER.  
  
-   Use a opção KEEPIDENTITY para importar valor de identidade do arquivo de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-pipes-to-import-data-from-a-file"></a>A. Usando pipes para importar dados de um arquivo  
 O exemplo a seguir importa informações sobre detalhes de pedidos para a tabela `AdventureWorks2012.Sales.SalesOrderDetail` do arquivo de dados especificado usando um pipe (`|`) como terminador de campo e `|\n` como terminador de linha.  
  
```  
BULK INSERT AdventureWorks2012.Sales.SalesOrderDetail  
   FROM 'f:\orders\lineitem.tbl'  
   WITH   
      (  
         FIELDTERMINATOR =' |',  
         ROWTERMINATOR =' |\n'  
      );  
```  
  
### <a name="b-using-the-firetriggers-argument"></a>B. Usando o argumento FIRE_TRIGGERS  
 O exemplo a seguir especifica o argumento `FIRE_TRIGGERS`.  
  
```  
BULK INSERT AdventureWorks2012.Sales.SalesOrderDetail  
   FROM 'f:\orders\lineitem.tbl'  
   WITH  
     (  
        FIELDTERMINATOR =' |',  
        ROWTERMINATOR = ':\n',  
        FIRE_TRIGGERS  
      );  
```  
  
### <a name="c-using-line-feed-as-a-row-terminator"></a>C. Usando alimentação de linha como um terminador de linha  
 O exemplo a seguir importa um arquivo que usa a alimentação de linha como um terminador de linha, como uma saída UNIX:  
  
```  
DECLARE @bulk_cmd varchar(1000);  
SET @bulk_cmd = 'BULK INSERT AdventureWorks2012.Sales.SalesOrderDetail  
FROM ''<drive>:\<path>\<filename>''   
WITH (ROWTERMINATOR = '''+CHAR(10)+''')';  
EXEC(@bulk_cmd);  
```  
  
> [!NOTE]  
>  Devido ao modo como o Microsoft Windows trata arquivos de texto, **(\n** automaticamente é substituído por **\r\n)**.  
  
### <a name="d-specifying-a-code-page"></a>D. Especificando uma página de código  
 O exemplo a seguir mostra como especificar uma página de código.  
  
```  
BULK INSERT MyTable  
FROM 'D:\data.csv'  
WITH  
( CODEPAGE = '65001',  
    DATAFILETYPE = 'char',  
    FIELDTERMINATOR = ','  
);  
```  
### <a name="e-importing-data-from-a-csv-file"></a>E. Importando dados de um arquivo CSV   
O exemplo a seguir mostra como especificar um arquivo CSV.   
```
BULK INSERT Sales.Invoices
FROM '\\share\invoices\inv-2016-07-25.csv'
WITH (FORMAT = 'CSV'); 
```

### <a name="f-importing-data-from-a-file-in-azure-blob-storage"></a>F. Importando dados de um arquivo no Armazenamento de Blobs do Azure   
O exemplo a seguir mostra como carregar dados de um arquivo CSV em um local de Armazenamento de Blobs do Azure, que foi configurado como uma fonte de dados externa. Isso requer uma credencial no escopo do banco de dados usando uma Assinatura de Acesso Compartilhado.    

```sql
BULK INSERT Sales.Invoices
FROM 'inv-2017-01-19.csv'
WITH (DATA_SOURCE = 'MyAzureInvoices',
     FORMAT = 'CSV'); 
```

### <a name="g-importing-data-from-a-file-in-azure-blob-storage-and-specifying-an-error-file"></a>G. Importando dados de um arquivo no armazenamento de blobs do Azure e especificando um arquivo de erro   
O exemplo a seguir mostra como carregar dados de um arquivo CSV em um local de Armazenamento de Blobs do Azure, que foi configurado como uma fonte de dados externa e também especificar um arquivo de erro. Isso requer uma credencial no escopo do banco de dados usando uma Assinatura de Acesso Compartilhado. Observe que, se for executada no Banco de Dados SQL, a opção ERRORFILE deverá vir acompanhada de ERRORFILE_DATA_SOURCE; caso contrário, a importação poderá falhar com um erro de permissões. O arquivo especificado em ERRORFILE não deve existir no contêiner.

```sql
BULK INSERT Sales.Invoices
FROM 'inv-2017-01-19.csv'
WITH (DATA_SOURCE = 'MyAzureInvoices',
     FORMAT = 'CSV',
     ERRORFILE = 'MyErrorFile',
     ERRORFILE_DATA_SOURCE = 'MyAzureInvoices'); 
```

Para obter exemplos de `BULK INSERT` completos, incluindo a configuração da credencial e da fonte de dados externa, consulte [Exemplos de acesso em massa a dados no Armazenamento de Blobs do Azure](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md).
  
### <a name="additional-examples"></a>Exemplos adicionais  
 Outros exemplos `BULK INSERT` são fornecidos nos tópicos a seguir:  
  
-   [Exemplos de importação e exportação em massa de documentos XML &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [Manter valores de identidade ao importar dados em massa &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [Manter valores nulos ou use os valores padrão durante a importação em massa &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [Especificar terminadores de campo e linha &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)  
  
-   [Usar um arquivo de formato para importação em massa de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Usar o formato de caractere para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato de caractere Unicode para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo Unicode para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar um arquivo de formato para ignorar uma coluna de tabela &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [Usar um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Importação e exportação em massa de dados &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [Utilitário bcp](../../tools/bcp-utility.md)   
 [Arquivos de formato para importação ou exportação de dados &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Preparar dados para importação ou exportação em massa &#40;SQL Server&#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)   
 [sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)  
  
  
