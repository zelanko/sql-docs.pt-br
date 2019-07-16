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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016742"
---
# <a name="static-sql"></a>SQL Estático
O embedded SQL mostrado na [exemplo de SQL inserido](../../odbc/reference/embedded-sql-example.md) é conhecido como SQL estático. Ele é chamado SQL estático porque as instruções SQL no programa são estáticas; ou seja, elas não alteram cada vez que o programa é executado. Conforme descrito na seção anterior, essas instruções são compiladas quando o restante do programa é compilado.  
  
 SQL estático funciona bem em muitas situações e pode ser usado em qualquer aplicativo para o qual o acesso a dados pode ser determinado em tempo de design de programa. Por exemplo, um programa de entrada de ordem sempre usa a mesma instrução para inserir um novo pedido e um sistema de reserva de companhia aérea sempre usa a mesma instrução para alterar o status de uma estação de disponível reservada. Cada uma dessas instruções deve ser generalizada com o uso de variáveis de host; valores diferentes podem ser inseridos em uma ordem de venda e estações diferentes podem ser reservadas. Como tais instruções podem ser codificados no programa, esses programas têm a vantagem que as declarações precisam ser analisados, validados e otimizado para apenas uma vez, em tempo de compilação. Isso resulta em código relativamente rápido.
