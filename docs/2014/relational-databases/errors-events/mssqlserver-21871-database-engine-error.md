---
title: MSSQLSERVER_21871 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 21871 (Database Engine error)
ms.assetid: d3215378-9282-444f-a18b-00b96fd0133d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 197d485fe851298a8e8d365c9fd1a52bf1251101
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553452"
---
# <a name="mssqlserver_21871"></a>MSSQLSERVER_21871
    
## <a name="details"></a>Detalhes  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|21871|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQLErrorNum21871|  
|Texto da mensagem|O publicador %s do banco de dados %s não foi redirecionado.|  
  
## <a name="explanation"></a>Explicação  
 `sp_validate_replica_hosts_as_publishers`O  verifica a tabela MSredirected_publishers no banco de dados de distribuição à procura de uma entrada para o publicador identificado e o banco de dados publicador.  `sp_validate_replica_hosts_as_publishers` retorna o erro 21871 quando nenhuma entrada é encontrada.  
  
## <a name="user-action"></a>Ação do usuário  
 `sp_validate_replica_hosts_as_publishers` só é relevante para publicadores redirecionados. Se o banco de dados publicador for membro de um grupo de disponibilidade, use o procedimento armazenado `sp_redirect_publisher` para associar o publicador e o banco de dados publicador com o Nome do Ouvinte do Grupo de Disponibilidade do grupo de disponibilidade.  
  
  
