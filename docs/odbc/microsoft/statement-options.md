---
title: Opções de instrução | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- custom statement options [ODBC]
- statement options [ODBC]
- ODBC driver for Oracle [ODBC], statement options
ms.assetid: cd73b769-c8b5-43e0-9f80-b3011b7a6162
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3bf99aace8b058e429898846466294cc42612070
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67948838"
---
# <a name="statement-options"></a>Opções de instrução
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Essas opções permitem a personalização de uma instrução de execução específica em um aplicativo.  
  
|Opção de instrução|Observações|  
|----------------------|-----------|  
|SQL_BIND_TYPE|Não é possível exceder 2.147.483.647 bytes ou memória disponível.|  
|SQL_CONCURRENCY|Para obter os valores permitidos, consulte as [combinações de tipo de cursor e simultaneidade](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md).|  
|SQL_CURSOR_TYPE|O driver não permite SQL_CURSOR_DYNAMIC. Consulte [SQLSetScrollOptions](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md) para obter mais informações. Para obter os valores permitidos, consulte as [combinações de tipo de cursor e simultaneidade](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md).|  
|SQL_GET_BOOKMARK|Retorna um valor inteiro de 32 bits que é o indicador para o número do registro atual. Somente obtenção; Não é possível definir.|  
|SQL_KEYSET_SIZE|Pode ser definido somente como 0.|  
|SQL_MAX_ROWS|O número máximo de linhas a serem retornadas de um conjunto de resultados.|  
|SQL_ROW_NUMBER|Retorna um inteiro de 32 bits especificando a posição da linha atual no conjunto de resultados. Somente obtenção; Não é possível definir.|  
|SQL_ROWSET_SIZE|Não pode exceder 4.294.967.296 linhas; no entanto, você deve ter memória virtual suficiente no seu computador para lidar com sua solicitação.|  
|SQL_USE_BOOKMARKS|Dá suporte à definição de SQL_USE_BOOKMARKS para SQL_UB_ON e expõe indicadores de comprimento fixo.|
