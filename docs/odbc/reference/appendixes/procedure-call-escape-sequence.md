---
title: Sequência de Escape de chamada de procedimento | Microsoft Docs
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
- escape sequences [ODBC], procedure call
- procedure call escape sequence [ODBC]
- ODBC escape sequences [ODBC], procedure call
ms.assetid: 269fbab0-e5f2-4a98-86c0-2d7b647acaae
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5cccd4828a7c7509a3876ac2b194ffccfc6a083d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="procedure-call-escape-sequence"></a>Sequência de Escape de chamada de procedimento
ODBC usa sequências de escape para chamadas de procedimento. A sintaxe dessa sequência de escape é da seguinte maneira:  
  
 **{**[? =]**chamar** *nome do procedimento*[**(**[*parâmetro*] [, [*parâmetro*]]... **)**]**}**  
  
 Na notação BNF, a sintaxe é:  
  
 *Escape de procedimento de ODBC* :: =  
  
 &#124;*ODBC de esc de iniciador* [? =] chamar *procedimento terminador de esc ODBC*  
  
 *procedimento* :: = *nome do procedimento* &#124; *nome do procedimento* (*lista de parâmetros de procedimento*)  
  
 *Identificador de procedimento* :: = *nome definido pelo usuário*  
  
 *nome do procedimento* :: = *identificador de procedimento*  
  
 &#124;*nome do proprietário*. *Identificador de procedimento*  
  
 &#124;*separador de catálogo de nome de catálogo* *identificador de procedimento*  
  
 &#124;*separador de catálogo de nome de catálogo* [*nome do proprietário*]. *Identificador de procedimento*  
  
 (A sintaxe de terceira é válida somente se a fonte de dados não oferece suporte a proprietários).  
  
 *nome do proprietário* :: = *nome definido pelo usuário*  
  
 *nome do catálogo* :: = *nome definido pelo usuário*  
  
 *separador de catálogo* :: = {*definido pela implementação*}  
  
 (O separador de catálogo é retornado por meio de **SQLGetInfo** com a opção de informações SQL_CATALOG_NAME_SEPARATOR.)  
  
 *lista de parâmetros de procedimento* :: = *parâmetro de procedimento*  
  
 &#124;*parâmetro de procedimento*, *lista de parâmetros de procedimento*  
  
 *parâmetro de procedimento* :: = *parâmetro dinâmico* &#124; *literal* &#124; *cadeia de caracteres vazia*  
  
 *cadeia de caracteres vazia* :: =  
  
 *Iniciador de esc ODBC* :: = {  
  
 *Terminador de esc ODBC* :: =}  
  
 (Se um parâmetro de procedimento é uma cadeia de caracteres vazia, o procedimento usa o valor padrão para esse parâmetro.)  
  
 Para determinar se a fonte de dados oferece suporte a procedimentos e o driver oferece suporte à sintaxe de invocação de procedimento ODBC, um aplicativo pode chamar **SQLGetInfo** com o tipo de informação SQL_PROCEDURES.
