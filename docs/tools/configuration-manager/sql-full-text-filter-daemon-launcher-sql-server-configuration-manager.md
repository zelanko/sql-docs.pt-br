---
title: Iniciador do Daemon de filtro de texto completo SQL (SQL Server Configuration Manager) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d0dc03db-5f76-4558-b041-1ac7b9b5bb16
caps.latest.revision: "8"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0829cbef976a5fc53166cf5616a900e8472e9e0d
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="sql-full-text-filter-daemon-launcher-sql-server-configuration-manager"></a>Iniciador do Daemon de Filtro de Texto Completo do SQL (SQL Server Configuration Manager)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]A partir do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], o serviço iniciador de Daemon de filtro de texto completo do SQL (iniciador FDHOST) é usado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pesquisa de texto completo para iniciar o processo de host do daemon de filtro, que manipula a filtragem da pesquisa de texto completo e a quebra de palavras. Esse serviço deve estar em execução para usar a pesquisa de texto completo. O Iniciador FDHOST é um serviço de reconhecimento de instâncias associado a uma instância específica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O serviço do Iniciador FDHOST propaga as informações da conta de serviço para cada processo do host do daemon de filtro iniciado. Para obter informações sobre os processos do host do daemon de filtro, consulte "Arquitetura da pesquisa de texto completo" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
  
