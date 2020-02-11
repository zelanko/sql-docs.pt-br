---
title: Tamanho do conjunto de linhas do cursor | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], rowset size
- ODBC cursors, rowset size
- rowsets [ODBC]
ms.assetid: 2febe2ae-fdc1-490e-a79f-c516bc8e7c3f
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5188b87e91725e2d0e86337261fc1f915189ff19
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73784246"
---
# <a name="cursor-rowset-size"></a>Tamanho do conjunto de linhas de cursor
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Os cursores ODBC não se limitam a buscar uma linha de cada vez. Eles podem recuperar várias linhas em cada chamada para **SQLFetch** ou [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md). Quando você está trabalhando com um banco de dados cliente/servidor, como o Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], é mais eficaz buscar várias linhas de uma vez. O número de linhas retornadas em uma busca é chamado de tamanho do conjunto de linhas e é especificado usando o SQL_ATTR_ROW_ARRAY_SIZE de [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
```  
SQLUINTEGER uwRowsize;  
SQLSetStmtAttr(m_hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)uwRowsetSize, SQL_IS_UINTEGER);  
```  
  
 Os cursores com um tamanho de conjunto de linhas maior que 1 são chamados de cursores em bloco.  
  
 Há duas opções para associar colunas do conjunto de resultados para cursores em bloco:  
  
-   Associação de coluna  
  
     Cada coluna é associada a uma matriz de variáveis. Cada matriz possui o mesmo número de elementos que o tamanho do conjunto de linhas.  
  
-   Associação de linha  
  
     Uma matriz baseada em estruturas que armazenam os dados e indicadores de todas as colunas em uma linha. A matriz tem o mesmo número de estruturas que o tamanho do conjunto de linhas.  
  
 Quando uma associação de coluna ou de linha é usada, cada chamada para **SQLFetch** ou **SQLFetchScroll** preenche as matrizes associadas com os dados do conjunto de linhas recuperado.  
  
 [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) também pode ser usado para recuperar dados de coluna de um cursor de bloco. Como **SQLGetData** trabalha uma linha de cada vez, **SQLSetPos** deve ser chamado para definir uma linha específica no conjunto de linhas como a linha atual antes de chamar **SQLGetData**.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client oferece uma otimização usando conjuntos de linhas para recuperar um conjunto de resultados inteiro rapidamente. Para usar essa otimização, defina os atributos de cursor para seus padrões (somente encaminhamento, somente leitura, tamanho do conjunto de linhas = 1) no momento em que **SQLExecDirect** ou **SQLExecute** é chamado. O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client configura um conjunto de resultados padrão. Esse procedimento é mais eficaz do que o uso de cursores de servidor ao transferir resultados para o cliente sem fazer rolagem. Depois que a instrução tiver sido executada, aumente o tamanho do conjunto de linhas e use a associação de coluna ou de linha. Isso permite [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usar um conjunto de resultados padrão para enviar linhas de resultado com eficiência para o cliente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , enquanto o driver ODBC do Native Client efetua pull continuamente de linhas dos buffers de rede no cliente.  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades do cursor](../../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
  
