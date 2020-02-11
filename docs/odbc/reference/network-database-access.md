---
title: Acesso ao banco de dados de rede | Microsoft Docs
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
ms.openlocfilehash: 2f8eaebca02ef3987e3613b5dd896e0f7c130086
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67938031"
---
# <a name="network-database-access"></a>Acesso ao banco de dados de rede
O acesso a um banco de dados em uma rede requer uma série de componentes, cada um dos quais é independente de e reside abaixo da interface de programação. Esses componentes são mostrados na ilustração a seguir.  
  
 ![Componentes para acessar um banco de dados em uma rede](../../odbc/reference/media/pr04.gif "pr04")  
  
 A seguir, uma descrição adicional de cada componente:  
  
-   **Interface de programação** Conforme descrito anteriormente nesta seção, a interface de programação contém as chamadas feitas pelo aplicativo. Essas interfaces (SQL inserido, módulos SQL e interfaces de nível de chamada) geralmente são específicas para cada DBMS, embora elas normalmente se baseiam em um padrão ANSI ou ISO.  
  
-   **Protocolo de fluxo de dados** O protocolo de fluxo de dados descreve o fluxo de dados transferidos entre o DBMS e seu cliente. Por exemplo, o protocolo pode exigir que o primeiro byte Descreva o que o restante do fluxo contém: uma instrução SQL a ser executada, um valor de erro retornado ou dados retornados. O formato do restante dos dados no fluxo dependeria desse sinalizador. Por exemplo, um fluxo de erro pode conter o sinalizador, um código de erro inteiro de 2 bytes, um comprimento de mensagem de erro de inteiro de 2 bytes e uma mensagem de erro.  
  
     O protocolo de fluxo de dados é um protocolo lógico e independente dos protocolos usados pela rede subjacente. Portanto, um único protocolo de fluxo de dados geralmente pode ser usado em várias redes diferentes. Os protocolos de fluxo de dados são normalmente proprietários e foram otimizados para funcionar com um DBMS específico.  
  
-   **Mecanismo de comunicação entre processos** O mecanismo de comunicação entre processos (IPC) é o processo pelo qual um processo se comunica com outro. Os exemplos incluem pipes nomeados, soquetes TCP/IP e soquetes DECnet. A escolha do mecanismo de IPC é restrita pelo sistema operacional e pela rede que está sendo usada.  
  
-   **Protocolo de rede** O protocolo de rede é usado para transportar o fluxo de dados em uma rede. Pode ser considerado o direcionamento que dá suporte aos mecanismos de IPC usados para implementar o protocolo de fluxo de dados, bem como suporte a operações básicas de rede, como transferências de arquivos e compartilhamento de impressão. Os protocolos de rede incluem NetBEUI, TCP/IP, DECnet e SPX/IPX e são específicos para cada rede.
