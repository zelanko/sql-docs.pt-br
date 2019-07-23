---
title: MSSQLSERVER_1461 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1461 (Database Engine error)
ms.assetid: fce10907-4753-441b-b624-f28e00ed7520
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6411b8eaf64daf16bc42636950f43fd37104629a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68033456"
---
# <a name="mssqlserver1461"></a>MSSQLSERVER_1461
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|1461|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBM_SAFETY_MISMATCH|  
|Texto da mensagem|Foram detectados níveis de segurança diferentes no espelhamento de banco de dados entre servidores para o banco de dados "%.*ls". O nível de segurança FULL será usado.|  
  
## <a name="explanation"></a>Explicação  
As conexões de espelhamento foram perdidas quando o nível de segurança da transação foi modificado porque as configurações de segurança da transação eram inconsistentes nos bancos de dados principal e espelho. A configuração de segurança padrão da segurança da transação completa será usada. A sessão será executada em modo de segurança alta.  
  
## <a name="user-action"></a>Ação do usuário  
Para desativar a segurança da transação, execute novamente a instrução ALTER DATABASE *database_name* SET PARTNER SAFETY OFF no banco de dados de entidade.  
  
