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
manager: craigg
ms.openlocfilehash: fe57ffa0d7628601fcb6dd19218715b32a57322b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47829474"
---
# <a name="statement-options"></a>Opções de instrução
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Essas opções permitem a personalização de uma instrução de execução específica dentro de um aplicativo.  
  
|Opção de instrução|Observações|  
|----------------------|-----------|  
|SQL_BIND_TYPE|Não pode exceder 2.147.483.647 bytes ou a memória disponível.|  
|SQL_CONCURRENCY|Para os valores permitidos, consulte a [tipo de Cursor e combinações de simultaneidade](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md).|  
|SQL_CURSOR_TYPE|O driver não permite SQL_CURSOR_DYNAMIC. Ver [SQLSetScrollOptions](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md) para obter mais informações. Para os valores permitidos, consulte a [tipo de Cursor e combinações de simultaneidade](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md).|  
|SQL_GET_BOOKMARK|Retorna um valor inteiro de 32 bits que é o indicador para o número do registro atual. Obter somente; não é possível definir.|  
|SQL_KEYSET_SIZE|Pode ser definido somente como 0.|  
|SQL_MAX_ROWS|O número máximo de linhas a serem retornadas de um resultado definido.|  
|SQL_ROW_NUMBER|Retorna um inteiro de 32 bits que especifica a posição da linha atual no conjunto de resultados. Obter somente; não é possível definir.|  
|SQL_ROWSET_SIZE|Não pode exceder 4.294.967.296 linhas; No entanto, você deve ter memória virtual suficiente em seu computador para processar sua solicitação.|  
|SQL_USE_BOOKMARKS|Dá suporte à configuração SQL_USE_BOOKMARKS para SQL_UB_ON e expõe os indicadores de comprimento fixo.|
