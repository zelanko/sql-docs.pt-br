---
title: "Gramática de forma formal | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shape commands [ADO], shape grammar
- data shaping [ADO], shape grammar
ms.assetid: ea691475-0f03-4abe-a785-b77e77712d1d
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ae47b751e9e62d84188927186f186c6c9d344ce0
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="formal-shape-grammar"></a>Gramática de forma formal
Esta é a gramática formal para a criação de qualquer comando de forma:  
  
-   Termos gramaticais necessários são cadeias de caracteres de texto delimitadas por colchetes angulares ("<>").  
  
-   Termos opcionais são delimitados por colchetes ("[]").  
  
-   Alternativas são indicadas por uma barra oblíqua ("&#124;").  
  
-   Alternativas de repetição são indicadas por um sinal de reticências ("...").  
  
-   *Alpha* indica uma cadeia de caracteres de letras em ordem alfabética.  
  
-   *Dígito* indica uma cadeia de números.  
  
-   *Dígitos Unicode* indica uma cadeia de caracteres de dígitos de unicode.  
  
 Todos os outros termos são literais.  
  
|Termo|Definição|  
|----------|----------------|  
|\<comando forma >|FORMA [\<exp tabela > [[como] \<alias >]] [\<forma de ação >]|  
|\<tabela exp >|{\<texto de comando do provedor >} &#124;<br /><br /> (\<comando forma >) &#124;<br /><br /> TABELA \<entre aspas-name > &#124;<br /><br /> \<nome entre aspas >|  
|\<forma de ação >|ACRESCENTAR \<lista de campos de um alias > &#124;<br /><br /> COMPUTAÇÃO \<lista de campos de um alias > [BY \<lista de campos >]|  
|\<lista de campos de um alias >|\<um alias de campo > [, \<campo um alias... >]|  
|\<campo de um alias >|\<campo exp > [[como] \<alias >]|  
|\<campo exp >|(\<relação exp >) &#124;<br /><br /> \<exp calculado > &#124;<br /><br /> \<agregação exp > &#124;<br /><br /> \<novo exp >|  
|< relation_exp >|\<exp tabela > [[como] \<alias >]<br /><br /> RELATE \<relação-condicional-list >|  
|\<relação de condicional de lista >|\<Relação condicional > [, \<relação condicional >...]|  
|\<Relação condicional >|\<nome do campo > TO \<filho ref >|  
|\<ref filho >|\<nome do campo > &#124;<br /><br /> PARÂMETRO \<ref param >|  
|\<ref param >|\<número >|  
|\<lista de campos >|\<nome do campo > [, \<campo-name >]|  
|\<agregação exp >|SUM (\<nome qualificado de campo >) &#124;<br /><br /> AVG (\<nome qualificado de campo >) &#124;<br /><br /> MIN (\<nome qualificado de campo >) &#124;<br /><br /> MAX (\<nome qualificado de campo >) &#124;<br /><br /> CONTAGEM (\<alias qualificado > &#124; \<nome qualificado >) &#124;<br /><br /> STDEV (\<nome qualificado de campo >) &#124;<br /><br /> QUALQUER (\<nome qualificado de campo >)|  
|\<exp calculado >|CÁLCULO (\<expressão >)|  
|\<nome qualificado de campo >|\<alias >. [\<alias >...] \<nome do campo >|  
|\<alias >|\<nome entre aspas >|  
|\<nome do campo >|\<entre aspas-name > [[como] \<alias >]|  
|\<nome entre aspas >|"\<cadeia de caracteres >" &#124;<br /><br /> '\<cadeia de caracteres >' &#124;<br /><br /> [\<cadeia de caracteres >] &#124;<br /><br /> \<nome >|  
|\<nome qualificado >|alias [.alias...]|  
|\<nome >|Alpha [alfa &#124; dígito &#124; _ &#124; # &#124;: &#124;...]|  
|\<número >|Dígito [dígito...]|  
|\<novo exp >|NOVO \<tipo de campo > [(\<número > [, \<número >])]|  
|\<tipo de campo >|Um tipo de dados OLE DB ou ADO.|  
|\<cadeia de caracteres >|caractere Unicode [caractere unicode....]|  
|\<expressão >|Um Visual Basic para a expressão de aplicativos cujos operandos são outras colunas não CALC na mesma linha.|  
  
## <a name="see-also"></a>Consulte também  
 [Acessar linhas em um conjunto de registros hierárquico](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [Visão geral de modelagem de dados](../../../ado/guide/data/data-shaping-overview.md)   
 [Provedores necessários para modelagem de dados](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Cláusula APPEND de forma](../../../ado/guide/data/shape-append-clause.md)   
 [Comandos de forma em geral](../../../ado/guide/data/shape-commands-in-general.md)   
 [Cláusula COMPUTE de forma](../../../ado/guide/data/shape-compute-clause.md)   
 [Funções do Visual Basic for Applications](../../../ado/guide/data/visual-basic-for-applications-functions.md)

