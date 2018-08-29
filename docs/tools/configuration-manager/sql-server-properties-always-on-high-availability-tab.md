---
title: Propriedades do SQL Server (Guia Alta Disponibilidade Always On) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d8630923-a600-4f1c-aca1-027453a3ec82
caps.latest.revision: 13
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: cfa08dbf9b1fd632c15ede1776055af0e06f8834
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "42784336"
---
# <a name="sql-server-properties-always-on-high-availability-tab"></a>Propriedades do SQL Server (Guia Alta disponibilidade AlwaysOn)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  Use a guia **Alta disponibilidade AlwaysOn** da caixa de diálogo **Propriedades do SQL Server** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager para habilitar ou desabilitar o recurso Grupos de Disponibilidade AlwaysOn no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Habilitar os Grupos de Disponibilidade AlwaysOn é pré-requisito para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usar grupos de disponibilidade como uma solução de recuperação de desastres de alta disponibilidade.  
  
##  <a name="Prerequisites"></a> Pré-requisitos  
 Para estar habilitada para Grupos de Disponibilidade AlwaysOn, uma instância de servidor deve atender aos seguintes pré-requisitos:  
  
-   A instância de servidor deve residir em um nó WSFC (Windows Server Failover Clustering).  
  
-   Para estar no mesmo grupo de disponibilidade, as instâncias devem estar no mesmo cluster WSFC. Um grupo de disponibilidade não pode abranger clusters de WSFC.  
  
-   A instância de servidor deve estar executando uma edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que dá suporte a [!INCLUDE[ssHADR](../../includes/sshadr-md.md)].  
  
-   Habilitar Grupos de Disponibilidade AlwaysOn para somente uma instância de servidor de cada vez. Depois de habilitar os Grupos de Disponibilidade AlwaysOn, aguarde até que o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenha reiniciado antes de habilitar a próxima instância de servidor.  
  
> [!NOTE]  
>  Para obter informações sobre suporte a recursos e informações sobre pré-requisitos adicionais, restrições e recomendações para [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], consulte os Manuais Online do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
## <a name="dialog-options"></a>Opções da caixa de diálogo  
 **Nome do cluster de failover do Windows**  
 Exibe o nome do cluster WSFC no qual o computador local é um nó.  
  
 **Habilitar Grupos de Disponibilidade AlwaysOn**  
 Use essa caixa de seleção para habilitar ou desabilitar os Grupos de Disponibilidade AlwaysOn nessa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], da seguinte maneira:  
  
-   Se essa caixa de seleção estiver vazia, os Grupos de Disponibilidade AlwaysOn estarão desabilitados no momento. Para habilitar os Grupos de Disponibilidade AlwaysOn, marque essa caixa de seleção, clique em **OK**e reinicie manualmente o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Se essa caixa de seleção já estiver selecionada, os Grupos de Disponibilidade AlwaysOn estarão habilitados no momento. Para desabilitar os Grupos de Disponibilidade AlwaysOn, desmarque a caixa de seleção e clique em **OK**. Isso faz a instância de servidor ser reiniciada.  
  
    > [!TIP]  
    >  Depois de desabilitar os Grupos de Disponibilidade AlwaysOn, você deve remover as réplicas de disponibilidade locais da instância de servidor. Se você remover a última réplica de um determinado grupo de disponibilidade, também deverá remover o grupo.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
  
> [!NOTE]  
>  Para obter mais informações sobre o acompanhamento depois de desabilitar os Grupos de Disponibilidade AlwaysOn e para obter informações sobre como criar e configurar grupos de disponibilidade, consulte os Manuais Online do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
  
