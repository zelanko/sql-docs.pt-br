---
title: Pasta de instantâneo | Microsoft Docs
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.replicationutilities.specifysnapshotfolder.f1
ms.assetid: 3eb1b73f-ddb3-4d09-be6e-811c414698e9
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 48b490c65662edf65018e98dd1bc3339f6aae6b6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055617"
---
# <a name="snapshot-folder"></a>Pasta do Instantâneo
  A página **Pasta do Instantâneo** aparece no Assistente para Configurar a Distribuição e no Assistente para Nova Publicação. O local especificado para a pasta do instantâneo será usado como padrão para todos os Publicadores habilitados nesse assistente (a pasta de instantâneo padrão não se aplica a Publicadores posteriormente habilitados usando a caixa de diálogo **Propriedades do Distribuidor** ). Você pode substituir esse padrão por qualquer Publicador na página **Publicadores** do Assistente para Configurar a Distribuição da caixa de diálogo **Propriedades do Distribuidor** .  
  
 A pasta de instantâneo é simplesmente um diretório que você designou como um compartilhamento, agentes que leem essa pasta e gravam nela devem ter permissões suficientes para acessá-la. Para obter mais informações sobre como proteger a pasta adequadamente, consulte [Secure the Snapshot Folder](security/secure-the-snapshot-folder.md) (Proteger a pasta de instantâneo). Antes de implementar replicação, teste se os agentes de replicação poderão se conectar à pasta de instantâneo. Faça logon na conta que será usada por cada agente e depois tente acessar a pasta de instantâneo.  
  
## <a name="options"></a>Opções  
 **Pasta do instantâneo**  
 Insira o caminho para a pasta onde você quer arquivos de instantâneo sejam armazenados.  
  
> [!NOTE]  
>  A[!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que você use um compartilhamento de rede como um local de pasta de instantâneo. Caminhos locais (os que iniciam com uma letra da unidade, como C:\\) não são acessíveis a agentes em outros computadores.  
  
## <a name="see-also"></a>Consulte Também  
 [Locais de pastas de instantâneos alternativos](alternate-snapshot-folder-locations.md)   
 [Configurar a distribuição](configure-distribution.md)   
 [Configurar a publicação e a distribuição](configure-publishing-and-distribution.md)   
 [Exibir e modificar as propriedades do distribuidor e do Publicador](view-and-modify-distributor-and-publisher-properties.md)   
 [Inicializar uma assinatura com um instantâneo](initialize-a-subscription-with-a-snapshot.md)  
  
  
