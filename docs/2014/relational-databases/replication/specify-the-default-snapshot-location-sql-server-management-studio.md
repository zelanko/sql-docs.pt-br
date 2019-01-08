---
title: Especificar o local do instantâneo padrão (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], default locations
- default snapshot locations
ms.assetid: 27c5d9ad-a915-4c59-a8b7-82e3af61ac4d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cd41dabe1554bc3f80adc4fdb6d8433f8aac9e7f
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52807328"
---
# <a name="specify-the-default-snapshot-location-sql-server-management-studio"></a>Especificar o local do instantâneo padrão (SQL Server Management Studio)
  Especifique o local de instantâneo padrão na página **Pasta de Instantâneo** do Assistente para Configurar Distribuição. Para obter mais informações sobre como usar o assistente, consulte [Configurar a publicação e a distribuição](configure-publishing-and-distribution.md). Se você criar uma publicação em um servidor que não esteja configurada como Distributor, especifique um local de instantâneo padrão na página **Pasta de Instantâneo** do Assistente para Novas Publicações. Para obter mais informações sobre como usar esse assistente, consulte [Criar uma publicação](publish/create-a-publication.md).  
  
 Modifique o local do instantâneo padrão na página **Publicadores** da caixa de diálogo **Propriedades do Distribuidor – \<Distribuidor>**. Para obter mais informações, consulte [Exibir e modificar as propriedades do Distribuidor e do Publicador](view-and-modify-distributor-and-publisher-properties.md). Defina a pasta de instantâneo para cada publicação na caixa de diálogo **Propriedades da Publicação – \<Publicação>**. Para obter mais informações, consulte [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md).  
  
### <a name="to-modify-the-default-snapshot-location"></a>Para modificar o local do instantâneo padrão.  
  
1.  Na página **Publicadores** da caixa de diálogo **Propriedades do Distribuidor – \<Distribuidor>**, clique no botão de propriedades (**...**) para o Publicador para o qual você deseja alterar a localização do instantâneo padrão.  
  
2.  Na caixa de diálogo **Propriedades do Publicador – \<Publisher>**, digite um valor para a propriedade **Pasta de Instantâneo Padrão**.  
  
    > [!NOTE]  
    >  O Snapshot Agent deve ter permissões de gravação para o diretório que você especificar, e o Distribution Agent ou Merge Agent devem ter permissões de leitura. Se as assinaturas pull forem usadas, será necessário especificar um diretório compartilhado como um caminho UNC, como \\\computername\snapshot. Para obter mais informações, consulte [Proteger a pasta de instantâneos](security/secure-the-snapshot-folder.md).  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Locais da pasta de instantâneos alternativos](alternate-snapshot-folder-locations.md)   
 [Inicializar uma assinatura com um instantâneo](initialize-a-subscription-with-a-snapshot.md)  
  
  
