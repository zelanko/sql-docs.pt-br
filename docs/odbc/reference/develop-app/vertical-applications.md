---
title: Aplicativos verticais | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], vertical applications
- vertical applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: d50ea3e6-7a9e-4fb6-8cd8-1d429d2f7b3c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cc88f38fd1ffe8b2ee0033ad0a2abc4f15fd5cf3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300371"
---
# <a name="vertical-applications"></a>Aplicativos verticais
Normalmente, os aplicativos verticais executam uma tarefa bem definida em relação a um único DBMS. Por exemplo, um aplicativo de entrada de pedido rastreia os pedidos em uma empresa. O que esses tipos de aplicativos têm em comum é que o esquema de banco de dados geralmente é projetado pelo desenvolvedor do aplicativo e, enquanto o aplicativo pode funcionar com vários DBMSs diferentes, ele funciona com um único DBMS para um único cliente.  
  
 Como os aplicativos verticais geralmente exigem determinada funcionalidade, como cursores roláveis ou transações, raramente dão suporte a todos os DBMSs. Em vez disso, eles tendem a ser altamente interoperáveis entre um conjunto limitado de DBMSs. Normalmente, os desenvolvedores de aplicativos verticais optam por oferecer suporte a esses DBMSs que representam uma grande fração do mercado e ignoram o restante. Eles podem até mesmo optar por dar suporte a drivers específicos para que esses DBMSs reduzam seus custos de teste e suporte a produtos.  
  
 Como os aplicativos verticais podem dar suporte a um conjunto conhecido de DBMSs, às vezes eles contêm código específico de driver ou DBMS específico. No entanto, esse código é melhor mantido para um mínimo porque requer tempo extra para manter.
