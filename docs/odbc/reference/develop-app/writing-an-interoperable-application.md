---
title: Escrevendo um Aplicativo Interoperável | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 553e718e0759e47701e7f8c04561693358d5dc52
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81289078"
---
# <a name="writing-an-interoperable-application"></a>Escrever um aplicativo interoperável
Sempre que um aplicativo usa o mesmo código contra mais de um motorista, esse código deve ser interoperável entre esses drivers. Na maioria dos casos, esta é uma tarefa fácil. Por exemplo, o código para buscar linhas com um cursor somente para frente é o mesmo para todos os drivers. Em alguns casos, isso pode ser mais difícil. Por exemplo, o código para construir identificadores para uso em instruções SQL precisa considerar o caso de identificador, citando e convenções de nomeação de uma parte, duas e três partes.  
  
 Em geral, o código interoperável deve lidar com problemas de suporte a recursos e variabilidade de recursos. *O suporte a recursos* refere-se a se um recurso específico é ou não suportado. Por exemplo, nem todas as transações de suporte de DBMSs e código interoperável devem funcionar corretamente, independentemente do suporte à transação. *A variabilidade do recurso* refere-se à variação na forma como um determinado recurso é suportado. Por exemplo, nomes de catálogo são colocados no início de identificadores em alguns DBMSs e no final de identificadores em outros.  
  
 Os aplicativos podem lidar com suporte a recursos e variabilidade de recursos no momento do projeto ou no tempo de execução. Para lidar com o suporte a recursos e a variabilidade no momento do design, um desenvolvedor olha para os DBMSs e drivers alvo e garante que o mesmo código será interoperável entre eles. Esta é geralmente a maneira pela qual aplicações com interoperabilidade baixa ou limitada lidam com esses problemas.  
  
 Por exemplo, se o desenvolvedor garantir que um aplicativo vertical funcionará apenas com quatro DBMSs específicos e se cada um desses DBMSs suportar transações, o aplicativo não precisará de código para verificar o suporte à transação em tempo de execução. Ele sempre pode assumir que as transações estão disponíveis devido à decisão do tempo de projeto de usar apenas quatro DBMSs, cada uma das quais suporta transações.  
  
 Para lidar com o suporte a recursos e a variabilidade no tempo de execução, o aplicativo deve testar diferentes capacidades no tempo de execução e agir de acordo. Esta é geralmente a maneira pela qual aplicações altamente interoperáveis lidam com esses problemas. Para problemas de suporte a recursos, isso significa escrever código que torna o recurso opcional ou código de escrita que emula o recurso quando ele não está disponível. Para problemas de variabilidade de recursos, isso significa escrever código que suporta todas as variações possíveis.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Verificar o suporte ao recurso e a variabilidade](../../../odbc/reference/develop-app/checking-feature-support-and-variability.md)  
  
-   [Recursos a serem inspecionados](../../../odbc/reference/develop-app/features-to-watch-for.md)
