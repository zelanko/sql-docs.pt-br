---
title: As propriedades de navegador do SQL Server (guia Avançado) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: configuration-manager
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ba79137a-cb72-4bf3-a650-e11d02cfce10
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5017cfa180e81bc0b20b3cd115504a99436bba7b
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MTE
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="sql-server-browser-properties-advanced-tab"></a>Propriedades do Navegador do SQL Server (guia Avançado)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
O programa Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executado como um serviço no servidor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escuta as solicitações de entrada de recursos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e fornece informações sobre as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas no computador.  
  
## <a name="options"></a>Opções  
 **Clusterizado**  
 Indica se este serviço for instalado como um recurso de um servidor clusterizado.  
  
 **Relatório de Comentários do Cliente**  
 Indica se o Monitoramento da Qualidade do Serviço foi habilitado neste serviço. Para obter mais informações sobre o Relatório de Comentários do Cliente, pesquise "Configurações de relatório de erro e uso" nos Manuais Online.  
  
 **Diretório de Despejo**  
 O local em que os despejos de memória são colocadas no caso de um erro.  
  
 **Relatório de Erros**  
 Quando definido como **Sim**, o programa Dr. Watson encaminhará informações para a [!INCLUDE[msCoName](../../includes/msconame-md.md)] ou para o servidor de erro, se ocorrer uma falha grave. Para obter mais informações sobre o Relatório de Erros, pesquise "Configurações de relatório de erro e uso" nos Manuais Online.  
  
 **ID da Instância**  
 Indica a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usou essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. A instância padrão é **MSSQL10_50.MSSQLSERVER**.  
  
## <a name="see-also"></a>Consulte Também  
 [Serviço Navegador do SQL Server](../../tools/configuration-manager/sql-server-browser-service.md)  
  
  
