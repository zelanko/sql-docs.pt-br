---
title: Elementos usados em instruções SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], elements supported
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: 85777525-1555-4731-8309-63a464c6b43a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e33beff29463172a26d53953dd5f563fe1f3f5c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63240959"
---
# <a name="elements-used-in-sql-statements"></a>Elementos usados em instruções SQL
Os seguintes elementos são usados nas instruções SQL listadas anteriormente.  
  
## <a name="element"></a>Elemento  
 *base-table-identifier* ::= *user-defined-name*  
  
 *base-table-name* ::= *base-table-identifier*  
  
 *Fator booliano* :: = [NOT] *booliano primário*  
  
 *boolean-primary* ::= comparison *-predicate* &#124; ( *search-condition* )  
  
 *termo booleano* :: = *fator booliano* [AND *booliano termo*]  
  
 *character-string-literal* ::= ''{*character*}...'' (*caractere* é qualquer caractere no conjunto de caracteres da fonte de dados/driver. Para incluir um caractere literal de aspas (") em um literal de caractere-cadeia de caracteres, use dois caracteres de aspas literais [' '].)  
  
 *column-identifier* ::= *user-defined-name*  
  
 *column-name* ::= [*table-name*.]*column-identifier*  
  
 *comparison-operator* ::= < &#124; > &#124; \<= &#124; >= &#124; = &#124; <>  
  
 *comparison-predicate* ::= *expression* comparison-operator expression  
  
 *tipo de dados* :: = *tipo de cadeia de caracteres de caractere* (*tipo de cadeia de caracteres de caractere* é qualquer tipo de dados para os quais a coluna "" DATA_TYPE"" no conjunto de resultados retornado por SQLGetTypeInfo é qualquer SQL_CHAR ou SQL_VARCHAR.)  
  
 *digit* ::= 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9  
  
 *dynamic-parameter* ::= ?  
  
 *expressão* :: = termo &#124; expressão {+&#124;-} termo  
  
 *factor* ::= [*+*&#124;*-*]*primary*  
  
 *insert-value* ::=  
  
 *dynamic-parameter*  
  
 &#124; *literal*  
  
 &#124; NULL  
  
 &#124; USER  
  
 *letter* ::= *lower-case-letter &#124; upper-case-letter*  
  
 *literal* ::= *character-string-literal*  
  
 *letras minúsculas maiusculas* :: = um &#124; b &#124; c &#124; 1!d &#124; e &#124; f &#124; g &#124; h &#124; , &#124; j &#124; k &#124; l &#124; m &#124; n &#124; o &#124; p &#124; q &#124; r &#124; s &#124; t &#124; u &#124; v &#124; w &#124; x &#124; y &#124; z  
  
 *ordem por cláusula* :: = ORDER BY *especificação de classificação* [, *especificação de classificação*]...  
  
 *primary* ::= *column-name*  
  
 &#124; *dynamic-parameter*  
  
 &#124; *literal*  
  
 &#124; ( *expression* )  
  
 *critério de pesquisa* :: = *booliano termo* [ou *critério de pesquisa*]  
  
 *lista de Select* :: = \* &#124; *selecione sublista* [, *selecione sublista*]...  (*lista seleção* não pode conter parâmetros.)  
  
 *select-sublist* ::= *expression*  
  
 *sort-specification* ::= {*unsigned-integer &#124; column-name*} [*ASC &#124; DESC*]  
  
 *table-identifier* ::= *user-defined-name*  
  
 *table-name* ::= *table-identifier*  
  
 *table-reference* ::= *table-name*  
  
 *table-reference-list* ::= *table-reference* [,*table-reference*]...  
  
 *term* ::= *factor* &#124; *term* {\*&#124;*/*} *factor*  
  
 *unsigned-integer* ::= {*digit*}  
  
 *superior de caso de letra* :: = *A &#124; B &#124; C &#124; 1!d &#124; E &#124; F &#124; G &#124; H &#124; , &#124; J &#124; K &#124; L &#124; M &#124; N &#124; s &#124; P &#124;Q &#124; R &#124; S &#124; T &#124; U &#124; V &#124; W &#124; X &#124; Y &#124; Z*  
  
 *user-defined-name* ::= *letter*[*digit* &#124; *letter* &#124; *_*]...
