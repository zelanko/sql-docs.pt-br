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
ms.openlocfilehash: f24e50b7f6dd8b129a2777ce1132ec426b7ea182
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68078979"
---
# <a name="writing-an-interoperable-application"></a>Escrever um aplicativo interoperável
Sempre que um aplicativo usa o mesmo código em relação a mais de um driver, esse código deve ser interoperável entre esses drivers. Na maioria dos casos, essa é uma tarefa fácil. Por exemplo, o código para buscar linhas com um cursor de somente avanço é o mesmo para todos os drivers. Em alguns casos, isso pode ser mais difícil. Por exemplo, o código para construir identificadores para uso em instruções SQL precisa considerar as convenções de nomenclatura de maiúsculas e minúsculas de identificador, de cotação e de uma parte, de duas partes e de três partes.  
  
 Em geral, o código interoperável deve lidar com problemas de suporte a recursos e variabilidade de recursos. *Suporte a recursos* refere-se a um recurso específico ou não ao qual há suporte. Por exemplo, nem todos os DBMSs dão suporte a transações e o código interoperável deve funcionar corretamente, independentemente do suporte a transações. A *variabilidade do recurso* se refere à variação da maneira em que há suporte para um recurso específico. Por exemplo, os nomes de catálogo são colocados no início dos identificadores em alguns DBMS e no final dos identificadores em outros.  
  
 Os aplicativos podem lidar com o suporte a recursos e variabilidade de recursos em tempo de design ou em tempo de execução. Para lidar com o suporte e a variabilidade do recurso em tempo de design, um desenvolvedor examina os DBMS e os drivers de destino e garante que o mesmo código será interoperável entre eles. Isso é geralmente a maneira como os aplicativos com interoperabilidade baixa ou limitada lidam com esses problemas.  
  
 Por exemplo, se o desenvolvedor garantir que um aplicativo vertical funcionará apenas com quatro DBMSs específicos e se cada um desses DBMSs oferecer suporte a transações, o aplicativo não precisará de um código para verificar o suporte a transações no tempo de execução. Ele sempre pode assumir que as transações estão disponíveis devido à decisão do tempo de design de usar apenas quatro DBMS, cada uma delas com suporte para transações.  
  
 Para lidar com o suporte e a variabilidade de recursos em tempo de execução, o aplicativo deve testar recursos diferentes em tempo de execução e agir de acordo. Geralmente, essa é a maneira em que aplicativos altamente interoperáveis lidam com esses problemas. Para problemas de suporte de recursos, isso significa escrever código que torna o recurso opcional ou gravando código que emula o recurso quando ele não está disponível. Para problemas de variabilidade de recurso, isso significa escrever código que dê suporte a todas as variações possíveis.  
  
 Esta seção contém os seguintes tópicos:  
  
-   [Verificar o suporte ao recurso e a variabilidade](../../../odbc/reference/develop-app/checking-feature-support-and-variability.md)  
  
-   [Recursos a serem inspecionados](../../../odbc/reference/develop-app/features-to-watch-for.md)
