---
title: Drivers | Microsoft Docs
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
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC]
- drivers [ODBC], about drivers
ms.assetid: d6795d92-877e-44e1-b7d5-2ff2fd3989bd
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2f25be027774c83a31077953eaf51ea8f643bf5e
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="drivers"></a>Drivers
*Drivers* bibliotecas que implementam as funções da API do ODBC. Cada tipo é específico para um determinado DBMS; Por exemplo, um driver para Oracle não pode acessar diretamente os dados em um DBMS Informix. Drivers exponham os recursos dos DBMSs subjacentes; eles não são necessários para implementar recursos não suportados pelo DBMS. Por exemplo, se o DBMS subjacente não oferece suporte a junções externas e não deve o driver. A única grande exceção a isso é que os drivers para os que não possuem mecanismos de banco de dados independente, como Xbase, devem implementar um mecanismo de banco de dados que oferece suporte a pelo menos uma quantidade mínima de SQL.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Tarefas de driver](../../odbc/reference/driver-tasks.md)  
  
-   [Arquitetura do driver](../../odbc/reference/driver-architecture.md)  
  
## <a name="see-also"></a>Consulte também  
 [Drivers ODBC fornecidos pela Microsoft](../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)

