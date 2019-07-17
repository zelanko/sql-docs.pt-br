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
ms.openlocfilehash: 5b2113167bb3440c0d772a99b4b8098104d7ed11
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68129254"
---
# <a name="standard-database-access-architectures"></a>Arquiteturas de acesso ao banco de dados padrão
Olhando para os componentes de acesso de banco de dados descritos na seção anterior, acontece que dois deles - programação interfaces e protocolos de fluxo de dados – são bons candidatos para padronização. Os outros dois componentes - mecanismo IPC e protocolos de rede - não apenas residem em um nível muito baixo, mas eles são altamente dependentes na rede e sistema operacional. Também há uma terceira abordagem - gateways, que oferece possibilidades para padronização.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Interface de programação padrão](../../odbc/reference/standard-programming-interface.md)  
  
-   [Protocolo de fluxo de dados padrão](../../odbc/reference/standard-data-stream-protocol.md)  
  
-   [Gateway padrão](../../odbc/reference/standard-gateway.md)
