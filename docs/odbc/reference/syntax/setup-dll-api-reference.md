---
title: Referência de API DLL de configuração | Microsoft Docs
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
ms.openlocfilehash: 25cff50b73868b5b3015dfc1a00c560c344a6d36
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298881"
---
# <a name="setup-dll-api-reference"></a>Referência de API de DLL de instalação
Esta seção descreve a sintaxe da API de configuração do driver DLL, que consiste em duas funções (**ConfigDriver** e **ConfigDSN**). **ConfigDriver** e **ConfigDSN** podem estar no DLL do driver ou em uma Configuração separada DLL.  
  
 Além disso, esta seção descreve a sintaxe da aPI de configuração do tradutor DLL, que consiste em uma única função (**ConfigTranslator**). **ConfigTranslator** pode estar no DLL do tradutor ou em uma Configuração separada DLL.  
  
 Cada função é rotulada com a versão do ODBC em que foi introduzida.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Função ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)  
  
-   [Função ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)  
  
-   [Função ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)
