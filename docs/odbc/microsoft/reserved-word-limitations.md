---
title: Limitações de palavras reservadas | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c884d8594c3c4511bed0e24f9b3dd43092176b4e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67988020"
---
# <a name="reserved-keyword-limitations"></a>Limitações de palavra-chave reservadas

Evite usar qualquer palavra-chave reservada ODBC como identificadores em suas tabelas SQL ou objetos relacionados. Se ocorrer um erro estranho em que você deve usar uma palavra-chave reservada como um identificador, você deve colocar o identificador com um par de *tiques* ('). Outro nome para a *escala* de *fundo é aspas*.

A limitação de palavra-chave reservada também se aplica a qualquer forma abreviada das palavras-chave reservadas.

Uma lista das palavras-chave reservadas do ODBC está disponível em:

- [Palavras-chave reservadas ODBC](https://docs.microsoft.com/sql/odbc/reference/appendixes/reserved-keywords).

- No *Guia de referência do programador de ODBC*, consulte o [Apêndice C: gramática SQL](https://docs.microsoft.com/sql/odbc/reference/appendixes/appendix-c-sql-grammar).

