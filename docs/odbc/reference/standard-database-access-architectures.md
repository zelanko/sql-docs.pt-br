---
title: "Arquiteturas de acesso de banco de dados padrão | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a9d41800-9068-4b76-895a-32b2853692dd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ff9ebb61d8a0446f4c6015dd5c0ae56c22ebfc45
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="standard-database-access-architectures"></a>Arquiteturas de acesso de banco de dados padrão
Olhando para os componentes de acesso de banco de dados descritos na seção anterior, acontece que dois deles, interfaces de programação e os dados de fluxo de protocolos — são bons candidatos para padronização. Os dois componentes, protocolos de rede e o mecanismo IPC — não apenas residem em um nível muito baixo, mas eles são altamente dependentes de rede e sistema operacional. Há também uma terceira abordagem — gateways — que fornece as possibilidades de padronização.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Interface de programação padrão](../../odbc/reference/standard-programming-interface.md)  
  
-   [Protocolo de fluxo de dados padrão](../../odbc/reference/standard-data-stream-protocol.md)  
  
-   [Gateway padrão](../../odbc/reference/standard-gateway.md)

