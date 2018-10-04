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
ms.openlocfilehash: 9ff5ee3c22a01b0b1963f1ca6021e72502aa377b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47724114"
---
# <a name="standard-database-access-architectures"></a>Arquiteturas de acesso ao banco de dados padrão
Olhando para os componentes de acesso de banco de dados descritos na seção anterior, acontece que dois deles — protocolos de fluxo de dados e as interfaces de programação — são bons candidatos para padronização. Os dois componentes, protocolos de rede e o mecanismo IPC — não só residem em um nível muito baixo, mas eles são altamente dependentes na rede e sistema operacional. Há também uma terceira abordagem — gateways — que oferece possibilidades para padronização.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Interface de programação padrão](../../odbc/reference/standard-programming-interface.md)  
  
-   [Protocolo de fluxo de dados padrão](../../odbc/reference/standard-data-stream-protocol.md)  
  
-   [Gateway padrão](../../odbc/reference/standard-gateway.md)
