---
title: Arquitetura ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], components
- ODBC architecture [ODBC]
ms.assetid: 2604f492-587b-4a51-9876-59a7870b3ef2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 83e35d58d180336c349e83c7991d27f7007aca4e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63273632"
---
# <a name="odbc-architecture"></a>Arquitetura ODBC
A arquitetura ODBC tem quatro componentes:  
  
-   **Aplicativo** executa processamento e chamadas de funções ODBC para enviar instruções SQL e recuperar os resultados.  
  
-   **Gerenciador de driver** carrega e descarrega drivers em nome de um aplicativo. Função ODBC processos chama ou passa para um driver.  
  
-   **Driver** função processos ODBC chama, envia solicitações SQL para uma fonte de dados específico e retorna os resultados para o aplicativo. Se necessário, o driver modifica uma solicitação de aplicativo para que a solicitação está em conformidade com a sintaxe com suporte pelo DBMS associado.  
  
-   **Fonte de dados** Consists dos dados que o usuário deseja acessar e seu sistema operacional associado, o DBMS, e a plataforma de rede (se houver) usado para acessar o DBMS.  
  
 Observe os seguintes pontos sobre a arquitetura do ODBC. Primeiro, vários drivers e fontes de dados podem existir, o que permite que o aplicativo acessar simultaneamente os dados de mais de uma fonte de dados. Em segundo lugar, a API do ODBC é usada em dois lugares: entre o aplicativo e o Gerenciador de Driver e entre o Gerenciador de Driver e cada driver. A interface entre o Gerenciador de Driver e os drivers às vezes é conhecida como o *interface de provedor de serviço* ou *SPI*. Para ODBC, o aplicativo de API (interface) e a interface de provedor de serviço (SPI) de programação são os mesmos; ou seja, o Gerenciador de Driver e cada driver tem a mesma interface para as mesmas funções.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Aplicativos](../../odbc/reference/applications.md)  
  
-   [O Gerenciador de Driver](../../odbc/reference/the-driver-manager.md)  
  
-   [Drivers](../../odbc/reference/drivers.md)  
  
-   [Fontes de dados](../../odbc/reference/data-sources.md)
