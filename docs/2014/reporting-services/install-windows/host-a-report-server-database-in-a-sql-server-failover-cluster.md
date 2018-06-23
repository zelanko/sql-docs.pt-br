---
title: Hospedar um banco de dados do servidor de relatório em um cluster de failover do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7bd5f019-2857-452f-a023-cc3b9e93aec4
caps.latest.revision: 4
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: d2a0a0fc008c2bdb08786d7cf32f76310f259b6d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008566"
---
# <a name="host-a-report-server-database-in-a-sql-server-failover-cluster"></a>Hospedar um banco de dados do servidor de relatório em um cluster de failover do SQL Server
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte de clustering de failover, permitindo o uso de vários discos para uma ou mais instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O clustering de failover tem suporte somente para o banco de dados do servidor de relatório; não é possível executar o serviço Servidor de Relatório como parte de um cluster de failover.  
  
 Para hospedar um banco de dados do servidor de relatório em um cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o cluster já deve estar instalado e configurado. Você pode selecionar o cluster de failover como o nome do servidor ao criar o banco de dados do servidor de relatório na página Configuração do Banco de Dados da ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Embora o serviço Servidor de Relatório não possa participar de um cluster de failover, é possível instalar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em um computador que tenha um cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado. O servidor de relatório é executado de maneira independente do cluster de failover. Se você instalar um servidor de relatório em um computador que tenha uma instância de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , não será preciso usar o cluster de failover para o banco de dados do servidor de relatório; você poderá usar outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para hospedar o banco de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Banco de dados do servidor de relatório &#40;modo nativo do SSRS&#41;](../report-server/report-server-database-ssrs-native-mode.md)   
 [Criar um banco de dados do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)  
  
  