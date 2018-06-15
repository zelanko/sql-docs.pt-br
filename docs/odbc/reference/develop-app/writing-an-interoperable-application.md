---
title: Escrevendo um aplicativo interoperável | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], feature support and variability
- interoperability [ODBC], writing interoperable applications
- feature support in interoperable applications [ODBC]
- feature variability in interoperable applications [ODBC]
ms.assetid: 8b42b8ae-7862-4b63-a0b3-2a204e0c43a5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6aae50c316072c0970ffea4eb953f4e0ee86c5d5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32915881"
---
# <a name="writing-an-interoperable-application"></a>Escrevendo um aplicativo de interoperabilidade
Sempre que um aplicativo usa o mesmo código com mais de um driver, esse código deve ser interoperável entre esses drivers. Na maioria dos casos, essa é uma tarefa fácil. Por exemplo, o código para buscar linhas com um cursor somente de avanço é o mesmo para todos os drivers. Em alguns casos, isso pode ser mais difícil. Por exemplo, o código para construir identificadores para uso em instruções SQL deve considerar o caso de identificador, cotar e convenções de nomenclatura de três partes, parte de uma e duas partes.  
  
 Em geral, o código interoperável precisa lidar com problemas de suporte de recurso e a variabilidade de recurso. *Suporte ao recurso* refere-se ou não há suporte para um determinado recurso. Por exemplo, nem todos os DBMSs oferecem suporte a transações e interoperável código deve funcionar corretamente, independentemente do suporte a transações. *Recurso variabilidade* refere-se à variação da maneira em que há suporte para um determinado recurso. Por exemplo, nomes de catálogo são colocados no início de identificadores em alguns DBMSs e no final de identificadores em outras.  
  
 Aplicativos podem lidar com o suporte ao recurso e a variabilidade de recurso em tempo de design ou em tempo de execução. Para lidar com o suporte ao recurso e a variabilidade em tempo de design, um desenvolvedor examina o destino DBMSs e drivers e garante que o mesmo código será interoperável entre eles. Isso geralmente é a maneira na qual aplicativos com pouca ou limitada interoperabilidade lidam com esses problemas.  
  
 Por exemplo, se o desenvolvedor garante que um aplicativo vertical só funcionará com quatro DBMSs específicos e se cada um desses DBMSs oferece suporte a transações, o aplicativo não precisa de código para verificar se há suporte a transações em tempo de execução. Ele sempre pode assumir as transações estão disponíveis devido a decisão de tempo de design para usar apenas quatro DBMSs, cada um deles oferece suporte a transações.  
  
 Para lidar com o suporte ao recurso e a variabilidade de tempo de execução, o aplicativo deve testar recursos diferentes em tempo de execução e agir de acordo. Isso geralmente é a maneira na qual os aplicativos altamente interoperáveis lidam com esses problemas. Para problemas de suporte ao recurso, isso significa que escrever código que faz com que o código do recurso opcional ou gravação que emula o recurso quando ele não está disponível. Para problemas de variação de recurso, isso significa que escrever código que oferece suporte a todas as possíveis variações.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Verificando o suporte ao recurso e a variabilidade](../../../odbc/reference/develop-app/checking-feature-support-and-variability.md)  
  
-   [Recursos a serem inspecionados](../../../odbc/reference/develop-app/features-to-watch-for.md)
