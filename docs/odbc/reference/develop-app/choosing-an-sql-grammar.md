---
title: Escolhendo uma gramática SQL | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6f7bf7e77f892f10de17402b59e732523d58fbc6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036554"
---
# <a name="choosing-an-sql-grammar"></a>Escolher uma gramática SQL
A primeira decisão a ser tomada ao construir instruções SQL é a gramática a ser usada. Além das gramáticas disponíveis de vários órgãos de padrões, como Open Group, ANSI e ISO, praticamente todos os fornecedores de DBMS definem sua própria gramática, cada um dos quais varia um pouco do padrão.  
  
 [Apêndice C: gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md), descreve a gramática SQL mínima para a qual todos os drivers ODBC devem dar suporte. Essa gramática é um subconjunto do nível de entrada do SQL-92. Os drivers podem dar suporte à gramática adicional para estar em conformidade com os níveis de transição intermediário, completo ou FIPS 127-2 definidos pelo SQL-92. Para obter mais informações, consulte [SQL mínimo de gramática](../../../odbc/reference/appendixes/sql-minimum-grammar.md) no Apêndice C: SQL GRAMMAR e sql-92.  
  
 O Apêndice C também define as *sequências de escape* que contêm a gramática padrão para recursos de linguagem comumente disponíveis, como junções externas, que não são cobertas pela gramática do SQL-92. Para obter mais informações, consulte [sequências de escape ODBC](../../../odbc/reference/appendixes/odbc-escape-sequences.md) no Apêndice C: gramática SQL e [sequências de escape](../../../odbc/reference/develop-app/escape-sequences.md), mais adiante nesta seção.  
  
 A gramática escolhida afeta a maneira como o driver processa a instrução. Os drivers devem modificar as sequências de escape SQL-92 e SQL definidas como ODBC para o SQL específico do DBMS. Como a maioria das gramáticas do SQL baseia-se em um ou mais dos vários padrões, a maioria dos drivers faz pouco ou nenhum trabalho para atender a esse requisito. Ele geralmente consiste apenas em procurar as sequências de escape definidas pelo ODBC e substituí-las por uma gramática específica do DBMS. Quando um driver encontra a gramática não reconhece, ele assume que a gramática é específica do DBMS e passa a instrução SQL sem modificação na fonte de dados para execução.  
  
 Portanto, há realmente duas opções de gramática a serem usadas: a gramática do SQL-92 (e as sequências de escape ODBC) e uma gramática específica do DBMS. Dos dois, apenas a gramática do SQL-92 é interoperável, de modo que todos os aplicativos interoperáveis devem usá-lo. Os aplicativos que não são interoperáveis podem usar a gramática do SQL-92 ou uma gramática específica do DBMS. As gramáticas específicas do DBMS têm duas vantagens: elas podem explorar quaisquer recursos não cobertos pelo SQL-92 e são marginalmente mais rápidas porque o driver não precisa modificá-los. O último recurso pode ser parcialmente imposto definindo o atributo SQL_ATTR_NOSCAN Statement, que impede o driver de Pesquisar e substituir sequências de escape.  
  
 Se a gramática do SQL-92 for usada, o aplicativo poderá descobrir como ele é modificado pelo driver chamando **SQLNativeSql**. Isso geralmente é útil ao depurar aplicativos. **SQLNativeSql** aceita uma instrução SQL e a retorna depois que o driver a modificou. Como essa função está no nível de conformidade da interface principal, há suporte para ele em todos os drivers.
