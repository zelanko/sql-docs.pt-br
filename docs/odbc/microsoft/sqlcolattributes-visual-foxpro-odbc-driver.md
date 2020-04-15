---
title: SQLColAttributea (Driver Visual FoxPro ODBC) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9508fa7b9ada8273e1250d7584e577892acf5c51
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307907"
---
# <a name="sqlcolattributes-visual-foxpro-odbc-driver"></a>SQLColAttributes (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver Visual FoxPro ODBC. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: Completo  
  
 Conformidade da API ODBC: Nível do núcleo  
  
 Retorna informações do descritor para uma coluna em um conjunto de resultados. As informações do descritor são retornadas como uma seqüência de caracteres, um valor dependente do descritor de 32 bits ou um valor inteiro.  
  
> [!NOTE]  
>  **SQLColAttributes** não podem ser usados para retornar informações sobre a coluna marcador (coluna 0).  
  
 O Visual FoxPro ODBC Driver suporta todos os valores *fDescType.* A tabela a seguir inclui comentários sobre a implementação dos valores selecionados pelo driver.  
  
|*fDescType*|Comentário|  
|-----------------|-------------|  
|SQL_COLUMN_AUTO_INCREMENT|Retorna FALSO: Visual FoxPro não tem contracampos.|  
|SQL_COLUMN_CASE_SENSITIVE|Sempre retorna TRUE se o tipo de coluna for Caractere.|  
|SQL_COLUMN_LABEL|Retorna o nome da coluna, que também é devolvido por SQL_COLUMN_NAME.|  
|SQL_COLUMN_MONEY|Retorna TRUE se o tipo de coluna for Moeda (representado por um "Y" no idioma Visual FoxPro).|  
|SQL_COLUMN_OWNER_NAME|Sempre retorna uma cadeia de caracteres vazia.|  
|SQL_COLUMN_QUALIFIER_NAME|Sempre retorna uma cadeia de caracteres vazia.|  
|SQL_COLUMN_SEARCHABLE|Devoluções SQL_UNSEARCHABLE para colunas do tipo Geral; essas colunas não podem ser usadas em uma cláusula WHERE.<br /><br /> Retorna SQL_SEARCHABLE para colunas de caractere saque ou memorando com NOCPTRANS não definido; estas colunas podem ser usadas em uma cláusula WHERE com qualquer operador de comparação.<br /><br /> Retorna SQL_ALL_EXCEPT_LIKE para todos os outros tipos de colunas; estas colunas podem ser usadas em uma cláusula WHERE com todos os operadores de comparação, exceto LIKE.|  
|SQL_COLUMN_TABLE_NAME|Sempre retorna uma cadeia de caracteres vazia.|  
  
 Para obter mais informações, consulte [SQLColAttributes](../../odbc/reference/syntax/sqlcolattributes-function.md) no *Programador ODBC*.
