---
title: Buscar e atualizar conjuntos de linhas (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rowsets [ODBC]
ms.assetid: cf0eb3b4-8b72-49fc-a845-95edc360cf93
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a799e2c4c7c3e7e3119fece847cb726751441c39
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82701886"
---
# <a name="fetch-and-update-rowsets-odbc"></a>Buscar e atualizar conjuntos de linhas (ODBC)
    
### <a name="to-fetch-and-update-rowsets"></a>Para buscar e atualizar conjuntos de linhas  
  
1.  Opcionalmente, chame [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) com SQL_ROW_ARRAY_SIZE para alterar o número de linhas (R) no conjunto de linhas.  
  
2.  Chame [SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401) ou [SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md) para obter um conjunto de linhas.  
  
3.  Se forem usadas colunas associadas, use os valores e comprimentos de dados disponíveis agora nos buffers de coluna associada para o conjunto de linhas.  
  
     Se forem usadas colunas desassociadas, para cada chamada de linha [SQLSetPos](https://go.microsoft.com/fwlink/?LinkId=58407) com SQL_POSITION para definir a posição do cursor; em seguida, para cada coluna desassociada:  
  
    -   Chame [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) uma ou mais vezes para obter os dados de colunas desassociadas após a última coluna associada do conjunto de linhas. As chamadas para [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) devem estar na ordem de aumento do número da coluna.  
  
    -   Chame [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) várias vezes para obter dados de uma coluna de textos ou imagens.  
  
4.  Configure quaisquer colunas de imagem ou texto de dados em execução.  
  
5.  Chame [SQLSetPos](https://go.microsoft.com/fwlink/?LinkId=58407) ou [SQLBulkOperations](https://go.microsoft.com/fwlink/?LinkId=58398) para definir a posição do cursor, atualizar, atualizar, excluir ou Adicionar linha (s) no conjunto de linhas.  
  
     Se as colunas de imagem ou texto de dados em execução forem usadas para uma operação de atualização ou adição, lide com elas.  
  
6.  Opcionalmente, execute uma instrução UPDATE ou DELETE posicionada, especificando o nome do cursor (disponível em [SQLGetCursorName](../../native-client-odbc-api/sqlgetcursorname.md)) e usando um identificador de instrução diferente na mesma conexão.  
  
## <a name="see-also"></a>Consulte Também  
 [Tópicos de instruções sobre o uso de cursores &#40;ODBC&#41;](using-cursors-how-to-topics-odbc.md)  
  
  
