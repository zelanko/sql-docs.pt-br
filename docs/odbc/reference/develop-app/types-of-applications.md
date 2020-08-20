---
description: Tipos de aplicativos
title: Tipos de aplicativos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- upgrading applications [ODBC], application types
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
- application upgrades [ODBC], application types
- application compatibility issues [ODBC]
ms.assetid: d346a64e-a32c-4153-a40f-5b53c2f57ef2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 54056a6111924fb584ac35a65d6f74e8dab1ba6c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465546"
---
# <a name="types-of-applications"></a>Tipos de aplicativos
Os aplicativos ODBC podem ser classificados da seguinte maneira:  
  
-   **ODBC puro 2.**  
     ** _x_ aplicativo** um aplicativo de 32 bits que:  
  
    -   Chama somente ODBC 2. funções *x* (incluindo a função ODBC 1,0 **SQLSetParam**). Isso inclui o ODBC 1. aplicativos *x* que foram portados para 32 bits.  
  
    -   Espera o ODBC 2. comportamento *x* para recursos que tiveram alterações comportamentais. (Consulte [alterações comportamentais](../../../odbc/reference/develop-app/behavioral-changes.md) para obter mais informações.)  
  
    -   Não foi recompilado com cabeçalhos ODBC 3,5.  
  
-   **ODBC puro 2.**  
     **_x_ aplicativo recompilado** um ODBC 2 puro. *x* aplicativo que foi recompilado usando os arquivos de cabeçalho ODBC 3,5, definindo ODBCVER = 0x0250.  
  
-   **ODBC puro 2.**  
     **_x_ aplicativo Unicode** um ODBC puro 2. *x* aplicativo recompilado que é compatível com Unicode e usa o tipo de dados SQL_WCHAR.  
  
-   **Grupo aberto puro e ISO** - **aplicativo ODBC em conformidade** Um aplicativo de 32 bits que:  
  
    -   Chama funções definidas nos padrões de grupo aberto ou CLI ISO. (Essas funções podem incluir funções de 3,0 preteridas.)  
  
    -   Não usa os tipos de dados Unicode.  
  
    -   Espera o comportamento do ODBC 3,0 para recursos que tiveram alterações comportamentais.  
  
-   **Aplicativo ODBC puro 3,0** Um aplicativo de 32 bits que:  
  
    -   É compilado com 3,0 cabeçalhos.  
  
    -   Chama qualquer função ODBC 3,0, possivelmente incluindo aquelas que foram preteridas.  
  
    -   Espera o comportamento do ODBC 3,0 para recursos que tiveram alterações comportamentais.  
  
-   **Aplicativo ODBC puro 3,5** Um aplicativo de 32 ou 64 bits que:  
  
    -   Pode usar tipos de dados Unicode.  
  
    -   Chama qualquer função ODBC 3,5, possivelmente incluindo aquelas que foram preteridas.  
  
    -   Espera o comportamento do ODBC 3,5 para recursos que tiveram alterações comportamentais.  
  
-   **Aplicativo ODBC puro 3,8 (ou posterior)** Um aplicativo de 32 bits ou 64 bits que:  
  
    -   Pode usar tipos de dados Unicode.  
  
    -   Chama qualquer função ODBC 3,8, possivelmente incluindo aquelas que foram preteridas.  
  
    -   Espera o comportamento do ODBC 3,8 para recursos que tiveram alterações comportamentais.  
  
-   **Aplicativo substituído** Um aplicativo de 32 ou 64 bits que:  
  
    -   Implementa um novo comportamento para a funcionalidade duplicada.  
  
    -   Usa quaisquer novos recursos em uma versão posterior do ODBC somente dentro do código condicional.  
  
    -   Tem um código condicional limitado para lidar com alterações comportamentais ou se registrou para ser uma versão anterior do aplicativo ODBC.
