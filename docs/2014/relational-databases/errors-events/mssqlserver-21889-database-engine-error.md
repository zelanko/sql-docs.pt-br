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
ms.openlocfilehash: 5c28a5c2d8b2b18d524c8069dca593da6c38d164
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553422"
---
# <a name="mssqlserver_21889"></a>MSSQLSERVER_21889
    
## <a name="details"></a>Detalhes  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|21889|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQLErrorNum21889|  
|Texto da mensagem|A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] '% s' não é um publicador de replicação. Execute `sp_adddistributor` na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] '%s' com o distribuidor '%s' para habilitar a instância para hospedar o banco de dados de publicação '%s'. Certifique-se de especificar as mesmas informações de logon e senha que foram usadas para o publicador original.|  
  
## <a name="explanation"></a>Explicação  
 Para hospedar o banco de dados publicador, a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser um publicador de replicação. `sp_validate_redirected_publisher` chama `sp_helpdistributor` no servidor remoto para determinar se o servidor é um publicador de replicação. Esse erro é retornado quando a execução do procedimento armazenado `sp_helpdistributor` indica que a instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não é um publicador de replicação.  
  
## <a name="user-action"></a>Ação do usuário  
 Execute `sp_adddistributor` na instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda o banco de dados publicador. Ao executar `sp_adddistributor`, especifique o distribuidor correto. Use o mesmo valor para o *@password* parâmetro que foi usado quando `sp_adddistributor` o foi executado inicialmente no distribuidor.  
  
  
