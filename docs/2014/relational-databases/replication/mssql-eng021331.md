---
title: MSSQL_ENG021331 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021331 error
ms.assetid: 9acd75d9-fda1-44cd-ba17-20295ad53ea0
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 63becb9b07114b6e0ae0589664ae80d82f8babb2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63023382"
---
# <a name="mssql_eng021331"></a>MSSQL_ENG021331
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|21331|  
|Origem do Evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Falha ao copiar o arquivo de script de usuário para o Distribuidor.(% ls)|  
  
## <a name="explanation"></a>Explicação  
 Esse erro pode ocorrer quando uma assinatura é inicializada manualmente e não é possível salvar os scripts gerados por replicação, ou especificados em um comando de replicação, no diretório especificado. O erro pode ser causado por um problema de permissão: quando uma assinatura é inicializada sem o uso de um instantâneo, a conta na qual o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executado no Publicador deve ter permissões de gravação na pasta do instantâneo no Distribuidor.  
  
## <a name="user-action"></a>Ação do usuário  
 Certifique-se de que o caminho correto foi especificado para a pasta do instantâneo e que a conta em que o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executado no Publicador tem permissões adequadas.  
  
## <a name="see-also"></a>Consulte Também  
 [Especificar o local do instantâneo padrão](snapshot-options.md#snapshot-folder-locations)   
 [Referência de erros e eventos &#40;Replicação&#41;](errors-and-events-reference-replication.md)   
 [Inicializar uma assinatura transacional sem um instantâneo](initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  
