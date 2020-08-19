---
description: Sequência de escape da chamada de procedimento
title: Sequência de escape de chamada de procedimento | Microsoft Docs
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
ms.openlocfilehash: ba88f3d78edeaa1ce4f4884977656cd8a4a16062
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483219"
---
# <a name="procedure-call-escape-sequence"></a>Sequência de escape da chamada de procedimento
O ODBC usa sequências de escape para chamadas de procedimento. A sintaxe dessa sequência de escape é a seguinte:  
  
 **{**[? =]**chamar** *procedimento-nome*[**(**[*parâmetro*] [, [*parâmetro*]]... **)**]**}**  
  
 Na notação BNF, a sintaxe é a seguinte:  
  
 *ODBC-Procedure-escape* :: =  
  
 &#124; *ODBC-ESC-Initiator* [? =] chamar o *procedimento ODBC-ESC-terminador*  
  
 *procedimento* :: = *procedure-name* &#124; nome *-* do-procedimento (*procedimento-parâmetro-List*)  
  
 *procedimento-identificador* :: = *nome definido pelo usuário*  
  
 *procedimento-nome* :: = *identificador de procedimento*  
  
 *Nome do proprietário*do &#124;. *identificador de procedimento*  
  
 Catálogo de nome de catálogo do &#124;-o *identificador do procedimento* do *separador*  
  
 *Catálogo de nome de catálogo &#124;-separador* [*nome-do-proprietário*]. *identificador de procedimento*  
  
 (A terceira sintaxe será válida somente se a fonte de dados não oferecer suporte a proprietários.)  
  
 *nome-do-proprietário* :: = *nome definido pelo usuário*  
  
 *Catalog-Name* :: = *nome definido pelo usuário*  
  
 *Catálogo-separador* :: = {*definição de implementação*}  
  
 (O separador de catálogo é retornado por meio de **SQLGetInfo** com a opção de informações SQL_CATALOG_NAME_SEPARATOR.)  
  
 *Procedure-parâmetro-List* :: = *procedimento-parâmetro*  
  
 Procedimento de &#124; *-parâmetro*, *procedimento-lista de parâmetros*  
  
 *Procedure-parâmetro* :: = *dynamic-parameter* &#124; *literal* &#124; *cadeia de caracteres vazia*  
  
 *Empty-cadeia de caracteres* :: =  
  
 *ODBC-ESC-Initiator* :: = {  
  
 *ODBC-ESC-terminador* :: =}  
  
 (Se um parâmetro de procedimento for uma cadeia de caracteres vazia, o procedimento usará o valor padrão para esse parâmetro.)  
  
 Para determinar se a fonte de dados dá suporte a procedimentos e o driver dá suporte à sintaxe de invocação de procedimento ODBC, um aplicativo pode chamar **SQLGetInfo** com o tipo de informação SQL_PROCEDURES.
