---
description: Hospedar um banco de dados do servidor de relatório em um cluster de failover do SQL Server
title: Hospedar um banco de dados do servidor de relatório em um cluster de failover do SQL Server | Microsoft Docs
ms.date: 03/30/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
ms.assetid: 7bd5f019-2857-452f-a023-cc3b9e93aec4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1bceb380b1c21f717ba6e20fd6a41c78cc393dba
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492661"
---
# <a name="host-a-report-server-database-in-a-sql-server-failover-cluster"></a>Hospedar um banco de dados do servidor de relatório em um cluster de failover do SQL Server
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte de clustering de failover, permitindo o uso de vários discos para uma ou mais instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O clustering de failover tem suporte somente para o banco de dados do servidor de relatório; não é possível executar o serviço Servidor de Relatório como parte de um cluster de failover.  
  
 Para hospedar um banco de dados do servidor de relatório em um cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o cluster já deve estar instalado e configurado. Você pode selecionar o cluster de failover como o nome do servidor ao criar o banco de dados do servidor de relatório na página Configuração do Banco de Dados da ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Embora o serviço Servidor de Relatório não possa participar de um cluster de failover, é possível instalar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em um computador que tenha um cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado. O servidor de relatório é executado de maneira independente do cluster de failover. Se você instalar um servidor de relatório em um computador que tenha uma instância de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , não será preciso usar o cluster de failover para o banco de dados do servidor de relatório; você poderá usar outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para hospedar o banco de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Banco de dados do servidor de relatório &#40;modo nativo do SSRS&#41;](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
 [Criar um banco de dados do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)  
  
  
