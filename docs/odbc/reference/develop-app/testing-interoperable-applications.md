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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114093"
---
# <a name="testing-interoperable-applications"></a>Testar aplicativos interoperáveis
Testando aplicativos interoperáveis na melhor das hipóteses é um demorado na pior das hipóteses impossível porque novos drivers continuamente aparecem no mercado e de negócios. No entanto, um nível razoável de testes é possível. Aplicativos com pouca ou limitada de interoperabilidade somente precisam ser testados em relação a esses drivers, que eles são garantidos para dar suporte. No entanto, eles devem ser testados totalmente em relação a esses drivers.  
  
 Aplicativos altamente interoperáveis não podem ser testados em relação a todos os drivers na prática. O melhor que a maioria dos desenvolvedores de aplicativo pode fazer é testá-las totalmente contra um pequeno número de drivers e cursorily vários outros. Drivers testados devem incluir os drivers mais populares para os DBMSs mais populares no mercado do aplicativo; Se o mercado abrange todos os DBMSs, drivers para DBMSs de desktop e servidor devem ser testados.  
  
 Um dos problemas em testes de aplicativos de ODBC é o número de componentes envolvidos: o aplicativo em si, o Gerenciador de Driver, o driver, o DBMS e possivelmente o software de rede ou gateways. Aplicativos podem tornar mais fácil rastrear erros ao postar mensagens de erro retornadas pelas funções ODBC por meio **SQLGetDiagField** e **SQLGetDiagRec**. Essas mensagens de identificam o fabricante e o componente nas quais ocorrem erros. Para obter mais informações, consulte [diagnóstico](../../../odbc/reference/develop-app/diagnostics.md).
