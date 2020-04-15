---
title: Aplicações Genéricas | Microsoft Docs
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
ms.openlocfilehash: 607676d5370f02ee1d39196bff9261bc897521ee
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305547"
---
# <a name="generic-applications"></a>Aplicativos genéricos
Aplicativos genéricos às vezes executam uma tarefa codificada, como uma planilha recuperando dados de um banco de dados. Eles também podem executar uma variedade de tarefas definidas pelo usuário, como um aplicativo de consulta genérico que permite ao usuário inserir e executar uma declaração SQL. O que os aplicativos genéricos têm em comum é que eles devem trabalhar com uma variedade de DBMSs diferentes e que o desenvolvedor não sabe de antemão quais serão esses DBMSs.  
  
 Portanto, as aplicações genéricas precisam ser altamente interoperáveis. O desenvolvedor deve fazer muitas escolhas, negociando a interoperabilidade por recursos, e deve escrever código que espera que os drivers suportem uma ampla gama de funcionalidades. Embora os aplicativos genéricos possam ser sintonizados para trabalhar com DBMSs populares, eles raramente contêm código específico do driver ou específico do DBMS.
