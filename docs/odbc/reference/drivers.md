---
description: Drivers
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 81e8989fc178728e687baa13b37e6055692d9413
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494589"
---
# <a name="drivers"></a>Drivers
*Drivers* são bibliotecas que implementam as funções na API ODBC. Cada um é específico para um DBMS específico; por exemplo, um driver para Oracle não pode acessar dados diretamente em um DBMS do Informix. Os drivers expõem os recursos dos DBMSs subjacentes; Eles não são necessários para implementar recursos não suportados pelo DBMS. Por exemplo, se o DBMS subjacente não oferecer suporte a junções externas, nenhum deverá ser o driver. A única exceção importante para isso é que os drivers para DBMSs que não têm mecanismos de banco de dados autônomos, como Xbase, devem implementar um mecanismo de banco de dados que, pelo menos, dá suporte a uma quantidade mínima de SQL.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Tarefas de driver](../../odbc/reference/driver-tasks.md)  
  
-   [Arquitetura do driver](../../odbc/reference/driver-architecture.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Drivers ODBC fornecidos pela Microsoft](../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)
