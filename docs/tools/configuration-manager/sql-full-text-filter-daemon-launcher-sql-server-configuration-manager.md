---
title: Iniciador do Daemon de Filtro de Texto Completo do SQL (SQL Server Configuration Manager) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d0dc03db-5f76-4558-b041-1ac7b9b5bb16
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5ad6f90d1165e1c7097425edfa13dd58e3a56681
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sql-full-text-filter-daemon-launcher-sql-server-configuration-manager"></a>Iniciador do Daemon de Filtro de Texto Completo do SQL (SQL Server Configuration Manager)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  A partir do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], o serviço do Iniciador do Daemon de Filtro de Texto Completo do SQL (Iniciador FDHOST) é usado pela pesquisa de texto completo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para iniciar o processo do host do daemon de filtro que manipula a filtragem da pesquisa de texto completo e a quebra de palavras. Esse serviço deve estar em execução para usar a pesquisa de texto completo. O Iniciador FDHOST é um serviço de reconhecimento de instâncias associado a uma instância específica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O serviço do Iniciador FDHOST propaga as informações da conta de serviço para cada processo do host do daemon de filtro iniciado. Para obter informações sobre os processos do host do daemon de filtro, consulte "Arquitetura da pesquisa de texto completo" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
  
