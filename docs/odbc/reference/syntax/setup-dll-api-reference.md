---
title: Referência de API de DLL de instalação | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], driver setup DLL
- driver setup DLL [ODBC]
ms.assetid: f9d03f17-1c0d-4e7c-9c04-8c316e07ef25
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fa09dad7423a56db064ade504f3b6598f3daf4ff
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="setup-dll-api-reference"></a>Referência de API de DLL de instalação
Esta seção descreve a sintaxe da API de DLL, que consiste em duas funções de instalação do driver (**ConfigDriver** e **ConfigDSN**). **ConfigDriver** e **ConfigDSN** pode ser na DLL do driver ou em um separado DLL de instalação.  
  
 Além disso, esta seção descreve a sintaxe da API de DLL, que consiste em uma única função de instalação do conversor (**ConfigTranslator**). **ConfigTranslator** pode ser no tradutor DLL ou em um separado DLL de instalação.  
  
 Cada função é rotulada com a versão do ODBC no qual ele foi introduzido.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Função ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)  
  
-   [Função ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)  
  
-   [Função ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)
