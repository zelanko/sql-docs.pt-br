---
title: Arquiteturas de acesso de banco de dados padrão | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a9d41800-9068-4b76-895a-32b2853692dd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5a0a8457dfde0090ac0d88d12079e88995b39efb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63232391"
---
# <a name="standard-database-access-architectures"></a>Arquiteturas de acesso ao banco de dados padrão
Olhando para os componentes de acesso de banco de dados descritos na seção anterior, acontece que dois deles - programação interfaces e protocolos de fluxo de dados – são bons candidatos para padronização. Os outros dois componentes - mecanismo IPC e protocolos de rede - não apenas residem em um nível muito baixo, mas eles são altamente dependentes na rede e sistema operacional. Também há uma terceira abordagem - gateways, que oferece possibilidades para padronização.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Interface de programação padrão](../../odbc/reference/standard-programming-interface.md)  
  
-   [Protocolo de fluxo de dados padrão](../../odbc/reference/standard-data-stream-protocol.md)  
  
-   [Gateway padrão](../../odbc/reference/standard-gateway.md)
