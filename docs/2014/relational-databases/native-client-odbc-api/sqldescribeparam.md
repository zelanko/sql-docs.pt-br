---
title: SQLDescribeParam | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLDescribeParam function
ms.assetid: 396e74b1-5d08-46dc-b404-2ef2003e4689
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d52d68cc0cd31e9dbb3da25c46901e126252607
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53359488"
---
# <a name="sqldescribeparam"></a>SQLDescribeParam
  Para descrever os parâmetros de qualquer instrução SQL, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client cria e executa um [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução SELECT quando SQLDescribeParam é chamado em um identificador de instrução ODBC preparado. Os metadados do conjunto de resultados determinam as características dos parâmetros na instrução preparada. SQLDescribeParam pode retornar qualquer código de erro que pode retornar SQLExecute ou SQLExecDirect.  
  
 Melhorias no mecanismo de banco de dados a partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] permitir SQLDescribeParam Obtenha descrições mais precisas dos resultados esperados. Esses resultados mais precisos podem ser diferentes dos valores retornados por SQLDescribeParam nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Descoberta de metadados](../native-client/features/metadata-discovery.md).  
  
 Também nesta nova [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], *ParameterSizePtr* agora retorna um valor que se alinha com a definição para o tamanho, em caracteres, da coluna ou expressão do marcador de parâmetro correspondente, conforme definido no [ODBC especificação](https://go.microsoft.com/fwlink/?LinkId=207044). Nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, *ParameterSizePtr* pode ser o valor correspondente do `SQL_DESC_OCTET_LENGTH` para o tipo ou um valor de tamanho de coluna irrelevante fornecido para SQLBindParameter para um tipo, o valor de qual deve ser ignorada (`SQL_INTEGER`, por exemplo).  
  
 O driver não oferece suporte SQLDescribeParam chamada nas seguintes situações:  
  
-   Depois de SQLExecDirect para qualquer [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções UPDATE ou DELETE que contém a cláusula FROM.  
  
-   Para qualquer instrução ODBC ou [!INCLUDE[tsql](../../includes/tsql-md.md)] que contenha um parâmetro em uma cláusula HAVING, ou comparada ao resultado de uma função SUM.  
  
-   Para qualquer instrução ODBC ou [!INCLUDE[tsql](../../includes/tsql-md.md)] que dependa de uma subconsulta que contém parâmetros.  
  
-   Para instruções SQL ODBC que contenham marcadores de parâmetro em ambas as expressões de uma comparação, like, ou predicado quantificado.  
  
-   Para qualquer consulta em que um dos parâmetros é um parâmetro para uma função.  
  
-   Quando há comentários (/ * \*/) na [!INCLUDE[tsql](../../includes/tsql-md.md)] comando.  
  
 Ao processar um lote de [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções, o driver também não suporta chamar SQLDescribeParam para marcadores de parâmetro nas instruções após a primeira instrução no lote.  
  
 Ao descrever os parâmetros de procedimentos armazenados preparados, SQLDescribeParam usa o procedimento armazenado do sistema [sp_sproc_columns](/sql/relational-databases/system-stored-procedures/sp-sproc-columns-transact-sql) para recuperar características de parâmetro. sp_sproc_columns pode informar dados para procedimentos armazenados no banco de dados do usuário atual. Preparando-se um nome totalmente qualificado de procedimento armazenado permite SQLDescribeParam executar em bancos de dados. Por exemplo, o sistema de procedimento armazenado [sp_who](/sql/relational-databases/system-stored-procedures/sp-who-transact-sql) pode ser preparada e executada em qualquer banco de dados como:  
  
```  
SQLPrepare(hstmt, "{call sp_who(?)}", SQL_NTS);  
```  
  
 SQLDescribeParam em execução após a preparação bem-sucedida retorna uma linha vazia definida quando conectado a qualquer banco de dados, mas `master`. A mesma chamada, preparada como a seguir, faz com que SQLDescribeParam seja bem-sucedido independentemente do banco de dados do usuário atual:  
  
```  
SQLPrepare(hstmt, "{call master..sp_who(?)}", SQL_NTS);  
```  
  
 Para tipos de dados de valor grande, o valor retornado em *DataTypePtr* é SQL_VARCHAR, SQL_VARBINARY ou SQL_NVARCHAR. Para indicar que o tamanho do parâmetro de tipo de dados de valor grande é "ilimitado", o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjuntos de drivers de ODBC do Native Client *ParameterSizePtr* como 0. Os valores de tamanho reais são retornados para os parâmetros padrão `varchar`.  
  
> [!NOTE]  
>  Se o parâmetro já tiver sido associado a um tamanho máximo para os parâmetros SQL_VARCHAR, SQL_VARBINARY ou SQL_WVARCHAR, o tamanho associado do parâmetro será retornado, não "ilimitado".  
  
 Para associar um parâmetro de entrada de tamanho "ilimitado", dados em execução devem ser usados. Não é possível associar um parâmetro de saída de tamanho "ilimitado" (não há nenhum método para streaming de dados de um parâmetro de saída, como [SQLGetData](sqlgetdata.md) faz para conjuntos de resultados).  
  
 No caso de parâmetros de saída, um buffer deve ser associado e se o valor for muito extenso, o buffer será preenchido e uma mensagem SQL_SUCCESS_WITH_INFO será retornada junto com o aviso "dados de cadeia de caracteres; truncamento à direita". Os dados que foram truncados são descartados em seguida.  
  
## <a name="sqldescribeparam-and-table-valued-parameters"></a>SQLDescribeParam e parâmetros com valor de tabela  
 Um aplicativo pode recuperar informações de parâmetro com valor de tabela para uma instrução preparada com SQLDescribeParam. Para obter mais informações, consulte [metadados de parâmetro com valor de tabela para instruções preparadas](../native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md).  
  
 Para obter mais informações sobre parâmetros com valor de tabela em geral, consulte [parâmetros com valor de tabela &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
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
  
 Para obter mais informações, consulte [aprimoramentos de data e hora &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqldescribeparam-support-for-large-clr-udts"></a>Suporte SQLDescribeParam para UDTs CLR grandes  
 `SQLDescribeParam` dá suporte a UDTs grandes do CLR. Para obter mais informações, consulte [Large CLR User-Defined tipos &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLDescribeParam](https://go.microsoft.com/fwlink/?LinkId=59339)   
 [Detalhes da implementação da API do ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
