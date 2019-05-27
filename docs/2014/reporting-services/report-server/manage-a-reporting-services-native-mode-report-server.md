---
title: Gerenciar um servidor de relatório no modo nativo do Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services Configuration tool
- configuration options [Reporting Services]
- report servers [Reporting Services], configuring
ms.assetid: 6ca03a09-d6a8-4c93-ba12-1c99dcbfb618
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: da2eb97e5ce57a2e6a82dda3e264b33e1e3a3b11
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66103787"
---
# <a name="manage-a-reporting-services-native-mode-report-server"></a>Gerenciar um servidor de relatório de modo nativo do Reporting Services
  Esta seção contém procedimentos para a configuração de uma instância do servidor de relatório de modo nativo usando o Gerenciador de Configurações do Reporting Services.  
  
## <a name="in-this-section"></a>Nesta seção  
 Os tópicos desta seção estão organizados em categorias para que seja possível localizar mais facilmente as instruções desejadas. A primeira seção contém tópicos para tarefas de configuração básica para um servidor de relatório no modo nativo. A segunda seção contém tópicos de configuração avançada. A terceira seção contém tópicos para configuração de um servidor de relatório para execução no modo integrado do SharePoint.  
  
### <a name="basic-configuration"></a>Configuração básica  
 [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
 Fornece etapas para iniciar a ferramenta Configuração do Reporting Services.  
  
 [Configurar uma conta de serviço &#40;SSRS Configuration Manager&#41;](../../sql-server/install/configure-a-service-account-ssrs-configuration-manager.md)  
 Explica como especificar informações de conta e senha para o serviço Servidor de Relatório.  
  
 [Registrar um SPN &#40;Nome da Entidade de Serviço&#41; para um servidor de relatório](register-a-service-principal-name-spn-for-a-report-server.md)  
 Explica como registrar manualmente um SPN para um servidor de relatório executado em uma conta de usuário de domínio em uma rede que use autenticação Kerberos.  
  
 [Configurar uma URL &#40;SSRS Configuration Manager&#41;](../install-windows/configure-a-url-ssrs-configuration-manager.md)  
 Explica como estabelecer uma ou mais URLs usadas para acessar o serviço Web Servidor de Relatórios e o Gerenciador de Relatórios.  
  
 [Criar um banco de dados de servidor de relatório do modo nativo &#40;SSRS Configuration Manager&#41;](../install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)  
 Fornece etapas para a criação de um banco de dados do servidor de relatório. Essa etapa é necessária para a implantação de uma instalação do Reporting Services.  
  
### <a name="advanced-or-optional-configuration"></a>Configuração avançada ou opcional  
 [Configurar uma implantação de expansão do servidor de relatório no modo nativo &#40;Gerenciador de configurações do SSRS&#41;](../install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)  
 Fornece etapas para a configuração de vários servidores de relatório para compartilhar um banco de dados do servidor de relatório.  
  
 [Configurar um servidor de relatório para entrega de email &#40;Configuration Manager do SSRS&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)  
 Fornece etapas para a configuração de um servidor de relatório para distribuição de email.  
  
 [Configurar um firewall para acesso ao servidor de relatório](configure-a-firewall-for-report-server-access.md)  
 Explica como abrir as portas usadas para solicitações de entrada e respostas de saída de um servidor de relatório.  
  
 [Configurar um servidor de relatório no modo nativo para a Administração Local &#40;SSRS&#41;](configure-a-native-mode-report-server-for-local-administration-ssrs.md)  
 Descreve as etapas adicionais necessárias para conexão com o Gerenciador de Relatórios ou com um servidor de relatório usando http://localhost.  
  
 [Configurar um servidor de relatório para administração remota](configure-a-report-server-for-remote-administration.md)  
 Explica como configurar uma instância do servidor de relatório remoto para que seja possível conectar e configurá-la a partir de um computador diferente.  
  
 [Ativar e desativar recursos do Reporting Services](turn-reporting-services-features-on-or-off.md)  
 Explica como remover recursos não usados em uma instalação do Reporting Services.  
  
 [Habilitar erros remotos &#40;Reporting Services&#41;](enable-remote-errors-reporting-services.md)  
 Explica como definir as propriedades do servidor em um servidor de relatório para retornar informações adicionais sobre condições de erros que ocorrem em servidores remotos.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar e administrar um servidor de relatório &#40;modo nativo do SSRS&#41;](configure-and-administer-a-report-server-ssrs-native-mode.md)   
 [Configuração e administração de um servidor de relatórios &#40;modo do SharePoint do Reporting Services&#41;](../configure-administer-report-server-reporting-services-sharepoint-mode.md)  
  
  
