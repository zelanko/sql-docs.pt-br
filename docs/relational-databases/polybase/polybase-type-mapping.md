---
title: Mapeamento de tipo com o PolyBase | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9839c46f477fe31d29214eed10dce0d673c9fd00
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47732594"
---
# <a name="type-mapping-with-polybase"></a>Mapeamento de tipo com o PolyBase

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve o mapeamento entre fontes de dados externas do PolyBase e o SQL Server. Você pode usar essas informações para definir corretamente as tabelas externas com o comando Transact-SQL [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md).

## <a name="overview"></a>Visão geral

Ao criar tabelas externas com o PolyBase, as definições de coluna, incluindo os tipos de dados e o número de colunas, precisam corresponder aos dados nos arquivos externos. Se houver uma incompatibilidade, as linhas do arquivo serão rejeitadas durante a consulta dos dados reais.  
  
Para tabelas externas que referenciam arquivos em fontes de dados externas, as definições de coluna e tipo devem ser mapeadas para o esquema exato do arquivo externo. Ao definir tipos de dados que referenciam dados armazenados no Hadoop/Hive, use os mapeamentos a seguir entre tipos de dados SQL e Hive e converta o tipo em um tipo de dados SQL ao selecionar uma opção nele. Os tipos incluem todas as versões do Hive, a menos que indicado de outra forma.

> [!NOTE]  
> O SQL Server não dá suporte ao valor de dados *infinity* do Hive em uma conversão. O PolyBase falhará com um erro de conversão de tipo de dados.

## <a name="hadoop-type-mapping-reference"></a>Referência de mapeamento de tipos Hadoop

| Tipo de dados SQL | Tipo de dados .NET            | Tipo de dados do Hive | Tipo de dados do Hadoop/Java | Comentários                       |
| ------------- | ------------------------- | -------------- | --------------------- | ------------------------------ |
| TINYINT       | Byte                      | TINYINT        | ByteWritable          | Apenas para números sem sinal.     |
| SMALLINT      | Int16                     | SMALLINT       | ShortWritable         |
| INT           | Int32                     | INT            | IntWritable           |
| BIGINT        | Int64                     | BIGINT         | LongWritable          |
| bit           | Booliano                   | booleano        | BooleanWritable       |
| FLOAT         | Double                    | double         | DoubleWritable        |
| REAL          | Single                    | FLOAT          | FloatWritable         |
| money         | Decimal                   | double         | DoubleWritable        |
| SMALLMONEY    | Decimal                   | double         | DoubleWritable        |
| NCHAR         | Cadeia de caracteres<br /><br /> Char[] | cadeia de caracteres         | text                  |
| NVARCHAR      | Cadeia de caracteres<br /><br /> Char[] | cadeia de caracteres         | Texto                  |
| char          | Cadeia de caracteres<br /><br /> Char[] | cadeia de caracteres         | Texto                  |
| varchar       | Cadeia de caracteres<br /><br /> Char[] | cadeia de caracteres         | Texto                  |
| BINARY        | Byte[]                    | BINARY         | BytesWritable         | Aplica-se ao Hive 0.8 e posterior. |
| varbinary     | Byte[]                    | BINARY         | BytesWritable         | Aplica-se ao Hive 0.8 e posterior. |
| Data          | DateTime                  | timestamp      | TimestampWritable     |
| smalldatetime | DateTime                  | timestamp      | TimestampWritable     |
| datetime2     | DateTime                  | timestamp      | TimestampWritable     |
| DATETIME      | DateTime                  | timestamp      | TimestampWritable     |
| time          | TimeSpan                  | timestamp      | TimestampWritable     |
| Decimal       | Decimal                   | Decimal        | BigDecimalWritable    | Aplica-se ao Hive 0.11 e posterior. |

<!--SQL Server 2019-->
::: moniker range=">= sql-server-ver15 || =sqlallproducts-allversions"

## <a name="oracle-type-mapping-reference"></a>Referência de mapeamento de tipos Oracle

| Tipo de dados de Oracle              | Tipo de SQL Server |
| ----------------------------- | --------------- |
| float                         | float           |
| Decimal                       | Decimal         |
| Int                           | Int             |
| Longo                          | Ntext           |
| Binary Float                  | Real            |
| Char                          | Nchar           |
| Varchar2                      | nvarchar        |
| Raw                           | Varbinary       |
| Long Raw                      | image           |
| Bfile                         | image           |
| Blob                          | image           |
| Clob                          | image           |
| Rowid                         | Varchar         |
| data                          | Datetime2       |
| Timestamp                     | Datetime2       |
| Timestamp with local timezone | Datetime2       |

### <a name="type-mismatch-float"></a>Tipos incompatíveis (Float)

A Oracle é compatível a precisão de ponto flutuante de 126, que é inferior àquela compatível com o SQL Server (53). Portanto, **Float (1 a 53)** pode ser mapeado diretamente, porém, além disso, ocorre perda de dados devido ao truncamento.

### <a name="type-mismatch-character-types"></a>Tipos incompatíveis (tipos de caracteres)

Para tipos como **Long** e **Bfile**, a Oracle é compatível com tipos de dados com tamanho de 4 GB. O SQL Server é compatível com um tamanho de 2 GB. Da mesma forma, para tipos de dados oracle **Blob** e **clob**, a Oracle pode ser compatível com até 128 TB, enquanto o SQL server **LONGVARBINARY** ou **WLONGVARBINARY** não são compatíveis com mais de 2 GB. Mapear tipos com um tipo de dados com tamanho superior a 2 GB pode resultar em truncamento de dados.  

### <a name="type-mismatch-timestamp"></a>Tipos incompatíveis (Timestamp)

**Timestamp** e **Timestamp with local timezone** no Oracle são compatíveis com precisão de nove frações de segundos. O SQL Server DateTime2 é compatível com a precisão de sete frações de segundo.

Além disso, o Simba mapeia **Date**, **Timestamp** e **Timestamp with local zone** para o tipo de ODBC **SQL_TIMESTAMP** e, eventualmente, para o tipo do SQL Server **Timestamp**. **Timestamp** é uma ID de linha exclusiva gerada automaticamente. O ideal é que **SQL_TIMESTAMP** seja mapeado para o tipo do SQL Server **DateTime/DateTime2** ou os tipos de Oracle **Date**, **Timestamp**, e **Timestamp with local zone** deve ser mapeado para o tipo de ODBC **SQL_TYPE_TIMESTAMP**.

### <a name="driver-configuration-option"></a>Opções de configuração de driver

O tamanho do buffer padrão para colunas **Long/LOB** é 1024 KB (configurável).

## <a name="mongo-type-mapping-reference"></a>Referência de mapeamento de tipos Mongo

| Tipo de dados BSON     | Tipo de SQL Server |
| ------------------ | --------------- |
| Double             | float           |
| Cadeia de caracteres             | nvarchar        |
| Object             |
| Array              |
| Dados binários        | nvarchar        |
| ID de objeto          | nvarchar        |
| Booliano            | bit             |
| data               | Datetime2       |
| Inteiro de 32 bits     | Int             |
| Timestamp          | nvarchar        |
| Inteiro de 64 bits     | BigInt          |
| DBPointer          | nvarchar        |
| Javascript         | nvarchar        |
| Chave máxima            | nvarchar        |
| Chave mínima            | nvarchar        |
| Símbolo             | nvarchar        |
| Expressão regular | nvarchar        |
| Indefinido/NULO     | nvarchar        |

### <a name="javascript-with-scope"></a>Javascript (com escopo)

O driver retorna o valor como uma cadeia de caracteres que contém “Javascript com escopo incompatível”.

### <a name="type-mismatch-string"></a>Tipos incompatíveis (cadeia de caracteres)

Cadeias de caracteres do MongoDB são convertidas no tipo **SQL_WVARCHAR** tipo com um tamanho de coluna padrão de 255. Esse tamanho de coluna é ajustável como parte da configuração do driver. Apesar de ser possível configurá-lo, o **SQL_WVARCHAR** ou o tipo do SQL Server **Varchar** é compatível com apenas no máximo 2 GB, enquanto o MongoDB pode conter dados de até 4 GB. Isso pode resultar em truncamento de dados.

### <a name="mongodb-driver-options"></a>Opções de driver do MongoDB

- **Habilitar o buffer duplo**: selecionado por padrão.
- **Documentos para efetuar fetch por bloco**: padrão de 4096.
- **Expor cadeia de caracteres como SQL_WVARCHAR**: selecionado por padrão. Se não forem selecionadas, as cadeias de caracteres são expostas como SQL_VARCHAR.
- **Tamanho da coluna de cadeia de caracteres**: padrão de 255.
- **Expor binário como SQL_LONGVARBINARY**: padrão selecionado. Se não for selecionado, o binário é exposto como SQL_VARBINARY.
- **Tamanho da coluna de binário**: padrão de 32767.
- **Habilitar transmissão**: padrão selecionado.

### <a name="schema-related-driver-configurations"></a>Configurações de driver relacionados ao esquema

- **LoadMetadataTable**: padrão do banco de dados. Solicita que o driver carregue a definição do esquema do arquivo JSON especificado.
- **LocalMetadataFile**: em caso de leitura de um arquivo, o caminho completo precisa ser especificado.
- **Método de amostragem**:  
  - **padrão para a frente**: o driver seleciona as amostras de dados a partir do primeiro registro.
  - **para trás**: o driver seleciona as amostras de dados a partir do último registro.
- **SamplingLimit**: padrão de 100 (número máximo de registros que o driver pode selecionar como amostras para gerar a definição de esquema temporário). Quando definido como 0, o driver seleciona todos os documentos como amostras.
- **SamplingStepSize**: padrão de 1 (intervalo no qual o driver seleciona os registros como amostras durante a verificação do banco de dados para gerar a definição de esquema temporário). Por exemplo, quando definido como 2, ele obtém um a cada dois registros no banco de dados.

## <a name="teradata-type-mapping-reference"></a>Referência de mapeamento de tipos Teradata

| Tipo de dados Teradata               | Tipo de SQL Server |
| -------------------------------- | --------------- |
| Int                              | Int             |
| Small Int                        | SmallInt        |
| Big Int                          | BigInt          |
| Byte Int                         | TinyInt         |
| Decimal                          | Decimal         |
| float                            | float           |
| Byte                             | Binary          |
| Varbyte                          | Varbinary       |
| Blob                             | image           |
| Char                             | Nchar           |
| Clob                             | Ntext           |
| Varchar                          | nvarchar        |
| Graphic                          | Nchar           |
| JSON                             | Ntext           |
| Vargraphic                       | nvarchar        |
| data                             | data            |
| Hora                             | Hora            |
| Time with Time Zone              | Hora            |
| Timestamp                        | Datetime2       |
| Interval Year                    |
| Interval year to month           |
| Interval Month                   |
| Interval Day                     |
| Interval Day to Hour             |
| Interval Day to Minute           |
| Interval Day to Second           |
| Interval Hour                    |
| Interval Hour to Minute          |
| Interval Hour to Second          |
| Interval Minute                  |
| Interval Minute to Second        |
| Interval Second                  |
| Period (DATE)                    |
| Period (TIME)                    |
| Period (TIME with Timezone)      |
| Period (Timestamp)               |
| Period (Timestamp with Timezone) |

### <a name="period-data-type"></a>Tipo de dados Period

O tipo de dados **Period** representam uma duração marcada por um limite de início e de final. Essencialmente, é uma tupla. Não há nenhum tipo equivalente ao SQL Server para **Período**.

### <a name="time-with-time-zone-and-timestamp"></a>Time with Time Zone e Timestamp

**Time with Time Zone** e **Timestamp** contém a diferença de fuso horário, que é perdido durante translação. Isso pode ser corrigido se for mapeado para **SQL_Type_Time/SQL_Type_Timestamp** para **datetimeoffset** em vez de **Time/DateTime2**.

### <a name="byteint"></a>ByteInt

O Simba mapeia o tipo de Teradata **ByteInt**, que pode conter valores entre 0 e 255, em **TinyInt** que pode conter valores de -127 a 127. Isso pode resultar em truncamento.  

### <a name="clob"></a>CLOB

O tipo de dados **CLOB** com o conjunto de caracteres **LATIN** pode aceitar 2097088000 caracteres. No entanto, além de 1073741823, o tamanho do buffer se torna negativo.  

### <a name="driver-configuration-options"></a>Opções de configuração de driver

- Use os dados **DATE** para os parâmetros **TIMESTAMP**.
- Habilite o modo de catálogo personalizado para aplicativos 2.X.
- Retorne a cadeia de caracteres vazia na coluna **CREATE_PARAMS** para **SQL_TIMESTAMP**.
- Retorno máximo. Tamanho de **CHAR/VARCHAR** como 32 K.

::: moniker-end

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como isso é usado, consulte o artigo de referência do Transact-SQL sobre [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md).
