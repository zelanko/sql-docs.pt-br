---
title: Buscar e atualizar conjuntos de linhas (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- rowsets [ODBC]
ms.assetid: cf0eb3b4-8b72-49fc-a845-95edc360cf93
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 740b549021c4ef5fc9253b8e774b3d5e38323b2d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121263"
---
# <a name="fetch-and-update-rowsets-odbc"></a>Buscar e atualizar conjuntos de linhas (ODBC)
    
### <a name="to-fetch-and-update-rowsets"></a>Para buscar e atualizar conjuntos de linhas  
  
1.  Opcionalmente, chame [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) com SQL_ROW_ARRAY_SIZE para alterar o número de linhas (R) no conjunto de linhas.  
  
2.  Chamar [SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401) ou [SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md) para obter um conjunto de linhas.  
  
3.  Se forem usadas colunas associadas, use os valores e comprimentos de dados disponíveis agora nos buffers de coluna associada para o conjunto de linhas.  
  
     Se forem usadas colunas desassociadas, para cada linha chame [SQLSetPos](http://go.microsoft.com/fwlink/?LinkId=58407) com SQL_POSITION para definir a posição do cursor; depois, para cada coluna desassociada:  
  
    -   Chamar [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) uma ou mais vezes para obter os dados para colunas desassociadas depois da última coluna do conjunto de linhas associada. Chamadas para [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) devem estar em ordem crescente de número da coluna.  
  
    -   Chame [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) várias vezes para obter dados de uma coluna de textos ou imagens.  
  
4.  Configure quaisquer colunas de imagem ou texto de dados em execução.  
  
5.  Chamar [SQLSetPos](http://go.microsoft.com/fwlink/?LinkId=58407) ou [SQLBulkOperations](http://go.microsoft.com/fwlink/?LinkId=58398) para definir a posição do cursor, atualizar, atualizar, excluir ou adicionar linhas no conjunto de linhas.  
  
     Se as colunas de imagem ou texto de dados em execução forem usadas para uma operação de atualização ou adição, lide com elas.  
  
6.  Opcionalmente, execute uma instrução UPDATE ou DELETE posicionada, especificando o nome de cursor (disponível em [SQLGetCursorName](../../native-client-odbc-api/sqlgetcursorname.md)) e usando um identificador de instrução diferente sobre a mesma conexão.  
  
## <a name="see-also"></a>Consulte também  
 [Usando os tópicos de instruções de cursores &#40;ODBC&#41;](using-cursors-how-to-topics-odbc.md)  
  
  