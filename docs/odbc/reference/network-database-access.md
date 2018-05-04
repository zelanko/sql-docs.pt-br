---
title: O banco de dados de acesso de rede | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- network database access [ODBC]
- standardizing database access [ODBC], network
ms.assetid: f31dd938-e992-436b-b613-145c23973064
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f86fa14b586b1b001b1825d35df62efeebe9e759
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="network-database-access"></a>Acesso de banco de dados de rede
Acessar um banco de dados em uma rede requer um número de componentes, cada um deles é independente do e reside abaixo, a interface de programação. Esses componentes são mostrados na ilustração a seguir.  
  
 ![Componentes para acessar um banco de dados em uma rede](../../odbc/reference/media/pr04.gif "pr04")  
  
 Uma descrição detalhada de cada componente a seguir:  
  
-   **Interface de programação** conforme descrito anteriormente nesta seção, a interface de programação contém as chamadas feitas pelo aplicativo. Essas interfaces (embedded SQL, SQL módulos e interfaces de nível de chamada) são geralmente específicas para cada DBMS, embora eles normalmente com base em um padrão ANSI ou ISO.  
  
-   **Protocolo de fluxo de dados** o protocolo de fluxo de dados descreve o fluxo de dados transferidos entre o DBMS e seu cliente. Por exemplo, o protocolo pode exigir o primeiro byte para descrever o que contém o restante do fluxo: uma instrução SQL a ser executada, um valor de erro retornado, ou dados retornados. O formato do restante dos dados no fluxo, em seguida, dependem desse sinalizador. Por exemplo, um fluxo de erro pode conter um código de erro de inteiro de 2 bytes, o sinalizador, um tamanho de mensagem de erro de inteiro de 2 bytes e uma mensagem de erro.  
  
     O protocolo de fluxo de dados é um protocolo de lógico e é independente dos protocolos usados pela rede subjacente. Assim, um protocolo de fluxo de dados geralmente pode ser usado em um número de redes diferentes. Protocolos de fluxo de dados são normalmente proprietários e foram otimizados para trabalhar com um determinado DBMS.  
  
-   **Entre processos mecanismo de comunicação** o mecanismo de comunicação entre processos (IPC) é o processo pelo qual um processo se comunica com o outro. Exemplos incluem DECnet soquetes, soquetes TCP/IP e pipes nomeados. A escolha do mecanismo IPC é restrito pelo sistema operacional e rede que está sendo usada.  
  
-   **Protocolo de rede** o protocolo de rede usado para transportar o fluxo de dados em uma rede. Ele pode ser considerado o encanamento que oferece suporte os mecanismos IPC usados para implementar os dados de fluxo de protocolo, bem como suporte a operações de rede básica, como transferências de arquivos e compartilhamento de impressão. Protocolos de rede incluem NetBEUI, TCP/IP, DECnet e SPX/IPX e são específicos para cada rede.
