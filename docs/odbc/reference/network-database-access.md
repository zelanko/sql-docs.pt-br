---
title: Banco de dados de acesso à rede | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- network database access [ODBC]
- standardizing database access [ODBC], network
ms.assetid: f31dd938-e992-436b-b613-145c23973064
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1ff13d2e46377b0d29c9bbc8e8ad1705dedc048b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47633404"
---
# <a name="network-database-access"></a>Acesso ao banco de dados de rede
Acessar um banco de dados em uma rede requer um número de componentes, cada um deles é independente do e reside abaixo, a interface de programação. Esses componentes são mostrados na ilustração a seguir.  
  
 ![Componentes para acessar um banco de dados em uma rede](../../odbc/reference/media/pr04.gif "pr04")  
  
 Segue uma descrição detalhada de cada componente:  
  
-   **Interface de programação** conforme descrito anteriormente nesta seção, a interface de programação contém as chamadas feitas pelo aplicativo. Essas interfaces (incorporado SQL, SQL módulos e interfaces de nível de chamada) são geralmente específicos de cada DBMS, embora elas geralmente são baseadas em um padrão ANSI ou ISO.  
  
-   **Data Stream Protocol** o protocolo de fluxo de dados descreve o fluxo de dados transferidos entre o DBMS e seu cliente. Por exemplo, o protocolo pode exigir o primeiro byte para descrever o que contém o restante do fluxo: uma instrução SQL a ser executada, um valor de erro retornado, ou dados retornados. O formato do resto dos dados no fluxo, em seguida, dependem desse sinalizador. Por exemplo, um fluxo de erro pode conter um código de erro de inteiro de 2 bytes, o sinalizador, um tamanho de mensagem de erro de inteiro de 2 bytes e uma mensagem de erro.  
  
     O protocolo de fluxo de dados é um protocolo de lógico e é independente dos protocolos usados pela rede subjacente. Assim, um protocolo de fluxo de dados único geralmente pode ser usado em um número de redes diferentes. Protocolos de fluxo de dados são normalmente proprietários e foram otimizados para funcionar com um DBMS específico.  
  
-   **Entre processos de mecanismo de comunicação** o mecanismo de comunicação entre processos (IPC) é o processo pelo qual um processo se comunica com os outros. Exemplos incluem DECnet soquetes, soquetes TCP/IP e pipes nomeados. A escolha do mecanismo IPC é restrito pelo sistema operacional e rede que está sendo usado.  
  
-   **Protocolo de rede** o protocolo de rede usado para transportar o fluxo de dados em uma rede. Ele pode ser considerado o encanamento que dá suporte os mecanismos IPC usados para implementar os dados de fluxo de protocolo, bem como suporte a operações de rede básica, como transferências de arquivos e compartilhamento de impressão. Protocolos de rede incluem NetBEUI, TCP/IP, DECnet e SPX/IPX e são específicos para cada rede.
