---
title: Informações do servidor Web | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.webserverinformation.f1
ms.assetid: 86d72275-45c7-459f-98cf-f5a366ed279c
caps.latest.revision: 18
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a6fce5e9b805927e0222516a6b53a5a2382a0a31
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37199006"
---
# <a name="web-server-information"></a>Informações do Servidor Web
  As informações do servidor Web são necessárias ao usar a opção de sincronização da Web para replicação de mesclagem. Para obter mais informações sobre como configurar a sincronização da Web, consulte [Configurar sincronização da Web](configure-web-synchronization.md).  
  
## <a name="options"></a>Opções  
 **Endereço do servidor Web**  
 Se tiver especificado um endereço do servidor Web na página **Instantâneo de FTP e Internet** da caixa de diálogo **Propriedades de Publicação**, ele será exibido nessa caixa de texto como padrão. Aceite o padrão ou insira um endereço do servidor Web completamente qualificado para o servidor IIS (Serviços de Informações da Internet) da [!INCLUDE[msCoName](../../includes/msconame-md.md)] que sincroniza com essa assinatura.  
  
 **Como cada Assinante se conectará ao servidor Web?**  
 Especifique o tipo de autenticação usado para conexão com o servidor Web. Recomendamos o uso da Autenticação Básica para conexões com o servidor IIS junto com o SSL (Secure Sockets Layer). Se você selecionar Autenticação Básica, insira o logon e a senha que serão usados para conexão do Assinante com o servidor IIS.  
  
## <a name="see-also"></a>Consulte também  
 [Create a Pull Subscription](create-a-pull-subscription.md)   
 [Exibir e modificar propriedades de assinatura pull](view-and-modify-pull-subscription-properties.md)   
 [Assinantes Não SQL Server](non-sql/non-sql-server-subscribers.md)   
 [Subscribe to Publications](subscribe-to-publications.md)   
 [Sincronização da Web para replicação de mesclagem](web-synchronization-for-merge-replication.md)  
  
  
