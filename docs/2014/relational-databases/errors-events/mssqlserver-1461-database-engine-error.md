---
title: MSSQLSERVER_1461 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1461 (Database Engine error)
ms.assetid: fce10907-4753-441b-b624-f28e00ed7520
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0af23b53c60ffeafcbaa99a7a499fe0a71cd551b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62869822"
---
# <a name="mssqlserver1461"></a>MSSQLSERVER_1461
    
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
  
  
