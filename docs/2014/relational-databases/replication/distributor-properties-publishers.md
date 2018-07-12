---
title: Propriedades do distribuidor, Publicadores | Microsoft Docs
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.rep.configdistwizard.distproperties.publishers.f1
helpviewer_keywords:
- Distributor Properties dialog box
ms.assetid: 31c81898-11ca-4d2f-afea-2fbc71e19ce4
caps.latest.revision: 20
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 32e2801e45c9d7e227be8fe067062da9eb3f4eea
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37162187"
---
# <a name="distributor-properties-publishers"></a>Propriedades do Distribuidor, Publicadores
  A página **Publicadores** da caixa de diálogo **Propriedades do Distribuidor** permite habilitar Publicadores a usarem esse Distribuidor. Você também pode definir propriedades associadas a esses Publicadores. Esteja ciente de que habilitar um Publicador a usar esse servidor como seu Distribuidor remoto não faz daquele servidor um Publicador. Você deve se conectar ao Publicador, configurá-lo para publicação e escolher esse servidor como o Distribuidor. Você pode configurar o Publicador e escolher um Distribuidor pelo Assistente para Nova Publicação.  
  
## <a name="options"></a>Opções  
 **Publicadores**  
 Selecione os servidores que têm permissão para usar esse Distribuidor. Clique no botão **(...)** próximo ao Publicador para exibir e definir propriedades adicionais.  
  
 **Adicionar**  
 Se o servidor que você deseja permitir não estiver na lista, clique em **Adicionar** para adicionar um Editor [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou um Editor Oracle à lista de Publicadores disponíveis. Se o servidor que você adicionar for o primeiro a usar esse Distribuidor como remoto, você será solicitado a fornecer uma senha de vínculo administrativo.  
  
 **Senha de vínculo administrativo**  
 Use para especificar ou atualizar a senha para a conexão que a replicação faz entre o Publicador e o Distribuidor remoto, usando o logon: **distributor_admin** .  
  
-   Se o  Distribuidor servir somente como Distribuidor local, essa senha será gerada aleatoriamente e configurada automaticamente.  
  
-   Se o Distribuidor já tiver um Publicador remoto, uma senha terá sido fornecida inicialmente nessa página ou na página **Senha do Distribuidor** do Assistente para Configurar Distribuição.  
  
-   Se você ativar o primeiro Publicador remoto para esse Distribuidor, você será solicitado a inserir uma senha.  
  
 Para mais informações sobre segurança de distribuidores, consulte [Proteger o distribuidor](security/secure-the-distributor.md).  
  
## <a name="see-also"></a>Consulte também  
 [Configurar Distribuição](configure-distribution.md)   
 [Configurar a publicação e a distribuição](configure-publishing-and-distribution.md)   
 [Create a Publication](publish/create-a-publication.md)   
 [Exibir e modificar propriedades de Publicador e Distribuidor](view-and-modify-distributor-and-publisher-properties.md)  
  
  
