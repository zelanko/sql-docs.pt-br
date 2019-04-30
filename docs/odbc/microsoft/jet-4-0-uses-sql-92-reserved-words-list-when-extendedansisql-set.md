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
manager: craigg
ms.openlocfilehash: c74a80bb38c406acb50e5e275f658a5f1d2b30d3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63208379"
---
# <a name="jet-40-uses-sql-92-reserved-words-list-when-extendedansisqlset"></a>O Jet 4.0 usa lista de palavras reservadas do SQL-92 com o ExtendedAnsiSQL_Set
Quando o sinalizador ExtendedAnsiSQL é ativado, o Jet 4.0 usa a lista de palavras reservadas de SQL-92. Tentando usar um SQL-92 reservado word como um nome de objeto sem aspas resultará em um erro de sintaxe. Quando o sinalizador ExtendedAnsiSQL for desativado, as novas palavras reservadas podem ser usadas como nomes de objeto como antes.
