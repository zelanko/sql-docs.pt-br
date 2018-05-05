---
title: Aplicativos verticais | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], vertical applications
- vertical applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: d50ea3e6-7a9e-4fb6-8cd8-1d429d2f7b3c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c89d0080f4cc29296d9e6dcd43911ee920af6683
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="vertical-applications"></a>Aplicativos verticais
Aplicativos verticais geralmente executam uma tarefa bem definida em relação a um único DBMS. Por exemplo, um aplicativo de entrada de ordem rastreia as ordens em uma empresa. O que esses tipos de aplicativos têm em comum é que o esquema de banco de dados é geralmente criado pelo desenvolvedor do aplicativo e, enquanto o aplicativo pode funcionar com um número de diferentes DBMSs, ele funciona com um único DBMS de um único cliente.  
  
 Como aplicativos verticais geralmente requerem certas funcionalidades, como cursores roláveis ou transações, eles raramente oferecem suporte a todos os DBMSs. Em vez disso, eles tendem a ser altamente interoperável entre um conjunto limitado de DBMSs. Normalmente, os desenvolvedores de aplicativos verticais escolher para dar suporte a esses DBMSs que representam uma grande parte do mercado e ignore o restante. Eles ainda podem escolher dar suporte a drivers específicos para esses DBMSs para reduzir seus testes e os custos de suporte do produto.  
  
 Como aplicativos verticais podem dar suporte a um conjunto conhecido de DBMSs, às vezes contiverem código específico do driver ou DBMS específico. No entanto, esse código melhor é reduzido ao mínimo porque ele requer mais tempo para manter.
