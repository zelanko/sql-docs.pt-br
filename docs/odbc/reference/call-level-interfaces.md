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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68135670"
---
# <a name="call-level-interfaces"></a>Interfaces de nível de chamada
A técnica final para enviar instruções SQL para o DBMS é por meio de uma CLI (interface de nível de chamada). Uma interface de nível de chamada fornece uma biblioteca de funções do DBMS que podem ser chamadas pelo programa do aplicativo. Portanto, em vez de tentar misturar SQL com outra linguagem de programação, uma interface de nível de chamada é semelhante às bibliotecas rotineiras que a maioria dos programadores estão acostumados a usar, como cadeias de caracteres, e/s ou bibliotecas matemáticas em C. Observe que os DBMSs que dão suporte ao SQL incorporado já têm uma interface de nível de chamada No entanto, essas chamadas não são documentadas e estão sujeitas a alterações sem aviso prévio.  
  
 As interfaces de nível de chamada são comumente usadas em arquiteturas de cliente/servidor, nas quais o programa de aplicativo (o cliente) reside em um computador e o DBMS (o servidor) reside em um computador diferente. O aplicativo chama as funções da CLI no sistema local e essas chamadas são enviadas pela rede para o DBMS para processamento.  
  
 Uma interface de nível de chamada é semelhante ao SQL dinâmico, pois as instruções SQL são passadas para o DBMS para processamento em tempo de execução, mas diferem do SQL inserido como um todo, pois não há instruções SQL inseridas e nenhum pré-compilador é necessário.  
  
 O uso de uma interface de nível de chamada normalmente envolve as seguintes etapas:  
  
1.  O aplicativo chama uma função CLI para se conectar ao DBMS.  
  
2.  O aplicativo cria uma instrução SQL e a coloca em um buffer. Em seguida, ele chama uma ou mais funções de CLI para enviar a instrução para o DBMS para preparação e execução.  
  
3.  Se a instrução for uma instrução SELECT, o aplicativo chamará uma função CLI para retornar os resultados em buffers de aplicativo. Normalmente, essa função retorna uma linha ou uma coluna de dados de cada vez.  
  
4.  O aplicativo chama uma função CLI para se desconectar do DBMS.
