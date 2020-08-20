---
description: Elementos usados em instruções SQL
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5c24f5dd55530e38ea47ed9a2b846d549bb26d56
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456569"
---
# <a name="elements-used-in-sql-statements"></a>Elementos usados em instruções SQL
Os elementos a seguir são usados nas instruções SQL listadas anteriormente.  
  
## <a name="element"></a>Elemento  
 *identificação de tabela base-identificador* :: = *nome definido pelo usuário*  
  
 *base-tabela-nome* :: = *base-tabela-identificador*  
  
 *booliano de fator* :: = [not] *booliano-primário*  
  
 *booliano-primário* :: = &#124;*de predicado de* comparação ( *condição de pesquisa* )  
  
 *valor booliano* :: = *booliano-fator* [e *booliano-termo*]  
  
 *caractere-Cadeia de caracteres-literal* :: = ' ' {*Character*}... ' ' (*Character* é qualquer caractere no conjunto de caracteres da fonte de dados/driver. Para incluir um caractere de aspa literal único (' ') em um caractere-Cadeia de caracteres literal, use dois caracteres de aspas literais [' ' ' '].)  
  
 *coluna-identificador* :: = *nome definido pelo usuário*  
  
 *nome da coluna* :: = [*nome-da-tabela*.] *identificador de coluna*  
  
 *comparação-operador* :: = < &#124; > &#124; \<= &#124; > = &#124; = &#124; <>  
  
 *comparação-predicado* :: = expressão de comparação-operador de *expressão*  
  
 *Data-Type* :: = *caractere-Cadeia de caracteres-* tipo (*caractere-Cadeia de caracteres-tipo* é qualquer tipo de dados para o qual a coluna "" data_type "" no conjunto de resultados retornado por SQLGetTypeInfo é SQL_CHAR ou SQL_VARCHAR.)  
  
 *dígito* :: = 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9  
  
 *parâmetro dinâmico* :: =?  
  
 *expressão* :: = Term &#124; expressão {+&#124;-} termo  
  
 *fator* :: = [ *+*&#124;*-* ]*primário*  
  
 *Inserir valor* :: =  
  
 *parâmetro dinâmico*  
  
 &#124; *literal*  
  
 &#124; NULO  
  
 &#124; USUÁRIO  
  
 *letra* :: = *letra minúscula maiúscula &#124; letra* maiúscula  
  
 *literal* :: = *Character-String-literal*  
  
 *letra* minúscula:: = a &#124; b &#124; c &#124; d &#124; e &#124; f &#124; g &#124; h &#124; i &#124; j &#124; k &#124; l &#124; m &#124; n &#124; o &#124; p &#124; q &#124; r &#124; s &#124; t &#124; u &#124; v &#124; w &#124; x &#124; y &#124; z  
  
 *ordem por cláusula* :: = ordem por *especificação de classificação* [, *classificação-especificação*]...  
  
 *primário* :: = *nome da coluna*  
  
 &#124; *parâmetro dinâmico*  
  
 &#124; *literal*  
  
 &#124; ( *expressão* )  
  
 *Search-Condition* :: = *booliano-Term* [ou *Search-Condition*]  
  
 *Select-List* :: = \* &#124; *selecionar-sublista* [, *selecionar-sublista*]...  (*Select-List* não pode conter parâmetros.)  
  
 *selecionar-sublista* :: = *expressão*  
  
 *classificação-especificação* :: = {*não assinado-inteiro &#124; nome-da-coluna*} [*ASC &#124; desc*]  
  
 *identificador de tabela* :: = *nome definido pelo usuário*  
  
 *nome da tabela* :: = *identificador de tabela*  
  
 *tabela-referência* :: = *nome da tabela*  
  
 *tabela-referência-lista* :: = *tabela-* referência [,*tabela-referência*]...  
  
 *termo* :: = *factor* &#124; *termo* { \*&#124;*/* } *fator*  
  
 *sem sinal-inteiro* :: = {*digit*}  
  
 *letra* maiúscula:: = *A &#124; B &#124; C &#124; D &#124; E &#124; F &#124; G &#124; H &#124; i &#124; J &#124; K &#124; L &#124; M &#124; N &#124; O &#124; P &#124; Q &#124; R &#124; S &#124; T &#124; U &#124; V &#124; W &#124; X &#124; Y &#124; Z*  
  
 *nome definido pelo usuário* :: = *letra*[*dígito* &#124; *letra* &#124; *_*]...
