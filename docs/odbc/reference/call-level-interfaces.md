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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4288a278f745d533c92d3d45892753ef1a74c2b3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306537"
---
# <a name="call-level-interfaces"></a>Interfaces de nível de chamada
A técnica final para enviar instruções SQL para o DBMS é através de uma interface de nível de chamada (CLI). Uma interface de nível de chamada fornece uma biblioteca de funções DBMS que podem ser chamadas pelo programa de aplicativos. Assim, em vez de tentar misturar SQL com outra linguagem de programação, uma interface de nível de chamada é semelhante às bibliotecas de rotina que a maioria dos programadores estão acostumados a usar, como as bibliotecas de string, I/O ou matemática em C. Observe que os DBMSs que suportam SQL incorporado já possuem uma interface de nível de chamada, as chamadas para as quais são geradas pelo pré-compilador. No entanto, essas chamadas não estão documentadas e sujeitas a alterações sem aviso prévio.  
  
 Interfaces de nível de chamada são comumente usadas em arquiteturas cliente/servidor, nas quais o programa de aplicativos (o cliente) reside em um computador e o DBMS (servidor) reside em um computador diferente. O aplicativo chama funções CLI no sistema local, e essas chamadas são enviadas através da rede para o DBMS para processamento.  
  
 Uma interface de nível de chamada é semelhante ao SQL dinâmico, na medida em que as instruções SQL são passadas para o DBMS para processamento em tempo de execução, mas difere do SQL incorporado como um todo, pois não há instruções SQL incorporadas e nenhum pré-compilador é necessário.  
  
 O uso de uma interface de nível de chamada normalmente envolve as seguintes etapas:  
  
1.  O aplicativo chama uma função CLI para se conectar ao DBMS.  
  
2.  O aplicativo constrói uma declaração SQL e coloca-a em um buffer. Em seguida, ele chama uma ou mais funções CLI para enviar a declaração ao DBMS para preparação e execução.  
  
3.  Se a declaração for uma declaração SELECT, o aplicativo chamará uma função CLI para retornar os resultados em buffers de aplicativos. Normalmente, essa função retorna uma linha ou uma coluna de dados por vez.  
  
4.  O aplicativo chama uma função CLI para se desconectar do DBMS.
