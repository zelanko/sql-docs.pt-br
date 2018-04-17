---
title: Tipos de aplicativos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- upgrading applications [ODBC], application types
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
- application upgrades [ODBC], application types
- application compatibility issues [ODBC]
ms.assetid: d346a64e-a32c-4153-a40f-5b53c2f57ef2
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e265ed5868e8c7d1b798aa75d343742547499aa1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="types-of-applications"></a>Tipos de aplicativos
Aplicativos ODBC podem ser classificados da seguinte maneira:  
  
-   **Puro ODBC 2.**  
     ***x* aplicativo** aplicativo A 32 bits que:  
  
    -   Chama o ODBC 2. *x* funções (incluindo a função ODBC 1.0 **SQLSetParam**). Esses incluem 1 do ODBC. *x* aplicativos que foram adaptados para 32 bits.  
  
    -   Espera ODBC 2. *x* comportamento para recursos que tiveram alterações de comportamento. (Consulte [alterações de comportamento](../../../odbc/reference/develop-app/behavioral-changes.md) para obter mais informações.)  
  
    -   Não foi recompilado com cabeçalhos de ODBC 3.5.  
  
-   **Puro ODBC 2.**  
     ***x* aplicativo recompilado** um puro ODBC 2. *x* aplicativo foi recompilado usando os arquivos de cabeçalho ODBC 3.5, definindo ODBCVER = 0x0250.  
  
-   **Puro ODBC 2.**  
     ***x* aplicativo Unicode** um puro ODBC 2. *x* recompilado aplicativo que é compatível com Unicode e usa o tipo de dados SQL_WCHAR.  
  
-   **Puro Open Group e ISO**–**aplicativos ODBC compatíveis com** aplicativo A 32 bits que:  
  
    -   Chama funções definidas nos padrões ISO CLI ou de grupo aberto. (Essas funções podem incluir 3.0 funções preteridas.)  
  
    -   Não use os tipos de dados Unicode.  
  
    -   Comportamento de ODBC 3.0 para recursos que tiveram alterações de comportamento de espera.  
  
-   **Aplicativo de 3.0 puro ODBC** aplicativo A 32 bits que:  
  
    -   É compilado com 3.0 cabeçalhos.  
  
    -   Chamar qualquer função ODBC 3.0, possivelmente incluindo aqueles que foram preteridos.  
  
    -   Comportamento de ODBC 3.0 para recursos que tiveram alterações de comportamento de espera.  
  
-   **Aplicativo de 3.5 ODBC puro** A 32 ou 64 bits que:  
  
    -   Pode usar tipos de dados Unicode.  
  
    -   Chamar qualquer função ODBC 3.5, possivelmente incluindo aqueles que foram preteridos.  
  
    -   Comportamento de ODBC 3.5 para recursos que tiveram alterações de comportamento de espera.  
  
-   **Puro aplicativo em ODBC 3.8 (ou posterior)** aplicativo A 32 bits ou 64 bits que:  
  
    -   Pode usar tipos de dados Unicode.  
  
    -   Chamar qualquer função ODBC 3.8, possivelmente incluindo aqueles que foram preteridos.  
  
    -   Comportamento do ODBC 3.8 para recursos que tiveram alterações de comportamento de espera.  
  
-   **Substituído aplicativo** A 32 ou 64 bits que:  
  
    -   Novo comportamento para funções duplicadas implementa.  
  
    -   Usa os novos recursos em uma versão posterior do ODBC somente dentro do código condicional.  
  
    -   Limitou condicional código para tratar alterações de comportamento ou foi registrado para ser uma versão anterior do aplicativo de ODBC.
