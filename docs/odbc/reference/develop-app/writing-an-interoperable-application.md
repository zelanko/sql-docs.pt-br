---
title: Escrevendo um aplicativo interoperável | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], feature support and variability
- interoperability [ODBC], writing interoperable applications
- feature support in interoperable applications [ODBC]
- feature variability in interoperable applications [ODBC]
ms.assetid: 8b42b8ae-7862-4b63-a0b3-2a204e0c43a5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8e559eab5787a64b6bdf0850147d7d9128fc435c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63208572"
---
# <a name="writing-an-interoperable-application"></a>Escrever um aplicativo interoperável
Sempre que um aplicativo usa o mesmo código em relação a mais de um driver, que o código deve ser interoperável entre esses drivers. Na maioria dos casos, isso é uma tarefa fácil. Por exemplo, o código para buscar linhas com um cursor somente de avanço é o mesmo para todos os drivers. Em alguns casos, isso pode ser mais difícil. Por exemplo, o código para construir identificadores para uso em instruções SQL precisa considerar o caso do identificador, citando e convenções de nomenclatura de três partes de uma parte e duas partes.  
  
 Em geral, o código interoperável precisa lidar com problemas de suporte ao recurso e a variabilidade de recurso. *Suporte ao recurso* refere-se ou não há suporte para um determinado recurso. Por exemplo, nem todos os DBMSs oferecem suporte a transações e interoperável código deve funcionar corretamente, independentemente do suporte a transações. *Recurso variabilidade* refere-se à variação da maneira em que há suporte para um determinado recurso. Por exemplo, nomes de catálogo são colocados no início de identificadores em alguns DBMSs e no final de identificadores em outras.  
  
 Aplicativos podem lidar com o suporte ao recurso e a variabilidade de recurso em tempo de design ou em tempo de execução. Para lidar com o suporte ao recurso e variabilidade em tempo de design, um desenvolvedor examina os drivers e DBMSs de destino e torna-se de que o mesmo código será interoperável entre eles. Isso geralmente é a maneira na qual os aplicativos com pouca ou limitada de interoperabilidade lidam com esses problemas.  
  
 Por exemplo, se o desenvolvedor garante que um aplicativo vertical só funcionará com quatro DBMSs específicos e se cada um desses DBMSs dá suporte a transações, o aplicativo não precisa de código para verificar se há suporte a transações em tempo de execução. Ele sempre pode assumir as transações estão disponíveis por causa do tempo de design decisão de usar apenas quatro DBMSs, cada um deles oferece suporte a transações.  
  
 Para lidar com o suporte ao recurso e variabilidade em tempo de execução, o aplicativo deve testar para recursos diferentes em tempo de execução e aja de forma adequada. Isso geralmente é a maneira na qual os aplicativos altamente interoperáveis lidam com esses problemas. Para problemas de suporte do recurso, isso significa escrever o código que torna o código de recurso opcional ou escrita que emula o recurso quando ele não está disponível. Para problemas de variabilidade de recurso, isso significa escrever um código que dá suporte a todas as variações possíveis.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Verificando o suporte ao recurso e a variabilidade](../../../odbc/reference/develop-app/checking-feature-support-and-variability.md)  
  
-   [Recursos a serem inspecionados](../../../odbc/reference/develop-app/features-to-watch-for.md)
