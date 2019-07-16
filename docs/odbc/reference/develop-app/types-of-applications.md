---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 70263b98f6b0e933f8b14fbfa74428c77317f462
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68087800"
---
# <a name="types-of-applications"></a>Tipos de aplicativos
Aplicativos ODBC podem ser classificados da seguinte maneira:  
  
-   **Puro ODBC 2.**  
     **_x_ aplicativo** aplicativo de 32 bits que:  
  
    -   Chamadas ODBC 2. *x* funções (incluindo a função ODBC 1.0 **SQLSetParam**). Eles incluem 1 do ODBC. *x* aplicativos que foram adaptados para 32 bits.  
  
    -   Espera que o ODBC 2. *x* comportamento para recursos que tiveram alterações de comportamento. (Consulte [alterações de comportamento](../../../odbc/reference/develop-app/behavioral-changes.md) para obter mais informações.)  
  
    -   Não foi recompilado com cabeçalhos de ODBC 3.5.  
  
-   **Puro ODBC 2.**  
     **_x_ aplicativo recompilado** um puro do ODBC 2. *x* aplicativo foi recompilado usando os arquivos de cabeçalho ODBC 3.5, definindo ODBCVER = 0x0250.  
  
-   **Puro ODBC 2.**  
     **_x_ aplicativo Unicode** um puro do ODBC 2. *x* recompilado aplicativo que é compatível com Unicode e usa o tipo de dados SQL_WCHAR.  
  
-   **Grupo aberto pura e ISO**-**compatível com aplicativos de ODBC** aplicativo de 32 bits que:  
  
    -   Chama funções definidas nos padrões do Open Group ou a CLI do ISO. (Essas funções podem incluir funções preteridas de 3.0).  
  
    -   Não usa os tipos de dados Unicode.  
  
    -   Espera que o comportamento de ODBC 3.0 para recursos que tiveram alterações de comportamento.  
  
-   **Aplicativo de 3.0 puro do ODBC** aplicativo de 32 bits que:  
  
    -   É compilado com 3.0 cabeçalhos.  
  
    -   Chamar qualquer função ODBC 3.0, possivelmente incluindo aqueles que foram preteridos.  
  
    -   Espera que o comportamento de ODBC 3.0 para recursos que tiveram alterações de comportamento.  
  
-   **Aplicativo de 3.5 puro do ODBC** de 32 ou 64 bits de aplicativo que:  
  
    -   Pode usar tipos de dados Unicode.  
  
    -   Chamar qualquer função ODBC 3.5, possivelmente incluindo aqueles que foram preteridos.  
  
    -   Espera que o comportamento de ODBC 3.5 para recursos que tiveram alterações de comportamento.  
  
-   **Aplicativo puro de 3,8 (ou posterior) do ODBC** aplicativo de 32 bits ou 64 bits que:  
  
    -   Pode usar tipos de dados Unicode.  
  
    -   Chamar qualquer função ODBC 3.8, possivelmente incluindo aqueles que foram preteridos.  
  
    -   Espera que o comportamento do ODBC 3.8 para recursos que tiveram alterações de comportamento.  
  
-   **Substituído aplicativo** de 32 ou 64 bits de aplicativo que:  
  
    -   Novo comportamento para funções duplicadas implementa.  
  
    -   Usa os novos recursos em uma versão posterior do ODBC somente dentro do código condicional.  
  
    -   Limitou o código condicional para lidar com alterações de comportamento ou se registrou para ser uma versão anterior do aplicativo de ODBC.
