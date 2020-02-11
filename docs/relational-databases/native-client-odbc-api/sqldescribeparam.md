---
title: SQLDescribeParam | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLDescribeParam function
ms.assetid: 396e74b1-5d08-46dc-b404-2ef2003e4689
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: aa74f982a5ff1894651d68f06689cba476a16452
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73787110"
---
# <a name="sqldescribeparam"></a>SQLDescribeParam
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Para descrever os parâmetros de qualquer instrução SQL, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client cria e executa uma [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução SELECT quando SQLDescribeParam é chamado em um identificador de instrução ODBC preparado. Os metadados do conjunto de resultados determinam as características dos parâmetros na instrução preparada. SQLDescribeParam pode retornar qualquer código de erro que SQLExecute ou SQLExecDirect possa retornar.  
  
 Melhorias no mecanismo de banco de dados [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] começando com permitir SQLDescribeParam para obter descrições mais precisas dos resultados esperados. Esses resultados mais precisos podem ser diferentes dos valores retornados pelo SQLDescribeParam em versões anteriores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]do. Para obter mais informações, veja [Descoberta de metadados](../../relational-databases/native-client/features/metadata-discovery.md).  
  
 Também novo no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], *ParameterSizePtr* agora retorna um valor que se alinha com a definição do tamanho, em caracteres, da coluna ou expressão do marcador de parâmetro correspondente, conforme definido na [especificação ODBC](https://go.microsoft.com/fwlink/?LinkId=207044). Nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, *ParameterSizePtr* poderia ser o valor correspondente de **SQL_DESC_OCTET_LENGTH** para o tipo, ou um valor de tamanho de coluna irrelevante que foi fornecido a SQLBindParameter para um tipo, o valor que deve ser ignorado (**SQL_INTEGER**, por exemplo).  
  
 O driver não dá suporte à chamada de SQLDescribeParam nas seguintes situações:  
  
-   Após SQLExecDirect para quaisquer [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções UPDATE ou DELETE que contenham a cláusula FROM.  
  
-   Para qualquer instrução ODBC ou [!INCLUDE[tsql](../../includes/tsql-md.md)] que contenha um parâmetro em uma cláusula HAVING, ou comparada ao resultado de uma função SUM.  
  
-   Para qualquer instrução ODBC ou [!INCLUDE[tsql](../../includes/tsql-md.md)] que dependa de uma subconsulta que contém parâmetros.  
  
-   Para instruções SQL ODBC que contenham marcadores de parâmetro em ambas as expressões de uma comparação, like, ou predicado quantificado.  
  
-   Para qualquer consulta em que um dos parâmetros é um parâmetro para uma função.  
  
-   Quando houver comentários (/* \*/) no [!INCLUDE[tsql](../../includes/tsql-md.md)] comando.  
  
 Ao processar um lote de [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções, o driver também não oferece suporte à chamada de SQLDescribeParam para marcadores de parâmetro em instruções após a primeira instrução no lote.  
  
 Ao descrever os parâmetros dos procedimentos armazenados preparados, o SQLDescribeParam usa o procedimento armazenado do sistema [sp_sproc_columns](../../relational-databases/system-stored-procedures/sp-sproc-columns-transact-sql.md) para recuperar as características do parâmetro. sp_sproc_columns pode relatar dados para procedimentos armazenados no banco de dados do usuário atual. Preparar um nome de procedimento armazenado totalmente qualificado permite que o SQLDescribeParam seja executado em bancos de dados. Por exemplo, o procedimento armazenado do sistema [sp_who](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) pode ser preparado e executado em qualquer banco de dados como:  
  
```  
SQLPrepare(hstmt, "{call sp_who(?)}", SQL_NTS);  
```  
  
 A execução de SQLDescribeParam após a preparação bem-sucedida retorna um conjunto de linhas vazio quando conectado a qualquer banco de dados, mas **mestre**. A mesma chamada, preparada da seguinte maneira, faz com que o SQLDescribeParam seja bem sucedido, independentemente do banco de dados de usuário atual:  
  
```  
SQLPrepare(hstmt, "{call master..sp_who(?)}", SQL_NTS);  
```  
  
 Para tipos de dados de valor grande, o valor retornado em *DataTypePtr* é SQL_VARCHAR, SQL_VARBINARY ou SQL_NVARCHAR. Para indicar que o tamanho do parâmetro de tipo de dados de valor grande é "ilimitado" [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o driver ODBC do Native Client define *ParameterSizePtr* como 0. Os valores de tamanho real são retornados para os parâmetros **varchar** padrão.  
  
> [!NOTE]  
>  Se o parâmetro já tiver sido associado a um tamanho máximo para os parâmetros SQL_VARCHAR, SQL_VARBINARY ou SQL_WVARCHAR, o tamanho associado do parâmetro será retornado, não "ilimitado".  
  
 Para associar um parâmetro de entrada de tamanho "ilimitado", dados em execução devem ser usados. Não é possível associar um parâmetro de saída de tamanho "ilimitado" (não há nenhum método para transmitir dados de um parâmetro de saída, como [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) para conjuntos de resultados).  
  
 No caso de parâmetros de saída, um buffer deve ser associado e se o valor for muito extenso, o buffer será preenchido e uma mensagem SQL_SUCCESS_WITH_INFO será retornada junto com o aviso "dados de cadeia de caracteres; truncamento à direita". Os dados que foram truncados são descartados em seguida.  
  
## <a name="sqldescribeparam-and-table-valued-parameters"></a>SQLDescribeParam e parâmetros com valor de tabela  
 Um aplicativo pode recuperar informações de parâmetro com valor de tabela para uma instrução preparada com SQLDescribeParam. Para obter mais informações, consulte [metadados de parâmetro com valor de tabela para instruções preparadas](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md).  
  
 Para obter mais informações sobre parâmetros com valor de tabela em geral, consulte [parâmetros com valor de tabela &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqldescribeparam-support-for-enhanced-date-and-time-features"></a>Suporte SQLDescribeParam para recursos avançados de data e hora  
 Os valores retornados para tipos de data/hora são os seguintes:  
  
||*DataTypePtr*|*ParameterSizePtr*|*DecimalDigitsPtr*|  
|-|-------------------|------------------------|------------------------|  
|DATETIME|SQL_TYPE_TIMESTAMP|23|3|  
|smalldatetime|SQL_TYPE_TIMESTAMP|16|0|  
|date|SQL_TYPE_DATE|10|0|  
|time|SQL_SS_TIME2|8, 10..16|0..7|  
|datetime2|SQL_TYPE_TIMESTAMP|19, 21..27|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|26, 28..34|0..7|  
  
 Para obter mais informações, consulte [melhorias de data e hora &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqldescribeparam-support-for-large-clr-udts"></a>Suporte SQLDescribeParam para UDTs CLR grandes  
 O **SQLDescribeParam** dá suporte a UDTs (tipos definidos pelo usuário) CLR grandes. Para obter mais informações, consulte [tipos CLR grandes definidos pelo usuário &#40;&#41;ODBC ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLDescribeParam](https://go.microsoft.com/fwlink/?LinkId=59339)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
