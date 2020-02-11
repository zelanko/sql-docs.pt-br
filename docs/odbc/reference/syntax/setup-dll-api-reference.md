---
title: Referência da API da DLL de instalação | Microsoft Docs
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
ms.openlocfilehash: 26e5c36b41f68627a634714cfa06525c99451450
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67947050"
---
# <a name="setup-dll-api-reference"></a>Referência de API de DLL de instalação
Esta seção descreve a sintaxe da API da DLL de instalação do driver, que consiste em duas funções (**ConfigDriver** e **ConfigDSN**). **ConfigDriver** e **ConfigDSN** podem estar na DLL do driver ou em uma DLL de instalação separada.  
  
 Além disso, esta seção descreve a sintaxe da API DLL de instalação do tradutor, que consiste em uma única função (**ConfigTranslator**). **ConfigTranslator** pode estar na DLL do tradutor ou em uma DLL de instalação separada.  
  
 Cada função é rotulada com a versão do ODBC na qual ela foi introduzida.  
  
 Esta seção contém os seguintes tópicos:  
  
-   [Função ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)  
  
-   [Função ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)  
  
-   [Função ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)
