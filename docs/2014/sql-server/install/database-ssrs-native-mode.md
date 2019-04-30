---
title: Banco de dados (modo nativo do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.databasesetup.F1
ms.assetid: 8c9bb3b3-ea77-4a5b-ba35-7451ed11083d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: d79b50e70f3eae3d9183ae220002136b39717e46
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63278557"
---
# <a name="database-ssrs-native-mode"></a>Banco de dados (modo nativo do SSRS)
  Use a página Banco de Dados para criar e configurar os bancos de dados do servidor de relatório que fornecem armazenamento interno para uma ou mais instâncias do servidor de relatório. Se você estiver configurando um servidor de relatório para usar um banco de dados de servidor de relatório remoto, deverá usar o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para criar o banco de dados.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 A criação de um banco de dados de servidor de relatório e a configuração da conexão são um processo de várias etapas. Para orientá-lo pelas etapas, esta página fornece Assistentes para cada tipo de tarefa. As permissões e logons são criados ou atualizados para você. Você pode monitorar o status de cada etapa na página Progresso. Se ocorrer um erro, você poderá clicar no erro para obter informações sobre como resolvê-lo.  
  
 Um banco de dados de servidor de relatório deve dar suporte a um modo de servidor específico. O modo padrão é o modo nativo, mas você também pode criar um banco de dados de servidor de relatório para o modo integrado do SharePoint se estiver executando um servidor de relatório em uma implantação maior de um produto ou tecnologia do SharePoint. Para obter mais informações, consulte [Criar um banco de dados de servidor de relatório no modo nativo &#40;Gerenciador de Configurações do SSRS&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md).  
  
 Para abrir essa página, inicie o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e clique em **Banco de Dados** no painel de navegação. Para obter mais informações, consulte [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="options"></a>Opções  
 **SQL Server Name**  
 Em Banco de Dados do Servidor de Relatório Atual, o **Nome do SQL Server** especifica o nome do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] que executa o banco de dados do servidor de relatório. Não é possível usar uma instância nomeada ou padrão em um computador local ou remoto.  
  
 **Database Name**  
 Especifica o nome do banco de dados do servidor de relatório que armazena dados do servidor.  
  
 **Modo de servidor de relatório**  
 Indica se o banco de dados do servidor de relatório dá suporte ao modo nativo ou ao modo integrado do SharePoint. Para obter mais informações, consulte [servidor de relatório do Reporting Services](../../../2014/reporting-services/reporting-services-report-server.md).  
  
 **Alterar banco de dados**  
 Inicia um assistente que orienta você durante todas as etapas necessárias para a criação ou a seleção de um banco de dados de servidor de relatório.  
  
 **Tipo de credencial**  
 Especifica credenciais que o servidor de relatório usa para conectar-se ao banco de dados do servidor de relatório. Os tipos de credencial que podem ser especificados incluem a conta de serviço, um usuário de domínio do Windows, o usuário local do Windows ou o logon do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações sobre como selecionar credenciais, consulte [configurar uma Conexão de banco de dados do servidor de relatório &#40;Configuration Manager do SSRS&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
 **Nome do Usuário**  
 Especifica uma conta de usuário de domínio se você estiver usando credenciais do Windows, ou um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se você estiver usando credenciais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se você estiver usando as credenciais do Windows, especifique-os neste formato:  *\<domínio >\\< conta\>*.  
  
 **Senha**  
 Especifica a senha para a conta.  
  
 **Alterar credenciais**  
 Inicia um assistente que o orienta por todas as etapas necessárias para a seleção de uma conta diferente ou a atualização da senha na conta usada para conectar ao banco de dados do servidor de relatório.  
  
## <a name="see-also"></a>Consulte também  
 [Criar um banco de dados de servidor de relatório do modo nativo &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [Tópicos de Ajuda F1 do Configuration Manager do Reporting Services &#40;modo nativo do SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Banco de dados do servidor de relatório &#40;modo nativo do SSRS&#41;](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
 [Configurar uma conexão de banco de dados do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
  
  
