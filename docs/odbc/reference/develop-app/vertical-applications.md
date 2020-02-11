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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6d0ed7a5f488765b56b2af0688ca14361590ab44
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68022111"
---
# <a name="vertical-applications"></a>Aplicativos verticais
Normalmente, os aplicativos verticais executam uma tarefa bem definida em relação a um único DBMS. Por exemplo, um aplicativo de entrada de pedido rastreia os pedidos em uma empresa. O que esses tipos de aplicativos têm em comum é que o esquema de banco de dados geralmente é projetado pelo desenvolvedor do aplicativo e, enquanto o aplicativo pode funcionar com vários DBMSs diferentes, ele funciona com um único DBMS para um único cliente.  
  
 Como os aplicativos verticais geralmente exigem determinada funcionalidade, como cursores roláveis ou transações, raramente dão suporte a todos os DBMSs. Em vez disso, eles tendem a ser altamente interoperáveis entre um conjunto limitado de DBMSs. Normalmente, os desenvolvedores de aplicativos verticais optam por oferecer suporte a esses DBMSs que representam uma grande fração do mercado e ignoram o restante. Eles podem até mesmo optar por dar suporte a drivers específicos para que esses DBMSs reduzam seus custos de teste e suporte a produtos.  
  
 Como os aplicativos verticais podem dar suporte a um conjunto conhecido de DBMSs, às vezes eles contêm código específico de driver ou DBMS específico. No entanto, esse código é melhor mantido para um mínimo porque requer tempo extra para manter.
