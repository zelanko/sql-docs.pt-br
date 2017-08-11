---
title: "Hospedar um banco de dados do servidor de relatório em um Cluster de Failover do SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 03/30/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7bd5f019-2857-452f-a023-cc3b9e93aec4
caps.latest.revision: 5
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b14768db398059289f280ca610c8b93ca95c468f
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="host-a-report-server-database-in-a-sql-server-failover-cluster"></a>Hospedar um banco de dados do servidor de relatório em um cluster de failover do SQL Server
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]oferece suporte a cluster para que você pode usar vários discos para uma ou mais de failover [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instâncias. O clustering de failover tem suporte somente para o banco de dados do servidor de relatório; não é possível executar o serviço Servidor de Relatório como parte de um cluster de failover.  
  
 Para hospedar um banco de dados do servidor de relatório em um cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o cluster já deve estar instalado e configurado. Você pode selecionar o cluster de failover como o nome do servidor ao criar o banco de dados do servidor de relatório na página Configuração do Banco de Dados da ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Embora o serviço Servidor de Relatório não possa participar de um cluster de failover, é possível instalar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em um computador que tenha um cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado. O servidor de relatório é executado de maneira independente do cluster de failover. Se você instalar um servidor de relatório em um computador que tenha uma instância de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , não será preciso usar o cluster de failover para o banco de dados do servidor de relatório; você poderá usar outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para hospedar o banco de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Banco de dados de servidor de relatório &#40; Modo nativo do SSRS &#41;](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
 [Criar um banco de dados do servidor de relatório &#40; Gerenciador de configurações do SSRS &#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)  
  
  

