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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bf536e06556e6b2e7b27f220d09a51f91b44d23c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304004"
---
# <a name="reserved-keyword-limitations"></a>Limitações de palavra-chave reservadas

Evite usar qualquer palavra-chave reservada ODBC como identificadores em suas tabelas SQL ou objetos relacionados. Se ocorrer um erro estranho em que você deve usar uma palavra-chave reservada como um identificador, você deve colocar o identificador com um par de *tiques* ('). Outro nome para a *escala* de *fundo é aspas*.

A limitação de palavra-chave reservada também se aplica a qualquer forma abreviada das palavras-chave reservadas.

Uma lista das palavras-chave reservadas do ODBC está disponível em:

- [Palavras-chave reservadas ODBC](https://docs.microsoft.com/sql/odbc/reference/appendixes/reserved-keywords).

- No *Guia de referência do programador de ODBC*, consulte o [Apêndice C: gramática SQL](https://docs.microsoft.com/sql/odbc/reference/appendixes/appendix-c-sql-grammar).

