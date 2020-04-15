---
title: Opções de Declaração | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca40765dff98e9102fbe36e88c7e79535f311d97
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299206"
---
# <a name="statement-options"></a>Opções de instrução
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Essas opções permitem a personalização de uma instrução de execução específica dentro de um aplicativo.  
  
|Opção de declaração|Observações|  
|----------------------|-----------|  
|SQL_BIND_TYPE|Não pode exceder 2.147.483.647 bytes ou memória disponível.|  
|SQL_CONCURRENCY|Para valores permitidos, consulte as [combinações tipo cursor e combinações de moedas .](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)|  
|SQL_CURSOR_TYPE|O motorista não permite SQL_CURSOR_DYNAMIC. Consulte [SQLSetScrollOptions](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md) para obter mais informações. Para valores permitidos, consulte as [combinações tipo cursor e combinações de moedas .](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)|  
|SQL_GET_BOOKMARK|Retorna um valor inteiro de 32 bits que é o marcador para o número de registro atual. Obter apenas; não pode definir.|  
|SQL_KEYSET_SIZE|Pode ser definido apenas para 0.|  
|SQL_MAX_ROWS|O número máximo de linhas para retornar de um conjunto de resultados.|  
|SQL_ROW_NUMBER|Retorna um inteiro de 32 bits especificando a posição da linha atual dentro do conjunto de resultados. Obter apenas; não pode definir.|  
|SQL_ROWSET_SIZE|Não pode exceder 4.294.967.296 linhas; no entanto, você deve ter memória virtual suficiente em seu computador para lidar com sua solicitação.|  
|SQL_USE_BOOKMARKS|Suporta a configuração SQL_USE_BOOKMARKS para SQL_UB_ON e expõe marcadores de comprimento fixo.|
