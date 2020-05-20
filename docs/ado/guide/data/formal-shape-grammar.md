---
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
ms.openlocfilehash: ce65f6961502a5bfe43278e4a29a11c4210d4af8
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758252"
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
|\<> de comando de forma|FORMA [ \< Table-exp> [[as] \< alias>]] [ \< forma-ação>]|  
|\<tabela-exp>|{ \< provedor-> de texto de comandos} &#124;<br /><br /> ( \< Shape-> de comando) &#124;<br /><br /> \<> &#124; de nome entre aspas de tabela<br /><br /> \<> de nome entre aspas|  
|\<> de ação de forma|ANEXAR \< lista de campos com alias> &#124;<br /><br /> COMPUTAÇÃO com \< alias de lista de campos> [por \< campo-lista>]|  
|\<> de lista de campos com alias|\<com alias> de campo [, \< alias-Field... >]|  
|\<> de campo com alias|\<campo-exp> [[AS] \< alias>]|  
|\<campo-exp>|( \<> relation-exp) &#124;<br /><br /> \<> &#124; calculada de exp<br /><br /> \<> &#124; agregados de exp<br /><br /> \<> New-exp|  
|<relation_exp>|\<tabela-exp> [[AS] \< alias>]<br /><br /> Relacionar \< relação-condicional-list>|  
|\<relaciona-condicional-List>|\<relation-condicional> [, \< relation-condicional>...]|  
|\<> relation-condicional|\<nome de campo> como \< Child-ref>|  
|\<> de referência filho|\<nome do campo> &#124;<br /><br /> PARÂMETRO \< param-ref>|  
|\<> param-ref|\<número>|  
|\<> de lista de campos|\<Field-Name> [, \< Field-name>]|  
|\<> agregados de exp|SUM ( \< Qualified-Field-name>) &#124;<br /><br /> AVG ( \< Qualified-Field-name>) &#124;<br /><br /> MIN ( \< Qualified-Field-name>) &#124;<br /><br /> MAX ( \< Qualified-Field-name>) &#124;<br /><br /> COUNT ( \< qualificado-alias> &#124; \< Qualified-Name>) &#124;<br /><br /> DESVPAD ( \< Qualified-Field-name>) &#124;<br /><br /> QUALQUER ( \< Qualified-Field-name>)|  
|\<> calculada de exp|CALC ( \< expressão>)|  
|\<> de nome de campo qualificado|\<> de alias. [ \< alias>...] \< nome do campo>|  
|\<> de alias|\<> de nome entre aspas|  
|\<nome do campo>|\<aspas-nome> [[AS] \< alias>]|  
|\<> de nome entre aspas|" \< string>" &#124;<br /><br /> ' \< string> ' &#124;<br /><br /> [ \< string>] &#124;<br /><br /> \<nome>|  
|\<> de nome qualificado|alias [. alias...]|  
|\<nome>|Alfa [Alpha &#124; digit &#124; _ &#124; # &#124;: &#124;...]|  
|\<número>|dígito [dígito...]|  
|\<> New-exp|NOVO \< campo-tipo> [( \< número> [, \< número>])]|  
|\<> de tipo de campo|Um tipo de dados OLE DB ou ADO.|  
|\<Cadeia de caracteres>|Unicode-Char [Unicode-Char...]|  
|\<> de expressão|Uma Visual Basic for Applications expressão cujos operandos são outras colunas não CALC na mesma linha.|  
  
## <a name="see-also"></a>Consulte Também  
 [Acessando linhas em um conjunto de registros hierárquico](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [Visão geral do data Shaping](../../../ado/guide/data/data-shaping-overview.md)   
 [Provedores necessários para o Shaping de dados](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Cláusula de ANEXAção de forma](../../../ado/guide/data/shape-append-clause.md)   
 [Comandos de forma em geral](../../../ado/guide/data/shape-commands-in-general.md)   
 [Cláusula COMPUTE de forma](../../../ado/guide/data/shape-compute-clause.md)   
 [Funções do Visual Basic for Applications](../../../ado/guide/data/visual-basic-for-applications-functions.md)
