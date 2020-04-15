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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: efe1fdccbef4f5c4a393083f6eb81efee759be5c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302565"
---
# <a name="sqldescribeparam"></a>SQLDescribeParam
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Para descrever os parâmetros de qualquer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] declaração SQL, o driver [!INCLUDE[tsql](../../includes/tsql-md.md)] ODBC do Cliente Nativo constrói e executa uma declaração SELECT quando o SQLDescribeParam é chamado em uma alça de declaração ODBC preparada. Os metadados do conjunto de resultados determinam as características dos parâmetros na instrução preparada. SQLDescribeParam pode retornar qualquer código de erro que SQLExecute ou SQLExecDirect possam retornar.  
  
 Melhorias no mecanismo [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] de banco de dados a partir de permitir que o SQLDescribeParam obtenha descrições mais precisas dos resultados esperados. Esses resultados mais precisos podem diferir dos valores retornados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]pelo SQLDescribeParam nas versões anteriores de . Para obter mais informações, veja [Descoberta de metadados](../../relational-databases/native-client/features/metadata-discovery.md).  
  
 Também novo [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]em , *ParameterSizePtr* agora retorna um valor que se alinha com a definição para o tamanho, em caracteres, da coluna ou expressão do marcador de parâmetro correspondente conforme definido na [especificação ODBC](https://go.microsoft.com/fwlink/?LinkId=207044). Nas versões [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores do Cliente Nativo, O *ParâmetroSizePtr* poderia ser o valor correspondente de **SQL_DESC_OCTET_LENGTH** para o tipo, ou um valor de tamanho de coluna irrelevante fornecido ao SQLBindParameter para um tipo, o valor do qual deve ser ignorado **(SQL_INTEGER,** por exemplo).  
  
 O driver não suporta chamar SQLDescribeParam nas seguintes situações:  
  
-   Após SQLExecDirect [!INCLUDE[tsql](../../includes/tsql-md.md)] para quaisquer instruções UPDATE ou DELETE contendo a cláusula FROM.  
  
-   Para qualquer instrução ODBC ou [!INCLUDE[tsql](../../includes/tsql-md.md)] que contenha um parâmetro em uma cláusula HAVING, ou comparada ao resultado de uma função SUM.  
  
-   Para qualquer instrução ODBC ou [!INCLUDE[tsql](../../includes/tsql-md.md)] que dependa de uma subconsulta que contém parâmetros.  
  
-   Para instruções SQL ODBC que contenham marcadores de parâmetro em ambas as expressões de uma comparação, like, ou predicado quantificado.  
  
-   Para qualquer consulta em que um dos parâmetros é um parâmetro para uma função.  
  
-   Quando houver comentários (/* \*/) no [!INCLUDE[tsql](../../includes/tsql-md.md)] comando.  
  
 Ao processar um [!INCLUDE[tsql](../../includes/tsql-md.md)] lote de declarações, o driver também não suporta chamar SQLDescribeParam para marcadores de parâmetros em declarações após a primeira instrução no lote.  
  
 Ao descrever os parâmetros dos procedimentos armazenados preparados, o SQLDescribeParam usa o procedimento armazenado no sistema [sp_sproc_columns](../../relational-databases/system-stored-procedures/sp-sproc-columns-transact-sql.md) para recuperar características dos parâmetros. sp_sproc_columns podem relatar dados para procedimentos armazenados no banco de dados do usuário atual. A preparação de um nome de procedimento armazenado totalmente qualificado permite que o SQLDescribeParam seja executado em bancos de dados. Por exemplo, o procedimento armazenado no sistema [sp_who](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) pode ser preparado e executado em qualquer banco de dados como:  
  
```  
SQLPrepare(hstmt, "{call sp_who(?)}", SQL_NTS);  
```  
  
 A execução do SQLDescribeParam após a preparação bem sucedida retorna um conjunto de linhas vazias quando conectado a qualquer banco de dados, mas **mestre**. A mesma chamada, preparada da seguinte forma, faz com que o SQLDescribeParam tenha sucesso independentemente do banco de dados do usuário atual:  
  
```  
SQLPrepare(hstmt, "{call master..sp_who(?)}", SQL_NTS);  
```  
  
 Para tipos de dados de grande valor, o valor devolvido no *DataTypePtr* é SQL_VARCHAR, SQL_VARBINARY ou SQL_NVARCHAR. Para indicar que o tamanho do parâmetro de tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de dados de grande valor é "ilimitado", o driver Cliente Nativo ODBC define *ParameterSizePtr* para 0. Os valores reais de tamanho são devolvidos para parâmetros padrão **de varchar.**  
  
> [!NOTE]  
>  Se o parâmetro já tiver sido associado a um tamanho máximo para os parâmetros SQL_VARCHAR, SQL_VARBINARY ou SQL_WVARCHAR, o tamanho associado do parâmetro será retornado, não "ilimitado".  
  
 Para associar um parâmetro de entrada de tamanho "ilimitado", dados em execução devem ser usados. Não é possível vincular um parâmetro de saída de tamanho "ilimitado" (não há nenhum método para transmitir dados de um parâmetro de saída, como [o SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) faz para conjuntos de resultados).  
  
 No caso de parâmetros de saída, um buffer deve ser associado e se o valor for muito extenso, o buffer será preenchido e uma mensagem SQL_SUCCESS_WITH_INFO será retornada junto com o aviso "dados de cadeia de caracteres; truncamento à direita". Os dados que foram truncados são descartados em seguida.  
  
## <a name="sqldescribeparam-and-table-valued-parameters"></a>SQLDescribeParam e parâmetros com valor de tabela  
 Um aplicativo pode recuperar informações de parâmetros de valor de tabela para uma declaração preparada com o SQLDescribeParam. Para obter mais informações, consulte [Metadados de parâmetros avaliados em tabela para declarações preparadas](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md).  
  
 Para obter mais informações sobre parâmetros de valor de tabela em geral, consulte [Parâmetros valorizados em tabela &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqldescribeparam-support-for-enhanced-date-and-time-features"></a>Suporte SQLDescribeParam para recursos avançados de data e hora  
 Os valores retornados para tipos de data/hora são os seguintes:  
  
||*DataTypePtr*|*ParâmetroSizePtr*|*Digitsptr decimal*|  
|-|-------------------|------------------------|------------------------|  
|DATETIME|SQL_TYPE_TIMESTAMP|23|3|  
|smalldatetime|SQL_TYPE_TIMESTAMP|16|0|  
|date|SQL_TYPE_DATE|10|0|  
|time|SQL_SS_TIME2|8, 10..16|0..7|  
|datetime2|SQL_TYPE_TIMESTAMP|19, 21..27|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|26, 28..34|0..7|  
  
 Para obter mais informações, consulte [melhorias de data e hora &#40;&#41;da ODBC ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqldescribeparam-support-for-large-clr-udts"></a>Suporte SQLDescribeParam para UDTs CLR grandes  
 **O SQLDescribeParam** suporta grandes tipos de UDTs (ClR definidos pelo usuário). Para obter mais informações, consulte [Grandes tipos definidos pelo usuário da CLR &#40;&#41;ODBC ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLDescribeParam](https://go.microsoft.com/fwlink/?LinkId=59339)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
