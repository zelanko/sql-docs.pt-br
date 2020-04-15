---
title: Elementos usados em declarações SQL | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 49a1cd54957426d4d14d84d43df670c8c3d96189
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307017"
---
# <a name="elements-used-in-sql-statements"></a>Elementos usados em instruções SQL
Os seguintes elementos são usados nas instruções SQL listadas anteriormente.  
  
## <a name="element"></a>Elemento  
 *identificador de tabela base* ::= *nome definido pelo usuário*  
  
 *nome da tabela base* :== *identificador de tabela base*  
  
 *fator booleano* ::= [NÃO] *boolean-primary*  
  
 *boolean-primário* ::= comparação *-predicado* &#124; *(condição de pesquisa)*  
  
 *boolean-term* ::= *boolean-factor* [AND *boolean-term*]  
  
 *caractere-string-literal* ::= ''{*caractere*}...'' *(caractere* é qualquer personagem no conjunto de caracteres do driver/fonte de dados. Para incluir um único caractere de citação literal ('') em um caractere-string-literal, use dois caracteres de citação literal ['''].)  
  
 *identificador de coluna* ::= *nome definido pelo usuário*  
  
 *nome da coluna* ::= [*nome da tabela*.] *coluna identificador*  
  
 *operador de comparação* ::= < &#124; > &#124; \<= &#124; >= &#124; = &#124; <>  
  
 *predicado de comparação* ::= expressão de comparação de *expressão-operador*  
  
 *tipo de dados* ::= *caractere-string-type* *(caractere-string-type* é qualquer tipo de dados para o qual a coluna "DATA_TYPE"" no conjunto de resultados retornado pelo SQLGetTypeInfo é SQL_CHAR ou SQL_VARCHAR.)  
  
 *dígito* ::= 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9  
  
 *parâmetro dinâmico* ::= ?  
  
 *expressão* ::= termo &#124; expressão {+&#124;-}  
  
 *fator* ::=*+* *-*[&#124;]*primário*  
  
 *valor de inserção* ::=  
  
 *parâmetro dinâmico*  
  
 &#124; *literal*  
  
 &#124; NULO  
  
 &#124; USUÁRIO  
  
 *letra* ::= letra minúscula &#124; letra *maiúscula*  
  
 *literal* ::= *caractere-string-literal*  
  
 *letras-maiúsculas* ::= um &#124; b &#124; c &#124; d &#124; e &#124; f &#124; g g &#124; h &#124; &#124; j &#124; &#124; &#124; l &#124; m &#124; n &#124; o &#124; p &#124; q &#124; r &#124; s &#124; t &#124; u &#124; v &#124; w &#124; x &#124; y &#124; z  
  
 *ordem por cláusula* ::= ORDEM POR *especificação de classificação* [, *especificação de classificação*]...  
  
 *principal* ::= *nome da coluna*  
  
 *&#124; parâmetro dinâmico*  
  
 &#124; *literal*  
  
 &#124; *(expressão)*  
  
 *condição de pesquisa* ::= *termo booleano* [condição *de pesquisa*]  
  
 *lista de seleção* ::= \* &#124; *sublista select* [, *select-sublist*]...  (lista*selecionada* não pode conter parâmetros.)  
  
 *seleção-sublista* ::= *expressão*  
  
 *especificação do tipo* ::= {*não assinado-inteiro-inteiro &#124; nome de coluna*} [*ASC &#124; DESC*]  
  
 *identificador de tabela* ::= *nome definido pelo usuário*  
  
 *nome da tabela* ::= *identificador de tabela*  
  
 *referência de tabela* ::= *nome da tabela*  
  
 *tabela-referência-lista* ::= *referência da tabela* [,*tabela-referência*]...  
  
 *termo* ::= *fator* \* &#124; */* *termo* {&#124;} *fator*  
  
 *inteiro sem assinatura* ::= {*dígito*}  
  
 *letras maiúsculas* ::= *Um &#124; B &#124; C &#124; D &#124; E &#124; F &#124; G &#124; H &#124; Eu &#124; J &#124; K &#124; L &#124; M &#124; N &#124; O &#124; P &#124; &#124; &#124; R &#124; S &#124; T &#124; U &#124; &#124; W &#124; X &#124; Y &#124; Y &#124; Z*  
  
 *nome definido pelo usuário* ::= *letra*[*dígito* &#124; *letra* &#124; *_*]...
