---
title: "Funções-tarefas do Reporting Services versus Grupos-permissões do SharePoint | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- security [Reporting Services], tasks
- roles [Reporting Services], predefined
- SharePoint integration [Reporting Services], permissions
- permissions [Reporting Services], native mode
- security [Reporting Services], predefined roles
- security [Reporting Services], SharePoint integrated mode
ms.assetid: 429f1dbb-183a-4097-bd1b-693da9fe7a36
caps.latest.revision: "19"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: b1ac3cd31061a749a035c9f4feb6ceef8bdebcd3
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="reporting-services-roles-tasks-vs-sharepoint-groups-permissions"></a>Funções-tarefas do Reporting Services versus Grupos-permissões do SharePoint
  Este tópico compara recursos de autorização baseado em função e tarefas no modo nativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] com os recursos de segurança nos produtos do SharePoint. Este tópico compara a terminologia e as características de funções, tarefas, grupos do SharePoint, níveis de permissão e permissões.  
  
||  
|-|  
|[!INCLUDE[applies](../../includes/applies-md.md)]<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo do SharePoint &#124; SharePoint 2010 e SharePoint 2013<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo nativo|  
  
 **Neste tópico:**  
  
-   [Comparar ferramentas de permissão e terminologia](#bkmk_compare_tools_terms)  
  
-   [Comparar funções do modo nativo e grupos do SharePoint](#bkmk_compare_roles_groups)  
  
-   [Comparando tarefas do modo nativo e permissões do SharePoint](#bkmk_compare_tasks_permissions)  
  
##  <a name="bkmk_compare_tools_terms"></a> Comparar ferramentas de permissão e terminologia  
 **Modo nativo:** os objetos de permissão do modo nativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (funções e tarefas) são criados no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e configurados para usuários individuais no Gerenciador de Relatórios.  
  
 **Modo do SharePoint:** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o modo do SharePoint utiliza os recursos de permissão do SharePoint. Os grupos e as permissões do SharePoint são gerenciados da página **Configurações de Site** a seguir.  
  
 A tabela a seguir compara objetos e conceitos relacionados à permissão entre o modo nativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e o SharePoint.  
  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo nativo|SharePoint|  
|---------------------------------------------|----------------|  
|**Função:** por exemplo “Gerenciador de Conteúdo”.|**Grupo:** por exemplo, o grupo padrão “Visualizadores”.|  
|---|**Grupo de nível de permissão:** por exemplo “Exibir Apenas” para o grupo “Visualizadores”.|  
|**Tarefas:** por exemplo “Gerenciar Relatórios”.|**Permissões:** por exemplo, dentro do grupo “Exibir Apenas”, há permissões relacionadas à lista de exibir itens, exibir versões e exibir páginas de aplicativo.|  
  
 Para obter mais informações sobre as permissões do SharePoint, consulte [Níveis de permissão e permissões](http://office.microsoft.com/windows-sharepoint-services-help/permission-levels-and-permissions-HA010100149.aspx) e [Determinar níveis de permissão e grupos no SharePoint 2013](http://technet.microsoft.com/library/cc262690.aspx).  
  
##  <a name="bkmk_compare_roles_groups"></a> Comparar funções do modo nativo e grupos do SharePoint  
 A tabela a seguir compara as definições de função predefinidas no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo nativo com os grupos padrão do SharePoint. Se os grupos do SharePoint não corresponderem à função específica desejada, crie um grupo personalizado e atribua níveis de permissão no SharePoint.  
  
 **Observação**: os grupos do SharePoint padrão disponíveis dependem do modelo de site usado para criar o site do SharePoint.  
  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Função|Grupos do SharePoint|  
|--------------------------------------|-----------------------|  
|**Navegador**<br /><br /> Exibição|Use o grupo **Visitantes** para conceder permissões para exibir relatórios. O grupo **Visitantes** tem permissões no nível de leitura que permitem aos membros do grupo exibir páginas, itens de lista e documentos.|  
|**Gerenciador de Conteúdo**<br /><br /> Permissões totais em todos os itens e operações do nível de item, inclusive permissões para definir segurança.|Use o grupo **Proprietários** para conceder controle total no gerenciamento de itens de servidor de relatório em um site do SharePoint. O grupo **Proprietários** tem permissões Controle Total, que permitem que os membros do grupo alterem o conteúdo, as páginas ou a funcionalidade do site. O acesso Controle Total deve ser limitado somente a administradores de site.|  
|**Meus Relatórios**|Não há nenhum grupo equivalente. **Meus Relatórios** não tem suporte em um servidor de relatório executado no modo do SharePoint. Você pode usar o recurso Meu Site no [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] se desejar usar uma funcionalidade equivalente.|  
|**Publicador**<br /><br /> Adicionar, atualizar, exibir e excluir relatórios, modelos de relatórios, fontes de dados compartilhadas e recursos.|Use o grupo **Membros** para conceder permissões para adicionar itens, editar itens e atualizar referências aos itens dependentes em um site do SharePoint. O grupo **Membros** tem permissões de nível Colaborar, que permitem aos membros do grupo exibir páginas, adicionar e atualizar itens e enviar alterações para aprovação.|  
|**Construtor de Relatórios**<br /><br /> Exibir relatórios, gerenciar assinaturas individuais automaticamente e abrir relatórios no Construtor de Relatórios.|Não há nenhum nível de permissão pronto predefinido ou grupo do SharePoint que seja equivalente à definição de relatório do Construtor de Relatórios. Por padrão, os usuários que pertencem ao grupo **Membros** ou ao grupo **Proprietários** têm permissão para usar o Construtor de Relatórios. Se desejar disponibilizar o Construtor de Relatórios para mais usuários, crie configurações de segurança personalizadas para fornecer um nível de permissão similar ao fornecido pela função do Construtor de Relatórios. Para obter mais informações, consulte [Definir permissões para itens do Servidor de Relatório em um site do SharePoint &#40;Reporting Services no modo integrado do SharePoint&#41;](../../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md).|  
|-|Use o grupo **Visualizadores** para conceder permissões para exibir relatórios renderizados. O grupo **Visualizadores** não pode baixar ou exibir o conteúdo de itens de relatório.<br /><br /> **Observação:** a partir do SQL Server 2012 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], o grupo **Visualizadores** não tem permissões para criar assinaturas.|  
|**Usuário do Sistema** e **Administrador do Sistema**|Estas funções não são necessárias para um servidor de relatório executado no modo do SharePoint. **Usuário do Sistema** e **Administrador do Sistema** correspondem às permissões no nível do farm do SharePoint ou do aplicativo Web. O servidor de relatório não fornece nenhuma funcionalidade que requer autorização nesse nível.|  
  
##  <a name="bkmk_compare_tasks_permissions"></a> Comparando tarefas do modo nativo e permissões do SharePoint  
 A tabela a seguir compara tarefas do modo nativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a permissões do SharePoint. A coluna **Tipo** indica se a tarefa do modo nativo está relacionada a uma função de sistema ou função e itens padrão. As funções do sistema gerenciam permissões em um nível do sistema, por exemplo, agendas compartilhadas.  
  
|Tarefa de modo nativo|Tipo de função|Permissão equivalente do SharePoint|  
|----------------------|---------------|--------------------------------------|  
|Relatórios de consumo|Item|Editar itens, Exibir itens.|  
|Criar relatórios vinculados|Item|Sem suporte.|  
|Gerenciar todas as assinaturas|Item|Gerenciar alertas.|  
|Gerenciar fontes de dados|Item|Adicionar itens, Editar itens, Excluir itens, Exibir itens.|  
|Gerenciar pastas|Item|Adicionar itens, Editar itens, Excluir itens, Exibir itens.|  
|Administrar assinaturas individuais|Item|Editar Itens<br /><br /> Antes do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], o nível de permissão necessário era Criar alertas.|  
|Gerenciar modelos|Item|Adicionar itens, Editar itens, Excluir itens, Exibir itens.|  
|Gerenciar histórico de relatório|Item|Editar itens, Exibir versões, Excluir versões.|  
|Gerenciar relatórios|Item|Adicionar itens, Editar itens, Excluir itens, Exibir itens.|  
|Gerenciar recursos|Item|Adicionar itens, Editar itens, Excluir itens, Exibir itens.|  
|Definir segurança para itens individuais|Item|Gerenciar permissões|  
|Exibir fontes de dados|Item|Exibir itens.|  
|Exibir pastas|Item|Exibir itens.|  
|Exibir modelos|Item|Exibir itens.|  
|Exibir relatórios|Item|Exibir itens.|  
|Exibir recursos|Item|Exibir itens.|  
||||  
|Executar definições de relatório|Sistema|Exibir itens.|  
|Gerar eventos|Sistema|Gerenciar site.|  
|Gerenciar trabalhos|Sistema|Nenhum (sem suporte).|  
|Gerenciar propriedades de servidor de relatório|Sistema|Nenhum (não aplicável). O servidor de relatório não controla se um usuário tem permissão para exibir configurações de integração em Administração Central.|  
|Gerenciar funções|Sistema|Gerenciar permissões.|  
|Gerenciar agendas compartilhadas|Sistema|Gerenciar site, Abrir.|  
|Gerenciar segurança de servidor de relatório|Sistema|Nenhum (não aplicável). O servidor de relatório não usa atribuições de função do nível de sistema em um servidor executado no modo integrado do SharePoint.|  
|Exibir propriedades do servidor de relatório|Sistema|Nenhum (não aplicável). O servidor de relatório não controla se um usuário tem permissão para exibir configurações de integração em Administração Central.|  
|Exibir agendas compartilhadas|Sistema|Abrir itens.|  
  
## <a name="see-also"></a>Consulte também  
 [Definir permissões para itens do Servidor de Relatório em um site do SharePoint &#40;Reporting Services no modo integrado do SharePoint&#41;](../../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)   
 [Definir permissões para operações do servidor de relatório em um aplicativo Web do SharePoint](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)   
 [Concedendo permissões para itens do servidor de relatório em um site do SharePoint](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Definições de função](../../reporting-services/security/role-definitions.md)   
 [Funções predefinidas](../../reporting-services/security/role-definitions-predefined-roles.md)  
  
  
