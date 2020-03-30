---
title: Opção de configuração de servidor max full-text crawl range | Microsoft Docs
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
- crawls [full-text search]
- max full-text crawl range option
ms.assetid: a49de86b-0891-4dcd-89c0-ead30aab00e0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 740d952640cef0400c379e9dfb25157331c9bfab
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68023749"
---
# <a name="max-full-text-crawl-range-server-configuration-option"></a>Opção max full-text crawl range de configuração de servidor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Use a opção **max full-text crawl range** para otimizar a utilização de CPU, o que melhora o desempenho durante um rastreamento completo. Usando esta opção, você pode especificar o número de partições que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deverá usar durante um rastreamento de índice completo. Por exemplo, se houver muitas CPUs e sua utilização não for a ideal, você pode aumentar o valor máximo dessa opção. Além dessa opção, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa vários outros fatores, como o número de linhas na tabela e o número de CPUs, para determinar o número real de partições usadas.  
  
 O valor padrão desta opção é 4; o valor mínimo é 1 e o valor máximo, 256. As alterações feitas nesta opção afetam somente os rastreamentos subsequentes. Os rastreamentos em andamento não serão afetados por alterações na configuração desta opção.  
  
 A opção **max full-text crawl range** é uma opção avançada. Se você estiver usando o procedimento armazenado do sistema **sp_configure** para alterar a configuração, só será possível alterar **max full-text crawl range** quando **show advanced options** for definido como 1. A configuração entra em vigor imediatamente sem a reinicialização do servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
