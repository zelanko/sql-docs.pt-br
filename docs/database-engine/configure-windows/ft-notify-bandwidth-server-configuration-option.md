---
title: Opção de configuração de servidor ft notify bandwidth | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: configure-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- ft notify bandwidth opion
- small memory buffers
- memory [SQL Server], buffers
ms.assetid: 9ca284c5-f3e0-4a67-a132-fff376ff0ffe
caps.latest.revision: 19
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1da0739321c11ab0ac712bbcfcbca6fb9292647c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="ft-notify-bandwidth-server-configuration-option"></a>Opção ft notify bandwidth de configuração de servidor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Use a opção **ft notify bandwidth** para especificar o tamanho a que pode crescer o pool de buffers de memória pequenos. Buffers de memória pequenos têm 64 KB (quilobytes). O valor do parâmetro *max* especifica o número máximo de buffers que o gerenciador de memória de texto completo deve manter em um pool de buffers pequenos. Se o valor de **max** for zero, não haverá limite máximo ao número de buffers no pool de buffers pequenos.  
  
 O valor do parâmetro **min** especifica o número mínimo de buffers de memória que deve ser mantido no pool de buffers de memória pequenos. Mediante solicitação do gerenciador de memória do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , todos os pools de buffers extra serão liberados, mas esse número mínimo de buffers será mantido. Se, contudo, o valor especificado de **min** for zero, todos os buffers de memória serão liberados.  
  
 Sob certas circunstâncias, o número de buffers alocados atualmente é menor que o valor especificado pelo parâmetro **min** .  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Opção de configuração de servidor ft crawl bandwidth](../../database-engine/configure-windows/ft-crawl-bandwidth-server-configuration-option.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
