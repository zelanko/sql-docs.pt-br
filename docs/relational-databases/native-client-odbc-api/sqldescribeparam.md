---
title: SQLDescribeParam | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords: SQLDescribeParam function
ms.assetid: 396e74b1-5d08-46dc-b404-2ef2003e4689
caps.latest.revision: "61"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dfe8843e8b3062f058cfc8de0235dfeecf029004
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="sqldescribeparam"></a>SQLDescribeParam
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Para descrever os parâmetros de qualquer instrução SQL, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client cria e executa um [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução SELECT quando SQLDescribeParam é chamado em um identificador de instrução ODBC preparado. Os metadados do conjunto de resultados determinam as características dos parâmetros na instrução preparada. SQLDescribeParam pode retornar qualquer código de erro que SQLExecute ou SQLExecDirect pode retornar.  
  
 Melhorias no mecanismo de banco de dados, começando com [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] permitir SQLDescribeParam obter descrições mais precisas dos resultados esperados. Esses resultados mais precisos podem ser diferentes dos valores retornados por SQLDescribeParam nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [descoberta de metadados](../../relational-databases/native-client/features/metadata-discovery.md).  
  
 Também novo no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], *ParameterSizePtr* agora retorna um valor que se alinha à definição para o tamanho, em caracteres, da coluna ou expressão do marcador de parâmetro correspondente conforme definido no [ODBC especificação de](http://go.microsoft.com/fwlink/?LinkId=207044). Em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, *ParameterSizePtr* poderia ser o valor correspondente de **SQL_DESC_OCTET_LENGTH** para o tipo ou um valor de tamanho de coluna irrelevante fornecido para SQLBindParameter para um tipo, o valor que deve ser ignorado (**SQL_INTEGER**, por exemplo).  
  
 O driver não oferece suporte SQLDescribeParam chamada nas seguintes situações:  
  
-   Depois de SQLExecDirect para qualquer [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções UPDATE ou DELETE que contém a cláusula FROM.  
  
-   Para qualquer instrução ODBC ou [!INCLUDE[tsql](../../includes/tsql-md.md)] que contenha um parâmetro em uma cláusula HAVING, ou comparada ao resultado de uma função SUM.  
  
-   Para qualquer instrução ODBC ou [!INCLUDE[tsql](../../includes/tsql-md.md)] que dependa de uma subconsulta que contém parâmetros.  
  
-   Para instruções SQL ODBC que contenham marcadores de parâmetro em ambas as expressões de uma comparação, like, ou predicado quantificado.  
  
-   Para qualquer consulta em que um dos parâmetros é um parâmetro para uma função.  
  
-   Quando há comentários (/ * \*/) no [!INCLUDE[tsql](../../includes/tsql-md.md)] comando.  
  
 Durante o processamento de um lote de [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções, o driver também não oferece suporte ao chamar SQLDescribeParam para marcadores de parâmetro em instruções depois da primeira instrução no lote.  
  
 Ao descrever os parâmetros de procedimentos armazenados preparados, SQLDescribeParam usa o procedimento armazenado do sistema [sp_sproc_columns](../../relational-databases/system-stored-procedures/sp-sproc-columns-transact-sql.md) para recuperar características de parâmetro. sp_sproc_columns pode informar dados para procedimentos armazenados no banco de dados do usuário atual. Preparar um nome de procedimento armazenado totalmente qualificado permite SQLDescribeParam executar em bancos de dados. Por exemplo, o sistema de procedimento armazenado [sp_who](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) pode ser preparada e executada em qualquer banco de dados como:  
  
```  
SQLPrepare(hstmt, "{call sp_who(?)}", SQL_NTS);  
```  
  
 Executar SQLDescribeParam após uma preparação bem-sucedida retorna uma linha vazia, defina quando conectado a qualquer banco de dados, mas **mestre**. A mesma chamada, preparada como a seguir, faz com que SQLDescribeParam tenha êxito, independentemente do banco de dados do usuário atual:  
  
```  
SQLPrepare(hstmt, "{call master..sp_who(?)}", SQL_NTS);  
```  
  
 Para tipos de dados de valor grande, o valor retornado em *DataTypePtr* é SQL_VARCHAR, SQL_VARBINARY ou SQL_NVARCHAR. Para indicar que o tamanho do parâmetro de tipo de dados de valor grande é "ilimitado", o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjuntos de driver ODBC Native Client *ParameterSizePtr* como 0. Valores de tamanho reais são retornados para o padrão **varchar** parâmetros.  
  
> [!NOTE]  
>  Se o parâmetro já tiver sido associado a um tamanho máximo para os parâmetros SQL_VARCHAR, SQL_VARBINARY ou SQL_WVARCHAR, o tamanho associado do parâmetro será retornado, não "ilimitado".  
  
 Para associar um parâmetro de entrada de tamanho "ilimitado", dados em execução devem ser usados. Não é possível associar um parâmetro de saída de tamanho "ilimitado" (não há nenhum método para streaming de dados de um parâmetro de saída, como [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) faz para conjuntos de resultados).  
  
 No caso de parâmetros de saída, um buffer deve ser associado e se o valor for muito extenso, o buffer será preenchido e uma mensagem SQL_SUCCESS_WITH_INFO será retornada junto com o aviso "dados de cadeia de caracteres; truncamento à direita". Os dados que foram truncados são descartados em seguida.  
  
## <a name="sqldescribeparam-and-table-valued-parameters"></a>SQLDescribeParam e parâmetros com valor de tabela  
 Um aplicativo pode recuperar informações de parâmetro com valor de tabela para uma instrução preparada com SQLDescribeParam. Para obter mais informações, consulte [metadados de parâmetro com valor de tabela para instruções preparadas](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md).  
  
 Para obter mais informações sobre parâmetros com valor de tabela em geral, consulte [parâmetros com valor de tabela &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqldescribeparam-support-for-enhanced-date-and-time-features"></a>Suporte SQLDescribeParam para recursos avançados de data e hora  
 Os valores retornados para tipos de data/hora são os seguintes:  
  
||*DataTypePtr*|*ParameterSizePtr*|*DecimalDigitsPtr*|  
|-|-------------------|------------------------|------------------------|  
|DATETIME|SQL_TYPE_TIMESTAMP|23|3|  
|smalldatetime|SQL_TYPE_TIMESTAMP|16|0|  
|Data|SQL_TYPE_DATE|10|0|  
|time|SQL_SS_TIME2|8, 10..16|0..7|  
|datetime2|SQL_TYPE_TIMESTAMP|19, 21..27|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|26, 28..34|0..7|  
  
 Para obter mais informações, consulte [data e hora melhorias &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqldescribeparam-support-for-large-clr-udts"></a>Suporte SQLDescribeParam para UDTs CLR grandes  
 **SQLDescribeParam** oferece suporte a grandes CLR definido pelo usuário (UDTs tipos). Para obter mais informações, consulte [Large CLR User-Defined tipos &#40; ODBC &#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLDescribeParam](http://go.microsoft.com/fwlink/?LinkId=59339)   
 [Detalhes da implementação da API do ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
