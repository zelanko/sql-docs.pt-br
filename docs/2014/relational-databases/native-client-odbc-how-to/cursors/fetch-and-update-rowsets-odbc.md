---
title: Buscar e atualizar conjuntos de linhas (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- rowsets [ODBC]
ms.assetid: cf0eb3b4-8b72-49fc-a845-95edc360cf93
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d41ba76ceaa157070fc2584c5ebd6d080f415420
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37419465"
---
# <a name="fetch-and-update-rowsets-odbc"></a>Buscar e atualizar conjuntos de linhas (ODBC)
    
### <a name="to-fetch-and-update-rowsets"></a>Para buscar e atualizar conjuntos de linhas  
  
1.  Opcionalmente, chame [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) com SQL_ROW_ARRAY_SIZE para alterar o número de linhas (R) no conjunto de linhas.  
  
2.  Chame [SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401) ou [SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md) para obter um conjunto de linhas.  
  
3.  Se forem usadas colunas associadas, use os valores e comprimentos de dados disponíveis agora nos buffers de coluna associada para o conjunto de linhas.  
  
     Se forem usadas colunas desassociadas, para cada linha chame [SQLSetPos](http://go.microsoft.com/fwlink/?LinkId=58407) com SQL_POSITION para definir a posição do cursor; depois, para cada coluna desassociada:  
  
    -   Chame [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) uma ou mais vezes para obter os dados dessas colunas depois da última coluna do conjunto de linhas associada. Chamadas para [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) devem estar em ordem crescente de número da coluna.  
  
    -   Chame [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) várias vezes para obter dados de uma coluna de textos ou imagens.  
  
4.  Configure quaisquer colunas de imagem ou texto de dados em execução.  
  
5.  Chame [SQLSetPos](http://go.microsoft.com/fwlink/?LinkId=58407) ou [SQLBulkOperations](http://go.microsoft.com/fwlink/?LinkId=58398) para definir a posição do cursor, atualizar, atualizar, excluir ou Adicionar linha (s) dentro do conjunto de linhas.  
  
     Se as colunas de imagem ou texto de dados em execução forem usadas para uma operação de atualização ou adição, lide com elas.  
  
6.  Opcionalmente, execute uma instrução UPDATE ou DELETE posicionada, especificando o nome de cursor (disponível no [SQLGetCursorName](../../native-client-odbc-api/sqlgetcursorname.md)) e usando um identificador de instrução diferentes sobre a mesma conexão.  
  
## <a name="see-also"></a>Consulte também  
 [Usando cursores tópicos de instruções &#40;ODBC&#41;](using-cursors-how-to-topics-odbc.md)  
  
  
