---
title: Listam de palavras reservadas do Jet 4.0 usa SQL-92 quando ExtendedAnsiSQL_Set | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 93d23216db950ed861449061f3e35e5e88a637fb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68058792"
---
# <a name="jet-40-uses-sql-92-reserved-words-list-when-extendedansisqlset"></a>O Jet 4.0 usa lista de palavras reservadas do SQL-92 com o ExtendedAnsiSQL_Set
Quando o sinalizador ExtendedAnsiSQL é ativado, o Jet 4.0 usa a lista de palavras reservadas de SQL-92. Tentando usar um SQL-92 reservado word como um nome de objeto sem aspas resultará em um erro de sintaxe. Quando o sinalizador ExtendedAnsiSQL for desativado, as novas palavras reservadas podem ser usadas como nomes de objeto como antes.
