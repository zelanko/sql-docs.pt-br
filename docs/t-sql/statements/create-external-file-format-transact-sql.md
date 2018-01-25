---
title: CRIAR um formato de arquivo externo (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 12/08/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL FILE FORMAT
- CREATE_EXTERNAL_FILE_FORMAT
dev_langs: TSQL
helpviewer_keywords:
- External
- External, file format
- PolyBase, external file format
ms.assetid: abd5ec8c-1a0e-4d38-a374-8ce3401bc60c
caps.latest.revision: "25"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ab389a5c811f915ff497057a5daf12374f1cedb7
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="create-external-file-format-transact-sql"></a>CREATE EXTERNAL FILE FORMAT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Cria uma definição de formato de arquivo externo do PolyBase para dados externos armazenados no Hadoop, o armazenamento de BLOBs do Azure ou o repositório Azure Data Lake. Criar um formato de arquivo externo é um pré-requisito para a criação de uma tabela externa do PolyBase. Criando um formato de arquivo externo, você deve especificar o layout real dos dados referenciados por uma tabela externa.  
  
 PolyBase suporta os seguintes formatos de arquivo:
  
-   Texto delimitado  
  
-   RCFile de hive  
  
-   Seção ORC
  
-   Parquet  
  
 Para criar uma tabela externa, consulte [CREATE EXTERNAL TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-table-transact-sql.md).
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe
  
```
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
  
<format_options> ::=  
{  
    FIELD_TERMINATOR = field_terminator  
    | STRING_DELIMITER = string_delimiter  
    | DATE_FORMAT = datetime_format  
    | USE_TYPE_DEFAULT = { TRUE | FALSE } 
    | Encoding = {'UTF8' | 'UTF16'} 
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *file_format_name*  
 Especifica um nome para o formato de arquivo externo.
  
 FORMAT_TYPE Especifica o formato dos dados externos.
  
 PARQUET Especifica um formato de Parquet.
  
 ORC  
 Especifica um formato de linha de otimização Colunar (ORC). Essa opção requer Hive versão 0.11 ou superior no cluster de Hadoop externo. No Hadoop, o formato de arquivo ORC oferece melhor desempenho que o formato de arquivo RCFILE e compactação.
  
 RCFILE (em combinação com SERDE_METHOD = *SERDE_method*) especifica um formato de arquivo de registro Colunar (RcFile). Essa opção requer que você especificar um serializador de Hive e o método desserializador (SerDe). Esse requisito é o mesmo se você usar o Hive/HiveQL no Hadoop para consultar arquivos RC. Observe que o método SerDe diferencia maiusculas de minúsculas.
  
 Exemplos de especificação de RCFile com os dois métodos de SerDe PolyBase oferece suporte.
  
-   FORMAT_TYPE = RCFILE, SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe'
  
-   FORMAT_TYPE = RCFILE, SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.ColumnarSerDe'
  
 DELIMITEDTEXT Especifica um formato de texto com os delimitadores de coluna, também chamado de terminadores de campo.
  
 FIELD_TERMINATOR = *field_terminator* aplica-se somente a arquivos de texto delimitado. O terminador de campo especifica um ou mais caracteres que marca o final de cada campo (coluna) no arquivo de texto delimitado. O padrão é o ꞌ de caractere de pipe | ꞌ. Para obter suporte garantido, é recomendável usar um ou mais caracteres ascii.
  
  
 Exemplos:  
  
-   FIELD_TERMINATOR = '|'  
  
-   FIELD_TERMINATOR = ' '  
  
-   FIELD_TERMINATOR = ꞌ\tꞌ  
  
-   FIELD_TERMINATOR = ' ~ | ~'  
  
 STRING_DELIMITER = *string_delimiter*  
 Especifica o terminador de campo de dados do tipo cadeia de caracteres no arquivo de texto delimitado. O delimitador de cadeia de caracteres é um ou mais caracteres de comprimento e está entre aspas simples. O padrão é a cadeia de caracteres vazia "". Para obter suporte garantido, é recomendável usar um ou mais caracteres ascii.
 
  
 Exemplos:  

-   STRING_DELIMITER = '"'

-   STRING_DELIMITER = '0x22' – hex aspas duplas
  
-   STRING_DELIMITER = '*'  
  
-   STRING_DELIMITER = ꞌ,ꞌ  
  
-   STRING_DELIMITER = '0x7E0x7E' – til duas vezes (por exemplo, ~ ~)
  
 DATA\_formato = *datetime_format* Especifica um formato personalizado para todos os dados de data e hora que podem aparecer em um arquivo de texto delimitado. Se o arquivo de origem usa os formatos de data e hora padrão, essa opção não é necessária. Apenas um formato de data e hora personalizado é permitido por arquivo. Não é possível especificar vários formatos de data e hora personalizado por arquivo. No entanto, você pode usar vários formatos de data e hora, se cada um deles é o formato padrão para seu tipo de dados do respectivos na definição da tabela externa.

PolyBase só usa o formato de data personalizada para importar os dados. Ele não usa o formato personalizado para gravar dados em um arquivo externo.

 Quando DATE_FORMAT não for especificado ou é a cadeia de caracteres vazia, o PolyBase usa os seguintes formatos padrão:
  
-   Data e hora: 'AAAA-MM-dd HH'  
  
-   SmallDateTime: 'AAAA-MM-dd hh: mm'  
  
-   Data: 'AAAA-MM-dd'  
  
-   DateTime2: 'yyyy-MM-dd HH:mm:ss'  
  
-   DateTimeOffset: 'yyyy-MM-dd HH:mm:ss'  
  
-   Hora: 'HH'  
  
 **Exemplos de formatos de data** estão na tabela a seguir.  
  
 Observações sobre a tabela:  
  
-   Ano, mês e dia podem ter uma variedade de formatos e pedidos. A tabela mostra apenas o **ymd** formato. Mês podem ter 1 ou 2 dígitos, ou 3 caracteres. Dia pode ter 1 ou 2 dígitos. Ano pode ter de 2 ou 4 dígitos.
  
-   Milissegundos (fffffff) não é necessária.
  
-   AM, pm (tt) não é necessária. O padrão é AM.
  
|Tipo de data|Exemplo|Description|  
|---------------|-------------|-----------------|  
|DateTime|DATE_FORMAT = 'AAAA-MM-dd HH:mm:ss.fff'|Além de ano, mês e dia, esse formato de data inclui 00-24 horas, 00-59 minutos, 00-59 segundos e 3 dígitos para milissegundos.|  
|DateTime|DATE_FORMAT = 'AAAA-MM-dd hh:mm:ss.ffftt'|Além de ano, mês e dia, esse formato de data inclui 00-12 horas, 00-59 minutos, 00-59 segundos, 3 dígitos para milissegundos e AM, am, PM ou pm. |  
|SmallDateTime|DATE_FORMAT = 'AAAA-MM-dd hh: mm'|Além de ano, mês e dia, esse formato de data inclui 00-23 horas, 00-59 minutos.|  
|SmallDateTime|DATE_FORMAT = 'AAAA-MM-dd hh:mmtt'|Além de ano, mês e dia, esse formato de data inclui 00-11 horas, 00-59 minutos, sem segundos e AM, am, PM ou pm.|  
|Data|DATE_FORMAT = 'AAAA-MM-dd'|Ano, mês e dia. Nenhum elemento de hora é incluído.|  
|Data|DATE_FORMAT = 'AAAA-MMM-dd'|Ano, mês e dia. Quando o mês é especificado com 3 M, o valor de entrada é uma ou cadeias de janeiro, fevereiro, março, abril, maio, Jun, julho, agosto, set, out, Nov ou dez.|  
|datetime2|DATE_FORMAT = 'AAAA-MM-dd: ss. FFFFFFF'|Além de ano, mês e dia, esse formato de data inclui 00-23 horas, 00-59 minutos, 00-59 segundos e 7 dígitos para milissegundos.|  
|datetime2|DATE_FORMAT = 'AAAA-MM-dd hh:mm:ss.ffffffftt'|Além de ano, mês e dia, esse formato de data inclui 00-11 horas, 00-59 minutos, 00-59 segundos, de 7 dígitos para milissegundos e AM, am, PM ou pm.|  
|DateTimeOffset|DATE_FORMAT = 'AAAA-MM-dd: ss. FFFFFFF zzz'|Além de ano, mês e dia, esse formato de data inclui 00-23 horas, 00-59 minutos, 00-59 segundos e 7 dígitos para milissegundos e o deslocamento de fuso horário que você coloca no arquivo de entrada como `{+&#124;-}HH:ss`. Por exemplo, desde a hora Los Angeles sem verão economia é 8 horas antes do UTC, um valor de -08:00 no arquivo de entrada especifica o fuso horário de Brasília.|  
|DateTimeOffset|DATE_FORMAT = 'AAAA-MM-dd hh:mm:ss.ffffffftt zzz'|Além de ano, mês e dia, esse formato de data inclui 00-11 horas, 00-59 minutos, 00-59 segundos, 7 dígitos para milissegundos, (AM, am, PM ou pm) e o deslocamento de fuso horário. Consulte a descrição da linha anterior.|  
|Hora|DATE_FORMAT = 'HH:mm:ss'|Não há nenhum valor de data, apenas de 00 a 23 horas, 00-59 minutos e 00-59 segundos.|  
  
 Todos os formatos de data com suporte:
  
|datetime|smalldatetime|date|datetime2|datetimeoffset|  
|--------------|-------------------|----------|---------------|--------------------|  
|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fff]|[M[M]]M-[d]d-[yy]yy HH:mm[:00]|[M[M]]M-[d]d-[yy]yy|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fffffff]|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fffffff] zzz|  
|[M[M]]M-[d]d-[yy]yy hh:mm:ss[.fff][tt]|[M [M]] M-[d] d-[AA] AA hh: mm [: 00] [tt]||[M [M]] M-[d] d-[AA] AA hh [. FFFFFFF] [tt]|[M [M]] M-[d] d-[AA] AA hh [. FFFFFFF] [tt] zzz|  
|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fff]|[M[M]]M-[yy]yy-[d]d HH:mm[:00]|[M[M]]M-[yy]yy-[d]d|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fffffff]|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fffffff] zzz|  
|[M[M]]M-[yy]yy-[d]d hh:mm:ss[.fff][tt]|[M [M]] M-[AA] AA-[d] d hh: mm [: 00] [tt]||[M[M]]M-[yy]yy-[d]d hh:mm:ss[.fffffff][tt]|[M [M]] M-[AA] AA-[d] d hh [. FFFFFFF] [tt] zzz|  
|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fff]|[yy]yy-[M[M]]M-[d]d HH:mm[:00]|[yy]yy-[M[M]]M-[d]d|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fffffff]|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fffffff]  zzz|  
|[yy]yy-[M[M]]M-[d]d hh:mm:ss[.fff][tt]|[AA] AA-[[M] M] M-[d] d hh: mm [: 00] [tt]||[yy]yy-[M[M]]M-[d]d hh:mm:ss[.fffffff][tt]|[AA] AA-[[M] M] M-[d] d hh [. FFFFFFF] [tt] zzz|  
|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fff]|[yy]yy-[d]d-[M[M]]M HH:mm[:00]|[yy]yy-[d]d-[M[M]]M|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fffffff]|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fffffff]  zzz|  
|[yy]yy-[d]d-[M[M]]M hh:mm:ss[.fff][tt]|[AA] AA-[d] d-[[M] M] M hh: mm [: 00] [tt]||[yy]yy-[d]d-[M[M]]M hh:mm:ss[.fffffff][tt]|[AA] AA-[d] d-[[M] M] M hh [. FFFFFFF] [tt] zzz|  
|[d]d-[M[M]]M-[yy]yy HH:mm:ss[.fff]|[d]d-[M[M]]M-[yy]yy HH:mm[:00]|[d]d-[M[M]]M-[yy]yy|[d]d-[M[M]]M-[yy]yy HH:mm:ss[.fffffff]|[d]d-[M[M]]M-[yy]yy HH:mm:ss[.fffffff] zzz|  
|[d] d-[[M] M] M-[AA] AA hh [. fff] [tt]|[d] d-[[M] M] M-[AA] AA hh: mm [: 00] [tt]||[d] d-[[M] M] M-[AA] AA hh [. FFFFFFF] [tt]|[d] d-[[M] M] M-[AA] AA hh [. FFFFFFF] [tt] zzz|  
|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fff]|[d]d-[yy]yy-[M[M]]M HH:mm[:00]|[d]d-[yy]yy-[M[M]]M|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fffffff]|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fffffff]  zzz|  
|[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fff][tt]|[d] d-[AA] AA-[[M] M] M hh: mm [: 00] [tt]||[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fffffff][tt]|[d] d-[AA] AA-[[M] M] M hh [. FFFFFFF] [tt] zzz|  
  
 Detalhes:  
  
-   Para separar os valores do mês, dia e ano, você pode usar '-', '/' ou '. '. Para simplificar, a tabela usa apenas o separador '-'.
  
-   Para especificar o mês como texto, use três ou mais caracteres. Meses com 1 ou 2 caracteres são interpretados como um número.
  
-   Para separar os valores de tempo, use o ': ' símbolo.
  
-   Letras entre colchetes são opcionais.
  
-   As letras 'tt' designam [AM | PM | am | pm]. AM é o padrão. Quando 'tt' for especificado, o valor de hora (hh) deve ser no intervalo de 0 a 12.
  
-   As letras 'zzz' designam o deslocamento de fuso horário para a zona de tempo atual do sistema no formato {+ |-} HH:ss].
  
 USE_TYPE_DEFAULT = {TRUE | **FALSE** } Especifica como tratar valores ausentes em arquivos de texto delimitados quando PolyBase recupera dados do arquivo de texto.
  
 TRUE quando cada valor ausente de armazenamento de recuperação de dados do arquivo de texto, usando o valor padrão para o tipo de dados da coluna correspondente na definição da tabela externa. Por exemplo, substitua um valor ausente com:  
  
-   0 se a coluna é definida como uma coluna numérica.
  
-   Cadeia de caracteres vazia "" se a coluna é uma coluna de cadeia de caracteres.
  
-   1900-01-01 se a coluna é uma coluna de data.
  
 Os valores FALSE repositório ausentes como NULL. Quaisquer valores NULL são armazenados usando a palavra NULL no arquivo de texto delimitado são importadas como a cadeia de caracteres 'Nulo'.
  
   Codificação = {'UTF8' | 'UTF16}' no Azure SQL Data Warehouse, o PolyBase pode ler UTF8 e codificado UTF16-LE delimitada por arquivos de texto. No SQL Server e PDW, PolyBase não suporta leitura UTF16 arquivos codificados.
  
 DATA_COMPRESSION = *data_compression_method* Especifica o método de compactação de dados para dados externos. Quando DATA_COMPRESSION não for especificado, o padrão é dados não compactados.
 Para funcionar adequadamente, Gzip compactada de arquivos devem ter a extensão de arquivo ".gz".
 
 O tipo de formato DELIMITEDTEXT dá suporte a esses métodos de compactação:
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec'
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'

 O tipo de formato RCFILE dá suporte a esse método de compactação:
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec'
  
 O tipo de formato de arquivo ORC dá suporte a esses métodos de compactação:
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec'
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'
  
 O tipo de formato de arquivo PARQUET oferece suporte a métodos de compactação do seguinte:
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY EXTERNAL FILE FORMAT.
  
## <a name="general-remarks"></a>Comentários gerais
 O formato de arquivo externo está no escopo do banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Ele está no escopo do servidor em [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
 As opções de formatação são todas opcionais e só se aplicam a arquivos de texto delimitado.  
  
 Quando os dados são armazenados em um dos formatos compactados, o PolyBase descompacta primeiro os dados antes de retornar os registros de dados.
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições
  
 O delimitador de linha em arquivos de texto delimitados deve ser suportado pelo LineRecordReader do Hadoop. Ou seja, ele deve ser o '\r', '\n' ou '\r\n'. Esses delimitadores não são configuráveis pelo usuário.
  
 As combinações de métodos suportados de SerDe com RCFiles e os métodos de compactação de dados com suporte são listadas anteriormente neste artigo. Nem todas as combinações são suportadas.
  
 O número máximo de consultas simultâneas de PolyBase é 32. Quando estiver executando 32 consultas simultâneas, cada consulta pode ler um máximo de 33.000 arquivos do local de arquivo externo. A pasta raiz e cada subpasta também são contados como um arquivo. Se o grau de simultaneidade é menor que 32, o local de arquivo externo pode conter mais de 33.000 arquivos.
  
 Devido a uma limitação no número de arquivos da tabela externa, é recomendável armazenar menor 30.000 arquivos em subpastas do local do arquivo externo e raiz. Além disso, é recomendável manter o número de subpastas sob o diretório raiz para um número pequeno. Quando há muitos arquivos são referenciados, pode ocorrer uma exceção de falta de memória da máquina Virtual Java.
  
  Quando exportar dados para o Hadoop ou armazenamento de BLOBs do Azure por meio do PolyBase, somente os dados são exportados, não o names(metadata) de coluna, conforme definido no comando CREATE EXTERNAL TABLE.

## <a name="locking"></a>Bloqueio  
 Leva um bloqueio compartilhado no objeto de formato de arquivo externo.
  
## <a name="performance"></a>Desempenho
 Usar arquivos compactados sempre vem com a compensação entre a transferência de menos dados entre a fonte de dados externa e o SQL Server enquanto aumenta o uso da CPU para compactar e descompactar os dados.
  
 Arquivos de texto gzip compactada não são divisíveis. Para melhorar o desempenho Gzip compactada para arquivos de texto, é recomendável gerar vários arquivos são armazenados no mesmo diretório na fonte de dados externa. Isso permite que o PolyBase ler e descompactar os dados mais rápidos por meio de vários processos de leitor e descompactação. O número ideal de arquivos compactados é o número máximo de processos de leitor de dados por nó de computação. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], o número máximo de processos de leitor de dados é de 8 por nó na versão atual. Em [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], o número máximo de processos de leitor de dados por nó varia por SLO. Consulte [Azure SQL Data Warehouse carregar padrões e estratégias de](https://blogs.msdn.microsoft.com/sqlcat/2016/02/06/azure-sql-data-warehouse-loading-patterns-and-strategies/) para obter detalhes.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-create-a-delimitedtext-external-file-format"></a>A. Criar um formato de arquivo externo DELIMITEDTEXT  
 Este exemplo cria um formato de arquivo externo denominado *textdelimited1* para um arquivo delimitado por texto. As opções listadas para o formato\_opções especificam que os campos no arquivo devem ser separados usando um caractere de pipe ' |'. O arquivo de texto também é compactado com o codec Gzip. Se dados\_compactação não for especificada, o arquivo de texto é compactado.
  
 Para um arquivo de texto delimitado, o método de compactação de dados pode ser o padrão de Codec, 'org.apache.hadoop.io.compress.DefaultCodec' ou o Gzip Codec, 'org.apache.hadoop.io.compress.GzipCodec'.
  
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
  
### <a name="b-create-an-rcfile-external-file-format"></a>B. Criar um formato de arquivo RCFile  
 Este exemplo cria um formato de arquivo externo para um RCFile que usa o org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe do método de serialização/desserialização. Ela também especifica para usar o Codec padrão para o método de compactação de dados. Se DATA_COMPRESSION não for especificado, o padrão é sem compactação.
  
```  
CREATE EXTERNAL FILE FORMAT rcfile1  
WITH (  
    FORMAT_TYPE = RCFILE,  
    SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe',  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec'  
);  
```  
  
### <a name="c-create-an-orc-external-file-format"></a>C. Criar um formato de arquivo ORC  
 Este exemplo cria um formato de arquivo externo para um arquivo ORC que compacta os dados com o método de compactação de dados org.apache.io.compress.SnappyCodec. Se DATA_COMPRESSION não for especificado, o padrão é sem compactação.
  
```  
CREATE EXTERNAL FILE FORMAT orcfile1  
WITH (  
    FORMAT_TYPE = ORC,  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'  
);  
```  
  
### <a name="d-create-a-parquet-external-file-format"></a>D. Criar um formato de arquivo externo PARQUET  
 Este exemplo cria um formato de arquivo externo para um arquivo Parquet que compacta os dados com o método de compactação de dados org.apache.io.compress.SnappyCodec. Se DATA_COMPRESSION não for especificado, o padrão é sem compactação.  
  
```  
CREATE EXTERNAL FILE FORMAT parquetfile1  
WITH (  
    FORMAT_TYPE = PARQUET,  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'  
);  
```  
  
## <a name="see-also"></a>Consulte também
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [CREATE EXTERNAL TABLE AS SELECT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [Criar tabela como SELECT &#40; Depósito de dados SQL do Azure &#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)   
 [sys.external_file_formats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)  
