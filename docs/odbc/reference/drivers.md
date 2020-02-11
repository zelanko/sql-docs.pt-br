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
ms.openlocfilehash: 6460410488186c94713d859bf2912f2844ca2736
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915437"
---
# <a name="drivers"></a>Drivers
*Drivers* são bibliotecas que implementam as funções na API ODBC. Cada um é específico para um DBMS específico; por exemplo, um driver para Oracle não pode acessar dados diretamente em um DBMS do Informix. Os drivers expõem os recursos dos DBMSs subjacentes; Eles não são necessários para implementar recursos não suportados pelo DBMS. Por exemplo, se o DBMS subjacente não oferecer suporte a junções externas, nenhum deverá ser o driver. A única exceção importante para isso é que os drivers para DBMSs que não têm mecanismos de banco de dados autônomos, como Xbase, devem implementar um mecanismo de banco de dados que, pelo menos, dá suporte a uma quantidade mínima de SQL.  
  
 Esta seção contém os seguintes tópicos:  
  
-   [Tarefas de driver](../../odbc/reference/driver-tasks.md)  
  
-   [Arquitetura do driver](../../odbc/reference/driver-architecture.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Drivers ODBC fornecidos pela Microsoft](../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)
