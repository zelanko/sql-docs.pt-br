---
title: Referência de API de DLL de instalação | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], driver setup DLL
- driver setup DLL [ODBC]
ms.assetid: f9d03f17-1c0d-4e7c-9c04-8c316e07ef25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d81bb9f5ec54f3d66089205f5b5941119d365501
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622204"
---
# <a name="setup-dll-api-reference"></a>Referência de API de DLL de instalação
Esta seção descreve a sintaxe da API de DLL, que consiste em duas funções de instalação do driver (**ConfigDriver** e **ConfigDSN**). **ConfigDriver** e **ConfigDSN** pode estar na DLL do driver ou DLL de instalação em um separado.  
  
 Além disso, esta seção descreve a sintaxe da API de DLL, que consiste em uma única função de configuração do translator (**ConfigTranslator**). **ConfigTranslator** pode estar no tradutor DLL ou DLL de instalação em um separado.  
  
 Cada função é rotulada com a versão do ODBC na qual ele foi introduzido.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Função ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)  
  
-   [Função ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)  
  
-   [Função ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)
