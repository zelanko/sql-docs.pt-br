---
title: Arquiteturas de acesso de banco de dados padrão | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a9d41800-9068-4b76-895a-32b2853692dd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1235aa339afdce6bc895c8d616ffdcdec8cae766
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="standard-database-access-architectures"></a>Arquiteturas de acesso de banco de dados padrão
Olhando para os componentes de acesso de banco de dados descritos na seção anterior, acontece que dois deles, interfaces de programação e os dados de fluxo de protocolos — são bons candidatos para padronização. Os dois componentes, protocolos de rede e o mecanismo IPC — não apenas residem em um nível muito baixo, mas eles são altamente dependentes de rede e sistema operacional. Há também uma terceira abordagem — gateways — que fornece as possibilidades de padronização.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Interface de programação padrão](../../odbc/reference/standard-programming-interface.md)  
  
-   [Protocolo de fluxo de dados padrão](../../odbc/reference/standard-data-stream-protocol.md)  
  
-   [Gateway padrão](../../odbc/reference/standard-gateway.md)
