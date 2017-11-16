---
title: "Arquivos de log de rastreamento padrão desabilitados | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Best Practices [Database Engine]
ms.assetid: c27761e6-75ed-4ee4-a236-0cbc42e500a1
caps.latest.revision: "10"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f952b34c502d604b258278e9ae870afdbf0c33f5
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="default-trace-log-files-disabled"></a>Arquivos de log de rastreamento padrão desabilitados
  Esta regra verifica os valores da opção habilitada sp_configure de rastreamento padrão do procedimento armazenado para determinar se o rastreamento padrão está definido como ON (1) ou OFF (0). Quando esta opção está habilitada, o rastreamento padrão fornece informações sobre as alterações na configuração e no DDL do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Em alguns casos, estas informações podem ser úteis para os clientes, o Atendimento ao consumidor e o Suporte do [!INCLUDE[msCoName](../../includes/msconame-md.md)] quando estiverem solucionando questões sobre o [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Use o procedimento armazenado sp_configure para habilitar o rastreamento definindo o valor habilitado de rastreamento padrão como 1.  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
