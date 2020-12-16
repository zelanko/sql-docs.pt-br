---
description: MSSQL_ENG021330
title: MSSQL_ENG021330 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021330 error
ms.assetid: e2bb2e21-62a7-4689-b68b-bdfba3fdd985
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 0014faab340070eec24e7beb7cf899b0b6d5eada
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97469097"
---
# <a name="mssql_eng021330"></a>MSSQL_ENG021330
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|21330|  
|Origem do Evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Falha ao criar um subdiretório no diretório de trabalho da replicação.(% ls)|  
  
## <a name="explanation"></a>Explicação  
 Esse erro pode ocorrer quando uma assinatura é inicializada manualmente e ocorre um problema ao criar o diretório em que os scripts de replicação são armazenados. O erro pode ser causado por um problema de permissão: quando uma assinatura é inicializada sem o uso de um instantâneo, a conta na qual o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executado no Publicador deve ter permissões de gravação na pasta do instantâneo no Distribuidor.  
  
## <a name="user-action"></a>Ação do usuário  
 Certifique-se de que o caminho correto foi especificado para a pasta do instantâneo e que a conta em que o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executado no Publicador tem permissões adequadas.  
  
## <a name="see-also"></a>Consulte Também  
 [Modificar opções de instantâneo](../../relational-databases/replication/snapshot-options.md)   
 [Referência de erros e eventos &#40;Replicação&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Inicializar uma assinatura transacional sem um instantâneo](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  
