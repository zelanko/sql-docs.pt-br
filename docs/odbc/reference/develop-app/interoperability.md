---
title: Interoperabilidade | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC]
- interoperability [ODBC], about interoperability
ms.assetid: 43b7c849-9d59-4002-9977-9e2c8730b859
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31b20a696c601ff91c591e4c717f468beca34e36
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306217"
---
# <a name="interoperability"></a>Interoperabilidade
*Interoperabilidade* é a capacidade de um único aplicativo de operar com muitos DBMSs diferentes. A necessidade de escrever aplicações genéricas e interoperáveis foi um dos principais fatores que levaram ao desenvolvimento da ODBC. No entanto, a interoperabilidade não é um caminho simples seguido de "não interoperável" para "completamente interoperável". O caminho tem muitas ramificações, e cada uma requer trocas entre recursos, velocidade, complexidade de código e tempo de desenvolvimento.  
  
 O processo de escrita de um aplicativo interoperável segue várias etapas:  
  
1.  Decidir se o aplicativo usará ODBC.  
  
2.  Escolher um nível de interoperabilidade e decidir quais trade-offs são necessários para atingir esse nível.  
  
3.  Escrevendo código interoperável e testando-o o mais plenamente possível.  
  
 Deve-se notar que a interoperabilidade é principalmente o domínio do autor do aplicativo. Os drivers são projetados para trabalhar com um único DBMS e, por definição, não são interoperáveis. Eles desempenham um papel na interoperabilidade, implementando e expondo corretamente o ODBC sobre um único DBMS.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [O ODBC é a resposta?](../../../odbc/reference/develop-app/is-odbc-the-answer.md)  
  
-   [Escolher um nível de interoperabilidade](../../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)  
  
-   [Determinar os drivers e DBMSs de destino](../../../odbc/reference/develop-app/determining-the-target-dbmss-and-drivers.md)  
  
-   [Considerar os recursos de banco de dados a serem usados](../../../odbc/reference/develop-app/considering-database-features-to-use.md)  
  
-   [Comprimento do ciclo do produto](../../../odbc/reference/develop-app/length-of-the-product-cycle.md)  
  
-   [Escrevendo um aplicativo interoperável](../../../odbc/reference/develop-app/writing-an-interoperable-application.md)  
  
-   [Testando aplicativos interoperáveis](../../../odbc/reference/develop-app/testing-interoperable-applications.md)
