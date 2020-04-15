---
title: Escolhendo uma Gramática SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], SQL grammar
- SQL grammar [ODBC], selecting
ms.assetid: 4e0d189b-e407-47e0-92a9-f9982230dd0e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2ca9911d3c88f2f540ff1332d77a2e1ebc6a4942
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299156"
---
# <a name="choosing-an-sql-grammar"></a>Escolher uma gramática SQL
A primeira decisão a tomar ao construir declarações SQL é qual gramática usar. Além das gramáticas disponíveis nos diversos órgãos de padrões, como Open Group, ANSI e ISO, praticamente todos os fornecedores de DBMS definem sua própria gramática, cada uma das quais varia ligeiramente do padrão.  
  
 [Apêndice C: Gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md), descreve a gramática SQL mínima que todos os drivers ODBC devem suportar. Esta gramática é um subconjunto do nível de entrada do SQL-92. Os drivers podem suportar gramática adicional para se adequar aos níveis transitórios intermediários, completos ou FIPS 127-2 definidos pelo SQL-92. Para obter mais informações, consulte [Gramática Mínima SQL](../../../odbc/reference/appendixes/sql-minimum-grammar.md) no apêndice C: Gramática SQL e SQL-92.  
  
 O apêndice C também define *seqüências* de fuga contendo gramática padrão para características de linguagem comumente disponíveis, como as junções externas, que não são cobertas pela gramática SQL-92. Para obter mais informações, consulte [seqüências de fuga ODBC](../../../odbc/reference/appendixes/odbc-escape-sequences.md) no apêndice C: Gramática SQL e [Seqüências de Fuga](../../../odbc/reference/develop-app/escape-sequences.md), mais tarde nesta seção.  
  
 A gramática escolhida afeta a forma como o driver processa a declaração. Os drivers devem modificar o SQL-92 SQL e as seqüências de escape definidas pelo ODBC para o SQL específico do DBMS. Como a maioria das gramáticas SQL são baseadas em um ou mais dos vários padrões, a maioria dos motoristas faz pouco ou nenhum trabalho para atender a esse requisito. Muitas vezes consiste apenas em procurar as seqüências de fuga definidas pela ODBC e substituí-las por gramática específica do DBMS. Quando um driver encontra gramática que não reconhece, ele assume que a gramática é específica do DBMS e passa a instrução SQL sem modificação na fonte de dados para execução.  
  
 Portanto, há realmente duas opções de gramática para usar: a gramática SQL-92 (e as seqüências de fuga ODBC) e uma gramática específica do DBMS. Dos dois, apenas a gramática SQL-92 é interoperável, então todas as aplicações interoperáveis devem usá-la. Aplicações que não são interoperáveis podem usar a gramática SQL-92 ou uma gramática específica do DBMS. Gramáticas específicas do DBMS têm duas vantagens: elas podem explorar quaisquer recursos não cobertos pelo SQL-92, e são marginalmente mais rápidos porque o driver não precisa modificá-los. Este último recurso pode ser parcialmente aplicado definindo o atributo de declaração SQL_ATTR_NOSCAN, que impede o motorista de procurar e substituir seqüências de fuga.  
  
 Se a gramática SQL-92 for usada, o aplicativo poderá descobrir como ele é modificado pelo driver, **chamando-o de SQLNativeSql**. Isso é muitas vezes útil ao depurar aplicativos. **SQLNativeSql** aceita uma declaração SQL e a devolve depois que o driver a modificou. Como esta função está no nível de conformidade da interface Core, ela é suportada por todos os drivers.
