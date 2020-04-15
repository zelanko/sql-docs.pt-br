---
title: Tipos de Aplicações | Microsoft Docs
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
ms.openlocfilehash: f14326c9cec1eb89e431154c91b680e4688fcdfa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305527"
---
# <a name="types-of-applications"></a>Tipos de aplicativos
As aplicações ODBC podem ser classificadas da seguinte forma:  
  
-   **ODBC 2 puro.**  
     ** _x_ Aplicativo** Um aplicativo de 32 bits que:  
  
    -   Chama apenas ODBC 2. *x* funções (incluindo a função ODBC 1.0 **SQLSetParam**). Estes incluem ODBC 1. *x* aplicativos que foram portados para 32 bits.  
  
    -   Espera ODBC 2. *x* comportamento para características que tiveram mudanças comportamentais. (Consulte [Mudanças comportamentais](../../../odbc/reference/develop-app/behavioral-changes.md) para obter mais informações.)  
  
    -   Não foi recompilado com cabeçalhos ODBC 3.5.  
  
-   **ODBC 2 puro.**  
     **_x_ Aplicativo recompilado** Um ODBC puro 2. *x* aplicativo que foi recompilado usando os arquivos de cabeçalho ODBC 3.5, definindo ODBCVER=0x0250.  
  
-   **ODBC 2 puro.**  
     **_x_ Aplicação Unicode** Um ODBC puro 2. *x* aplicativo recompilado que é compatível com Unicode e usa o SQL_WCHAR tipo de dados.  
  
-   **Pure Open Group e ISO**-**compatível com o Aplicativo ODBC** Um aplicativo de 32 bits que:  
  
    -   Funções de chamadas definidas nos padrões Open Group ou ISO CLI. (Essas funções podem incluir funções 3.0 depreciadas.)  
  
    -   Não usa os tipos de dados Unicode.  
  
    -   Espera-se o comportamento do ODBC 3.0 para características que tiveram alterações comportamentais.  
  
-   **Aplicação ODBC 3.0 pura** Um aplicativo de 32 bits que:  
  
    -   É compilado com cabeçalhos 3.0.  
  
    -   Chama qualquer função ODBC 3.0, possivelmente incluindo aquelas que são preteridas.  
  
    -   Espera-se o comportamento do ODBC 3.0 para características que tiveram alterações comportamentais.  
  
-   **Aplicação ODBC 3.5 pura** Um aplicativo de 32 ou 64 bits que:  
  
    -   Pode usar tipos de dados Unicode.  
  
    -   Chama qualquer função ODBC 3.5, possivelmente incluindo aquelas que são preteridas.  
  
    -   Espera-se o comportamento do ODBC 3.5 para características que tiveram alterações comportamentais.  
  
-   **Aplicação ODBC pura 3.8 (ou posterior)** Um aplicativo de 32 bits ou 64 bits que:  
  
    -   Pode usar tipos de dados Unicode.  
  
    -   Chama qualquer função ODBC 3.8, possivelmente incluindo aquelas que são preteridas.  
  
    -   Espera-se o comportamento do ODBC 3.8 para características que tiveram alterações comportamentais.  
  
-   **Aplicativo substituído** Um aplicativo de 32 ou 64 bits que:  
  
    -   Implementa um novo comportamento para funcionalidade duplicada.  
  
    -   Usa quaisquer novos recursos em uma versão posterior do ODBC apenas dentro de código condicional.  
  
    -   Tem código condicional limitado para lidar com mudanças comportamentais ou registrou-se como uma versão anterior do aplicativo ODBC.
