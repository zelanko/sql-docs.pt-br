---
title: Iniciar e parar o serviço do Servidor de Relatório | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-server
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- stopping Report Server service
- Report Server Windows service, starting
- Report Server service, starting
- starting Report Server service
ms.assetid: 6ec69ac3-27b0-472d-91e1-733af9078ed2
caps.latest.revision: 55
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 5a93f4759fb0c079b843235bd7fb0491fa802e95
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33026513"
---
# <a name="start-and-stop-the-report-server-service"></a>Iniciar e parar o serviço Servidor de Relatório
  O servidor de relatório é implementado como um serviço do Windows que contém o serviço Web do servidor de relatório, o Gerenciador de Relatórios e um aplicativo executado em segundo plano. O serviço deve ser executado se você desejar usar alguma funcionalidade do servidor de relatório. Parar o serviço para todas as operações do servidor de relatório.  
  
 Enquanto o serviço está parado, as solicitações para o relatório agendado e o processamento de assinaturas que teria ocorrido caso o serviço fosse executado são adicionados à fila. Isso ocorre porque os trabalhos que são executados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent criam os eventos. Se desejar evitar operações pendentes enquanto o serviço está desabilitado, pare o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent também.  
  
 Você pode usar uma variedade de ferramentas para iniciar ou parar o serviço de Servidor de Relatório, incluindo a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager e a ferramenta Serviços fornecida no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 Se estiver fazendo mais do que iniciar ou parar o serviço, como alterar a conta de serviço, use a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . O uso de outras ferramentas para alterar a conta de serviço pode romper a instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações, veja [Configurar a conta de serviço do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md).  
  
 Você não pode pausar e retomar o serviço. Não há nenhum parâmetro de início. Embora não haja nenhuma dependência explícita, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deverá estar em execução se você der suporte a assinaturas ou operações de relatório agendadas no servidor de relatório.  
  
### <a name="to-start-or-stop-the-service-using-the-reporting-services-configuration-tool"></a>Para iniciar ou parar o serviço usando a ferramenta Configuração do Reporting Services  
  
1.  Inicie a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e conecte-se ao servidor de relatório.  
  
2.  Na página Status do Servidor de Relatórios, clique em **Parar** ou **Iniciar**.  
  
### <a name="to-start-or-stop-the-service-using-services-in-administrative-tools"></a>Para iniciar ou parar o serviço usando Serviços em Ferramentas Administrativas  
  
-   Em Ferramentas Administrativas, abra Serviços, clique com o botão direito do mouse em **SQL Server Reporting Services (MSSQLSERVER)** e clique em **Parar** ou **Reiniciar**.  
  
 Se estiver executando várias instâncias ou se o servidor de relatório for executado como uma instância nomeada, verifique se o nome da instância entre parênteses corresponde à instância do servidor de relatório que deseja parar ou reiniciar.  
  
### <a name="to-start-or-stop-the-service-using-sql-server-configuration-manager"></a>Para iniciar ou parar o serviço usando o SQL Server Configuration Manager  
  
1.  Inicie o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.  
  
2.  Selecione SQL Server Services, clique com o botão direito do mouse em **SQL Server Reporting Services**e clique em **Parar** ou **Reiniciar**.  
  
## <a name="see-also"></a>Consulte Também  
 [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Iniciar, parar ou pausar o serviço do SQL Server Agent](http://msdn.microsoft.com/library/c95a9759-dd30-4ab6-9ab0-087bb3bfb97c)  
  
  
