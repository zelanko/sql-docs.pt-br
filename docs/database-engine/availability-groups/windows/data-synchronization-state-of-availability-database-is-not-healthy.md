---
title: O estado de sincronização de dados do banco de dados de disponibilidade não está íntegro | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.agdashboard.arp3datasynchealthy.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 4fd003e7-808e-4b0e-b28a-47d9f2616f06
author: MashaMSFT
ms.author: mathoma
manager: erikre
ms.openlocfilehash: 8ae1f9db8c3bbd0b2c86e18814ca919c2e558baa
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47738394"
---
# <a name="data-synchronization-state-of-availability-database-is-not-healthy"></a>O estado de sincronização de dados do banco de dados de disponibilidade não é íntegro
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>Introdução  
  
|||  
|-|-|  
|**Nome da Política**|Estado de Sincronização dos Dados do Banco de Dados de Disponibilidade|  
|**Problema**|O estado de sincronização de dados do banco de dados de disponibilidade não é íntegro.|  
|**Categoria**|**Aviso**|  
|**Faceta**|Banco de dados de disponibilidade|  
  
## <a name="description"></a>Descrição  
 Esta política acumula o estado de sincronização de dados de todos os bancos de dados de disponibilidade (também chamados de "réplicas de banco de dados") na réplica de disponibilidade. A política estará em estado não íntegro quando alguma réplica de banco de dados não estiver no estado de sincronização de dados esperado. Caso contrário, a política estará em um estado íntegro.  
  
> [!NOTE]  
>  Para esta versão do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], as informações sobre possíveis causas e soluções estão localizadas em [O estado de sincronização de dados de algum banco de dados de disponibilidade não é íntegro](http://go.microsoft.com/fwlink/p/?LinkId=220858) no TechNet Wiki.  
  
## <a name="possible-causes"></a>Causas possíveis  
 O estado de sincronização de dados deste banco de dados de disponibilidade não é íntegro. Em uma réplica de disponibilidade de confirmação de transação, todos os bancos de dados de disponibilidade devem estar no estado SYNCHRONIZING. Em uma réplica de disponibilidade da confirmação síncrona, todo banco de dados de disponibilidade deve estar no estado SYNCHRONIZING.  
  
## <a name="possible-solution"></a>Solução possível  
 Use a política de réplica de banco de dados para localizar a réplica de banco de dados em estado de sincronização de dados não íntegro e depois resolva o problema na réplica de banco de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](~/database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  


