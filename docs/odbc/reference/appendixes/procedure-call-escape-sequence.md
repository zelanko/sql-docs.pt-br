---
title: Sequência de Escape da chamada de procedimento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], procedure call
- procedure call escape sequence [ODBC]
- ODBC escape sequences [ODBC], procedure call
ms.assetid: 269fbab0-e5f2-4a98-86c0-2d7b647acaae
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 914bd4759552680a57c345dc3a7c3bc1bcc103a6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188501"
---
# <a name="procedure-call-escape-sequence"></a>Sequência de escape da chamada de procedimento
ODBC usa sequências de escape para chamadas de procedimento. A sintaxe dessa sequência de escape é da seguinte maneira:  
  
 **{** [?=]**call** *procedure-name*[ **(** [*parameter*][,[*parameter*]]... **)** ] **}**  
  
 Na notação BNF, a sintaxe é:  
  
 *Escape de procedimento de ODBC* :: =  
  
 &#124;*Esc-ODBC-iniciador* [? =] chamar *procedimento terminador de esc ODBC*  
  
 *procedure* ::= *procedure-name* &#124; *procedure-name* (*procedure-parameter-list*)  
  
 *procedure-identifier* ::= *user-defined-name*  
  
 *procedure-name* ::= *procedure-identifier*  
  
 &#124; *owner-name*.*procedure-identifier*  
  
 &#124;*separador de catálogo do nome do catálogo* *identificador de procedimento*  
  
 &#124;*separador de catálogo do nome do catálogo* [*nome do proprietário*]. *Identificador de procedimento*  
  
 (A sintaxe a terceira é válida somente se a fonte de dados não der suporte a proprietários.)  
  
 *owner-name* ::= *user-defined-name*  
  
 *catalog-name* ::= *user-defined-name*  
  
 *catalog-separator* ::= {*implementation-defined*}  
  
 (O separador de catálogo é retornado por **SQLGetInfo** com a opção de informações SQL_CATALOG_NAME_SEPARATOR.)  
  
 *procedure-parameter-list* ::= *procedure-parameter*  
  
 &#124; *procedure-parameter*, *procedure-parameter-list*  
  
 *procedure-parameter* ::= *dynamic-parameter* &#124; *literal* &#124; *empty-string*  
  
 *empty-string* ::=  
  
 *Iniciador do ODBC-esc* :: = {  
  
 *Terminador de esc ODBC* :: =}  
  
 (Se um parâmetro de procedimento é uma cadeia de caracteres vazia, o procedimento usa o valor padrão para esse parâmetro.)  
  
 Para determinar se a fonte de dados oferece suporte aos procedimentos e o driver dá suporte a sintaxe de invocação de procedimento ODBC, um aplicativo pode chamar **SQLGetInfo** com o tipo de informação SQL_PROCEDURES.
