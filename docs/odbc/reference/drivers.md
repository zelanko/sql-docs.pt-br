---
title: Motoristas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC]
- drivers [ODBC], about drivers
ms.assetid: d6795d92-877e-44e1-b7d5-2ff2fd3989bd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7c8b40641be3db34fc6929edecdd5dd923700957
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294179"
---
# <a name="drivers"></a>Drivers
*Drivers* são bibliotecas que implementam as funções na API ODBC. Cada um é específico para um DBMS específico; por exemplo, um driver para Oracle não pode acessar diretamente dados em um Informix DBMS. Os drivers expõem as capacidades dos DBMSs subjacentes; eles não são obrigados a implementar recursos não suportados pelo DBMS. Por exemplo, se o DBMS subjacente não suportar as junções externas, então o driver também não deve. A única grande exceção a isso é que os drivers para DBMSs que não possuem mecanismos de banco de dados autônomos, como o Xbase, devem implementar um mecanismo de banco de dados que pelo menos suporte uma quantidade mínima de SQL.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Tarefas de driver](../../odbc/reference/driver-tasks.md)  
  
-   [Arquitetura do driver](../../odbc/reference/driver-architecture.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Drivers ODBC fornecidos pela Microsoft](../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)
