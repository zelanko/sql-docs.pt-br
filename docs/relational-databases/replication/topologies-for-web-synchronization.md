---
title: Topologias para sincronização da Web | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Web synchronization, topologies
- IIS server configuration [SQL Server replication]
ms.assetid: 59444faf-bcb6-4421-a3df-8715753e453b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8da7a2f89bbe0a63cb438b464a217805cfa97db6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85719504"
---
# <a name="topologies-for-web-synchronization"></a>Topologias para sincronização da Web
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Escolha uma opção entre uma variedade de topologias de replicação de sincronização da Web do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os modos comuns para configurar a sincronização da Web incluem:  
  
-   Servidor único  
  
-   Dois servidores  
  
-   Vários sistemas de Serviços de Informações da Internet (IIS) da [!INCLUDE[msCoName](../../includes/msconame-md.md)] e republicação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 Para obter mais informações sobre como configurar a sincronização da Web, consulte [Configurar sincronização da Web](../../relational-databases/replication/configure-web-synchronization.md).  
  
## <a name="single-server"></a>Servidor único  
 Na topologia mais simples, o IIS, o Editor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o Distribuidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] residem em um único servidor. Os assinantes sincronizam conectando-se ao IIS no Publicador. O Publicador pode ser localizado atrás de um firewall.  
  
> [!NOTE]  
>  Essa configuração só é recomendada para cenários de intranet. Para demais cenários, é recomendado que o servidor de IIS e o Publicador/Distribuidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estejam em computadores separados.  
  
 ![Sincronização da Web com um só servidor](../../relational-databases/replication/media/web-sync02.gif "Sincronização da Web com um só servidor")  
  
## <a name="two-servers"></a>Dois servidores  
 Você pode colocar o IIS em um servidor e configurar o Publicador e o Distribuidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em outro servidor. O servidor que executa o IIS pode ser isolado da Internet por um firewall. Os assinantes sincronizam conectando-se ao IIS.  
  
 ![Sincronização da Web com dois servidores](../../relational-databases/replication/media/web-sync03.gif "Sincronização da Web com dois servidores")  
  
## <a name="multiple-iis-systems-and-sql-server-republishing"></a>Vários sistemas ISS e republicação do SQL Server  
 Se precisar dar suporte a um grande número de Assinantes que sincronizam ao mesmo tempo, você pode particionar o trabalho em vários computadores executando o IIS.  
  
 ![Sincronização da Web com vários servidores IIS](../../relational-databases/replication/media/web-sync04.gif "Sincronização da Web com vários servidores IIS")  
  
 Se um equilíbrio de carga adicional for necessário no computador executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode criar uma hierarquia de republicação em vários computadores. O Publicador de alto nível publica dados aos Assinantes, que por sua vez publicam novamente os dados, equilibrando a carga das solicitações dos Assinantes.  
  
> [!NOTE]  
>  Assinantes só podem sincronizar com um Publicador específico. Por exemplo, um Assinante para o republicador A não pode sincronizar com o republicador B quando A não estiver disponível.  
  
 ![Sincronização da Web com republicação](../../relational-databases/replication/media/web-sync05.gif "Sincronização da Web com republicação")  
  
## <a name="see-also"></a>Consulte Também  
 [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md)   
 [Sincronização da Web para replicação de mesclagem](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
