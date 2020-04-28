---
title: SQLColAttributes (driver ODBC do Visual FoxPro) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307907"
---
# <a name="sqlcolattributes-visual-foxpro-odbc-driver"></a>SQLColAttributes (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: completo  
  
 Conformidade da API ODBC: nível de núcleo  
  
 Retorna informações de descritor para uma coluna em um conjunto de resultados. As informações do descritor são retornadas como uma cadeia de caracteres, um valor dependente de descritor de 32 bits ou um valor inteiro.  
  
> [!NOTE]  
>  **SQLColAttributes** não pode ser usado para retornar informações sobre a coluna Bookmark (coluna 0).  
  
 O driver ODBC do Visual FoxPro dá suporte a todos os valores de *fDescType* . A tabela a seguir inclui comentários sobre a implementação do driver dos valores selecionados.  
  
|*fDescType*|Comentário|  
|-----------------|-------------|  
|SQL_COLUMN_AUTO_INCREMENT|Retorna FALSE: o Visual FoxPro não tem nenhum campo de contador.|  
|SQL_COLUMN_CASE_SENSITIVE|Sempre retornará TRUE se o tipo de coluna for Character.|  
|SQL_COLUMN_LABEL|Retorna o nome da coluna, que também é retornado por SQL_COLUMN_NAME.|  
|SQL_COLUMN_MONEY|Retornará TRUE se o tipo de coluna for Currency (representado por um "Y" na linguagem do Visual FoxPro).|  
|SQL_COLUMN_OWNER_NAME|Sempre retorna uma cadeia de caracteres vazia.|  
|SQL_COLUMN_QUALIFIER_NAME|Sempre retorna uma cadeia de caracteres vazia.|  
|SQL_COLUMN_SEARCHABLE|Retorna SQL_UNSEARCHABLE para colunas do tipo geral; essas colunas não podem ser usadas em uma cláusula WHERE.<br /><br /> Retorna SQL_SEARCHABLE para colunas do tipo Character ou Memo com NOCPTRANS não definido; essas colunas podem ser usadas em uma cláusula WHERE com qualquer operador de comparação.<br /><br /> Retorna SQL_ALL_EXCEPT_LIKE para todos os outros tipos de coluna; essas colunas podem ser usadas em uma cláusula WHERE com todos os operadores de comparação, exceto como.|  
|SQL_COLUMN_TABLE_NAME|Sempre retorna uma cadeia de caracteres vazia.|  
  
 Para obter mais informações, consulte [SQLColAttributes](../../odbc/reference/syntax/sqlcolattributes-function.md) na *referência do programador de ODBC*.
