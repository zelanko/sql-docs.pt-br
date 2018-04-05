---
title: SQLColAttributes (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLColAttribute function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: d403dfa0-c26d-47d4-91d9-2f29aa387399
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8cef195281e4793af925174eb0e13ed6a5ff8667
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlcolattributes-visual-foxpro-odbc-driver"></a>SQLColAttributes (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do Driver ODBC do Visual FoxPro. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: completo  
  
 ODBC API conformidade: Nível de núcleo  
  
 Retorna informações de descritor para uma coluna em um conjunto de resultados. Informações do descritor são retornadas como uma cadeia de caracteres, um valor de descritor dependente de 32 bits ou um valor inteiro.  
  
> [!NOTE]  
>  **SQLColAttributes** não pode ser usado para retornar informações sobre a coluna de indicador (coluna 0).  
  
 O Driver de ODBC do Visual FoxPro oferece suporte a todos os *fDescType* valores. A tabela a seguir inclui comentários na implementação do driver de valores selecionados.  
  
|*fDescType*|Comentário|  
|-----------------|-------------|  
|SQL_COLUMN_AUTO_INCREMENT|Retorna FALSE: Do Visual FoxPro não tem contador campos.|  
|SQL_COLUMN_CASE_SENSITIVE|Sempre retorna TRUE se o tipo de coluna for caractere.|  
|SQL_COLUMN_LABEL|Retorna o nome da coluna, que também é retornado por SQL_COLUMN_NAME.|  
|SQL_COLUMN_MONEY|Retorna VERDADEIRO se o tipo de coluna é a moeda (representada por um "Y" na linguagem do Visual FoxPro).|  
|SQL_COLUMN_OWNER_NAME|Sempre retorna uma cadeia de caracteres vazia.|  
|SQL_COLUMN_QUALIFIER_NAME|Sempre retorna uma cadeia de caracteres vazia.|  
|SQL_COLUMN_SEARCHABLE|Retorna SQL_UNSEARCHABLE para colunas do tipo geral; Essas colunas não podem ser usadas em uma cláusula WHERE.<br /><br /> Não defina retorna SQL_SEARCHABLE para colunas do tipo caractere ou Memorando com NOCPTRANS; Essas colunas podem ser usadas em uma cláusula WHERE com qualquer operador de comparação.<br /><br /> Retorna SQL_ALL_EXCEPT_LIKE para todos os outros tipos de coluna. Essas colunas podem ser usadas em uma cláusula WHERE com todos os operadores de comparação exceto SEMELHANTE.|  
|SQL_COLUMN_TABLE_NAME|Sempre retorna uma cadeia de caracteres vazia.|  
  
 Para obter mais informações, consulte [SQLColAttributes](../../odbc/reference/syntax/sqlcolattributes-function.md) no *referência do programador de ODBC*.
