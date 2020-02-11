---
title: Testando aplicativos interoperáveis | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], testing interoperable applications
- testing interoperable applications [ODBC]
ms.assetid: 489083cb-8430-40be-9ef2-d75b9a2eea88
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 59f6f5a37e65c802c8d51a1f56a40380f054e39b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68114093"
---
# <a name="testing-interoperable-applications"></a>Testar aplicativos interoperáveis
O teste de aplicativos interoperáveis é o melhor dos negócios demorados e, na pior das hipóteses, porque novos drivers aparecem continuamente no mercado. No entanto, um grau razoável de teste é possível. Aplicativos com interoperabilidade limitada ou baixa só precisam ser testados em relação aos drivers aos quais eles têm garantia de suporte. No entanto, eles devem ser totalmente testados em relação a esses drivers.  
  
 Aplicativos altamente interoperáveis não podem ser testados praticamente em todos os drivers. O melhor que a maioria dos desenvolvedores de aplicativos pode fazer é testá-los totalmente em relação a um pequeno número de drivers e cursorily-los em vários outros. Os drivers testados devem incluir os drivers mais populares para os DBMSs mais populares no mercado do aplicativo; Se o mercado abranger todos os DBMSs, os drivers para DBMSs de área de trabalho e de servidor devem ser testados.  
  
 Um dos problemas no teste de aplicativos ODBC é o número de componentes envolvidos: o próprio aplicativo, o Gerenciador de driver, o driver, o DBMS e possivelmente software de rede ou gateways. Os aplicativos podem facilitar o controle de erros postando as mensagens de erro retornadas pelas funções ODBC por meio de **SQLGetDiagField** e **SQLGetDiagRec**. Essas mensagens identificam o fabricante e o componente em que ocorrem erros. Para obter mais informações, consulte [Diagnostics](../../../odbc/reference/develop-app/diagnostics.md).
