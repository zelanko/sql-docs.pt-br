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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305127"
---
# <a name="odbc-architecture"></a>Arquitetura ODBC
A arquitetura ODBC tem quatro componentes:  
  
-   **Aplicação** Executa o processamento e chama as funções do ODBC para enviar instruções SQL e recuperar resultados.  
  
-   **Gerente de Driver** Carrega e descarrega motoristas em nome de um aplicativo. Processa chamadas de função ODBC ou passa-as para um driver.  
  
-   **Motorista** Processa chamadas de função ODBC, envia solicitações SQL para uma fonte de dados específica e retorna os resultados para o aplicativo. Se necessário, o motorista modifica a solicitação de um aplicativo para que a solicitação esteja em conformidade com a sintaxe suportada pelo DBMS associado.  
  
-   **Fonte de dados** Consiste nos dados que o usuário deseja acessar e seu sistema operacional associado, DBMS, e plataforma de rede (se houver) usado para acessar o DBMS.  
  
 Observe os seguintes pontos sobre a arquitetura ODBC. Primeiro, vários drivers e fontes de dados podem existir, o que permite que o aplicativo acesse simultaneamente dados de mais de uma fonte de dados. Em segundo lugar, a API ODBC é usada em dois lugares: entre o aplicativo e o Driver Manager, e entre o Driver Manager e cada motorista. A interface entre o Driver Manager e os drivers é às vezes referida como a interface do *provedor de serviços,* ou *SPI*. Para o ODBC, a interface de programação de aplicativos (API) e a interface do provedor de serviços (SPI) são as mesmas; ou seja, o Driver Manager e cada driver têm a mesma interface para as mesmas funções.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Aplicativos](../../odbc/reference/applications.md)  
  
-   [O Gerenciador de Driver](../../odbc/reference/the-driver-manager.md)  
  
-   [Drivers](../../odbc/reference/drivers.md)  
  
-   [Fontes de Dados](../../odbc/reference/data-sources.md)
