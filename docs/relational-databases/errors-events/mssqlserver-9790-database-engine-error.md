---
title: MSSQLSERVER_9790 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9790 (Database Engine error)
ms.assetid: 83fd379f-5deb-4f97-8cb4-282e3d3fed94
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 67aa62efb3f77c82aec4b1f5d654532cfadd74fb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67903818"
---
# <a name="mssqlserver9790"></a>MSSQLSERVER_9790
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|9790|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SB3_XMIT_ERROR_ENTRANCE_BROKER_SINGLE_USER|  
|Texto da mensagem|Não é possível rotear a mensagem de entrada. O banco de dados de sistema MSDB que contém informações de roteamento está no modo SINGLE USER.|  
  
## <a name="explanation"></a>Explicação  
Ocorreu um erro ao tentar classificar uma mensagem recebida sem-cabo porque o banco de dados MSDB estava no modo usuário único.  
  
## <a name="user-action"></a>Ação do usuário  
Altere o MSDB para o modo MULTI USER com o comando ALTER DATABASE.  
  
