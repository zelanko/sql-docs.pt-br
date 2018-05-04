---
title: Interfaces de nível de chamada | Microsoft Docs
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
- SQL statements [ODBC], CLI
- CLI [ODBC], using CLI
- sending SQL statements to DBMS [ODBC]
- SQL [ODBC], CLI
- call-level interface [ODBC], using call-level interface
ms.assetid: 42257bb6-0bf1-4533-a4ef-4a6dd2aecb18
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5df7ff90e8b290f6fb55f1c62b59eee10d83cd8e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="call-level-interfaces"></a>Interfaces de nível de chamada
A técnica final para enviar instruções SQL para o DBMS é por meio de uma interface de nível de chamada (CLI). Uma interface de nível de chamada fornece uma biblioteca de funções DBMS que pode ser chamado pelo programa de aplicativo. Assim, em vez de tentar blend SQL com outra linguagem de programação, uma interface de nível de chamada é semelhante às bibliotecas rotina a maioria dos programadores estão acostumados a usar, como a cadeia de caracteres, e/s ou bibliotecas matemáticas em C. Observe que os que oferecem suporte para SQL incorporado já tem uma interface de nível de chamada, as chamadas que são geradas pelo pré-compilador. No entanto, essas chamadas são não documentado e sujeito a alterações sem aviso prévio.  
  
 Interfaces de nível de chamada são usadas em arquiteturas de cliente/servidor, na qual o programa de aplicativo (cliente) reside em um computador e o DBMS (o servidor) reside em um computador diferente. O aplicativo chama as funções CLI no sistema local, e as chamadas são enviadas pela rede para o DBMS para processamento.  
  
 Uma interface de nível de chamada é semelhante ao SQL dinâmico, instruções SQL são passadas para o DBMS para processamento em tempo de execução, mas ele difere do SQL inserido como um todo em que não há nenhuma instrução SQL incorporada e nenhum pré-compilador é necessária.  
  
 Usando uma interface de nível de chamada geralmente envolve as seguintes etapas:  
  
1.  O aplicativo chama uma função CLI para se conectar ao DBMS.  
  
2.  O aplicativo compila uma instrução SQL e coloca-o em um buffer. Depois, ele chama uma ou mais funções CLI para enviar a instrução para o DBMS para preparação e execução.  
  
3.  Se a instrução for uma instrução SELECT, o aplicativo chama uma função CLI para retornar os resultados em buffers do aplicativo. Normalmente, essa função retorna uma linha ou uma coluna de dados por vez.  
  
4.  O aplicativo chama uma função CLI para se desconectar do DBMS.
