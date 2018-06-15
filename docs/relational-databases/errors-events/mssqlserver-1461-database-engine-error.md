---
title: MSSQLSERVER_1461 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 1461 (Database Engine error)
ms.assetid: fce10907-4753-441b-b624-f28e00ed7520
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 17c5d9e85013e7e977f07e9000c896d46d1b26c0
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34318287"
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
  
