---
description: Informações do Servidor Web
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
ms.openlocfilehash: 7ba110489a2ec2623018563257953d764ef371c2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88325954"
---
# <a name="web-server-information"></a>Informações do Servidor Web
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
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
  
  
