---
title: "Aplicativos genéricos | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], generic applications
- interoperability [ODBC], levels
- generic applications [ODBC]
ms.assetid: dda2a3c4-76ef-40a6-b3a1-9e95bed61618
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4c36060d3c908436376babae7376478849da87ff
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="generic-applications"></a>Aplicativos genéricos
Aplicativos genéricos, às vezes, executam uma tarefa embutida, como uma planilha recuperando dados de um banco de dados. Eles também podem executar uma variedade de tarefas definidas pelo usuário, como um aplicativo de consultas genérico, permitindo que o usuário insira e executar uma instrução SQL. Quais aplicativos genéricos têm em comum é que eles devem trabalhar com uma variedade de diferentes DBMSs e que o desenvolvedor não sabe com antecedência quais esses DBMSs serão.  
  
 Portanto, os aplicativos genéricos precisam ser altamente interoperável. O desenvolvedor deve fazer muitas opções, contrabalançando a interoperabilidade de recursos e deve escrever o código que espera drivers para dar suporte a uma ampla variedade de funcionalidade. Enquanto aplicativos genéricos podem ser ajustados para trabalhar com DBMSs populares, elas raramente contêm código específico do driver ou DBMS específico.
