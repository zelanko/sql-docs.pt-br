---
title: "Referência de API de DLL de instalação | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC drivers [ODBC], driver setup DLL
- driver setup DLL [ODBC]
ms.assetid: f9d03f17-1c0d-4e7c-9c04-8c316e07ef25
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 953fbdf89defc5b17e3899cad3ec2077c693df9d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="setup-dll-api-reference"></a>Referência de API de DLL de instalação
Esta seção descreve a sintaxe da API de DLL, que consiste em duas funções de instalação do driver (**ConfigDriver** e **ConfigDSN**). **ConfigDriver** e **ConfigDSN** pode ser na DLL do driver ou em um separado DLL de instalação.  
  
 Além disso, esta seção descreve a sintaxe da API de DLL, que consiste em uma única função de instalação do conversor (**ConfigTranslator**). **ConfigTranslator** pode ser no tradutor DLL ou em um separado DLL de instalação.  
  
 Cada função é rotulada com a versão do ODBC no qual ele foi introduzido.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Função ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)  
  
-   [Função ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)  
  
-   [Função ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)
