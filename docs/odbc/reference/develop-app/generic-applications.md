---
description: Aplicativos genéricos
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9980edcaf34182b4c7f43aa8e935d095f2345138
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476678"
---
# <a name="generic-applications"></a>Aplicativos genéricos
Os aplicativos genéricos às vezes executam uma tarefa embutida em código, como uma planilha que recupera dados de um banco de dado. Eles também podem executar uma variedade de tarefas definidas pelo usuário, como um aplicativo de consulta genérico, permitindo que o usuário insira e execute uma instrução SQL. O que os aplicativos genéricos têm em comum é que eles devem trabalhar com uma variedade de DBMSs diferentes e que o desenvolvedor não sabe com antecedência quais são esses DBMSs.  
  
 Portanto, os aplicativos genéricos precisam ser altamente interoperáveis. O desenvolvedor deve fazer muitas escolhas, realizar interoperabilidade para recursos e deve escrever código que espere que os drivers ofereçam suporte a uma ampla gama de funcionalidades. Embora aplicativos genéricos possam ser ajustados para funcionar com DBMSs populares, raramente contêm código específico de driver ou DBMS específico.
