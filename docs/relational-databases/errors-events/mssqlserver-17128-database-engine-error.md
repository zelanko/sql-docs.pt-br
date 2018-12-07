---
title: MSSQLSERVER_17128 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17128 (Database Engine error)
ms.assetid: 7b15a5e6-fd41-47ce-ba87-54f72acea4bb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3091a7a47be4504ace63302f4c821c3e15616d08
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52538675"
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
Falha nas alocações ou reservas de memória iniciais do pool de buffers. O SQL Server foi encerrado.  
  
## <a name="user-action"></a>Ação do usuário  
Isso geralmente ocorre ao iniciar o SQL Server em um computador extremamente pequeno (bem menor que os requisitos mínimos do sistema).  
  
