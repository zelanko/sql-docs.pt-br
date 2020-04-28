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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6e78202eff69e6b30dc1e97d80f464dad75bb201
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280029"
---
# <a name="standard-database-access-architectures"></a>Arquiteturas de acesso ao banco de dados padrão
Examinando os componentes de acesso ao banco de dados descritos na seção anterior, acontece que dois deles – interfaces de programação e protocolos de fluxo são bons candidatos à padronização. Os outros dois componentes – mecanismo IPC e protocolos de rede-não só residem em um nível muito baixo, mas são altamente dependentes da rede e do sistema operacional. Também há uma terceira abordagem – gateways, que fornece possibilidades de padronização.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Interface de programação padrão](../../odbc/reference/standard-programming-interface.md)  
  
-   [Protocolo de fluxo de dados padrão](../../odbc/reference/standard-data-stream-protocol.md)  
  
-   [Gateway padrão](../../odbc/reference/standard-gateway.md)
