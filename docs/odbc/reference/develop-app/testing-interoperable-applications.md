---
title: Testando aplicativos interoperáveis | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], testing interoperable applications
- testing interoperable applications [ODBC]
ms.assetid: 489083cb-8430-40be-9ef2-d75b9a2eea88
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e1f783dcd15321dc08b798b1c0e071b4b43a2caa
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="testing-interoperable-applications"></a>Testando aplicativos interoperáveis
Testando aplicativos interoperáveis na melhor das hipóteses é um demorado na pior das hipóteses impossível porque novos drivers continuamente aparecem no mercado e de negócios. No entanto, um nível razoável de testes é possível. Aplicativos com a interoperabilidade limitada ou baixa somente precisam ser testados em relação os drivers que eles têm garantia de suporte. No entanto, eles devem ser testados totalmente em relação a esses drivers.  
  
 Aplicativos altamente interoperáveis não podem ser testados praticamente em todos os drivers. É o melhor que a maioria dos desenvolvedores de aplicativo pode fazer para testá-las completamente contra um pequeno número de drivers e cursorily vários outros. Drivers testados devem incluir os drivers mais populares para os mais populares DBMSs no mercado do aplicativo; Se o mercado abrange todos os DBMSs, drivers de desktop e servidor DBMSs devem ser testados.  
  
 Um dos problemas em testes de aplicativos de ODBC é o número de componentes envolvidos: o aplicativo em si, o Gerenciador de Driver, o driver, o DBMS e possivelmente o software de rede ou gateways. Aplicativos podem tornar mais fácil rastrear erros postando as mensagens de erro retornadas pelas funções ODBC por meio de **SQLGetDiagField** e **SQLGetDiagRec**. Essas mensagens de identificam o fabricante e o componente nas quais ocorrem erros. Para obter mais informações, consulte [diagnóstico](../../../odbc/reference/develop-app/diagnostics.md).
