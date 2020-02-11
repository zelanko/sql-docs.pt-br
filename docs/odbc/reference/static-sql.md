---
title: SQL estático | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- static SQL [ODBC]
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- SQL statements [ODBC], static SQL
- embedded SQL [ODBC]
- SQL [ODBC], static SQL
ms.assetid: 667d92ec-fed9-4028-81d4-bb9ba867356a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2e6d053e4d2a5520432c4c1debbafb35fdb17bc4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68016742"
---
# <a name="static-sql"></a>SQL Estático
O SQL inserido mostrado no [exemplo de SQL inserido](../../odbc/reference/embedded-sql-example.md) é conhecido como SQL estático. Ele é chamado de SQL estático porque as instruções SQL no programa são estáticas; ou seja, elas não são alteradas sempre que o programa é executado. Conforme descrito na seção anterior, essas instruções são compiladas quando o restante do programa é compilado.  
  
 O SQL estático funciona bem em muitas situações e pode ser usado em qualquer aplicativo para o qual o acesso a dados possa ser determinado no tempo de design do programa. Por exemplo, um programa de entrada de pedidos sempre usa a mesma instrução para inserir um novo pedido, e um sistema de reserva de viagens sempre usa a mesma instrução para alterar o status de um assento de disponível para reservado. Cada uma dessas instruções seria generalizada com o uso de variáveis de host; valores diferentes podem ser inseridos em uma ordem de venda e diferentes estações podem ser reservadas. Como essas instruções podem ser embutidas em código no programa, esses programas têm a vantagem de que as instruções precisam ser analisadas, validadas e otimizadas apenas uma vez, no momento da compilação. Isso resulta em código relativamente rápido.
