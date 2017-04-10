---
title: "Informa&#231;&#245;es do Servidor Web | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newsubwizard.webserverinformation.f1"
ms.assetid: 86d72275-45c7-459f-98cf-f5a366ed279c
caps.latest.revision: 19
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 19
---
# Informa&#231;&#245;es do Servidor Web
  As informações do servidor Web são necessárias ao usar a opção de sincronização da Web para replicação de mesclagem. Para obter informações sobre como configurar a sincronização da Web, consulte [Configurar sincronização da Web](../../relational-databases/replication/configure-web-synchronization.md).  
  
## Opções  
 **Endereço do servidor Web**  
 Se você especificou um endereço de servidor Web no **instantâneo de FTP andInternet** página do **Propriedades de publicação** caixa de diálogo, ele aparece na caixa de texto como padrão. Aceite o padrão ou insira um endereço do servidor Web completamente qualificado para o servidor IIS (Serviços de Informações da Internet) da [!INCLUDE[msCoName](../../includes/msconame-md.md)] que sincroniza com essa assinatura.  
  
 **Como cada Assinante se conectará ao servidor Web?**  
 Especifique o tipo de autenticação usado para conexão com o servidor Web. Recomendamos o uso da Autenticação Básica para conexões com o servidor IIS junto com o SSL (Secure Sockets Layer). Se você selecionar Autenticação Básica, insira o logon e a senha que serão usados para conexão do Assinante com o servidor IIS.  
  
## Consulte também  
 [Criar uma assinatura pull](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Exibir e modificar propriedades de assinatura pull](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [Assinantes não SQL Server](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)   
 [Sincronização da Web para replicação de mesclagem.](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  