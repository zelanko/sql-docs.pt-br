---
title: Propriedades do SQL Server (guia alta disponibilidade AlwaysOn) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- configmgr-client
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d8630923-a600-4f1c-aca1-027453a3ec82
caps.latest.revision: 12
author: mikeraymsft
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 24f1a371cf69c825d9ec251fa4271c5c8d596210
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37303156"
---
# <a name="sql-server-properties-alwayson-high-availability-tab"></a>Propriedades do SQL Server (guia Alta disponibilidade AlwaysOn)
  Use a guia **Alta disponibilidade AlwaysOn** da caixa de diálogo **Propriedades do SQL Server** no Gerenciador de Configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para habilitar ou desabilitar o recurso Grupos de Disponibilidade AlwaysOn no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Habilitar os Grupos de Disponibilidade AlwaysOn é pré-requisito para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usar grupos de disponibilidade como uma solução de recuperação de desastres de alta disponibilidade.  
  
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
  
 **Habilitar grupos de disponibilidade AlwaysOn**  
 Use essa caixa de seleção para habilitar ou desabilitar os Grupos de Disponibilidade AlwaysOn nessa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], da seguinte maneira:  
  
-   Se essa caixa de seleção estiver vazia, os Grupos de Disponibilidade AlwaysOn estarão desabilitados no momento. Para habilitar os Grupos de Disponibilidade AlwaysOn, marque essa caixa de seleção, clique em **OK**e reinicie manualmente o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Se essa caixa de seleção já estiver selecionada, os Grupos de Disponibilidade AlwaysOn estarão habilitados no momento. Para desabilitar os Grupos de Disponibilidade AlwaysOn, desmarque a caixa de seleção e clique em **OK**. Isso faz a instância de servidor ser reiniciada.  
  
    > [!TIP]  
    >  Depois de desabilitar os Grupos de Disponibilidade AlwaysOn, você deve remover as réplicas de disponibilidade locais da instância de servidor. Se você remover a última réplica de um determinado grupo de disponibilidade, também deverá remover o grupo.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
  
> [!NOTE]  
>  Para obter mais informações sobre o acompanhamento depois de desabilitar os Grupos de Disponibilidade AlwaysOn e para obter informações sobre como criar e configurar grupos de disponibilidade, consulte os Manuais Online do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
  
