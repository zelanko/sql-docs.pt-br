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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68129254"
---
# <a name="standard-database-access-architectures"></a>Arquiteturas de acesso ao banco de dados padrão
Examinando os componentes de acesso ao banco de dados descritos na seção anterior, acontece que dois deles – interfaces de programação e protocolos de fluxo são bons candidatos à padronização. Os outros dois componentes – mecanismo IPC e protocolos de rede-não só residem em um nível muito baixo, mas são altamente dependentes da rede e do sistema operacional. Também há uma terceira abordagem – gateways, que fornece possibilidades de padronização.  
  
 Esta seção contém os seguintes tópicos:  
  
-   [Interface de programação padrão](../../odbc/reference/standard-programming-interface.md)  
  
-   [Protocolo de fluxo de dados padrão](../../odbc/reference/standard-data-stream-protocol.md)  
  
-   [Gateway padrão](../../odbc/reference/standard-gateway.md)
