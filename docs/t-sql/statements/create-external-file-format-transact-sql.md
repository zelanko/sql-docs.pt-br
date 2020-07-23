---
title: CREATE EXTERNAL FILE FORMAT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/08/2020
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL FILE FORMAT
- CREATE_EXTERNAL_FILE_FORMAT
dev_langs:
- TSQL
helpviewer_keywords:
- External
- External, file format
- PolyBase, external file format
ms.assetid: abd5ec8c-1a0e-4d38-a374-8ce3401bc60c
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 129ac690a0615062bb620c8b81dfbdb16a41659e
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942668"
---
# <a name="create-external-file-format-transact-sql"></a>CREATE EXTERNAL FILE FORMAT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

Cria um objeto de formato de arquivo externo definindo dados externos armazenados no Hadoop, no Armazenamento de Blobs do Azure, no Azure Data Lake Storage ou para os fluxos de entrada e de saída associados a Fluxos Externos. Criar um formato de arquivo externo é um pré-requisito para criar uma tabela externa. Ao criar um formato de arquivo externo, você especificará o layout real dos dados referenciados por uma tabela externa.  
  
Os seguintes formatos de arquivo são compatíveis:
  
- Texto delimitado  
  
- RCFile do Hive  
  
- ORC do Hive
  
- Parquet

- JSON – Aplica-se somente ao SQL do Azure no Edge.


Para criar uma tabela externa, confira [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md).
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe
  
```syntaxsql
-- Create an external file format for PARQUET files.  
CREATE EXTERNAL FILE FORMAT file_format_name  
WITH (  
    FORMAT_TYPE = PARQUET  
     [ , DATA_COMPRESSION = {  
        'org.apache.hadoop.io.compress.SnappyCodec'  
      | 'org.apache.hadoop.io.compress.GzipCodec'      }  
    ]);  
  
--Create an external file format for ORC files.  
CREATE EXTERNAL FILE FORMAT file_format_name  
WITH (  
    FORMAT_TYPE = ORC  
     [ , DATA_COMPRESSION = {  
        'org.apache.hadoop.io.compress.SnappyCodec'  
      | 'org.apache.hadoop.io.compress.DefaultCodec'      }  
    ]);  
  
--Create an external file format for RCFILE.  
CREATE EXTERNAL FILE FORMAT file_format_name  
WITH (  
    FORMAT_TYPE = RCFILE,  
    SERDE_METHOD = {  
        'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe'  
      | 'org.apache.hadoop.hive.serde2.columnar.ColumnarSerDe'  
    }  
    [ , DATA_COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec' ]);  
  
--Create an external file format for DELIMITED TEXT files.  
CREATE EXTERNAL FILE FORMAT file_format_name  
WITH (  
    FORMAT_TYPE = DELIMITEDTEXT  
    [ , FORMAT_OPTIONS ( <format_options> [ ,...n  ] ) ]  
    [ , DATA_COMPRESSION = {  
           'org.apache.hadoop.io.compress.GzipCodec'  
         | 'org.apache.hadoop.io.compress.DefaultCodec'  
        }  
     ]);  

-- Create an external file format for JSON files.
CREATE EXTERNAL FILE FORMAT file_format_name  
WITH (  
    FORMAT_TYPE = JSON  
     [ , DATA_COMPRESSION = {  
        'org.apache.hadoop.io.compress.SnappyCodec'  
      | 'org.apache.hadoop.io.compress.GzipCodec'      
      | 'org.apache.hadoop.io.compress.DefaultCodec'  }  
    ]);  
 
<format_options> ::=  
{  
    FIELD_TERMINATOR = field_terminator  
    | STRING_DELIMITER = string_delimiter 
    | First_Row = integer -- ONLY AVAILABLE SQL DW
    | DATE_FORMAT = datetime_format  
    | USE_TYPE_DEFAULT = { TRUE | FALSE } 
    | Encoding = {'UTF8' | 'UTF16'} 
}  
```  
  
## <a name="arguments"></a>Argumentos  
*file_format_name*  
Especifica um nome para o formato de arquivo externo.
  
FORMAT_TYPE = [ PARQUET | ORC | RCFILE | DELIMITEDTEXT] Especifica o formato dos dados externos.
  
- PARQUET Especifica um formato Parquet.
  
- ORC  
  Especifica um formato ORC (Optimized Row Columnar). Essa opção requer o Hive versão 0.11 ou superior no cluster do Hadoop externo. No Hadoop, o formato de arquivo ORC oferece melhor compactação e desempenho que o formato de arquivo RCFILE.

- RCFILE (em combinação com SERDE_METHOD = *SERDE_method*) Especifica um formato RcFile (Record Columnar file). Essa opção requer que você especifique um método SerDe (serializador e desserializador) do Hive. Esse requisito é o mesmo para usar o Hive/HiveQL no Hadoop para consultar arquivos RC. Observe que o método SerDe diferencia maiúsculas de minúsculas.

  Exemplos de especificação de RCFile com os dois métodos SerDe compatíveis com o PolyBase.

  - FORMAT_TYPE = RCFILE, SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe'

  - FORMAT_TYPE = RCFILE, SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.ColumnarSerDe'

- DELIMITEDTEXT Especifica um formato de texto com delimitadores de coluna, também chamado de terminadores de campo.
   
- O JSON especifica um formato JSON. Aplica-se somente ao SQL do Azure no Edge. 
  
FIELD_TERMINATOR = *field_terminator*  
Aplica-se somente a arquivos de texto delimitado. O terminador de campo especifica um ou mais caracteres que marcam o final de cada campo (coluna) no arquivo de texto delimitado. O padrão é o caractere barra vertical ꞌ|ꞌ. Para garantir o suporte, é recomendável usar um ou mais caracteres ASCII.
  
  
Exemplos:  
  
-   FIELD_TERMINATOR = '|'  
  
-   FIELD_TERMINATOR = ' '  
  
-   FIELD_TERMINATOR = ꞌ\tꞌ  
  
-   FIELD_TERMINATOR = '~|~'  
  
STRING_DELIMITER = *string_delimiter*  
Especifica o terminador de campo dos dados da cadeia de caracteres de tipo no arquivo de texto delimitado. O delimitador de cadeia de caracteres tem um ou mais caracteres de comprimento e está entre aspas simples. O padrão é a cadeia de caracteres vazia "". Para garantir o suporte, é recomendável usar um ou mais caracteres ASCII.
 
  
 Exemplos:  

-   STRING_DELIMITER = '"'

-   STRING_DELIMITER = '0x22' – hexa de aspas duplas
  
-   STRING_DELIMITER = '*'  
  
-   STRING_DELIMITER = ꞌ,ꞌ  
  
-   STRING_DELIMITER = '0x7E0x7E' – dois tils (por exemplo, ~~)
 
 FIRST_ROW = *First_row_int*  
Especifica o número de linha lido primeiro em todos os arquivos durante o carregamento do PolyBase. Esse parâmetro pode assumir valores de 1 a 15. Se o valor for definido como dois, a primeira linha em todos os arquivos (linha de cabeçalho) será ignorada quando os dados forem carregados. As linhas são ignoradas com base na existência de terminadores de linhas (/r/n, /r, /n). Quando essa opção é usada para exportação, as linhas são adicionadas aos dados para garantir que o arquivo possa ser lido sem perda de dados. Se o valor for definido como >2, a primeira linha exportada será a de nomes de colunas da tabela externa.

 DATE\_FORMAT = *datetime_format*  
Especifica um formato personalizado para todos os dados de data e hora que podem aparecer em um arquivo de texto delimitado. Se o arquivo de origem usar os formatos datetime padrão, essa opção não será necessária. Apenas um formato datetime personalizado é permitido por arquivo. Não é possível especificar mais de um formato datetime personalizado por arquivo. No entanto, você poderá usar mais de um formato datetime se cada um deles estiver no formato padrão do tipo de dados respectivo na definição da tabela externa.

O PolyBase só usa o formato de data personalizado para importar os dados. Ele não usa o formato personalizado para gravar dados em um arquivo externo.

 Quando DATE_FORMAT não for especificado ou for a cadeia de caracteres vazia, o PolyBase usará os seguintes formatos padrão:
  
-   DateTime: 'aaaa-MM-dd HH:mm:ss'  
  
-   SmallDateTime: 'aaaa-MM-dd HH:mm'  
  
-   Data: 'aaaa-MM-dd'  
  
-   DateTime2: 'aaaa-MM-dd HH:mm:ss'  
  
-   DateTimeOffset: 'aaaa-MM-dd HH:mm:ss'  
  
-   Time: 'HH:mm:ss'  
  
**Há exemplos de formatos de data** na tabela a seguir:
  
Observações sobre a tabela:  
  
-   Ano, mês e dia podem ter uma variedade de formatos e ordens. A tabela mostra apenas o formato **amd**. Mês pode ter um ou dois dígitos, ou três caracteres. Dia pode ter um ou dois dígitos. Ano pode ter dois ou quatro dígitos.
  
-   Milissegundos (fffffff) não são necessários.
  
-   Am, pm (tt) não são necessários. O padrão é AM.
  
|Tipo de data|Exemplo|Descrição|  
|---------------|-------------|-----------------|  
|Datetime|DATE_FORMAT = 'aaaa-MM-dd HH:mm:ss.fff'|Além de ano, mês e dia, esse formato de data inclui 00 a 24 horas, 00 a 59 minutos, 00 a 59 segundos e 3 dígitos para milissegundos.|  
|Datetime|DATE_FORMAT = 'aaaa-MM-dd hh:mm:ss.ffftt'|Além de ano, mês e dia, esse formato de data inclui 00 a 12 horas, 00 a 59 minutos, 00 a 59 segundos, 3 dígitos para milissegundos e AM, am, PM ou pm. |  
|SmallDateTime|DATE_FORMAT = 'aaaa-MM-dd HH:mm'|Além de ano, mês e dia, esse formato de data inclui 00 a 23 horas e 00 a 59 minutos.|  
|SmallDateTime|DATE_FORMAT = 'aaaa-MM-dd hh:mmtt'|Além de ano, mês e dia, esse formato de data inclui 00 a 11 horas, 00 a 59 minutos, não inclui segundos e inclui AM, am, PM ou pm.|  
|Data|DATE_FORMAT = 'aaaa-MM-dd'|Ano, mês e dia. Não é incluído nenhum elemento de hora.|  
|Data|DATE_FORMAT = 'aaaa-MMM-dd'|Ano, mês e dia. Quando o mês é especificado com 3 Ms, o valor de entrada é uma das cadeias de caracteres Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov ou Dec.|  
|DateTime2|DATE_FORMAT = 'aaaa-MM-dd HH:mm:ss.fffffff'|Além de ano, mês e dia, esse formato de data inclui 00 a 23 horas, 00 a 59 minutos, 00 a 59 segundos e 7 dígitos para milissegundos.|  
|DateTime2|DATE_FORMAT = 'aaaa-MM-dd hh:mm:ss.ffffffftt'|Além de ano, mês e dia, esse formato de data inclui 00 a 11 horas, 00 a 59 minutos, 00 a 59 segundos, 7 dígitos para milissegundos e AM, am, PM ou pm.|  
|DateTimeOffset|DATE_FORMAT = 'aaaa-MM-dd HH:mm:ss.fffffff zzz'|Além de ano, mês e dia, esse formato de data inclui 00 a 23 horas, 00 a 59 minutos, 00 a 59 segundos, 7 dígitos para milissegundos e a diferença de fuso horário que você coloca no arquivo de entrada como `{+&#124;-}HH:ss`. Por exemplo, com o horário de Los Angeles sem horário de verão está 8 horas atrás do UTC, o valor -08:00 no arquivo de entrada especifica o fuso horário de Los Angeles.|  
|DateTimeOffset|DATE_FORMAT = 'aaaa-MM-dd hh:mm:ss.ffffffftt zzz'|Além de ano, mês e dia, esse formato de data inclui 00 a 11 horas, 00 a 59 minutos, 00 a 59 segundos, 7 dígitos para milissegundos, (AM, am, PM ou pm) e a diferença de fuso horário. Veja a descrição na linha anterior.|  
|Hora|DATE_FORMAT = 'HH:mm:ss'|Não há nenhum valor de data, apenas de 00 a 23 horas, 00 a 59 minutos e 00 a 59 segundos.|  
  
 Todos os formatos de data compatíveis:
  
|DATETIME|smalldatetime|date|datetime2|datetimeoffset|  
|--------------|-------------------|----------|---------------|--------------------|  
|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fff]|[M[M]]M-[d]d-[aa]aa HH:mm[:00]|[M[M]]M-[d]d-[aa]aa|[M[M]]M-[d]d-[aa]aa HH:mm:ss[.fffffff]|[M[M]]M-[d]d-[aa]aa HH:mm:ss[.fffffff] zzz|  
|[M[M]]M-[d]d-[aa]aa hh:mm:ss[.fff][tt]|[M[M]]M-[d]d-[aa]aa hh:mm[:00][tt]||[M[M]]M-[d]d-[aa]aa hh:mm:ss[.fffffff][tt]|[M[M]]M-[d]d-[aa]aa hh:mm:ss[.fffffff][tt] zzz|  
|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fff]|[M[M]]M-[yy]yy-[d]d HH:mm[:00]|[M[M]]M-[yy]yy-[d]d|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fffffff]|[M[M]]M-[aa]aa-[d]d HH:mm:ss[.fffffff] zzz|  
|[M[M]]M-[aa]aa-[d]d hh:mm:ss[.fff][tt]|[M[M]]M-[aa]aa-[d]d hh:mm[:00][tt]||[M[M]]M-[aa]aa-[d]d hh:mm:ss[.fffffff][tt]|[M[M]]M-[aa]aa-[d]d hh:mm:ss[.fffffff][tt] zzz|  
|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fff]|[yy]yy-[M[M]]M-[d]d HH:mm[:00]|[yy]yy-[M[M]]M-[d]d|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fffffff]|[aa]aa-[M[M]]M-[d]d HH:mm:ss[.fffffff] zzz|  
|[aa]aa-[M[M]]M-[d]d hh:mm:ss[.fff][tt]|[aa]aa-[M[M]]M-[d]d hh:mm[:00][tt]||[aa]aa-[M[M]]M-[d]d hh:mm:ss[.fffffff][tt]|[aa]aa-[M[M]]M-[d]d hh:mm:ss[.fffffff][tt] zzz|  
|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fff]|[aa]aa-[d]d-[M[M]]M HH:mm[:00]|[yy]yy-[d]d-[M[M]]M|[aa]aa-[d]d-[M[M]]M HH:mm:ss[.fffffff]|[aa]aa-[d]d-[M[M]]M HH:mm:ss[.fffffff] zzz|  
|[aa]aa-[d]d-[M[M]]M hh:mm:ss[.fff][tt]|[aa]aa-[d]d-[M[M]]M hh:mm[:00][tt]||[aa]aa-[d]d-[M[M]]M hh:mm:ss[.fffffff][tt]|[aa]aa-[d]d-[M[M]]M hh:mm:ss[.fffffff][tt] zzz|  
|[d]d-[M[M]]M-[aa]aa HH:mm:ss[.fff]|[d]d-[M[M]]M-[aa]aa HH:mm[:00]|[d]d-[M[M]]M-[aa]aa|[d]d-[M[M]]M-[aa]aa HH:mm:ss[.fffffff]|[d]d-[M[M]]M-[aa]aa HH:mm:ss[.fffffff] zzz|  
|[d]d-[M[M]]M-[aa]aa hh:mm:ss[.fff][tt]|[d]d-[M[M]]M-[aa]aa hh:mm[:00][tt]||[d]d-[M[M]]M-[aa]aa hh:mm:ss[.fffffff][tt]|[d]d-[M[M]]M-[aa]aa hh:mm:ss[.fffffff][tt] zzz|  
|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fff]|[d]d-[aa]aa-[M[M]]M HH:mm[:00]|[d]d-[yy]yy-[M[M]]M|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fffffff]|[d]d-[aa]aa-[M[M]]M HH:mm:ss[.fffffff] zzz|  
|[d]d-[aa]aa-[M[M]]M hh:mm:ss[.fff][tt]|[d]d-[aa]aa-[M[M]]M hh:mm[:00][tt]||[d]d-[aa]aa-[M[M]]M hh:mm:ss[.fffffff][tt]|[d]d-[aa]aa-[M[M]]M hh:mm:ss[.fffffff][tt] zzz|  
  
 Detalhes:  
  
-   Para separar os valores de mês, dia e ano, use '-', '/' ou '.'. Para simplificar, a tabela use apenas o separador ‘-’.
  
-   Para especificar o mês como texto, use três ou mais caracteres. Os meses com um ou dois caracteres são interpretados como um número.
  
-   Para separar os valores de tempo, use o símbolo ':'.
  
-   As letras entre colchetes são opcionais.
  
-   As letras 'tt' designam [AM|PM|am|pm]. AM é o padrão. Quando 'tt' for especificado, o valor de hora (hh) precisará estar no intervalo de 0 a 12.
  
-   As letras 'zzz' designam a diferença do fuso horário atual do sistema no formato {+|-}HH:ss].
  
 USE_TYPE_DEFAULT = { TRUE | **FALSE** }  
 Especifica como tratar valores ausentes em arquivos de texto delimitados quando o PolyBase recuperar dados do arquivo de texto.
  
 TRUE  
 Ao recuperar dados do arquivo de texto, armazene cada valor ausente, usando o valor padrão para o tipo de dados da coluna correspondente na definição da tabela externa. Por exemplo, substitua um valor ausente por:  
  
-   0 se a coluna for definida como uma coluna numérica. Não há suporte a colunas decimais. Elas gerarão erros.
  
-   A cadeia de caracteres vazia "" se a coluna for uma coluna de cadeia de caracteres.
  
-   1900-01-01 se a coluna for uma coluna de data.
  
 FALSE  
 Armazene todos os valores ausentes como NULL. Todos os valores NULL que estão armazenados usando a palavra NULL no arquivo de texto delimitado são importados como a cadeia de caracteres 'NULL'.
  
   Codificação = {'UTF8' | 'UTF16'}  
 No SQL Data Warehouse do Azure e o PDW (APS CU7.4), o PolyBase pode ler arquivos de texto delimitados codificados em UTF8 e UTF16-LE. No SQL Server, o PolyBase não dá suporte à leitura de arquivos codificados em UTF16.
  
 DATA_COMPRESSION = *data_compression_method*  
 Especifica o método de compactação de dados para os dados externos. Quando DATA_COMPRESSION não for especificado, o padrão será dados não compactados.
 Para funcionar corretamente, os arquivos compactados pelo Gzip precisam ter a extensão de arquivo ".gz".
 
 O tipo de formato DELIMITEDTEXT é compatível com estes métodos de compactação:
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec'
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'

 O tipo de formato RCFILE é compatível com este método de compactação:
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec'
  
 O tipo de formato de arquivo ORC é compatível com este método de compactação:
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec'
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'
  
 O tipo de formato de arquivo PARQUET é compatível com este método de compactação:
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'

 O tipo de formato de arquivo JSON é compatível com os seguintes métodos de compactação:
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'

-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec'
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY EXTERNAL FILE FORMAT.
  
## <a name="general-remarks"></a>Comentários gerais
 O formato de arquivo externo está no escopo do banco de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Ele está no escopo do servidor no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
 As opções de formato são todas opcionais e só se aplicam a arquivos de texto delimitado.  
  
 Quando os dados são armazenados em um dos formatos compactados, o PolyBase primeiro descompacta os dados antes de retornar os registros de dados.
  
## <a name="limitations-and-restrictions"></a>Limitações e Restrições
  
 O delimitador de linha nos arquivos de texto delimitados precisa ser compatível com o LineRecordReader do Hadoop. Ou seja, ele precisa ser '\r', '\n' ou '\r\n'. Esses delimitadores não podem ser configurados pelo usuário.
  
 As combinações de métodos SerDe compatíveis com RCFiles e os métodos de compactação de dados compatíveis estão listados anteriormente neste artigo. Nem todas as combinações são compatíveis.
  
 O número máximo de consultas simultâneas do PolyBase é 32. Quando houver 32 consultas simultâneas em execução, cada consulta poderá ler no máximo 33.000 arquivos do local do arquivo externo. A pasta raiz e cada subpasta também são contadas como arquivos. Se o grau de simultaneidade for menor que 32, o local do arquivo externo poderá conter mais de 33.000 arquivos.
  
 Devido à limitação no número de arquivos da tabela externa, é recomendável armazenar menos de 30.000 arquivos na pasta raiz e nas subpastas no local do arquivo externo. Além disso, é recomendável manter um número pequeno de subpastas no diretório raiz. Quando muitos arquivos são referenciados, pode ocorrer uma exceção de falta de memória da Máquina Virtual Java.
  
  Ao exportar dados para o Hadoop ou para o Armazenamento de Blobs do Azure pelo PolyBase, somente os dados são exportados, não a coluna names(metadata), conforme a definição no comando CREATE EXTERNAL TABLE.

## <a name="locking"></a>Bloqueio  
 Coloca um bloqueio compartilhado no objeto EXTERNAL FILE FORMAT.
  
## <a name="performance"></a>Desempenho
 O uso de arquivos compactados sempre traz a desvantagem de transferir menos dados entre a fonte de dados externa e o SQL Server e aumentar o uso da CPU para compactar e descompactar os dados.
  
 Os arquivos de texto compactados com gzip não são divisíveis. Para melhorar o desempenho dos arquivos de texto compactados com Gzip, é recomendável gerar vários arquivos armazenados no mesmo diretório na fonte de dados externa. Essa estrutura de arquivo permite que o PolyBase leia e descompacte os dados com mais rapidez por meio de vários processos do leitor e de descompactação. O número ideal de arquivos compactados é o número máximo de processos do leitor de dados por nó de computação. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], o número máximo de processos de leitor de dados é de 8 por nó, exceto o SQL Data Warehouse do Azure Gen2, que é de 20 leitores por nó. No [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], o número máximo de processos do leitor de dados por nó varia por SLO. Confira [Azure SQL Data Warehouse loading patterns and strategies](https://blogs.msdn.microsoft.com/sqlcat/2017/05/17/azure-sql-data-warehouse-loading-patterns-and-strategies/) (Padrões e estratégias de carregamento do SQL Data Warehouse do Azure) para obter detalhes.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-create-a-delimitedtext-external-file-format"></a>a. Criar um formato de arquivo externo DELIMITEDTEXT  
 Este exemplo cria um formato de arquivo externo denominado *textdelimited1* para um arquivo de texto delimitado. As opções listadas para FORMAT\_OPTIONS especificam que os campos no arquivo devem ser separados usando um caractere de barra vertical '|'. O arquivo de texto também é compactado com o codec Gzip. Se DATA\_COMPRESSION não for especificado, o arquivo de texto será descompactado.
  
 Para um arquivo de texto delimitado, o método de compactação de dados pode ser o Codec padrão, 'org.apache.hadoop.io.compress.DefaultCodec' ou o Codec do Gzip, 'org.apache.hadoop.io.compress.GzipCodec'.
  
```  
CREATE EXTERNAL FILE FORMAT textdelimited1  
WITH (  
    FORMAT_TYPE = DELIMITEDTEXT,  
    FORMAT_OPTIONS (  
        FIELD_TERMINATOR = '|',  
        DATE_FORMAT = 'MM/dd/yyyy' ),  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
);  
```  
  
### <a name="b-create-an-rcfile-external-file-format"></a>B. Criar um formato de arquivo externo RCFile  
 Este exemplo cria um formato de arquivo externo para um RCFile que usa o método de serialização/desserialização org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe. Ela também especifica o uso do Codec padrão para o método de compactação de dados. Se DATA_COMPRESSION não for especificado, o padrão será sem compactação.
  
```  
CREATE EXTERNAL FILE FORMAT rcfile1  
WITH (  
    FORMAT_TYPE = RCFILE,  
    SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe',  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec'  
);  
```  
  
### <a name="c-create-an-orc-external-file-format"></a>C. Criar um formato de arquivo externo ORC  
 Este exemplo cria um formato de arquivo externo para um arquivo ORC que compacta os dados com o método de compactação de dados org.apache.io.compress.SnappyCodec. Se DATA_COMPRESSION não for especificado, o padrão será sem compactação.
  
```  
CREATE EXTERNAL FILE FORMAT orcfile1  
WITH (  
    FORMAT_TYPE = ORC,  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'  
);  
```  
  
### <a name="d-create-a-parquet-external-file-format"></a>D. Criar um formato de arquivo externo PARQUET  
 Este exemplo cria um formato de arquivo externo para um arquivo Parquet que compacta os dados com o método de compactação de dados org.apache.io.compress.SnappyCodec. Se DATA_COMPRESSION não for especificado, o padrão será sem compactação.  
  
```  
CREATE EXTERNAL FILE FORMAT parquetfile1  
WITH (  
    FORMAT_TYPE = PARQUET,  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'  
);  
```  
### <a name="e-create-a-delimited-text-file-skipping-header-row-azure-sql-dw-only"></a>E. Criar um arquivo de texto delimitado, ignorando a linha de cabeçalho (somente SQL DW do Azure)
 Este exemplo cria um formato de arquivo externo para o arquivo CSV com uma única linha de cabeçalho. 
  
```  
CREATE EXTERNAL FILE FORMAT skipHeader_CSV
WITH (FORMAT_TYPE = DELIMITEDTEXT,
      FORMAT_OPTIONS(
          FIELD_TERMINATOR = ',',
          STRING_DELIMITER = '"',
          FIRST_ROW = 2, 
          USE_TYPE_DEFAULT = True)
)
```   
### <a name="f-create-a-json-external-file-format"></a>F. Criar um formato de arquivo externo do JSON  
 Este exemplo cria um formato de arquivo externo para um arquivo JSON que compacta os dados com o método de compactação de dados org.apache.io.compress.SnappyCodec. Se DATA_COMPRESSION não for especificado, o padrão será sem compactação. Este exemplo se aplica ao SQL do Azure no Edge e atualmente não é compatível com outros produtos SQL. 
  
```  
CREATE EXTERNAL FILE FORMAT jsonFileFormat  
WITH (  
    FORMAT_TYPE = JSON,  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'  
);  
```  

## <a name="see-also"></a>Consulte Também
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [CREATE EXTERNAL TABLE AS SELECT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [CREATE TABLE AS SELECT &#40;SQL Data Warehouse do Azure&#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)   
 [sys.external_file_formats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)  
