---
title: Jet 4.0 usa lista de palavras reservadas SQL-92 quando ExtendedAnsiSQL_Set | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- extendedANSISQL [ODBC], reserved words
ms.assetid: 7645187e-7777-4c07-9686-0a80d5c5834d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6988e0da1ecb881e0f6e88e35b66f1a6284f9b7a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299956"
---
# <a name="jet-40-uses-sql-92-reserved-words-list-when-extendedansisql_set"></a>O Jet 4.0 usa lista de palavras reservadas do SQL-92 com o ExtendedAnsiSQL_Set
Quando a bandeira ExtendedAnsiSQL é ligada, o Jet 4.0 usa a lista de palavras reservadas SQL-92. Tentar usar uma palavra reservada SQL-92 como um nome de objeto não citado resultará em um erro de sintaxe. Quando o sinalizador ExtendedAnsiSQL é desligado, as novas palavras reservadas podem ser usadas como nomes de objetos como antes.
