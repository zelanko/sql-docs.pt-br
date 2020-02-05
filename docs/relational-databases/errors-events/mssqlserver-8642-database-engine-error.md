---
title: MSSQLSERVER_8642 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8642 (Database Engine error)
ms.assetid: fc498059-202f-4d0b-8599-4e784b47c186
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 614f4a3db9ebce75f2f7c45c301745871b6f5b43
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68063205"
---
# <a name="mssqlserver_8642"></a>MSSQLSERVER_8642
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|8642|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|EXCHNGSTART_ERR|  
|Texto da mensagem|O processador de consultas não pôde iniciar os recursos de threads necessários para execução paralela da consulta.|  
  
## <a name="explanation"></a>Explicação  
O servidor não dispõe de recursos de thread suficientes.  
  
## <a name="user-action"></a>Ação do usuário  
Reduza a carga no servidor e execute a consulta novamente.  
  
