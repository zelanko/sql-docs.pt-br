---
title: "Elementos usados em instruções SQL | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], elements supported
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: 85777525-1555-4731-8309-63a464c6b43a
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f619ebbbc3bb7c0ebbc90025a65c7f0530e3e4e3
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="elements-used-in-sql-statements"></a>Elementos usados em instruções SQL
Os seguintes elementos são usados nas instruções SQL listadas anteriormente.  
  
## <a name="element"></a>Elemento  
 *Identificador da tabela de base de* :: = *nome definido pelo usuário*  
  
 *nome da tabela base* :: = *identificador de tabela de base*  
  
 *fator de booliano* :: = [não] *booliano primário*  
  
 *booliano primário* :: = comparação*-predicado* &#124; ( *critério de pesquisa* )  
  
 *termo Boolean* :: = *booliano fator* [AND *termo boolean*]  
  
 *literal de cadeia de caracteres* :: = ' {*caracteres*}... ' (*caracteres* é qualquer caractere no conjunto de caracteres da fonte de dados/driver. Para incluir um caractere literal de aspas simples (') em um literal de caractere-cadeia de caracteres, use dois caracteres de aspas literal [' '].)  
  
 *Identificador da coluna* :: = *nome definido pelo usuário*  
  
 *nome da coluna* :: = [*nome de tabela*.] *identificador de coluna*  
  
 *operador de comparação* :: = < &#124; > &#124; \<= &#124; > = &#124; = &#124; <>  
  
 *predicado de comparação* :: = *expressão* expressão de operador de comparação  
  
 *tipo de dados* :: = *tipo de cadeia de caracteres* (*tipo de cadeia de caracteres* é qualquer tipo de dados para o qual a coluna "" DATA_TYPE"" no conjunto de resultados retornado por SQLGetTypeInfo ou SQL_CHAR ou SQL_VARCHAR.)  
  
 *Dígito* :: = 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9  
  
 *parâmetro dinâmico* :: =?  
  
 *expressão* :: = termo &#124; expressão {+ &#124; –} termo  
  
 *fator de* :: = [*+*&#124; *–*]*primário*  
  
 *Inserir valor* :: =  
  
 *parâmetro dinâmico*  
  
 &#124; *literal*  
  
 &#124; NULL  
  
 &#124; USUÁRIO  
  
 *letra* :: = *case letras minúsculas &#124; superior de caso de letra*  
  
 *literal* :: = *literal de cadeia de caracteres*  
  
 *letras minúsculas case* :: = um &#124; b &#124; c &#124; d &#124; e &#124; f &#124; g &#124; h &#124; i &#124; j &#124; k &#124; l &#124; m &#124; n &#124; o &#124; p &#124; p &#124; r &#124; s &#124; t &#124; u &#124; v &#124; w &#124; x &#124; s &#124; z  
  
 *ordem por cláusula* :: = ORDER BY *especificação de classificação* [, *especificação de classificação*]...  
  
 *primário* :: = *nome de coluna*  
  
 &#124; *parâmetro dinâmico*  
  
 &#124; *literal*  
  
 &#124; ( *expressão* )  
  
 *critério de pesquisa* :: = *termo boolean* [ou *critério de pesquisa*]  
  
 *lista de Select* :: = \* &#124; *selecione sublista* [, *selecione sublista*]...  (*lista de select* não pode conter parâmetros.)  
  
 *Selecione sublista* :: = *expressão*  
  
 *especificação de classificação* :: = {*inteiro não assinado &#124; o nome da coluna*} [*ASC &#124; DESC*]  
  
 *Identificador de tabela* :: = *nome definido pelo usuário*  
  
 *nome da tabela* :: = *identificador de tabela*  
  
 *referência de tabela* :: = *nome de tabela*  
  
 *lista de referências de tabela* :: = *referência de tabela* [,*referência de tabela*]...  
  
 *termo* :: = *fator* &#124; *termo* {\*&#124; */* } *fator*  
  
 *inteiro não assinado* :: = {*dígitos*}  
  
 *Letra de caso superior* :: = *A &#124; B &#124; C &#124; D &#124; E &#124; F &#124; G &#124; H &#124; &#124; J &#124; K &#124; L &#124; M &#124; N &#124; S &#124; P &#124; P &#124; R &#124; S &#124; T &#124; U &#124; V &#124; W &#124; X &#124; S &#124; Z*  
  
 *nome definido pelo usuário* :: = *letra*[*dígitos* &#124; *letra* &#124; *_*]...
