---
title: Propriedades do SQL Server (Guia Alta disponibilidade AlwaysOn)
description: Para usar os grupos de disponibilidade como uma solução de recuperação de desastres e alta disponibilidade, acione o recurso Grupos de Disponibilidade Always On no SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: d8630923-a600-4f1c-aca1-027453a3ec82
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: d623bd63cfb9d2d72f41bf498259b1d13fe651b8
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478417"
---
# <a name="sql-server-properties-always-on-high-availability-tab"></a>Propriedades do SQL Server (Guia Alta disponibilidade AlwaysOn)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  Use a guia **Alta disponibilidade AlwaysOn** da caixa de diálogo **Propriedades do SQL Server** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager para habilitar ou desabilitar o recurso Grupos de Disponibilidade AlwaysOn no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Habilitar os Grupos de Disponibilidade AlwaysOn é pré-requisito para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usar grupos de disponibilidade como uma solução de recuperação de desastres de alta disponibilidade.  
  
##  <a name="prerequisites"></a><a name="Prerequisites"></a> Pré-requisitos  
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
  
-   Se essa caixa de seleção estiver vazia, os Grupos de Disponibilidade AlwaysOn estarão desabilitados no momento. Para habilitar os Grupos de Disponibilidade AlwaysOn, marque essa caixa de seleção, clique em **OK** e reinicie manualmente o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Se essa caixa de seleção já estiver selecionada, os Grupos de Disponibilidade AlwaysOn estarão habilitados no momento. Para desabilitar os Grupos de Disponibilidade AlwaysOn, desmarque a caixa de seleção e clique em **OK**. Isso faz a instância de servidor ser reiniciada.  
  
    > [!TIP]  
    >  Depois de desabilitar os Grupos de Disponibilidade AlwaysOn, você deve remover as réplicas de disponibilidade locais da instância de servidor. Se você remover a última réplica de um determinado grupo de disponibilidade, também deverá remover o grupo.  
  
## <a name="ui-element-list"></a>Lista de elementos da interface do usuário  
  
> [!NOTE]  
>  Para obter mais informações sobre o acompanhamento depois de desabilitar os Grupos de Disponibilidade AlwaysOn e para obter informações sobre como criar e configurar grupos de disponibilidade, consulte os Manuais Online do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
  
