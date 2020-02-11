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
ms.openlocfilehash: f6b1544f5562468db03a649c263993039a722a3c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68139303"
---
# <a name="generic-applications"></a>Aplicativos genéricos
Os aplicativos genéricos às vezes executam uma tarefa embutida em código, como uma planilha que recupera dados de um banco de dado. Eles também podem executar uma variedade de tarefas definidas pelo usuário, como um aplicativo de consulta genérico, permitindo que o usuário insira e execute uma instrução SQL. O que os aplicativos genéricos têm em comum é que eles devem trabalhar com uma variedade de DBMSs diferentes e que o desenvolvedor não sabe com antecedência quais são esses DBMSs.  
  
 Portanto, os aplicativos genéricos precisam ser altamente interoperáveis. O desenvolvedor deve fazer muitas escolhas, realizar interoperabilidade para recursos e deve escrever código que espere que os drivers ofereçam suporte a uma ampla gama de funcionalidades. Embora aplicativos genéricos possam ser ajustados para funcionar com DBMSs populares, raramente contêm código específico de driver ou DBMS específico.
