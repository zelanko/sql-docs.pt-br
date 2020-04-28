---
title: Identificadores entre aspas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], quoted identifiers
- quoted identifiers [ODBC]
ms.assetid: 729ba55f-743b-4a04-8c39-ac0a9914211d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0c03fa8bbc059566288997b29c899056f26de252
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81281999"
---
# <a name="quoted-identifiers"></a>Identificadores entre aspas
Em uma instrução SQL, identificadores contendo caracteres especiais ou palavras-chave de correspondência devem ser colocados entre *caracteres de aspas de identificador*; os identificadores incluídos nesses caracteres são conhecidos como *identificadores entre aspas* (também conhecidos como *identificadores delimitados* no SQL-92). Por exemplo, o identificador de contas a pagar é citado na seguinte instrução **Select** :  
  
```  
SELECT * FROM "Accounts Payable"  
```  
  
 O motivo para a cotação de identificadores é tornar a instrução analisável. Por exemplo, se as contas a pagar não tiverem sido enlimitadas na instrução anterior, o analisador assumiria que havia duas tabelas, contas e contas a pagar e retornará um erro de sintaxe de que elas não foram separadas por uma vírgula. O caractere de aspas de identificador é específico do driver e é recuperado com a opção SQL_IDENTIFIER_QUOTE_CHAR em **SQLGetInfo**. As listas de caracteres especiais e de palavras-chave são recuperadas com as opções SQL_SPECIAL_CHARACTERS e SQL_KEYWORDS em **SQLGetInfo**.  
  
 Para serem seguros, os aplicativos interoperáveis geralmente citam todos os identificadores, exceto aqueles em pseudovariáveis, como a coluna de ROWID no Oracle. **SQLSpecialColumns** retorna uma lista de pseudo colunas. Além disso, se houver restrições específicas do aplicativo em que os caracteres especiais possam aparecer em um nome de objeto, é melhor que os aplicativos interoperáveis não usem caracteres especiais nessas posições.
