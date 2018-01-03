---
title: Drivers | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC]
- drivers [ODBC], about drivers
ms.assetid: d6795d92-877e-44e1-b7d5-2ff2fd3989bd
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b2c7299dbbb9cce2f3c97344df33acf27d89c39f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="drivers"></a>Drivers
*Drivers* bibliotecas que implementam as funções da API do ODBC. Cada tipo é específico para um determinado DBMS; Por exemplo, um driver para Oracle não pode acessar diretamente os dados em um DBMS Informix. Drivers exponham os recursos dos DBMSs subjacentes; eles não são necessários para implementar recursos não suportados pelo DBMS. Por exemplo, se o DBMS subjacente não oferece suporte a junções externas e não deve o driver. A única grande exceção a isso é que os drivers para os que não possuem mecanismos de banco de dados independente, como Xbase, devem implementar um mecanismo de banco de dados que oferece suporte a pelo menos uma quantidade mínima de SQL.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Tarefas de driver](../../odbc/reference/driver-tasks.md)  
  
-   [Arquitetura do driver](../../odbc/reference/driver-architecture.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Drivers ODBC fornecidos pela Microsoft](../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)
