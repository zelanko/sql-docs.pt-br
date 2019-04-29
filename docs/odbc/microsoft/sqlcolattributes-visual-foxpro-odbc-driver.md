---
title: SQLColAttributes (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColAttribute function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: d403dfa0-c26d-47d4-91d9-2f29aa387399
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e34929315d3a3548799bc605dbb8f3c4a2f665d0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62928169"
---
# <a name="sqlcolattributes-visual-foxpro-odbc-driver"></a>SQLColAttributes (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas de Driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte a: Completo  
  
 Conformidade com a API ODBC: Nível de núcleo  
  
 Retorna informações de descritor para uma coluna em um conjunto de resultados. Informações do descritor são retornadas como uma cadeia de caracteres, um valor de descritor dependente de 32 bits ou um valor inteiro.  
  
> [!NOTE]  
>  **SQLColAttributes** não pode ser usado para retornar informações sobre a coluna de indicador (coluna 0).  
  
 O Driver de ODBC do Visual FoxPro dá suporte a todas *fDescType* valores. A tabela a seguir inclui comentários sobre a implementação do driver de valores selecionados.  
  
|*fDescType*|Comentário|  
|-----------------|-------------|  
|SQL_COLUMN_AUTO_INCREMENT|Retorna FALSE: Do Visual FoxPro não tem nenhum campo contador.|  
|SQL_COLUMN_CASE_SENSITIVE|Sempre retorna TRUE se o tipo de coluna for caractere.|  
|SQL_COLUMN_LABEL|Retorna o nome de coluna, que também é retornado por SQL_COLUMN_NAME.|  
|SQL_COLUMN_MONEY|Retornará TRUE se o tipo de coluna é a moeda (representada por um "Y" na linguagem do Visual FoxPro).|  
|SQL_COLUMN_OWNER_NAME|Sempre retorna uma cadeia de caracteres vazia.|  
|SQL_COLUMN_QUALIFIER_NAME|Sempre retorna uma cadeia de caracteres vazia.|  
|SQL_COLUMN_SEARCHABLE|Retorna SQL_UNSEARCHABLE para colunas do tipo geral; Essas colunas não podem ser usadas em uma cláusula WHERE.<br /><br /> Não defina retorna SQL_SEARCHABLE para colunas do tipo de caractere ou Memorando com NOCPTRANS; Essas colunas podem ser usadas em uma cláusula WHERE com qualquer operador de comparação.<br /><br /> Retorna SQL_ALL_EXCEPT_LIKE para todos os outros tipos de coluna. Essas colunas podem ser usadas em uma cláusula WHERE com todos os operadores de comparação, exceto SEMELHANTE.|  
|SQL_COLUMN_TABLE_NAME|Sempre retorna uma cadeia de caracteres vazia.|  
  
 Para obter mais informações, consulte [SQLColAttributes](../../odbc/reference/syntax/sqlcolattributes-function.md) na *referência do programador de ODBC*.
