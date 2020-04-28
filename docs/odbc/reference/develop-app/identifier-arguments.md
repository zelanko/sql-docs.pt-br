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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6831eab30daebe37baecebe3ed7053537d7de8f8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300156"
---
# <a name="identifier-arguments"></a>Argumentos do identificador
Se uma cadeia de caracteres em um argumento de identificador estiver entre aspas, o driver removerá espaços em branco à esquerda e à direita e tratará literalmente a cadeia de caracteres entre aspas. Se a cadeia de caracteres não estiver entre aspas, o driver removerá os espaços em branco à direita e dobrará a cadeia de caracteres para letras maiúsculas. Definir um argumento de identificador para um ponteiro nulo retorna SQL_ERROR e SQLSTATE HY009 (uso inválido de ponteiro NULL), a menos que o argumento seja um nome de catálogo e os catálogos não tenham suporte.  
  
 Esses argumentos serão tratados como argumentos de identificador se o atributo de instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE. Nesse caso, o sublinhado (_) e o sinal de porcentagem (%) será tratado como o caractere real, não como um caractere de padrão de pesquisa. Esses argumentos são tratados como um argumento comum ou um argumento de padrão, dependendo do argumento, se esse atributo for definido como SQL_FALSE.  
  
 Embora os identificadores que contenham caracteres especiais devam ser colocados em instruções SQL, eles não devem ser colocados entre aspas quando passados como argumentos de função de catálogo, porque os caracteres de aspas passados para as funções de catálogo são interpretados literalmente. Por exemplo, suponha que o caractere de aspas de identificador (que é específico de driver e retornado por meio de **SQLGetInfo**) seja uma aspa dupla ("). A primeira chamada para **SQLTables** retorna um conjunto de resultados que contém informações sobre a tabela contas a pagar, enquanto a segunda chamada retorna informações sobre a tabela "contas a pagar", que provavelmente não é o que foi pretendido.  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, "Accounts Payable", SQL_NTS, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "\"Accounts Payable\"", SQL_NTS, NULL, 0);  
```  
  
 Identificadores entre aspas são usados para distinguir um verdadeiro nome de coluna de uma pseudo coluna de mesmo nome, como ROWID no Oracle. Se "ROWID" for passado em um argumento de uma função de catálogo, a função funcionará com a pseudo coluna de ROWID, se existir. Se a pseudo coluna não existir, a função funcionará com a coluna "ROWID". Se ROWID for passado em um argumento de uma função de catálogo, a função funcionará com a coluna ROWID.  
  
 Para obter mais informações sobre identificadores entre aspas, consulte [identificadores entre aspas](../../../odbc/reference/develop-app/quoted-identifiers.md).
