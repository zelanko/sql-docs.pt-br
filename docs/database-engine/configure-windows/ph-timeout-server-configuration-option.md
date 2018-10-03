---
title: Opção de configuração de servidor PH timeout | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- time limit for protocol handler wait [SQL Server]
- timeout options [SQL Server], ph timeout option
- protocols [SQL Server], timing out
- ph timeout option
ms.assetid: ed19a07c-83fe-4582-9c9e-41b1ce571850
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fca08d3b59c9d7c53713ad3ec74c439dddc57c07
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47798814"
---
# <a name="ph-timeout-server-configuration-option"></a>Opção de configuração de servidor PH timeout
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Use a opção tempo limite PH para especificar o tempo, em segundos, que o manipulador de protocolo de texto completo deve aguardar para se conectar a um banco de dados antes que o tempo limite seja excedido. O valor padrão é 60 segundos. Aumente o valor tempo limite ph quando as tentativas de conexão estiverem excedendo o tempo limite devido a problemas temporários na rede.  
  
 O manipulador de protocolo de texto completo é hospedado no host de daemon de filtro e é usado para buscar no SQL Server os dados de texto completo a serem indexados. Para obter mais informações sobre os componentes da pesquisa de texto completo, veja [Pesquisa de Texto Completo](../../relational-databases/search/full-text-search.md).  
  
 Ao tentar buscar uma linha de dados, se o manipulador de protocolo não puder se conectar ao SQL Server dentro do tempo especificado, ele informará um erro de tempo limite para aquela linha. A busca de texto completo será feita na linha mais tarde. Para obter mais informações sobre o gatherer de texto completo, veja [Popular índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Pesquisa de Texto Completo](../../relational-databases/search/full-text-search.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
