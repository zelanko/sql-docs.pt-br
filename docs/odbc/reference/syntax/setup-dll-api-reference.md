---
description: Referência de API de DLL de instalação
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5cb3e20a1c25d206a1dd27367bbe4a128af0818f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487329"
---
# <a name="setup-dll-api-reference"></a>Referência de API de DLL de instalação
Esta seção descreve a sintaxe da API da DLL de instalação do driver, que consiste em duas funções (**ConfigDriver** e **ConfigDSN**). **ConfigDriver** e **ConfigDSN** podem estar na DLL do driver ou em uma DLL de instalação separada.  
  
 Além disso, esta seção descreve a sintaxe da API DLL de instalação do tradutor, que consiste em uma única função (**ConfigTranslator**). **ConfigTranslator** pode estar na DLL do tradutor ou em uma DLL de instalação separada.  
  
 Cada função é rotulada com a versão do ODBC na qual ela foi introduzida.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Função ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)  
  
-   [Função ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)  
  
-   [Função ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)
