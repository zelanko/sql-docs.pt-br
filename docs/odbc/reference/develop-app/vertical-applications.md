---
title: Aplicações Verticais | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300371"
---
# <a name="vertical-applications"></a>Aplicativos verticais
Os aplicativos verticais normalmente executam uma tarefa bem definida contra um único DBMS. Por exemplo, um aplicativo de entrada de pedidos rastreia os pedidos em uma empresa. O que esses tipos de aplicativos têm em comum é que o esquema de banco de dados geralmente é projetado pelo desenvolvedor de aplicativos e, embora o aplicativo possa funcionar com uma série de DBMSs diferentes, ele funciona com um único DBMS para um único cliente.  
  
 Como os aplicativos verticais geralmente requerem certas funcionalidades, como cursores roláveis ou transações, eles raramente suportam todos os DBMSs. Em vez disso, eles tendem a ser altamente interoperáveis entre um conjunto limitado de DBMSs. Normalmente, os desenvolvedores de aplicativos verticais optam por apoiar esses DBMSs que representam uma grande fração do mercado e ignoram o resto. Eles podem até optar por apoiar drivers específicos para esses DBMSs para reduzir seus custos de teste e suporte ao produto.  
  
 Como os aplicativos verticais podem suportar um conjunto conhecido de DBMSs, eles às vezes contêm código específico do driver ou específico do DBMS. No entanto, esse código é melhor mantido ao mínimo porque requer tempo extra para manter.
