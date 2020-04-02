---
title: Mapeamento de tipo com o PolyBase | Microsoft Docs
description: Veja nessas tabelas o mapeamento entre as fontes de dados externas do PolyBase e o SQL Server. Definir tabelas externas com CREATE EXTERNAL TABLE do Transact-SQL.
ms.date: 09/24/2018
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
ms.openlocfilehash: 9d4dd55daf26c9f927e23c0f269a084c711d0481
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "80215736"
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
| bit           | Boolean                   | booleano        | BooleanWritable       |
| FLOAT         | Double                    | double         | DoubleWritable        |
| real          | Single                    | FLOAT          | FloatWritable         |
| money         | Decimal                   | double         | DoubleWritable        |
| SMALLMONEY    | Decimal                   | double         | DoubleWritable        |
| NCHAR         | String<br /><br /> Char[] | string         | Varchar               |
| NVARCHAR      | String<br /><br /> Char[] | string         | Varchar               |
| char          | String<br /><br /> Char[] | string         | Varchar               |
| varchar       | String<br /><br /> Char[] | string         | Varchar               |
| binary        | Byte[]                    | binary         | BytesWritable         | Aplica-se ao Hive 0.8 e posterior. |
| varbinary     | Byte[]                    | binary         | BytesWritable         | Aplica-se ao Hive 0.8 e posterior. |
| date          | Datetime                  | timestamp      | TimestampWritable     |
| smalldatetime | Datetime                  | timestamp      | TimestampWritable     |
| datetime2     | Datetime                  | timestamp      | TimestampWritable     |
| DATETIME      | Datetime                  | timestamp      | TimestampWritable     |
| time          | TimeSpan                  | timestamp      | TimestampWritable     |
| decimal       | Decimal                   | decimal        | BigDecimalWritable    | Aplica-se ao Hive 0.11 e posterior. |

<!--SQL Server 2019-->
::: moniker range=">= sql-server-ver15 || =sqlallproducts-allversions"

## <a name="oracle-type-mapping-reference"></a>Referência de mapeamento de tipos Oracle

| Tipo de dados de Oracle | Tipo de SQL Server | 
| -------------    | --------------- |
|Float             |Float            |
|NUMBER            |Decimal          |
|LONG              |nvarchar         |
|BINARY_FLOAT      |Real             | 
|BINARY_DOUBLE     |Float            | 
|CHAR              |Char             |
|VARCHAR2          |Varchar          | 
|NVARCHAR2         |nvarchar         | 
|RAW               |Varbinary        |
|LONG RAW          |Varbinary        | 
|BLOB              |Varbinary        |
|CLOB              |Varchar          |
|NCLOB             | nvarchar        | 
|ROWID             |Varchar          |
|UROWID            |Varchar          | 
|DATE              |Datetime2        |
|timestamp         |Datetime2        | 

**Tipos incompatíveis** 

**Flutuante:** A Oracle é compatível a precisão de ponto flutuante de 126, que é inferior àquela compatível com o SQL Server (53). Portanto, **Float (1 a 53)** pode ser mapeado diretamente, porém, além disso, ocorre perda de dados devido ao truncamento.

**Carimbo de data/hora:** carimbo de data/hora e carimbo de data/hora com fluxo horário local no Oracle são compatíveis com a precisão de 9 segundos fracionários, enquanto DateTime2 do SQL Server dá suporte à precisão de apenas 7 segundos fracionários. 




## <a name="mongodb-type-mapping"></a>Mapeamento de tipo do MongoDB

| Tipo de dados BSON     | Tipo de SQL Server |
| ------------------ | --------------- |
| Double             | Float           |
| String             | nvarchar        |
| Dados binários        | nvarchar        |
| ID de objeto          | nvarchar        |
| Boolean            | bit             |
| Data               | Datetime2       |
| Inteiro de 32 bits     | Int             |
| Timestamp          | nvarchar        |
| Inteiro de 64 bits     | BigInt          |
|Decimal 128         | Decimal         | 
| DBPointer          | nvarchar        |
| Javascript         | nvarchar        |
| Chave máxima            | nvarchar        |
| Chave mínima            | nvarchar        |
| Símbolo             | nvarchar        |
| Expressão regular | nvarchar        |
| Indefinido/NULO     | nvarchar        |


O MongoDB usa documentos BSON para armazenar os registros de dados. Diferentemente de cenários anteriores, o BSON é sem esquema e dá suporte à inserção de documentos e matrizes em outros documentos. Isso proporciona flexibilidade ao usuário. 


## <a name="teradata-type-mapping-reference"></a>Referência de mapeamento de tipos Teradata

| Tipo de dados Teradata | Tipo de SQL Server | 
| -------------      | -------------   |
|INTEGER             |Int              |
|SMALLINT            |SmallInt         |
|bigint              |BigInt           |
|BYTEINT             |SmallInt         |
|DECIMAL             |Decimal          |
|FLOAT               |Decimal          |
|BYTE                |Binário           |
|VARBYTE             |Varbinary        |
|BLOB                |varbinary        |
|CHAR                |Nchar            |
|CLOB                |nvarchar         |
|VARCHAR             |nvarchar         |
|Graphic             |Nchar            |
|JSON                |nvarchar         |
|VARGRAPHIC          |nvarchar         |
|DATE                |Data             |
|timestamp           |Datetime2        |
|TIME                |Hora             |
|TIME WITH TIME ZONE |Hora             |
|TIMESTAMP WITH TIME ZONE|Hora         |

::: moniker-end

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como isso é usado, consulte o artigo de referência do Transact-SQL sobre [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md).
