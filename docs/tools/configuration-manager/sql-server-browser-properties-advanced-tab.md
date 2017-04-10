---
title: "Propriedades do Navegador do SQL Server (guia Avan&#231;ado) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ba79137a-cb72-4bf3-a650-e11d02cfce10
caps.latest.revision: 19
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 19
---
# Propriedades do Navegador do SQL Server (guia Avan&#231;ado)
  O programa Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executado como um serviço no servidor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escuta as solicitações de entrada de recursos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e fornece informações sobre as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas no computador.  
  
## Opções  
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
  
## Consulte também  
 [Serviço Navegador do SQL Server](../../tools/configuration-manager/sql-server-browser-service.md)  
  
  