---
title: Drivers | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2e3996aafa0e4f5b389e4f46d5df3b22632daad9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47710034"
---
# <a name="drivers"></a>Drivers
*Drivers* são bibliotecas que implementam as funções na API do ODBC. Cada um é específica para um determinado DBMS; Por exemplo, um driver para Oracle não pode acessar diretamente os dados em um DBMS Informix. Drivers de exponham as capacidades dos DBMSs subjacentes; eles não são necessários para implementar recursos não suportados pelo DBMS. Por exemplo, se o DBMS subjacente não oferece suporte a junções externas, então nenhum deles deve ser o driver. A única grande exceção a isso é que os drivers para os que não possuem mecanismos de banco de dados autônomo, como Xbase, devem implementar um mecanismo de banco de dados que oferece suporte a pelo menos uma quantidade mínima de SQL.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Tarefas de driver](../../odbc/reference/driver-tasks.md)  
  
-   [Arquitetura do driver](../../odbc/reference/driver-architecture.md)  
  
## <a name="see-also"></a>Consulte também  
 [Drivers ODBC fornecidos pela Microsoft](../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)
