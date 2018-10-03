---
title: Buscar e atualizar conjuntos de linhas (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rowsets [ODBC]
ms.assetid: cf0eb3b4-8b72-49fc-a845-95edc360cf93
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f0669adbf316b27dcec6c57d33aff4fa25168459
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47625394"
---
# <a name="fetch-and-update-rowsets-odbc"></a>Buscar e atualizar conjuntos de linhas (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

    
### <a name="to-fetch-and-update-rowsets"></a>Para buscar e atualizar conjuntos de linhas  
  
1.  Opcionalmente, chame [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) com SQL_ROW_ARRAY_SIZE para alterar o número de linhas (R) no conjunto de linhas.  
  
2.  Chame [SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401) ou [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) para obter um conjunto de linhas.  
  
3.  Se forem usadas colunas associadas, use os valores e comprimentos de dados disponíveis agora nos buffers de coluna associada para o conjunto de linhas.  
  
     Se forem usadas colunas desassociadas, para cada linha chame [SQLSetPos](http://go.microsoft.com/fwlink/?LinkId=58407) com SQL_POSITION para definir a posição do cursor; depois, para cada coluna desassociada:  
  
    -   Chame [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) uma ou mais vezes para obter os dados dessas colunas depois da última coluna do conjunto de linhas associada. Chamadas para [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) devem estar em ordem crescente de número da coluna.  
  
    -   Chame [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) várias vezes para obter dados de uma coluna de textos ou imagens.  
  
4.  Configure quaisquer colunas de imagem ou texto de dados em execução.  
  
5.  Chame [SQLSetPos](http://go.microsoft.com/fwlink/?LinkId=58407) ou [SQLBulkOperations](http://go.microsoft.com/fwlink/?LinkId=58398) para definir a posição do cursor, atualizar, atualizar, excluir ou Adicionar linha (s) dentro do conjunto de linhas.  
  
     Se as colunas de imagem ou texto de dados em execução forem usadas para uma operação de atualização ou adição, lide com elas.  
  
6.  Opcionalmente, execute uma instrução UPDATE ou DELETE posicionada, especificando o nome de cursor (disponível no [SQLGetCursorName](../../../relational-databases/native-client-odbc-api/sqlgetcursorname.md)) e usando um identificador de instrução diferentes sobre a mesma conexão.  
  
## <a name="see-also"></a>Consulte também  
 [Usando cursores tópicos de instruções &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/cursors/using-cursors-how-to-topics-odbc.md)  
  
  
