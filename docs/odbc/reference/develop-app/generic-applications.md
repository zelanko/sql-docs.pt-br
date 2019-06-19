---
title: Aplicativos genéricos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], generic applications
- interoperability [ODBC], levels
- generic applications [ODBC]
ms.assetid: dda2a3c4-76ef-40a6-b3a1-9e95bed61618
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 59110f66c512845ff5ce1f2f246c05c63fa755b9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63061494"
---
# <a name="generic-applications"></a>Aplicativos genéricos
Aplicativos genéricos, às vezes, executam uma tarefa embutida, como uma planilha que recuperar dados de um banco de dados. Eles também podem executar uma variedade de tarefas definidas pelo usuário, como um aplicativo de consultas genérico, permitindo que o usuário inserir e executar uma instrução SQL. Quais aplicativos genéricos têm em comum é que eles devem trabalhar com uma variedade de diferentes DBMSs e que o desenvolvedor não sabe com antecedência quais serão esses DBMSs.  
  
 Portanto, os aplicativos genéricos precisam ser altamente interoperável. O desenvolvedor deve fazer muitas escolhas, contrabalançando a interoperabilidade para recursos e deve escrever o código que espera que os drivers para dar suporte a uma ampla variedade de funcionalidade. Enquanto os aplicativos genéricos podem ser ajustados para trabalhar com DBMSs populares, eles raramente contém código específico do driver ou específicos de DBMS.
