---
title: Conceder permissões em itens de servidor de relatório em um site do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: security
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
- permissions [Reporting Services], native mode
- security [Reporting Services], SharePoint integrated mode
ms.assetid: 0eb2f34a-3643-4b03-81c2-5741ba7ebefd
caps.latest.revision: 13
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 5afd2bd25aa33ce35b719f1b32000342e47d3f20
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33028053"
---
# <a name="granting-permissions-on-report-server-items-on-a-sharepoint-site"></a>Concedendo permissões para itens do servidor de relatório em um site do SharePoint
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] fornece recursos de segurança internos que podem ser usados para conceder acesso a itens do servidor de relatório acessados nos sites e bibliotecas do SharePoint. Se você já tiver atribuído permissões a usuários, esses mesmos usuários terão acesso a itens e operações do servidor de relatórios assim que você configurar a integração entre o [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] e um servidor de relatório. Você pode usar permissões existentes para carregar definições de relatório e outros documentos, exibir relatórios, criar assinaturas e gerenciar itens.  
  
 Se você não atribuiu permissões ou se não estiver familiarizado com os recursos de segurança no [!INCLUDE[SPF2010](../../includes/spf2010-md.md)], siga essas orientações:  
  
1.  Na documentação do produto do [!INCLUDE[SPF2010](../../includes/spf2010-md.md)], leia sobre as configurações de segurança padrão para os grupos padrão do SharePoint para que você saiba como gerenciar permissões e acesso de usuário.  
  
2.  Analise a lista de permissões que afeta especificamente o acesso a operações e itens do servidor de relatório. Para obter mais informações, consulte [Usar a segurança interna no Windows SharePoint Services para itens do servidor de relatório](../../reporting-services/security/use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md).  
  
3.  Atribua as contas do usuário e do grupo a grupos do SharePoint predefinidos.  
  
4.  Opcionalmente, crie novos níveis de permissão e grupos ou modifique os existentes para variar as permissões de acesso ao servidor à medida que as necessidades específicas surgem.  
  
 Para usar os recursos de segurança do [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] com itens do servidor de relatório, você deve ter um servidor de relatório que execute no modo integrado do SharePoint.  
  
## <a name="about-permissions-permission-levels-and-sharepoint-groups"></a>Sobre permissões, níveis de permissão e grupos do SharePoint  
 A lista a seguir fornece uma breve introdução aos recursos de segurança do [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]. Para obter mais informações, consulte "Ajuda e instruções do Windows SharePoint" no site do SharePoint.  
  
-   Objetos protegíveis incluem sites, listas, bibliotecas, pastas e documentos.  
  
-   Uma permissão é uma autorização para executar uma tarefa específica. [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] fornece 33 permissões predefinidas que você pode combinar em um nível de permissão.  
  
-   Um nível de permissão é um conjunto de permissões que pode ser concedido a usuários ou grupos do SharePoint em um objeto que pode ser protegido como um site, biblioteca, lista, pasta, item ou documento. É equivalente a uma definição de função em [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Há cinco níveis de permissão predefinidos. Você pode personalizá-los ou criar novos, se necessário.  
  
-   Um grupo do SharePoint é um grupo de usuários que você pode criar em um site do SharePoint para gerenciar permissões para o site e fornecer uma lista de distribuição de email para membros do site. Um grupo do SharePoint consiste em contas de grupo e de usuário do Windows ou de logons de usuário, se você estiver usando a Autenticação de Formulários. [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] fornece três grupos. Você pode personalizá-los ou criar novos, se necessário.  
  
-   A herança de permissão permite que subsites, listas e bibliotecas e itens herdem as configurações de segurança do site pai. Você pode usar as permissões herdadas para acessar itens do servidor de relatório armazenados em uma biblioteca do SharePoint. Usar a herança de permissão e os grupos predefinidos do SharePoint pode ajudar a simplificar sua implantação e fornece acesso imediato à maioria das operações do servidor de relatório.  
  
## <a name="who-sets-permissions"></a>Quem define permissões  
 O administrador que instala o [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]que executa o Assistente de Configuração do SharePoint e cria o site do portal se torna o proprietário padrão do site do portal. O proprietário do site pode definir permissões na Administração Central para um farm ou aplicativo da Web independente do SharePoint e pode definir permissões no site de nível superior para cada aplicativo da Web do SharePoint. Essa pessoa também pode designar proprietários de site adicionais.  
  
 No site de nível superior de um aplicativo da Web do SharePoint, os administradores de coleção de sites podem definir permissões para vários sites por meio da hierarquia de sites. Os proprietários de sites individuais podem executar as mesmas tarefas relativas a um subsite.  
  
 Um administrador de servidor ou de coleção de sites pode definir opções que determinar se outros proprietários de site podem definir permissões. Dependendo do nível de permissões que você tem, talvez você não possa criar nem personalizar os grupos do SharePoint nem os níveis de permissão.  
  
## <a name="using-predefined-sharepoint-groups-and-permission-levels"></a>Usando níveis de permissão e grupos predefinidos do SharePoint  
 As recomendações contidas na documentação do produto [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] sugerem que você use os grupos padrão do SharePoint (que são *Proprietários do* **Nome do site**, *Proprietários do* **Nome do site**e *Proprietários do* **Nome do site**) e atribua permissões no nível do site. A maiouia dos usuários aos quais você atribui permissões deve ser membros dos grupos *Nome do site* **Visitantes** ou *Nome do site* **Membros** . As permissões no site pai são herdadas ao longo da hierarquia de site. Você pode dividir a herança de permissão por itens específicos que exigem restrições adicionais.  
  
 Os seguintes grupos do SharePoint têm os seguintes níveis de permissão predefinidos:  
  
-   O grupo **Proprietários** tem permissões Controle Total, que permitem que os membros do grupo alterem o conteúdo, as páginas ou a funcionalidade do site. O acesso Controle Total deve ser limitado somente a administradores de site.  
  
-   O grupo **Membros** tem permissões de nível Colaborar, que permitem aos membros do grupo exibir páginas, editar itens, enviar alterações para aprovação, adicionar e excluir itens de uma lista.  
  
-   O grupo **Visitantes** tem permissões no nível de leitura que permitem aos membros do grupo exibir páginas, itens de lista e documentos.  
  
 Os grupos do SharePoint têm níveis de permissão que fornecem acesso imediato a muitas operações do servidor de relatório. Se você achar que as configurações de segurança internas não fornecem o nível de acesso necessário, você poderá criar níveis de permissão ou grupos personalizados.  
  
 Para obter mais informações sobre quais operações do servidor de relatório têm suporte por meio dos recursos de segurança padrão, consulte [Usar a segurança interna no Windows SharePoint Services para itens do servidor de relatório](../../reporting-services/security/use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md).  
  
 Para usar os recursos de segurança internos, você deve atribuir as contas do grupo ou usuário do Windows aos grupos do SharePoint. Com exceção do administrador do servidor e do proprietário do site do portal que têm acesso automático ao [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] quando o software é instalado, a todos os outros usuários devem ser concedidas permissões para acessar o servidor.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Usar a segurança interna no Windows SharePoint Services para itens do servidor de relatório](../../reporting-services/security/use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)  
 Explica como podem ser usados os níveis de permissão e grupos do SharePoint predefinidos para acessar itens do servidor de relatório.  
  
 [Referência à permissão de listas e sites do SharePoint para itens do servidor de relatório](../../reporting-services/security/sharepoint-site-and-list-permission-reference-for-report-server-items.md)  
 Fornece uma referência de todas as permissões de produtos do SharePoint que podem ser usadas para acessar operações do servidor de relatórios.  
  
 [Definir permissões para operações do servidor de relatório em um aplicativo Web do SharePoint](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)  
 Descreve requisitos de permissão para relatórios ad hoc e sugere abordagens para tornar os recursos disponíveis.  
  
 [Comparar funções e tarefas no Reporting Services com grupos e permissões do SharePoint](../../reporting-services/security/reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)  
 Fornece um breve resumo de como os grupos do SharePoint são comparados com definições de função predefinidas no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 [Definir permissões para itens do Servidor de Relatório em um site do SharePoint &#40;Reporting Services no modo integrado do SharePoint&#41;](../../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)  
 Fornece instruções para criar novos grupos do SharePoint que têm permissão para iniciar o Construtor de Relatórios e definir a segurança do item do modelo. Este tópico também contém diretrizes gerais sobre como definir permissões personalizadas para qualquer item do servidor de relatório ou operação.  
  
## <a name="see-also"></a>Consulte Também  
 [Segurança e proteção do Reporting Services](../../reporting-services/security/reporting-services-security-and-protection.md)  
  
  
