---
description: Pasta do Instantâneo
title: Pasta de instantâneo | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.replicationutilities.specifysnapshotfolder.f1
ms.assetid: 3eb1b73f-ddb3-4d09-be6e-811c414698e9
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: c754399380dfac4b267e4ff9c816ef2dc4e9f81f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420360"
---
# <a name="snapshot-folder"></a>Pasta do Instantâneo
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

A página **Pasta do Instantâneo** aparece no Assistente para Configurar a Distribuição e no Assistente para Nova Publicação. O local especificado para a pasta do instantâneo será usado como padrão para todos os Publicadores habilitados nesse assistente (a pasta de instantâneo padrão não se aplica a Publicadores posteriormente habilitados usando a caixa de diálogo **Propriedades do Distribuidor** ). Você pode substituir esse padrão por qualquer Publicador na página **Publicadores** do Assistente para Configurar a Distribuição da caixa de diálogo **Propriedades do Distribuidor** .  
  
A pasta de instantâneo é simplesmente um diretório que você designou como um compartilhamento, agentes que leem essa pasta e gravam nela devem ter permissões suficientes para acessá-la. Para obter mais informações sobre como proteger a pasta adequadamente, consulte [Secure the Snapshot Folder](../../relational-databases/replication/security/secure-the-snapshot-folder.md) (Proteger a pasta de instantâneo). Antes de implementar replicação, teste se os agentes de replicação poderão se conectar à pasta de instantâneo. Faça logon na conta que será usada por cada agente e depois tente acessar a pasta de instantâneo.  

Para a Instância Gerenciada de SQL do Azure, a pasta de instantâneo precisa ser um compartilhamento de arquivo do Azure. 
  
## <a name="options"></a>Opções  
 **Pasta do instantâneo**  
 Insira o caminho para a pasta onde você quer arquivos de instantâneo sejam armazenados.  
  
> [!NOTE]  
> A[!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que você use um compartilhamento de rede como um local de pasta de instantâneo. Caminhos locais (os que iniciam com uma letra da unidade, como C:\\) não são acessíveis a agentes em outros computadores.  
  
## <a name="see-also"></a>Consulte Também  
 [Modificar opções de instantâneo](../../relational-databases/replication/snapshot-options.md)   
 [Configurar Distribuição](../../relational-databases/replication/configure-distribution.md)   
 [Configurar a publicação e a distribuição](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Exibir e modificar propriedades de Publicador e Distribuidor](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Inicializar uma assinatura com um instantâneo](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
