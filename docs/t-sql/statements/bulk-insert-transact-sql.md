---
title: "A inserção em MASSA (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 01/04/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 80b16fd446ff72c6a673a576d9a8deb9514be8b2
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="bulk-insert-transact-sql"></a>BULK INSERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Importa um arquivo de dados para uma tabela ou exibição de banco de dados em um formato especificado pelo usuário no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
   [ [ , ] ERRORFILE_DATASOURCE = 'data_source_name' ]   
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
 É o nome do banco de dados no qual a tabela ou exibição especificada reside. Se não for especificado, ele será o banco de dados atual.  
  
 *schema_name*  
 É o nome do esquema da tabela ou exibição. *schema_name* é opcional se o esquema padrão para o usuário que está executando a operação de importação em massa for o esquema da tabela especificada ou exibição. Se *esquema* não for especificado e o esquema padrão do usuário que está executando a operação de importação em massa é diferente da tabela especificada ou exibição, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará uma mensagem de erro e a operação de importação em massa será cancelada.  
  
 *table_name*  
 É o nome da tabela ou exibição para a qual os dados serão importados em massa. Só podem ser usadas exibições nas quais todas as colunas se referem à mesma tabela base. Para obter mais informações sobre as restrições de carregamento de dados em exibições, consulte [INSERT &#40; Transact-SQL &#41; ](../../t-sql/statements/insert-transact-sql.md).  
  
 **'** *data_file* **'**  
 É o caminho completo do arquivo de dados que contém dados a serem importados na tabela ou exibição especificada. BULK INSERT pode importar dados de um disco (inclusive rede, disco flexível, disco rígido e assim por diante).   
 
 *data_file* deve especificar um caminho válido do servidor no qual [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução. Se *data_file* é remoto do arquivo, especifique o nome de convenção de nomenclatura Universal (UNC). Um nome UNC tem a forma \\ \\ *Systemname*\\*ShareName*\\*caminho* \\ *FileName*. Por exemplo, `\\SystemX\DiskZ\Sales\update.txt`.   
**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Começando com [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP1.1, o data_file pode ser no armazenamento de BLOBs do Azure.

**'** *data_source_name* **'**   
**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Uma fonte de dados externa nomeada está apontando para o local de armazenamento de BLOBs do Azure do arquivo que será importado. Fonte de dados externa deve ser criada usando o `TYPE = BLOB_STORAGE` opção adicionada no [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1. Para obter mais informações, consulte [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).    
  
 BATCHSIZE  **=**  *batch_size*  
 Especifica o número de linhas em um lote. Cada lote é copiado para o servidor como uma transação. Em caso de falha, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] confirmará ou reverterá a transação para cada lote. Por padrão, todos os dados no arquivo de dados especificado são um lote. Para obter informações sobre considerações de desempenho, consulte “Comentários”, posteriormente neste tópico.  
  
 CHECK_CONSTRAINTS  
 Especifica que todas as restrições na tabela ou exibição de destino devem ser verificadas durante a operação de importação em massa. Sem a opção CHECK_CONSTRAINTS, quaisquer restrições CHECK e FOREIGN KEY são ignoradas e, depois da operação, a restrição na tabela é marcada como não confiável.  
  
> [!NOTE]  
>  Restrições UNIQUE e PRIMARY KEY são sempre impostas. Durante a importação para uma coluna de caracteres que é definida com uma restrição NOT NULL, BULK INSERT insere uma cadeia de caracteres em branco quando não há um valor no arquivo de texto.  
  
 Em algum momento, você deve examinar as restrições na tabela inteira. Se a tabela não vazia antes da operação de importação em massa, o custo de revalidação da restrição poderá exceder o custo da aplicação de restrições CHECK aos dados incrementais.  
  
 Uma situação na qual talvez você queira desabilitar as restrições (o comportamento padrão) é quando os dados de entrada contiverem linhas que violam as restrições. Com as restrições CHECK desabilitadas, você pode importar os dados e, em seguida, usar [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções para remover os dados inválidos.  
  
> [!NOTE]  
>  A opção de MAXERRORS não se aplica à verificação de restrição.  
  
 Página de código  **=**  { **'**ACP**'** | **'**OEM**'**  |  **'**RAW**'** | **'***code_page***'** }  
 Especifica a página de código dos dados no arquivo de dados. Página de código é relevante apenas se os dados contiverem **char**, **varchar**, ou **texto** colunas com valores de caractere maiores que **127** ou menos que **32**.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)]recomenda que você especifique um nome de agrupamento para cada coluna em uma [arquivo de formato](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md).  
  
|Valor de CODEPAGE|Description|  
|--------------------|-----------------|  
|ACP|Colunas de **char**, **varchar**, ou **texto** tipo de dados são convertidos a partir de [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)] / [!INCLUDE[msCoName](../../includes/msconame-md.md)] página de código do Windows (ISO 1252) para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] página de código.|  
|OEM (padrão)|Colunas de **char**, **varchar**, ou **texto** tipo de dados são convertidos da página de código OEM do sistema para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] página de código.|  
|RAW|Nenhuma conversão de uma página de código em outra ocorre; essa opção é a mais rápida.|  
|*code_page*|Número de página de código específico, por exemplo, 850.<br /><br /> **\*\*Importante \* \***  versões anteriores ao [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] não oferecem suporte a página de código 65001 (codificação UTF-8).|  
  
 DATAFILETYPE  **=**  { **'char'** | **'native'** | **'widechar'**  |  **'widenative'** }  
 Especifica que BULK INSERT executa a operação de importação usando o valor de tipo de arquivo de dados especificado.  
  
|Valor DATAFILETYPE|Todos os dados representados em:|  
|------------------------|------------------------------|  
|**char** (padrão)|Formato de caractere.<br /><br /> Para obter mais informações, veja [Usar o formato de caractere para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md).|  
|**nativo**|Tipos de dados (banco de dados) nativo. Criar o arquivo de dados nativos, os dados de importação em massa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o **bcp** utilitário.<br /><br /> O valor nativo oferece uma alternativa de alto desempenho ao valor char.<br /><br /> Para obter mais informações, veja [Usar o formato nativo para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md).|  
|**widechar**|Caracteres unicode.<br /><br /> Para obter mais informações, consulte [Usar o formato de caractere Unicode para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md).|  
|**widenative**|Tipos de dados nativos (banco de dados), exceto em **char**, **varchar**, e **texto** colunas, na qual os dados são armazenados como Unicode. Criar o **widenative** arquivo de dados pelos dados de importação em massa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o **bcp** utilitário.<br /><br /> O **widenative** valor oferece uma alternativa de alto desempenho para **widechar**. Se o arquivo de dados contiver [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)] caracteres estendidos, especifique **widenative**.<br /><br /> Para obter mais informações, veja [Usar o formato nativo Unicode para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md).|  
  
  ERRORFILE **='***file_name***'**  
 Especifica o arquivo usado para coletar linhas com erros de formatação e que não podem ser convertidas em um conjunto de linhas OLE DB. Essas linhas são copiadas do arquivo de dados para esse arquivo de erro "no estado em que se encontram".  
  
 O arquivo de erro é criado quando o comando é executado. Ocorrerá um erro se o arquivo já existir. Além disso, é criado um arquivo de controle com a extensão .ERROR.txt. Ele faz referência a cada linha do arquivo de erro e fornece um diagnóstico de erros. Assim que os erros forem corrigidos, os dados poderão ser carregados.   
**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
Começando com [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)], o `error_file_path` pode estar no armazenamento de BLOBs do Azure.

'errorfile_data_source_name'   
**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
Uma fonte de dados externa nomeada está apontando para o local de armazenamento de BLOBs do Azure do arquivo de erro que conterá os erros encontrados durante a importação. Fonte de dados externa deve ser criada usando o `TYPE = BLOB_STORAGE` opção adicionada no [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1. Para obter mais informações, consulte [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).
 
 FIRSTROW  **=**  *first_row*  
 Especifica o número da primeira linha a carregar. O padrão é a primeira linha no arquivo de dados especificado. FIRSTROW tem base 1.  
  
> [!NOTE]  
>  O atributo FIRSTROW não tem o objetivo de ignorar cabeçalhos de coluna. Não há suporte para ignorar cabeçalhos por parte da instrução BULK INSERT. Ao ignorar linhas, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] examina somente os terminadores de campo e não valida os dados nos campos das linhas ignoradas.  
  
 FIRE_TRIGGERS  
 Especifica que qualquer gatilho de inserção definido na tabela de destino seja executado durante a operação de importação em massa. Se os gatilhos forem definidos para operações INSERT na tabela de destino, eles serão disparados para cada lote concluído.  
  
 Se FIRE_TRIGGERS não for especificado, nenhum gatilho de inserção será executado.  

FORMATFILE_DATASOURCE  **=**  'data_source_name'   
**Aplica-se a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 1.1.   
Uma fonte de dados externa nomeada está apontando para o local de armazenamento de BLOBs do Azure do formato de arquivo que define o esquema de dados importados. Fonte de dados externa deve ser criada usando o `TYPE = BLOB_STORAGE` opção adicionada no [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1. Para obter mais informações, consulte [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).
  
 KEEPIDENTITY  
 Especifica que o valor, ou valores, de identidade no arquivo de dados importado deve ser usado para a coluna de identidade. Se KEEPIDENTITY não for especificado, os valores de identidade dessa coluna serão verificados, mas não importados e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atribuirá valores exclusivos automaticamente com base nos valores de semente e de incremento especificados durante a criação da tabela. Se o arquivo de dados não contiver valores para a coluna de identidade na tabela ou exibição, use um arquivo de formato para especificar que a coluna de identidade na tabela ou exibição deve ser ignorada ao importar dados. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atribui automaticamente valores exclusivos para a coluna. Para obter mais informações, veja [DBCC CHECKIDENT &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md).  
  
 Para obter mais informações, consulte sobre como manter identificar valores, consulte [manter identidade valores quando dados em massa importando &#40; SQL Server &#41; ](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md).  
  
 KEEPNULLS  
 Especifica que colunas vazias devem reter um valor nulo durante a operação de importação em massa, em vez de ter qualquer valor padrão para as colunas inseridas. Para obter mais informações, veja [Manter valores nulos ou usar os valores padrão durante a importação em massa &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md).  
  
 KILOBYTES_PER_BATCH  **=**  *kilobytes_per_batch*  
 Especifica o número aproximado de kilobytes (KB) de dados por lote como *kilobytes_per_batch*. Por padrão, KILOBYTES_PER_BATCH é desconhecido. Para obter informações sobre considerações de desempenho, consulte “Comentários”, posteriormente neste tópico.  
  
 LASTROW**=***last_row*  
 Especifica o número da última linha a ser carregada. O padrão é 0, que indica a última fila no arquivo de dados especificado.  
  
 MAXERRORS  **=**  *max_errors*  
 Especifica o número máximo de erros de sintaxe permitido nos dados antes que a operação de importação em massa seja cancelada. Cada linha que não pode ser importada pela operação de importação em massa é ignorada e contada como um erro. Se *max_errors* não for especificado, o padrão é 10.  
  
> [!NOTE]  
>  A opção MAX_ERRORS não se aplica a verificações de restrição ou à conversão **money** e **bigint** tipos de dados.  
  
 ORDEM ({ *coluna* [ASC | DESC]} [ **,**... *n* ] )  
 Especifica como os dados no arquivo de dados são classificados. O desempenho da importação em massa será melhorado se os dados importados forem armazenados de acordo com o índice clusterizado na tabela, se houver. Se o arquivo de dados for classificado em outra ordem, ou seja, diferente da ordem de uma chave de índice clusterizado, ou se não houver nenhum índice clusterizado na tabela, a cláusula ORDER será ignorada. Os nomes das colunas fornecidos devem ser nomes de colunas válidas na tabela de destino. Por padrão, a operação de inserção em massa supõe que o arquivo de dados não esteja ordenado. Para obter uma importação em massa otimizada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também valida que os dados importados sejam classificados.  
  
 *n*  
 É um espaço reservado que indica que várias colunas podem ser especificadas.  
  
 ROWS_PER_BATCH  **=**  *rows_per_batch*  
 Indica o número aproximado de linhas de dados no arquivo de dados.  
  
 Por padrão, todos os dados de arquivo são enviados ao servidor como uma única transação, e o número de linhas no lote é desconhecido para o otimizador de consulta. Se você especificar ROWS_PER_BATCH (com um valor > 0), o servidor usará esse valor para otimizar a operação da importação em massa. O valor especificado para ROWS_PER_BATCH deve ser aproximadamente igual ao número real de linhas. Para obter informações sobre considerações de desempenho, consulte “Comentários”, posteriormente neste tópico.  
  
 
 TABLOCK  
 Especifica que um bloqueio no nível de tabela é adquirido durante a operação de importação em massa. Uma tabela pode ser carregada simultaneamente através de vários clientes se não tiver nenhum índice e TABLOCK for especificado. Por padrão, o comportamento de bloqueio é determinado pela opção de tabela **bloqueio de tabela em carregamento em massa**. Manter um bloqueio durante a operação de importação em massa reduz a contenção de bloqueio na tabela e em alguns casos pode melhorar significativamente o desempenho. Para obter informações sobre considerações de desempenho, consulte “Comentários”, posteriormente neste tópico.  
  
 Para o índice columnstore. o comportamento de bloqueio é diferente porque ele internamente é dividido em vários conjuntos de linhas.  Cada thread carrega dados exclusivamente em cada conjunto de linhas colocando um bloqueio X no conjunto de linhas, permitindo que o carregamento de dados em paralelo com sessões de carregamento de dados concorrentes. O uso da opção TABLOCK fará com que o thread levar um bloqueio X na tabela (ao contrário de bloqueio BU para conjuntos de linhas tradicionais), que impedirão que outros threads simultâneos para carregar dados simultaneamente.  

### <a name="input-file-format-options"></a>Opções de formato de arquivo de entrada
  
FORMATO  **=**  'CSV'   
**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Especifica um arquivo de valores separados por vírgula compatível para o [RFC 4180](https://tools.ietf.org/html/rfc4180) padrão.

FIELDQUOTE  **=**  'field_quote'   
**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Especifica um caractere que será usado como o caractere de aspas no arquivo CSV. Se não for especificado, o caractere de aspas (") será usado como o caractere de aspas conforme definido no [RFC 4180](https://tools.ietf.org/html/rfc4180) padrão.
  
 FORMATFILE **='***format_file_path***'**  
 Especifica o caminho completo de um arquivo de formato. Um arquivo de formato descreve o arquivo de dados que contém as respostas armazenadas criadas usando o **bcp** utilitário na mesma tabela ou exibição. O arquivo de formato deverá ser usado se:  
  
-   O arquivo de dados contiver colunas maiores ou menos colunas que a tabela ou exibição.  
  
-   As colunas estiverem em uma ordem diferente.  
  
-   Os delimitadores de coluna variarem.  
  
-   Houver outras alterações no formato de dados. Arquivos de formato normalmente são criados usando o **bcp** utility e modificados com um editor de texto conforme necessário. Para obter mais informações, consulte [bcp Utility](../../tools/bcp-utility.md).  

**Aplica-se ao:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Começando com [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 1.1 CTP, o format_file_path pode ser no armazenamento de BLOBs do Azure.

 FIELDTERMINATOR **='***field_terminator***'**  
 Especifica o terminador de campo a ser usado para **char** e **widechar** arquivos de dados. O terminador de campo padrão é \t (caractere de tabulação). Para obter mais informações, veja [Especificar terminadores de campo e linha &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).  

 ROWTERMINATOR **='***row_terminator***'**  
 Especifica o terminador de linha a ser usado para **char** e **widechar** arquivos de dados. O terminador de linha padrão é **\r\n** (caractere de nova linha).  Para obter mais informações, veja [Especificar terminadores de campo e linha &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).  

  
## <a name="compatibility"></a>Compatibilidade  
 O BULK INSERT impõe validação estrita de dados e verificações de dados lidos de um arquivo que podem provocar falha nos scripts existentes quando executadas com dados inválidos. Por exemplo, BULK INSERT verifica se:  
  
-   As representações nativas de **float** ou **real** tipos de dados são válidos.  
  
-   Dados Unicode têm um comprimento regular de byte.  
  
## <a name="data-types"></a>Tipos de dados  
  
### <a name="string-to-decimal-data-type-conversions"></a>Conversões do tipo de dados de cadeia de caracteres em decimal  
 As conversões de tipo de dados de cadeia de caracteres em decimal usadas em BULK INSERT seguem as mesmas regras que o [!INCLUDE[tsql](../../includes/tsql-md.md)] [converter](../../t-sql/functions/cast-and-convert-transact-sql.md) função, que rejeita cadeias de caracteres representando valores numéricos que usam notação científica. Portanto, BULK INSERT trata essas cadeias de caracteres como valores inválidos e relata erros de conversão.  
  
 Para contornar esse comportamento, use um arquivo de formato de notação científica de importação em massa de **float** dados em uma coluna decimal. No arquivo de formato, descreva explicitamente a coluna como **real** ou **float** dados. Para obter mais informações sobre esses tipos de dados, consulte [float e real &#40; Transact-SQL &#41; ](../../t-sql/data-types/float-and-real-transact-sql.md).  
  
> [!NOTE]  
>  Arquivos de formato representam **real** dados como o **SQLFLT4** tipo de dados e **float** dados como o **SQLFLT8** tipo de dados. Para obter informações sobre arquivos de formato não XML, consulte [especificar o tipo de armazenamento de arquivo usando bcp &#40; SQL Server &#41; ](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md).  
  
#### <a name="example-of-importing-a-numeric-value-that-uses-scientific-notation"></a>Exemplo de importação de um valor numérico que usa notação científica  
 Este exemplo usa a seguinte tabela:  
  
```  
CREATE TABLE t_float(c1 float, c2 decimal (5,4));  
```  
  
 O usuário quer importar dados em massa para a tabela `t_float`. O arquivo de dados, C:\t_float-c.dat, contém notação científica **float** dados; por exemplo:  
  
```  
8.0000000000000002E-28.0000000000000002E-2  
```  
  
 Entretanto, BULK INSERT não pode importar esses dados diretamente em `t_float`, porque sua segunda coluna, `c2`, usa o tipo de dados `decimal`. Portanto, um arquivo de formato é necessário. O arquivo de formato deve mapear a notação científica **float** dados para o formato decimal de coluna `c2`.  
  
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
|SQLCHAR ou SQLVARCHAR|Os dados são enviados na página de código do cliente ou na página de código implicada pelo agrupamento. O efeito é o mesmo que especificar DATAFILETYPE **= 'char'** sem especificar um arquivo de formato.|  
|SQLNCHAR ou SQLNVARCHAR|Os dados são enviados como Unicode. O efeito é o mesmo que especificar DATAFILETYPE **= 'widechar'** sem especificar um arquivo de formato.|  
|SQLBINARY ou SQLVARBIN|Os dados são enviados sem qualquer conversão.|  
  
## <a name="general-remarks"></a>Comentários gerais  
 Para obter uma comparação da instrução BULK INSERT, da instrução INSERT ... Selecione \* FROM OPENROWSET e o **bcp** command, consulte [importação e exportação de dados &#40; SQL Server &#41; ](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md).  
  
 Para obter informações sobre como preparar dados para importação em massa, consulte [preparar dados para importação ou exportação em massa &#40; SQL Server &#41; ](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).  
  
 A instrução BULK INSERT pode ser executada dentro de uma transação definida pelo usuário para importar dados em uma tabela ou exibição. Opcionalmente, para usar várias correspondências para obter dados de importação em massa, uma transação pode especificar a cláusula BATCHSIZE na instrução de BULK INSERT. Se uma transação de vários lotes for revertida, todo o lote enviado pela transação ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será revertido.  
  
## <a name="interoperability"></a>Interoperabilidade  
  
### <a name="importing-data-from-a-csv-file"></a>Importando dados de um arquivo CSV  
Começando com [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 1.1 CTP, BULK INSERT suporta o formato CSV.  
Antes de [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 1.1 CTP, arquivos de valores separados por vírgulas (CSV) não são suportados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] operações de importação em massa. No entanto, em alguns casos, um arquivo CSV pode ser usado como o arquivo de dados para uma importação em massa de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter informações sobre os requisitos para importar dados de um arquivo de dados CSV, consulte [preparar dados para importação ou exportação em massa &#40; SQL Server &#41; ](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).  
  
## <a name="logging-behavior"></a>Comportamento de log  
 Para obter informações sobre quando as operações de inserção de linhas executadas por importações em massa são registradas no log de transações, veja [Pré-requisitos para log mínimo em importação em massa](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
##  <a name="Limitations"></a> Restrições  
 Ao usar um arquivo de formato com BULK INSERT, você pode especificar até somente 1024 campos. Isso é o mesmo que o número máximo de colunas permitido em uma tabela. Se você usar BULK INSERT com um arquivo de dados que contém mais de 1024 campos, o BULK INSERT gerará o erro 4822. O [utilitário bcp](../../tools/bcp-utility.md) não tem essa limitação, portanto, para arquivos de dados que contêm mais de 1024 campos, use o **bcp** comando.  
  
## <a name="performance-considerations"></a>Considerações sobre desempenho  
 Se o número de páginas a ser liberado em um único lote exceder um limite interno, poderá ocorrer um exame completo do pool de buffers para identificar quais páginas devem ser liberadas quando o lote for confirmado. Esse exame completo pode prejudicar o desempenho da importação em massa. Um caso provável de exceder o limite interno ocorre quando um pool de buffers grande é combinado com um subsistema de E/S lento. Para evitar estouros de buffer em máquinas grandes, não use a dica TABLOCK (que removerá as otimizações em massa) ou use um tamanho de lote menor (que preserva as otimizações em massa).  
  
 Como os computadores variam, é recomendável testar vários tamanhos de lote com seu carregamento de dados para descobrir o que funciona melhor para você.  
  
## <a name="security"></a>Segurança  
  
### <a name="security-account-delegation-impersonation"></a>Delegação de conta de segurança (representação)  
 Se um usuário usar um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o perfil de segurança da conta de processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será usado. Um logon que usa a autenticação do SQL Server não pode ser autenticado fora do Mecanismo de Banco de Dados. Assim, quando um comando BULK INSERT é iniciado por um logon que usa a autenticação do SQL Server, a conexão aos dados é feita por meio do contexto de segurança da conta de processo do SQL Server (a conta usada pelo serviço de Mecanismo de Banco de Dados do SQL Server). Para ler a fonte de dados com êxito, você deve dar à conta usada pelo Mecanismo de Banco de Dados do SQL Server acesso ao banco de dados. Em contrapartida, se um usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fizer logon por meio da Autenticação do Windows, ele poderá acessar, no modo somente leitura, aqueles arquivos que podem ser acessados pela conta do usuário, a despeito do perfil de segurança do processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Ao executar a instrução BULK INSERT usando **sqlcmd** ou **osql**, de um computador, inserindo dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um segundo computador e especificando uma *data_file* no terceiro computador por meio de um caminho UNC, você pode receber um erro 4861.  
  
 Para resolver esse erro, use [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação e especificar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usa o perfil de segurança de logon a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta do processo ou configurar o Windows para habilitar a delegação de conta de segurança. Para obter informações sobre como habilitar uma conta de usuário que seja confiável para a delegação, consulte a Ajuda do Windows.  
  
 Para obter mais informações sobre essa e outras considerações de segurança para usar BULK INSERT, consulte [importação em massa dados usando BULK INSERT ou OPENROWSET &#40; BULK... &#41; &#40; SQL Server &#41; ](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).  
  
### <a name="permissions"></a>Permissões  
 Requer as permissões INSERT e ADMINISTER BULK OPERATIONS. Além disso, a permissão ALTER TABLE será necessária se uma ou mais das seguintes afirmações for verdadeira:  
  
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
>  Devido a como o Microsoft Windows trata arquivos de texto **(\n** automaticamente é substituído por **\r\n)**.  
  
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
### <a name="e-importing-data-from-a-csv-file"></a>E. Importar dados de um arquivo CSV   
O exemplo a seguir mostra como especificar um arquivo CSV.   
```
BULK INSERT Sales.Invoices
FROM '\\share\invoices\inv-2016-07-25.csv'
WITH (FORMAT = 'CSV'); 
```

### <a name="f-importing-data-from-a-file-in-azure-blob-storage"></a>F. Importando dados de um arquivo no armazenamento de BLOBs do Azure   
O exemplo a seguir mostra como carregar dados de um arquivo csv em um local de armazenamento de BLOBs do Azure, que foi configurado como uma fonte de dados externa. Isso requer uma credencial no escopo do banco de dados usando uma assinatura de acesso compartilhado.    

```tsql
BULK INSERT Sales.Invoices
FROM 'inv-2017-01-19.csv'
WITH (DATA_SOURCE = 'MyAzureInvoices',
     FORMAT = 'CSV'); 
```

Para concluir `BULK INSERT` exemplos, incluindo a configuração de credencial e a fonte de dados externa, consulte [exemplos de Bulk acesso aos dados no armazenamento de BLOBs do Azure](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md).
  
### <a name="additional-examples"></a>Exemplos adicionais  
 Outros `BULK INSERT` exemplos são fornecidos nos tópicos a seguir:  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Importação e exportação em massa de dados &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [bcp Utility](../../tools/bcp-utility.md)   
 [Arquivos de formato para importar ou exportar dados &#40; SQL Server &#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Preparar dados para exportação em massa ou importar &#40; SQL Server &#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)   
 [sp_tableoption &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)  
  
  

