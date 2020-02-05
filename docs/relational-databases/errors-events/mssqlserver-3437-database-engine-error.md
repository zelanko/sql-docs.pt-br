---
title: MSSQLSERVER_3437 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3437 (Database Engine error)
ms.assetid: b38216e2-b650-43bd-97af-061d54f60031
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8c0e4b8a9e7e8dacb2369af4c9f43000ba1a9702
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68132309"
---
# <a name="mssqlserver_3437"></a>MSSQLSERVER_3437
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|3437|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|NODTC|  
|Texto da mensagem|Ocorreu um erro ao recuperar o banco de dados '%.*ls.' Não é possível se conectar ao MS DTC (Coordenador de Transações Distribuídas da Microsoft) para verificar o status de conclusão da transação %S_XID. Corrija o MS DTC e execute a recuperação novamente.|  
  
## <a name="explanation"></a>Explicação  
Uma ou mais transações distribuídas que estavam usando o MS DTC (Coordenador de Transações Distribuídas da [!INCLUDE[msCoName](../../includes/msconame-md.md)]) estavam incompletas quando o banco de dados foi desligado. A recuperação desse banco de dados falhou porque o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode se conectar ao MS DTC para concluir ou reverter as transações.  
  
## <a name="user-action"></a>Ação do usuário  
Para recuperar esse banco de dados, você precisa primeiro resolver o problema no MS DTC. Para investigar o problema com o MS DTC, examine os logs de eventos do Windows. Se você não conseguir resolver o problema com o MS DTC para recuperar o banco de dados, restaure um backup do banco de dados.  
  
