---
title: MSSQLSERVER_17130 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 17130 (Database Engine error)
ms.assetid: 7ce6afca-221d-402f-89df-da7e74a339a8
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c3395687ca0808cacd2e7b8e975e9503d49fde72
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver17130"></a>MSSQLSERVER_17130
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|17130|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|INIT_NOLOCKSPACE|  
|Texto da mensagem|Não há memória suficiente para o número de bloqueios configurado. Tente começar com uma tabela de hash de bloqueio menor, que pode causar impacto no desempenho. Contate o administrador de banco de dados para configurar mais memória para a instância do Mecanismo de Banco de Dados.|  
  
## <a name="explanation"></a>Explicação  
Não há memória suficiente para o tamanho da tabela de hash do gerenciador de bloqueios desejado.  Ocorrerá uma tentativa para alocar uma tabela de hash menor.  
  
## <a name="user-action"></a>Ação do usuário  
Verifique os parâmetros de configuração da memória do servidor (min/max server memory) e verifique se há pressões de memória. Forneça mais memória ao SQL Server.  
  
