---
title: Banco de dados (modo nativo do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.databasesetup.F1
ms.assetid: 8c9bb3b3-ea77-4a5b-ba35-7451ed11083d
caps.latest.revision: 8
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 7bce0a9aa3adcddb7363224138a7ec3f51a47622
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37183933"
---
# <a name="database-ssrs-native-mode"></a>Banco de dados (modo nativo do SSRS)
  Use a página Banco de Dados para criar e configurar os bancos de dados do servidor de relatório que fornecem armazenamento interno para uma ou mais instâncias do servidor de relatório. Se você estiver configurando um servidor de relatório para usar um banco de dados do servidor de relatório remoto, você deve usar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager para criar o banco de dados.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 A criação de um banco de dados de servidor de relatório e a configuração da conexão são um processo de várias etapas. Para orientá-lo pelas etapas, esta página fornece Assistentes para cada tipo de tarefa. As permissões e logons são criados ou atualizados para você. Você pode monitorar o status de cada etapa na página Progresso. Se ocorrer um erro, você poderá clicar no erro para obter informações sobre como resolvê-lo.  
  
 Um banco de dados de servidor de relatório deve dar suporte a um modo de servidor específico. O modo padrão é o modo nativo, mas você também pode criar um banco de dados de servidor de relatório para o modo integrado do SharePoint se estiver executando um servidor de relatório em uma implantação maior de um produto ou tecnologia do SharePoint. Para obter mais informações, consulte [Criar um banco de dados de servidor de relatório no modo nativo &#40;Gerenciador de Configurações do SSRS&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md).  
  
 Para abrir essa página, inicie o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager e clique em **banco de dados** no painel de navegação. Para obter mais informações, consulte [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="options"></a>Opções  
 **Nome do SQL Server**  
 No banco de dados de servidor de relatório atual, **nome do SQL Server** Especifica o nome da [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] que executa o banco de dados do servidor de relatório. Não é possível usar uma instância nomeada ou padrão em um computador local ou remoto.  
  
 **Database Name**  
 Especifica o nome do banco de dados do servidor de relatório que armazena dados do servidor.  
  
 **Modo de servidor de relatório**  
 Indica se o banco de dados do servidor de relatório dá suporte ao modo nativo ou ao modo integrado do SharePoint. Para obter mais informações, consulte [servidor de relatório do Reporting Services](../../../2014/reporting-services/reporting-services-report-server.md).  
  
 **Alterar banco de dados**  
 Inicia um assistente que orienta você durante todas as etapas necessárias para a criação ou a seleção de um banco de dados de servidor de relatório.  
  
 **Tipo de credencial**  
 Especifica credenciais que o servidor de relatório usa para conectar-se ao banco de dados do servidor de relatório. Tipos de credencial, você pode especificar incluem a conta de serviço, um usuário de domínio do Windows, o usuário local do Windows, ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon de banco de dados. Para obter mais informações sobre como selecionar credenciais, consulte [configurar uma Conexão de banco de dados do servidor de relatório &#40;Configuration Manager do SSRS&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
 **Nome do Usuário**  
 Especifica uma conta de usuário de domínio, se você estiver usando credenciais do Windows ou um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon se você estiver usando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] credenciais. Se você estiver usando as credenciais do Windows, especifique-os neste formato:  *\<domínio >\\< conta\>*.  
  
 **Senha**  
 Especifica a senha para a conta.  
  
 **Alterar credenciais**  
 Inicia um assistente que o orienta por todas as etapas necessárias para a seleção de uma conta diferente ou a atualização da senha na conta usada para conectar ao banco de dados do servidor de relatório.  
  
## <a name="see-also"></a>Consulte também  
 [Criar um banco de dados de servidor de relatório do modo nativo &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [Tópicos de Ajuda F1 do Configuration Manager do Reporting Services &#40;modo nativo do SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Banco de dados do servidor de relatório &#40;modo nativo do SSRS&#41;](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
 [Configurar uma Conexão de banco de dados do servidor de relatório &#40;Configuration Manager do SSRS&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
  
  
