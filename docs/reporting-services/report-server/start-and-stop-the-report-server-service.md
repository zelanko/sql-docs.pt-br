---
title: "Iniciar e parar o servi&#231;o Servidor de Relat&#243;rio | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "parando o serviço Servidor de Relatório"
  - "Serviço Windows Servidor de Relatórios, iniciando"
  - "serviço Servidor de Relatório, iniciando"
  - "iniciando o serviço Servidor de Relatório"
ms.assetid: 6ec69ac3-27b0-472d-91e1-733af9078ed2
caps.latest.revision: 55
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 55
---
# Iniciar e parar o servi&#231;o Servidor de Relat&#243;rio
  O servidor de relatório é implementado como um serviço do Windows que contém o serviço Web do servidor de relatório, o Gerenciador de Relatórios e um aplicativo executado em segundo plano. O serviço deve ser executado se você desejar usar alguma funcionalidade do servidor de relatório. Parar o serviço para todas as operações do servidor de relatório.  
  
 Enquanto o serviço está parado, as solicitações para o relatório agendado e o processamento de assinaturas que teria ocorrido caso o serviço fosse executado são adicionados à fila. Isso ocorre porque os trabalhos que são executados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent criam os eventos. Se desejar evitar operações pendentes enquanto o serviço está desabilitado, pare o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent também.  
  
 Você pode usar uma variedade de ferramentas para iniciar ou parar o serviço de Servidor de Relatório, incluindo a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager e a ferramenta Serviços fornecida no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 Se estiver fazendo mais do que iniciar ou parar o serviço, como alterar a conta de serviço, use a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . O uso de outras ferramentas para alterar a conta de serviço pode romper a instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações, veja [Configurar a conta de serviço do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md).  
  
 Você não pode pausar e retomar o serviço. Não há nenhum parâmetro de início. Embora não haja nenhuma dependência explícita, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deverá estar em execução se você der suporte a assinaturas ou operações de relatório agendadas no servidor de relatório.  
  
### Para iniciar ou parar o serviço usando a ferramenta Configuração do Reporting Services  
  
1.  Inicie a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e conecte-se ao servidor de relatório.  
  
2.  Na página Status do Servidor de Relatórios, clique em **Parar** ou **Iniciar**.  
  
### Para iniciar ou parar o serviço usando Serviços em Ferramentas Administrativas  
  
-   Em Ferramentas Administrativas, abra Serviços, clique com o botão direito do mouse em **SQL Server Reporting Services (MSSQLSERVER)** e clique em **Parar** ou **Reiniciar**.  
  
 Se estiver executando várias instâncias ou se o servidor de relatório for executado como uma instância nomeada, verifique se o nome da instância entre parênteses corresponde à instância do servidor de relatório que deseja parar ou reiniciar.  
  
### Para iniciar ou parar o serviço usando o SQL Server Configuration Manager  
  
1.  Inicie o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.  
  
2.  Selecione SQL Server Services, clique com o botão direito do mouse em **SQL Server Reporting Services** e clique em **Parar** ou **Reiniciar**.  
  
## Consulte também  
 [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Iniciar, parar ou pausar o serviço do SQL Server Agent](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
  