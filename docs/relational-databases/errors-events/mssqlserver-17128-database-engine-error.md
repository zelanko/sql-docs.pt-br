---
title: MSSQLSERVER_17128 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 17128 (Database Engine error)
ms.assetid: 7b15a5e6-fd41-47ce-ba87-54f72acea4bb
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4e3f897039ce723eecc7c4fc2779bb9ad0d8e3aa
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver17128"></a>MSSQLSERVER_17128
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|17128|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|INIT_NOBUFSPACE|  
|Texto da mensagem|initdata: Nenhuma memória para buffers de kernel.|  
  
## <a name="explanation"></a>Explicação  
Ocorreu uma falha nas alocações ou reservas de memória iniciais do pool de buffers e o SQL Server foi encerrado.  
  
## <a name="user-action"></a>Ação do usuário  
Isso geralmente ocorre ao iniciar o SQL Server em um computador extremamente pequeno – bem menor que os requisitos mínimos de sistema.  
  
