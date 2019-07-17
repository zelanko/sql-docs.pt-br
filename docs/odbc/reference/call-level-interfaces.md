---
title: Interfaces de nível de chamada | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], CLI
- CLI [ODBC], using CLI
- sending SQL statements to DBMS [ODBC]
- SQL [ODBC], CLI
- call-level interface [ODBC], using call-level interface
ms.assetid: 42257bb6-0bf1-4533-a4ef-4a6dd2aecb18
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c6c37084ad91a931c4479ecf826c5cb554765412
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135670"
---
# <a name="call-level-interfaces"></a>Interfaces de nível de chamada
A técnica final para enviar instruções SQL para o DBMS é por meio de uma interface de nível de chamada (CLI). Uma interface de nível de chamada fornece uma biblioteca de funções DBMS que pode ser chamada pelo programa de aplicativo. Assim, em vez de tentar blend SQL com outra linguagem de programação, uma interface de nível de chamada é semelhante às bibliotecas de rotina, a maioria dos programadores estão acostumados a usar, como a cadeia de caracteres, e/s ou bibliotecas de matemática em C. Observe que DBMSs que dão suporte a SQL inserido já tem uma interface de nível de chamada, as chamadas para o qual são geradas pelo pré-compilador. No entanto, essas chamadas são não documentados e sujeito a alterações sem aviso prévio.  
  
 Interfaces de nível de chamada são comumente usadas em arquiteturas de cliente/servidor, em que o programa de aplicativo (cliente) reside em um computador e o DBMS (o servidor) reside em um computador diferente. O aplicativo chama funções CLI no sistema local, e essas chamadas são enviadas pela rede para o DBMS para processamento.  
  
 Uma interface de nível de chamada é semelhante ao SQL dinâmico, em que as instruções SQL são passadas para o DBMS para o processamento em tempo de execução, mas ele difere do embedded SQL como um todo em que não há nenhum instruções SQL inseridas e nenhum pré-compilador é necessária.  
  
 Usando uma interface de nível de chamada normalmente envolve as seguintes etapas:  
  
1.  O aplicativo chama uma função CLI para se conectar ao DBMS.  
  
2.  O aplicativo compila uma instrução SQL e coloca-o em um buffer. Depois, ele chama uma ou mais funções CLI para enviar a instrução para o DBMS para preparação e execução.  
  
3.  Se a instrução for uma instrução SELECT, o aplicativo chama uma função CLI para retornar os resultados em buffers do aplicativo. Normalmente, essa função retorna uma linha ou uma coluna de dados por vez.  
  
4.  O aplicativo chama uma função CLI para se desconectar do DBMS.
