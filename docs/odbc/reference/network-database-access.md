---
title: Acesso ao banco de dados da rede | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2237c725d6fe3696d1f28d80c09f22183f718de8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295579"
---
# <a name="network-database-access"></a>Acesso ao banco de dados de rede
Acessar um banco de dados em uma rede requer uma série de componentes, cada um dos quais é independente e reside abaixo, a interface de programação. Esses componentes são mostrados na ilustração a seguir.  
  
 ![Componentes para acessar um banco de dados em uma rede](../../odbc/reference/media/pr04.gif "pr04")  
  
 Segue-se uma descrição adicional de cada componente:  
  
-   **Interface de Programação** Como descrito anteriormente nesta seção, a interface de programação contém as chamadas feitas pelo aplicativo. Essas interfaces (sql embarcadas, módulos SQL e interfaces de nível de chamada) são geralmente específicas para cada DBMS, embora geralmente sejam baseadas em um padrão ANSI ou ISO.  
  
-   **Protocolo de fluxo de dados** O protocolo de fluxo de dados descreve o fluxo de dados transferidos entre o DBMS e seu cliente. Por exemplo, o protocolo pode exigir o primeiro byte para descrever o que o resto do fluxo contém: uma declaração SQL a ser executada, um valor de erro retornado ou dados retornados. O formato do resto dos dados no fluxo dependeria então dessa bandeira. Por exemplo, um fluxo de erro pode conter o sinalizador, um código de erro inteiro de 2 bytes, um comprimento de mensagem de erro inteiro de 2 bytes e uma mensagem de erro.  
  
     O protocolo de fluxo de dados é um protocolo lógico e é independente dos protocolos usados pela rede subjacente. Assim, um único protocolo de fluxo de dados geralmente pode ser usado em várias redes diferentes. Os protocolos de fluxo de dados são tipicamente proprietários e foram otimizados para trabalhar com um DBMS específico.  
  
-   **Mecanismo de Comunicação Interprocess** O mecanismo de comunicação entre processos (IPC) é o processo pelo qual um processo se comunica com outro. Exemplos incluem tubos nomeados, tomadas TCP/IP e tomadas DECnet. A escolha do mecanismo iPC é restrita pelo sistema operacional e rede que está sendo utilizado.  
  
-   **Protocolo de rede** O protocolo de rede é usado para transportar o fluxo de dados por uma rede. Pode ser considerado o encanamento que suporta os mecanismos de IPC usados para implementar o protocolo de fluxo de dados, bem como apoiar operações básicas de rede, como transferências de arquivos e compartilhamento de impressão. Os protocolos de rede incluem NetBEUI, TCP/IP, DECnet e SPX/IPX e são específicos para cada rede.
