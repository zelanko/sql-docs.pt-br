---
title: Procedimento Chamada Seqüência de Fuga | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1194efe6a21c456a722ccd4352661c998f0316d9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298216"
---
# <a name="procedure-call-escape-sequence"></a>Sequência de escape da chamada de procedimento
O DBC usa seqüências de fuga para chamadas de procedimento. A sintaxe desta seqüência de fuga é a seguinte:  
  
 **{**[?=] nome *de procedimento de***chamada** [**[**[*parâmetro*][[,[parâmetro ]]...*parameter* **)**]**}**  
  
 Na notação da BNF, a sintaxe é a seguinte:  
  
 *ODBC-procedimento-fuga* ::=  
  
 &#124; *ODBC-esc-initiator* [?=] procedimento de chamada *ODBC-esc-terminator*  
  
 *procedimento* ::= *nome do procedimento-nome* *&#124;* *(procedimento-parâmetro-lista)*  
  
 *identificador de procedimento* ::= *nome definido pelo usuário*  
  
 *nome do procedimento* ::= *identificador de procedimento*  
  
 &#124; *nome do proprietário*. *identificador de procedimento*  
  
 *&#124; identificador de procedimento* de *separador de catálogo de catálogo*  
  
 *&#124;-nome de catálogo -separador* *[nome do proprietário*]. *identificador de procedimento*  
  
 (A terceira sintaxe só é válida se a fonte de dados não suportar proprietários.)  
  
 *nome do proprietário* ::= *nome definido pelo usuário*  
  
 *nome do catálogo* ::= *nome definido pelo usuário*  
  
 *catálogo-separador* ::= {*implementação definida*}  
  
 (O separador de catálogo é devolvido através **do SQLGetInfo** com a opção de SQL_CATALOG_NAME_SEPARATOR informações.)  
  
 *procedimento-parâmetro-lista* ::= *procedimento-parâmetro*  
  
 &#124; *parâmetro de procedimento,* *lista de parâmetros-procedimento*  
  
 *procedimento-parâmetro* ::= *parâmetro dinâmico* &#124; *literal* &#124; de *cadeia vazia*  
  
 *corda vazia* ::=  
  
 *ODBC-esc-iniciador* ::= {  
  
 *ODBC-esc-terminator* ::= }  
  
 (Se um parâmetro de procedimento for uma seqüência de string vazia, o procedimento usará o valor padrão para esse parâmetro.)  
  
 Para determinar se a fonte de dados suporta procedimentos e o driver suporta a sintaxe de invocação do procedimento ODBC, um aplicativo pode ligar para **o SQLGetInfo** com o tipo de informação SQL_PROCEDURES.
