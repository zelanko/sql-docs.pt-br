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
manager: craigg
ms.openlocfilehash: df7a2d036692cefcd1b2ea2338d51938a11ea85a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47610474"
---
# <a name="vertical-applications"></a>Aplicativos verticais
Aplicativos verticais geralmente executam uma tarefa bem definida em relação a um único DBMS. Por exemplo, um aplicativo de entrada de pedidos rastreia os pedidos em uma empresa. O que esses tipos de aplicativos têm em comum é que o esquema de banco de dados geralmente é criado pelo desenvolvedor do aplicativo e, embora o aplicativo possa funcionar com um número de diferentes DBMSs, ele funciona com um DBMS único para um único cliente.  
  
 Como aplicativos verticais geralmente requerem certas funcionalidades, como cursores roláveis ou transações, eles raramente oferecem suporte a todos os DBMSs. Em vez disso, eles tendem a ser altamente interoperável entre um conjunto limitado de DBMSs. Normalmente, os desenvolvedores de aplicativos verticais escolhe dar suporte a esses DBMSs que representam uma grande parte do mercado e ignorar o restante. Eles ainda podem optar por dar suporte a drivers específicos para esses DBMSs reduzir seus testes e os custos de suporte do produto.  
  
 Como aplicativos verticais podem dar suporte a um conjunto conhecido de DBMSs, às vezes contêm código específico do driver ou específicos de DBMS. No entanto, esse código melhor é mantido no mínimo, porque ela requer mais tempo para manter.
