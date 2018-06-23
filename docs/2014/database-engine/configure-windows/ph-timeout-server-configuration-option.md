---
title: Opção de configuração de servidor PH timeout | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- time limit for protocol handler wait [SQL Server]
- timeout options [SQL Server], ph timeout option
- protocols [SQL Server], timing out
- ph timeout option
ms.assetid: ed19a07c-83fe-4582-9c9e-41b1ce571850
caps.latest.revision: 28
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: f1e1caba1d80516359b5ef57f24a165e6d6d7598
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122707"
---
# <a name="ph-timeout-server-configuration-option"></a>Opção de configuração de servidor PH timeout
  Use a opção tempo limite PH para especificar o tempo, em segundos, que o manipulador de protocolo de texto completo deve aguardar para se conectar a um banco de dados antes que o tempo limite seja excedido. O valor padrão é 60 segundos. Aumente o valor tempo limite ph quando as tentativas de conexão estiverem excedendo o tempo limite devido a problemas temporários na rede.  
  
 O manipulador de protocolo de texto completo é hospedado no host de daemon de filtro e é usado para buscar no SQL Server os dados de texto completo a serem indexados. Para obter mais informações sobre os componentes da pesquisa de texto completo, veja [Pesquisa de Texto Completo](../../relational-databases/search/full-text-search.md).  
  
 Ao tentar buscar uma linha de dados, se o manipulador de protocolo não puder se conectar ao SQL Server dentro do tempo especificado, ele informará um erro de tempo limite para aquela linha. A busca de texto completo será feita na linha mais tarde. Para obter mais informações sobre o gatherer de texto completo, veja [Popular índices de texto completo](../../relational-databases/indexes/indexes.md).  
  
## <a name="see-also"></a>Consulte também  
 [Pesquisa de Texto Completo](../../relational-databases/search/full-text-search.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
