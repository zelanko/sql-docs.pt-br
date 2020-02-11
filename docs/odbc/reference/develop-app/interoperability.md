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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 434b27bffe3b32aa9fa0c5c6fd3a7100e8c7ea8d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138859"
---
# <a name="interoperability"></a>Interoperabilidade
A *interoperabilidade* é a capacidade de um único aplicativo operar com vários DBMSs diferentes. A necessidade de escrever aplicativos genéricos e interoperáveis era um dos principais fatores que levam ao desenvolvimento do ODBC. No entanto, a interoperabilidade não é um caminho simples seguido de "não interoperável" para "completamente interoperável". O caminho tem muitos branches, e cada um exige compensações entre recursos, velocidade, complexidade de código e tempo de desenvolvimento.  
  
 O processo de gravação de um aplicativo interoperável segue várias etapas:  
  
1.  Decidindo se o aplicativo usará o ODBC.  
  
2.  Escolher um nível de interoperabilidade e decidir quais compensações são necessárias para alcançar esse nível.  
  
3.  Escrever código interoperável e testá-lo o mais completo possível.  
  
 Deve-se observar que a interoperabilidade é principalmente o domínio do gravador de aplicativos. Os drivers são projetados para funcionar com um único DBMS e, por definição, não são interoperáveis. Eles desempenham uma função na interoperabilidade, implementando e expondo corretamente o ODBC em um único DBMS.  
  
 Esta seção contém os seguintes tópicos:  
  
-   [O ODBC é a resposta?](../../../odbc/reference/develop-app/is-odbc-the-answer.md)  
  
-   [Escolher um nível de interoperabilidade](../../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)  
  
-   [Determinar os drivers e DBMSs de destino](../../../odbc/reference/develop-app/determining-the-target-dbmss-and-drivers.md)  
  
-   [Considerar os recursos de banco de dados a serem usados](../../../odbc/reference/develop-app/considering-database-features-to-use.md)  
  
-   [Comprimento do ciclo do produto](../../../odbc/reference/develop-app/length-of-the-product-cycle.md)  
  
-   [Escrever um aplicativo interoperável](../../../odbc/reference/develop-app/writing-an-interoperable-application.md)  
  
-   [Testar aplicativos interoperáveis](../../../odbc/reference/develop-app/testing-interoperable-applications.md)
