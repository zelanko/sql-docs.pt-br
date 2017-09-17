---
title: Aplicativos verticais | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], vertical applications
- vertical applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: d50ea3e6-7a9e-4fb6-8cd8-1d429d2f7b3c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a3f4f8eca8309cb40b6ef9d2a7f9baac77c05f84
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="vertical-applications"></a>Aplicativos verticais
Aplicativos verticais geralmente executam uma tarefa bem definida em relação a um único DBMS. Por exemplo, um aplicativo de entrada de ordem rastreia as ordens em uma empresa. O que esses tipos de aplicativos têm em comum é que o esquema de banco de dados é geralmente criado pelo desenvolvedor do aplicativo e, enquanto o aplicativo pode funcionar com um número de diferentes DBMSs, ele funciona com um único DBMS de um único cliente.  
  
 Como aplicativos verticais geralmente requerem certas funcionalidades, como cursores roláveis ou transações, eles raramente oferecem suporte a todos os DBMSs. Em vez disso, eles tendem a ser altamente interoperável entre um conjunto limitado de DBMSs. Normalmente, os desenvolvedores de aplicativos verticais escolher para dar suporte a esses DBMSs que representam uma grande parte do mercado e ignore o restante. Eles ainda podem escolher dar suporte a drivers específicos para esses DBMSs para reduzir seus testes e os custos de suporte do produto.  
  
 Como aplicativos verticais podem dar suporte a um conjunto conhecido de DBMSs, às vezes contiverem código específico do driver ou DBMS específico. No entanto, esse código melhor é reduzido ao mínimo porque ele requer mais tempo para manter.
