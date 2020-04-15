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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 55710d8ea734cba86ae5e4daa725f75e94e65a64
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81279898"
---
# <a name="static-sql"></a>SQL Estático
O SQL incorporado mostrado no [SQL Incorporado Exemplo](../../odbc/reference/embedded-sql-example.md) é conhecido como SQL estático. É chamado de SQL estático porque as instruções SQL no programa são estáticas; ou seja, eles não mudam cada vez que o programa é executado. Conforme descrito na seção anterior, essas instruções são compiladas quando o resto do programa é compilado.  
  
 O Static SQL funciona bem em muitas situações e pode ser usado em qualquer aplicativo para o qual o acesso aos dados pode ser determinado na hora do projeto do programa. Por exemplo, um programa de entrada de pedidos sempre usa a mesma instrução para inserir um novo pedido, e um sistema de reserva de companhia aérea sempre usa a mesma instrução para alterar o status de um assento de disponível para reservado. Cada uma dessas declarações seria generalizada através do uso de variáveis host; diferentes valores podem ser inseridos em uma ordem de venda, e diferentes lugares podem ser reservados. Como tais declarações podem ser codificadas no programa, tais programas têm a vantagem de que as declarações precisam ser analisados, validados e otimizados apenas uma vez, no momento da compilação. Isso resulta em código relativamente rápido.
