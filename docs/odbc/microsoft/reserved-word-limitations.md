---
title: Limitações de Palavras Reservadas | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ed42f083-c9e8-4ee4-9d64-d879bf955c78
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bf536e06556e6b2e7b27f220d09a51f91b44d23c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304004"
---
# <a name="reserved-keyword-limitations"></a>Limitações de palavras-chave reservadas

Evite usar quaisquer palavras-chave reservadas pela ODBC como identificadores em suas tabelas SQL ou objetos relacionados. Se surgir um caso estranho em que você deve usar uma palavra-chave reservada como identificador, você deve cercar o identificador com um par de *backticks* ('). Outro nome para *backtick* é *backquote*.

A limitação de palavra-chave reservada também se aplica a qualquer forma abreviada das palavras-chave reservadas.

Uma lista das palavras-chave reservadas da ODBC está disponível em:

- [Palavras-chave reservadas da ODBC](https://docs.microsoft.com/sql/odbc/reference/appendixes/reserved-keywords).

- No *Guia de Referência do Programador ODBC,* consulte o [apêndice C: Gramática SQL](https://docs.microsoft.com/sql/odbc/reference/appendixes/appendix-c-sql-grammar).

