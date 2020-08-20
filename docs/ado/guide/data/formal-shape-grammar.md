---
description: Gramática de forma formal
title: Gramática forma formal | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO], shape grammar
- data shaping [ADO], shape grammar
ms.assetid: ea691475-0f03-4abe-a785-b77e77712d1d
author: rothja
ms.author: jroth
ms.openlocfilehash: 6a8d92abc3a1b0d7e6d39ac4149c186c5a2fc2eb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453368"
---
# <a name="formal-shape-grammar"></a>Gramática de forma formal
Essa é a gramática formal para a criação de qualquer comando de forma:  
  
-   Os termos gramaticais necessários são cadeias de caracteres de texto delimitadas por colchetes angulares ("<>").  
  
-   Os termos opcionais são delimitados por colchetes ("[]").  
  
-   As alternativas são indicadas por um virgule ("&#124;").  
  
-   As alternativas de repetição são indicadas por reticências ("...").  
  
-   *Alfa* indica uma cadeia de letras alfabéticas.  
  
-   *Dígito* indica uma cadeia de números.  
  
-   *Unicode-digit* indica uma cadeia de caracteres de dígitos Unicode.  
  
 Todos os outros termos são literais.  
  
|Termo|Definição|  
|----------|----------------|  
|\<shape-command>|SHAPE [ \<table-exp> [as] \<alias> ]] [ \<shape-action> ]|  
|\<table-exp>|{ \<provider-command-text> } &#124;<br /><br /> ( \<shape-command> ) &#124;<br /><br /> &#124; de tabela \<quoted-name><br /><br /> \<quoted-name>|  
|\<shape-action>|ACRESCENTAR \<aliased-field-list> &#124;<br /><br /> COMPUTAÇÃO \<aliased-field-list> [por \<field-list> ]|  
|\<aliased-field-list>|\<aliased-field> [, \<aliased-field...>]|  
|\<aliased-field>|\<field-exp> [[AS] \<alias> ]|  
|\<field-exp>|( \<relation-exp> ) &#124;<br /><br /> \<calculated-exp> &#124;<br /><br /> \<aggregate-exp> &#124;<br /><br /> \<new-exp>|  
|<relation_exp>|\<table-exp> [[AS] \<alias> ]<br /><br /> RELACIONADA \<relation-cond-list>|  
|\<relation-cond-list>|\<relation-cond> [, \<relation-cond>...]|  
|\<relation-cond>|\<field-name> Para \<child-ref>|  
|\<child-ref>|\<field-name> &#124;<br /><br /> METER \<param-ref>|  
|\<param-ref>|\<number>|  
|\<field-list>|\<field-name> [, \<field-name>]|  
|\<aggregate-exp>|SUM ( \<qualified-field-name> ) &#124;<br /><br /> Méd ( \<qualified-field-name> ) &#124;<br /><br /> MIN ( \<qualified-field-name> ) &#124;<br /><br /> MÁXIMO ( \<qualified-field-name> ) &#124;<br /><br /> CONTAGEM ( \<qualified-alias> &#124; \<qualified-name> ) &#124;<br /><br /> DESVPAD ( \<qualified-field-name> ) &#124;<br /><br /> ANY ( \<qualified-field-name> )|  
|\<calculated-exp>|CALC ( \<expression> )|  
|\<qualified-field-name>|\<alias>.[\<alias>...]\<field-name>|  
|\<alias>|\<quoted-name>|  
|\<field-name>|\<quoted-name> [[AS] \<alias> ]|  
|\<quoted-name>|" \<string> " &#124;<br /><br /> ' \<string> ' &#124;<br /><br /> [ \<string> ] &#124;<br /><br /> \<name>|  
|\<qualified-name>|alias [. alias...]|  
|\<name>|Alfa [Alpha &#124; digit &#124; _ &#124; # &#124;: &#124;...]|  
|\<number>|dígito [dígito...]|  
|\<new-exp>|NOVO \<field-type> [( \<number> [, \<number> ])]|  
|\<field-type>|Um tipo de dados OLE DB ou ADO.|  
|\<string>|Unicode-Char [Unicode-Char...]|  
|\<expression>|Uma Visual Basic for Applications expressão cujos operandos são outras colunas não CALC na mesma linha.|  
  
## <a name="see-also"></a>Consulte Também  
 [Acessando linhas em um conjunto de registros hierárquico](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [Visão geral do data Shaping](../../../ado/guide/data/data-shaping-overview.md)   
 [Provedores necessários para o Shaping de dados](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Cláusula de ANEXAção de forma](../../../ado/guide/data/shape-append-clause.md)   
 [Comandos de forma em geral](../../../ado/guide/data/shape-commands-in-general.md)   
 [Cláusula COMPUTE de forma](../../../ado/guide/data/shape-compute-clause.md)   
 [Funções do Visual Basic for Applications](../../../ado/guide/data/visual-basic-for-applications-functions.md)
