---
title: Testando Aplicações Interoperáveis | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c1d43c7aad2501591c497475f6c250ac33712aa7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307737"
---
# <a name="testing-interoperable-applications"></a>Testar aplicativos interoperáveis
Testar aplicativos interoperáveis é, na melhor das hipóteses, um negócio demorado e, na pior das hipóteses, impossível porque novos drivers aparecem continuamente no mercado. No entanto, um grau razoável de teste é possível. Aplicações com interoperabilidade limitada ou baixa só precisam ser testadas contra os drivers que eles têm garantia de suporte. No entanto, eles devem ser totalmente testados contra esses motoristas.  
  
 Aplicações altamente interoperáveis não podem ser testadas praticamente contra todos os drivers. O melhor que a maioria dos desenvolvedores de aplicativos pode fazer é testá-los totalmente contra um pequeno número de drivers e cursoriamente contra vários outros. Os drivers testados devem incluir os drivers mais populares para os DBMSs mais populares no mercado de aplicativos; se o mercado abrange todos os DBMSs, os drivers para DBMSs desktop e servidor devem ser testados.  
  
 Um dos problemas no teste de aplicativos ODBC é o número de componentes envolvidos: o próprio aplicativo, o Driver Manager, o driver, o DBMS e, possivelmente, software de rede ou gateways. Os aplicativos podem facilitar a verificação de erros postando as mensagens de erro retornadas pelas funções ODBC através **do SQLGetDiagField** e **do SQLGetDiagRec**. Essas mensagens identificam o fabricante e o componente em que ocorrem erros. Para obter mais informações, consulte [Diagnósticos](../../../odbc/reference/develop-app/diagnostics.md).
