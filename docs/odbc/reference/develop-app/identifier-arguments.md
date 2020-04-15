---
title: Argumentos identificadores | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300156"
---
# <a name="identifier-arguments"></a>Argumentos do identificador
Se uma seqüência em um argumento identificador for citada, o driver removerá os espaços em branco de liderança e de arrasto e trata literalmente a string dentro das aspas. Se a string não for citada, o driver removerá os espaços em branco e dobrará a corda para maiúsculas. Definir um argumento identificador para um ponteiro nulo retorna SQL_ERROR e SQLSTATE HY009 (uso inválido do ponteiro nulo), a menos que o argumento seja um nome de catálogo e catálogos não sejam suportados.  
  
 Esses argumentos são tratados como argumentos identificadores se o atributo de declaração SQL_ATTR_METADATA_ID for definido como SQL_TRUE. Neste caso, o sublinhado (_) e o sinal percentual (%) será tratado como o personagem real, não como um personagem padrão de pesquisa. Esses argumentos são tratados como um argumento comum ou um argumento padrão, dependendo do argumento, se esse atributo for definido para SQL_FALSE.  
  
 Embora os identificadores contendo caracteres especiais devem ser citados em instruções SQL, eles não devem ser citados quando passados como argumentos de função de catálogo, porque caracteres de citação passados para funções de catálogo são interpretados literalmente. Por exemplo, suponha que o caractere de citação do identificador (que é específico do driver e devolvido através **do SQLGetInfo)** seja uma marca de cotação dupla ("). A primeira chamada para **sqltables** retorna um conjunto de resultados contendo informações sobre a tabela Contas a pagar, enquanto a segunda chamada retorna informações sobre a tabela "Contas a pagar", que provavelmente não é o que se pretendia.  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, "Accounts Payable", SQL_NTS, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "\"Accounts Payable\"", SQL_NTS, NULL, 0);  
```  
  
 Identificadores citados são usados para distinguir um nome de coluna verdadeiro de uma pseudo-coluna de mesmo nome, como ROWID no Oracle. Se "ROWID" for aprovado em um argumento de uma função de catálogo, a função funcionará com a pseudo-coluna ROWID se ela existir. Se a pseudo-coluna não existir, a função funcionará com a coluna "ROWID". Se ROWID for aprovado em um argumento de uma função de catálogo, a função funcionará com a coluna ROWID.  
  
 Para obter mais informações sobre identificadores citados, consulte [Identificadores citados](../../../odbc/reference/develop-app/quoted-identifiers.md).
