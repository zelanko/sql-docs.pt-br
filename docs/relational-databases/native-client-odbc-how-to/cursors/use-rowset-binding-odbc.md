---
title: Usar o conjunto de linhas de associação (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rowset binding [ODBC]
ms.assetid: a7be05f0-6b11-4b53-9fbc-501e591eef09
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8dad8d3992bfef695b54f82e5d8d9548b6280b32
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/05/2019
ms.locfileid: "67584516"
---
# <a name="use-rowset-binding-odbc"></a>Usar associação de conjunto de linhas (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

    
### <a name="to-use-column-wise-binding"></a>Para usar uma associação por coluna  
  
1.  Para cada coluna associada, siga este procedimento:  
  
    -   Aloque uma matriz de R (ou mais) buffers de coluna para armazenar valores de dados, onde R é o número de linhas no conjunto de linhas.  
  
    -   Outra opção é alocar uma matriz de R (ou mais) buffers de coluna para armazenar comprimentos de dados.  
  
    -   Chame [SQLBindCol](../../../relational-databases/native-client-odbc-api/sqlbindcol.md) para associar o valor de dados e a matrizes de comprimento de dados da coluna para a coluna do conjunto de linhas.  
  
2.  Chame [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) para definir os seguintes atributos:  
  
    -   Defina SQL_ATTR_ROW_ARRAY_SIZE como o número de linhas no conjunto de linhas (R).  
  
    -   Defina SQL_ATTR_ROW_BIND_TYPE como SQL_BIND_BY_COLUMN.  
  
    -   Defina o atributo SQL_ATTR_ROWS FETCHED_PTR de modo que aponte para uma variável SQLUINTEGER que contém o número de linhas buscadas.  
  
    -   Defina SQL_ATTR_ROW_STATUS_PTR de modo que aponte para uma matriz[R] de variáveis SQLUSSMALLINT que contém indicadores de status de linha.  
  
3.  Executar a instrução.  
  
4.  Cada chamada para [SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401) ou [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) recupera linhas R e transfere os dados para as colunas associadas.  

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

### <a name="to-use-row-wise-binding"></a>Para usar uma associação por linha  
  
1.  Aloque uma matriz[R] de estruturas, onde R é o número de linhas no conjunto de linhas. A estrutura tem um elemento para cada coluna e cada elemento tem duas partes:  
  
    -   A primeira parte é uma variável do tipo de dados apropriado que contém os dados de coluna.  
  
    -   A segunda parte é uma variável SQLINTEGER que contém o indicador de coluna.  
  
2.  Chame [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) para definir os seguintes atributos:  
  
    -   Defina SQL_ATTR_ROW_ARRAY_SIZE como o número de linhas no conjunto de linhas (R).  
  
    -   Defina SQL_ATTR_ROW_BIND_TYPE como o tamanho da estrutura alocada na Etapa 1.  
  
    -   Defina o atributo SQL_ATTR_ROWS_FETCHED_PTR de modo que aponte para uma variável SQLUINTEGER que contém o número de linhas buscadas.  
  
    -   Defina SQL_ATTR_PARAMS_STATUS_PTR de modo que aponte para uma matriz[R] de variáveis SQLUSSMALLINT que contém indicadores de status de linha.  
  
3.  Para cada coluna no conjunto de resultados, chame [SQLBindCol](../../../relational-databases/native-client-odbc-api/sqlbindcol.md) para apontar o ponteiro de comprimento de dados da coluna e valor de dados para suas variáveis no primeiro elemento da matriz de estruturas alocadas na etapa 1.  
  
4.  Executar a instrução.  
  
5.  Cada chamada para [SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401) ou [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) recupera linhas R e transfere os dados para as colunas associadas.  
  
## <a name="see-also"></a>Consulte também  
 [Usando cursores tópicos de instruções &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/cursors/using-cursors-how-to-topics-odbc.md)   
 [Como os cursores são implementados](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)   
 [Usar cursores &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/cursors/use-cursors-odbc.md)  
  
  
