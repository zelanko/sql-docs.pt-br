---
title: Argumentos de identificador | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- identifier arguments [ODBC]
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], identifier
ms.assetid: b9de003f-cb49-4dec-b528-14a5b8ff12bd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 156dfaf5c6a6a4ec06a0c96b5f726383cba32ba6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47609924"
---
# <a name="identifier-arguments"></a>Argumentos do identificador
Se uma cadeia de caracteres em um argumento de identificador está entre aspas, o driver remove à direita e espaços em branco e literalmente trata a cadeia de caracteres entre aspas. Se a cadeia de caracteres não está entre aspas, o driver remove dobras e espaços em branco à direita a cadeia de caracteres em maiusculas. A configuração de um argumento de identificador como um ponteiro nulo retorna SQL_ERROR e SQLSTATE HY009 (uso inválido de ponteiro nulo), a menos que o argumento é um nome de catálogo e não há suporte para catálogos.  
  
 Esses argumentos são tratados como argumentos de identificador se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE. Nesse caso, o sublinhado (_) e o sinal de porcentagem (%) será tratado como o caractere real, não como um caractere de padrão de pesquisa. Esses argumentos são tratados como um argumento comum ou um argumento padrão, dependendo do argumento, se esse atributo for definido como SQL_FALSE.  
  
 Embora os identificadores que contêm caracteres especiais devem estar entre aspas em instruções SQL, eles devem não ser colocado entre aspas quando passados como argumentos de função de catálogo, porque os caracteres de aspas passados para funções de catálogo são interpretados literalmente. Por exemplo, suponha que o identificador de caractere de aspas (que é específico do driver e retornado por meio **SQLGetInfo**) é uma marca de aspas duplas ("). A primeira chamada para **SQLTables** retorna um conjunto de resultados contendo informações sobre a tabela de contas a pagar, enquanto a segunda chamada retorna informações sobre a tabela "Contas a pagar", que é provavelmente não é o pretendido.  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, "Accounts Payable", SQL_NTS, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "\"Accounts Payable\"", SQL_NTS, NULL, 0);  
```  
  
 Identificadores entre aspas são usados para distinguir um nome de coluna true de uma coluna de pseudo o mesmo nome, como o ROWID no Oracle. Se "ROWID" é passado um argumento de uma função de catálogo, a função funcionará com a coluna de pseudo ROWID se ele existir. Se a coluna pseudo não existir, a função funcionará com a coluna "ROWID". Se ROWID é passado um argumento de uma função de catálogo, a função funcionará com a coluna ROWID.  
  
 Para obter mais informações sobre identificadores entre aspas, consulte [identificadores entre aspas](../../../odbc/reference/develop-app/quoted-identifiers.md).
