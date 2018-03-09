---
title: Aplicativos verticais | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], vertical applications
- vertical applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: d50ea3e6-7a9e-4fb6-8cd8-1d429d2f7b3c
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 81f0b9b75a1431b071e20425ba7f0386fe7a1b00
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="vertical-applications"></a>Aplicativos verticais
Aplicativos verticais geralmente executam uma tarefa bem definida em relação a um único DBMS. Por exemplo, um aplicativo de entrada de ordem rastreia as ordens em uma empresa. O que esses tipos de aplicativos têm em comum é que o esquema de banco de dados é geralmente criado pelo desenvolvedor do aplicativo e, enquanto o aplicativo pode funcionar com um número de diferentes DBMSs, ele funciona com um único DBMS de um único cliente.  
  
 Como aplicativos verticais geralmente requerem certas funcionalidades, como cursores roláveis ou transações, eles raramente oferecem suporte a todos os DBMSs. Em vez disso, eles tendem a ser altamente interoperável entre um conjunto limitado de DBMSs. Normalmente, os desenvolvedores de aplicativos verticais escolher para dar suporte a esses DBMSs que representam uma grande parte do mercado e ignore o restante. Eles ainda podem escolher dar suporte a drivers específicos para esses DBMSs para reduzir seus testes e os custos de suporte do produto.  
  
 Como aplicativos verticais podem dar suporte a um conjunto conhecido de DBMSs, às vezes contiverem código específico do driver ou DBMS específico. No entanto, esse código melhor é reduzido ao mínimo porque ele requer mais tempo para manter.
