---
title: Arquitetura ODBC | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC architecture [ODBC], components
- ODBC architecture [ODBC]
ms.assetid: 2604f492-587b-4a51-9876-59a7870b3ef2
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 495a8c03361e7a7bf94ef7c0a403a1894d24836e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="odbc-architecture"></a>Arquitetura ODBC
A arquitetura ODBC tem quatro componentes:  
  
-   **Aplicativo** executa processamento e chamadas de funções ODBC para enviar instruções SQL e recuperar resultados.  
  
-   **O Gerenciador de driver** carrega e descarrega drivers em nome de um aplicativo. Função ODBC processos chama ou passa para um driver.  
  
-   **Driver** função processos ODBC chama, envia solicitações SQL para uma fonte de dados específica e retorna resultados para o aplicativo. Se necessário, o driver modifica uma solicitação de aplicativo para que a solicitação está em conformidade com a sintaxe com suporte pelo DBMS associado.  
  
-   **Fonte de dados** Consists dos dados que o usuário deseja acesso e seu sistema operacional, DBMS, e a plataforma de rede (se houver) usado para acessar o DBMS.  
  
 Observe os seguintes pontos sobre a arquitetura do ODBC. Primeiro, vários drivers e fontes de dados podem existir, o que permite que o aplicativo acessar dados simultaneamente de mais de uma fonte de dados. Em segundo lugar, a API de ODBC é usada em dois lugares: entre o aplicativo e o Gerenciador de Driver e entre o Gerenciador de Driver e cada driver. A interface entre o Gerenciador de Driver e os drivers às vezes é conhecida como o *interface de provedor de serviço,* ou *ida*. Para ODBC, o application programming interface (API) e a interface de provedor de serviço (IDA) são iguais. ou seja, o Gerenciador de Driver e cada driver tem a mesma interface para as mesmas funções.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Aplicativos](../../odbc/reference/applications.md)  
  
-   [O Gerenciador de Driver](../../odbc/reference/the-driver-manager.md)  
  
-   [Drivers](../../odbc/reference/drivers.md)  
  
-   [Fontes de dados](../../odbc/reference/data-sources.md)
