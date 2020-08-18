---
description: MSSQLSERVER_21871
title: MSSQLSERVER_21871 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 21871 (Database Engine error)
ms.assetid: d3215378-9282-444f-a18b-00b96fd0133d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 52f82fbebc9f164152f6047a90bbb1238e1a2bb7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88332782"
---
# <a name="mssqlserver_21871"></a>MSSQLSERVER_21871
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|21871|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQLErrorNum21871|  
|Texto da mensagem|O publicador %s do banco de dados %s não foi redirecionado.|  
  
## <a name="explanation"></a>Explicação  
**sp_validate_replica_hosts_as_publishers** verifica a tabela MSredirected_publishers no banco de dados de distribuição em busca de uma entrada para o publicador identificado e o banco de dados publicador.  **sp_validate_replica_hosts_as_publishers** retorna o erro 21871 quando nenhuma entrada é encontrada.  
  
## <a name="user-action"></a>Ação do usuário  
**sp_validate_replica_hosts_as_publishers** só é relevante para publicadores redirecionados. Se o banco de dados publicador for membro de um grupo de disponibilidade, use o procedimento armazenado **sp_redirect_publisher** para associar o publicador e o banco de dados publicador ao Nome do Ouvinte do Grupo de Disponibilidade do grupo de disponibilidade.  
  
