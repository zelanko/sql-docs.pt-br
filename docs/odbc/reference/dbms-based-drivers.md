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
manager: craigg
ms.openlocfilehash: cc35f7bceff2d9e92b70448040bb602117b76c84
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63186289"
---
# <a name="dbms-based-drivers"></a>Drivers baseados em DBMS
Drivers baseados em DBMS são usados com fontes de dados como Oracle ou SQL Server que fornecem um mecanismo de banco de dados autônomo para o driver a ser usado. Esses drivers acessam os dados físicos por meio do mecanismo autônomo; ou seja, eles enviar instruções SQL para e recuperar os resultados do mecanismo.  
  
 Como drivers baseados em DBMS usam um mecanismo de banco de dados existente, eles normalmente são mais fáceis de escrever do que drivers baseados em arquivo. Embora um driver baseados em DBMS pode ser facilmente implementado, convertendo as chamadas ODBC para chamadas à API nativas, isso resulta em um driver mais lento. Uma maneira melhor para implementar um driver de DBMS é usar o protocolo de fluxo de dados subjacente, que geralmente é o que faz a API nativa. Por exemplo, um driver do SQL Server deve usar o protocolo TDS (o fluxo de protocolo para o SQL Server) em vez de biblioteca de DB (a API nativa para o SQL Server). Uma exceção a essa regra é quando o ODBC é a API nativa. Por exemplo, Watcom SQL é um mecanismo autônomo que reside no mesmo computador que o aplicativo e é carregado diretamente como o driver.  
  
 Drivers baseados em DBMS atuam como cliente em uma configuração de cliente/servidor em que a fonte de dados atua como o servidor. Na maioria dos casos, o cliente (driver) e o servidor (fonte de dados) residem em computadores diferentes, embora ambos podem residir no mesmo computador executando um sistema operacional multitarefa. Uma terceira possibilidade é uma *gateway,* que fica entre o driver e a fonte de dados. Um gateway é uma parte do software que faz com que um DBMS para se parecer com o outro. Por exemplo, aplicativos escritos para usar o SQL Server também podem acessar dados do DB2 por meio do Gateway Micro Decisionware DB2; Este produto faz com que o DB2 para se parecer com o SQL Server.  
  
 A ilustração a seguir mostra três configurações diferentes de drivers baseados em DBMS. A primeira configuração, o driver e a fonte de dados residem no mesmo computador. Na segunda, o driver e a fonte de dados residem em computadores diferentes. O terceiro, o driver e a fonte de dados residem em computadores diferentes e um gateway fica entre eles, que residem em outra máquina.  
  
 ![Três configurações para o DBMS&#45;com base em drivers](../../odbc/reference/media/pr07.gif "pr07")
