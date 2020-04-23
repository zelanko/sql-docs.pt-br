---
title: Informações do servidor Web | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.webserverinformation.f1
ms.assetid: 86d72275-45c7-459f-98cf-f5a366ed279c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: bebf91748c10f1b33c199c3afc227cb8f16b4f88
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81529170"
---
# <a name="web-server-information"></a>Informações do Servidor Web
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  As informações do servidor Web são necessárias ao usar a opção de sincronização da Web para replicação de mesclagem. Para obter mais informações sobre como configurar a sincronização da Web, consulte [Configurar sincronização da Web](../../relational-databases/replication/configure-web-synchronization.md).  
  
## <a name="options"></a>Opções  
 **Endereço do servidor Web**  
 Se tiver especificado um endereço do servidor Web na página **Instantâneo de FTP e Internet** da caixa de diálogo **Propriedades de Publicação**, ele será exibido nessa caixa de texto como padrão. Aceite o padrão ou insira um endereço do servidor Web completamente qualificado para o servidor IIS (Serviços de Informações da Internet) da [!INCLUDE[msCoName](../../includes/msconame-md.md)] que sincroniza com essa assinatura.  
  
 **Como cada Assinante se conectará ao servidor Web?**  
 Especifique o tipo de autenticação usado para conexão com o servidor Web. Recomendamos o uso da Autenticação Básica para conexões com o servidor IIS junto com o protocolo TSL, conhecido anteriormente como protocolo SSL. Se você selecionar Autenticação Básica, insira o logon e a senha que serão usados para conexão do Assinante com o servidor IIS.  
  
## <a name="see-also"></a>Consulte Também  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Exibir e modificar propriedades de assinatura pull](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [Sincronização da Web para replicação de mesclagem](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
