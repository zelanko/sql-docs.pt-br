---
title: Propriedades da publicação, lista de acesso à publicação | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.pubproperties.publicationaccesslist.f1
ms.assetid: 9587bb9e-c66c-4e70-8171-09b943ec2d50
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a9e94541f6c71da9ac40ecd34aacb11d7392b2df
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48224146"
---
# <a name="publication-properties-publication-access-list"></a>Propriedades de Publicação, Lista de Acesso à Publicação
  A página **Lista de Acesso à Publicação** da caixa de diálogo **Propriedades de Publicação** permite adicionar e remover logons, contas e grupos da PAL (Lista de Acesso à Publicação). A PAL é o mecanismo primário de segurança do Publicador. Quando você cria uma publicação, a replicação cria uma PAL para a publicação. A PAL, cuja função é semelhante à lista de controle de acesso do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, contém uma lista de logons, contas e grupos com acesso garantido à publicação.  
  
 Quando um Assinante se conecta ao Publicador ou ao Distribuidor e solicita acesso à publicação, o logon do Assinante é comparado com as informações de autenticação na PAL. Isso fornece segurança adicional ao Publicador, impedindo que o logon do Publicador e do Distribuidor seja usado por uma ferramenta cliente para executar modificações no Publicador diretamente. Para obter mais informações, consulte [Secure the Publisher](security/secure-the-publisher.md) (Proteger o publicador).  
  
## <a name="options"></a>Opções  
 **Adicionar**  
 Adicione uma nova entrada à lista. Você só pode adicionar os nomes de logon, conta ou grupo já definidos no Publicador e no Distribuidor Eles serão definidos em ambos os servidores se as contas de domínio ou contas locais tiverem sido criadas em ambos.  
  
 **Remover**  
 Remova a entrada selecionada da lista.  
  
 **Remover Tudo**  
 Remova todas as entradas da lista.  
  
## <a name="see-also"></a>Consulte também  
 [Create a Publication](publish/create-a-publication.md)   
 [Exibir e modificar as propriedades da publicação](publish/view-and-modify-publication-properties.md)   
 [Publicar dados e objetos de banco de dados](publish/publish-data-and-database-objects.md)  
  
  
