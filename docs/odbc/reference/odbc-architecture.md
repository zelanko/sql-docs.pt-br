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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 07435dc1a5fbe800f2260e914f315cfe93dd8d1b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305127"
---
# <a name="odbc-architecture"></a>Arquitetura ODBC
A arquitetura ODBC tem quatro componentes:  
  
-   Do **aplicativo** Executa o processamento e chama as funções ODBC para enviar instruções SQL e recuperar resultados.  
  
-   **Gerenciador de driver** Carrega e descarrega drivers em nome de um aplicativo. Processa chamadas de função ODBC ou as passa para um driver.  
  
-   Do **Driver** Processa chamadas de função ODBC, envia solicitações SQL para uma fonte de dados específica e retorna os resultados para o aplicativo. Se necessário, o driver modifica a solicitação de um aplicativo para que a solicitação esteja em conformidade com a sintaxe suportada pelo DBMS associado.  
  
-   **Fonte de dados** Consiste nos dados que o usuário deseja acessar e seu sistema operacional, DBMS e plataforma de rede associados (se houver) usados para acessar o DBMS.  
  
 Observe os pontos a seguir sobre a arquitetura ODBC. Primeiro, vários drivers e fontes de dados podem existir, o que permite que o aplicativo acesse dados simultaneamente de mais de uma fonte de dados. Em segundo lugar, a API ODBC é usada em dois locais: entre o aplicativo e o Gerenciador de driver e entre o Gerenciador de driver e cada driver. A interface entre o Gerenciador de driver e os drivers, às vezes, é chamada de *interface do provedor de serviços* ou *SPI*. Para ODBC, a API (interface de programação de aplicativo) e a SPI (Service Provider interface) são as mesmas; ou seja, o Gerenciador de driver e cada driver têm a mesma interface para as mesmas funções.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Aplicativos](../../odbc/reference/applications.md)  
  
-   [O Gerenciador de Driver](../../odbc/reference/the-driver-manager.md)  
  
-   [Drivers](../../odbc/reference/drivers.md)  
  
-   [Fontes de Dados](../../odbc/reference/data-sources.md)
