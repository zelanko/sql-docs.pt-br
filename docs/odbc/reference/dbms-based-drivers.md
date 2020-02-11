---
title: Drivers baseados em DBMS | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- drivers [ODBC], DBMS-based drivers
- DBMS-based drivers [ODBC]
- ODBC architecture [ODBC], drivers
ms.assetid: e2208ee0-4cd6-4f0d-bb71-a0b54f7d9330
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fcd2221d9a0bb9cba42745901e5f00a6f8c8415e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68111255"
---
# <a name="dbms-based-drivers"></a>Drivers baseados em DBMS
Os drivers baseados em DBMS são usados com fontes de dados como Oracle ou SQL Server que fornecem um mecanismo de banco de dados autônomo para o driver usar. Esses drivers acessam os dados físicos por meio do mecanismo autônomo; ou seja, eles enviam instruções SQL para e recuperam os resultados do mecanismo.  
  
 Como os drivers baseados em DBMS usam um mecanismo de banco de dados existente, geralmente são mais fáceis de escrever do que os drivers baseados em arquivo. Embora um driver baseado em DBMS possa ser facilmente implementado com a tradução de chamadas ODBC para chamadas de API nativas, isso resulta em um driver mais lento. Uma maneira melhor de implementar um driver baseado em DBMS é usar o protocolo de fluxo de dados subjacente, que geralmente é o que a API nativa faz. Por exemplo, um driver de SQL Server deve usar o TDS (o protocolo de fluxo de dados para SQL Server) em vez da biblioteca de BD (a API nativa para SQL Server). Uma exceção a essa regra é quando o ODBC é a API nativa. Por exemplo, Watcom SQL é um mecanismo autônomo que reside no mesmo computador que o aplicativo e é carregado diretamente como o driver.  
  
 Os drivers baseados em DBMS atuam como o cliente em uma configuração de cliente/servidor em que a fonte de dados atua como o servidor. Na maioria dos casos, o cliente (driver) e o servidor (fonte de dados) residem em computadores diferentes, embora ambos possam residir no mesmo computador que executa um sistema operacional multitarefa. Uma terceira possibilidade é um *Gateway,* que fica entre o driver e a fonte de dados. Um gateway é uma parte do software que faz com que um DBMS se pareça com o outro. Por exemplo, os aplicativos escritos para usar SQL Server também podem acessar dados do DB2 por meio do gateway do DB2 de tomada de decisões; Este produto faz com que o DB2 pareça SQL Server.  
  
 A ilustração a seguir mostra três configurações diferentes de drivers baseados em DBMS. Na primeira configuração, o driver e a fonte de dados residem no mesmo computador. No segundo, o driver e a fonte de dados residem em computadores diferentes. No terceiro, o driver e a fonte de dados residem em computadores diferentes e um gateway fica entre eles, que residem em outro computador.  
  
 ![Três configurações para drivers baseados no DBMS&#45;](../../odbc/reference/media/pr07.gif "pr07")
