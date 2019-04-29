---
title: MSSQLSERVER_21889 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 21889 (Database Engine error)
ms.assetid: ae199540-7986-4cc2-b782-cd22793236d3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 262b2c795da92b2ef32c6956d9a2deda0e45a39d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62915223"
---
# <a name="mssqlserver21889"></a>MSSQLSERVER_21889
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|21889|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQLErrorNum21889|  
|Texto da mensagem|A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] '% s' não é um publicador de replicação. Execute `sp_adddistributor` na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] '%s' com o distribuidor '%s' para habilitar a instância para hospedar o banco de dados de publicação '%s'. Certifique-se de especificar as mesmas informações de logon e senha que foram usadas para o publicador original.|  
  
## <a name="explanation"></a>Explicação  
 Para hospedar o banco de dados publicador, a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser um publicador de replicação. `sp_validate_redirected_publisher` chama `sp_helpdistributor` no servidor remoto para determinar se o servidor é um publicador de replicação. Esse erro é retornado quando a execução do procedimento armazenado `sp_helpdistributor` indica que a instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não é um publicador de replicação.  
  
## <a name="user-action"></a>Ação do usuário  
 Execute `sp_adddistributor` na instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda o banco de dados publicador. Ao executar `sp_adddistributor`, especifique o distribuidor correto. Use o mesmo valor para o *@password* parâmetro que o usado quando `sp_adddistributor` foi executado inicialmente no distribuidor.  
  
  
