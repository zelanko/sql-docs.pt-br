---
title: "Referência à permissão de listas e sites do SharePoint para itens do servidor de relatório | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
- security [Reporting Services], SharePoint integrated mode
- permission sets [Reporting Services]
ms.assetid: 1fcb27bd-4c4a-43f4-bfff-e42a59c87c49
caps.latest.revision: "14"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 3eff319ce6f754b7e602b26bf1b5032d11a7b0f3
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="sharepoint-site-and-list-permission-reference-for-report-server-items"></a>Referência à permissão de listas e sites do SharePoint para itens do servidor de relatório
  Este tópico fornece uma referência das permissões no SharePoint que podem ser usadas para conceder acesso a operações do servidor de relatório para um servidor de relatório executado em modo integrado do SharePoint. Se você estiver criando níveis de permissão personalizados, este tópico poderá ajudá-lo a escolher as permissões a serem usadas.  
  
 O SharePoint fornece trinta e três permissões que podem ser usadas para controlar o acesso a conteúdos e operações. Algumas, mas não todas delas são aplicáveis a documentos e operações que envolvem um servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Você pode usar as tabelas de referência de permissão deste artigo para saber quais permissões dão suporte a tarefas específicas de relatórios.  
  
 Cada tabela começa com uma lista de permissões do SharePoint e uma descrição. A tabela inclui três colunas que indicam como uma permissão é usada em níveis de permissão predefinidos. Os níveis de permissões predefinidos incluem o seguinte:  
  
|Nível de permissão|Abreviação|  
|----------------------|------------------|  
|Controle total|**F**|  
|Contribuir|**C**|  
|Visitante|**V**|  
  
 As permissões que não afetam um servidor de relatórios não são listadas. Todas as permissões para personalização são excluídas deste artigo de referência. Embora seja possível incluir itens de servidor de relatório em um site personalizado, o servidor de relatório não trata diretamente de solicitações ou operações personalizadas.  
  
||  
|-|  
|[!INCLUDE[applies](../../includes/applies-md.md)]<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo do SharePoint &#124; SharePoint 2010 e SharePoint 2013.|  
  
## <a name="list-permissions"></a>Permissões de lista  
 As permissões que você define na biblioteca que contém os itens de servidor de relatório determinam como os usuários acessam esses itens.  
  
|Permissão|Description|F|C|V|Operação do servidor de relatório|  
|----------------|-----------------|-------|-------|-------|-----------------------------|  
|Gerenciar Listas|Criar e excluir listas, adicionar ou remover colunas em uma lista e adicionar ou remover exibições públicas de uma lista.|X|||Criar uma pasta em uma biblioteca do SharePoint durante uma operação de publicação usando uma ferramenta de criação. Esta permissão também é exigida para o gerenciamento de históricos de relatórios.|  
|Adicionar Itens|Adicionar itens a listas e documentos a bibliotecas de documentos, além de adicionar comentários a discussões na Web.|X|X||Adicionar relatórios, modelos de relatórios, fontes de dados compartilhados e recursos (arquivos de imagem externos) às bibliotecas do SharePoint. Crie fontes de dados compartilhados. Gerar modelos de relatórios utilizando fontes de dados compartilhados. Iniciar o Construtor de Relatórios e criar um novo relatório ou carregar um modelo no Construtor de Relatórios.|  
|Editar Itens|Editar itens em listas, documentos em bibliotecas de documentos, comentários de discussões na Web em documentos e personalizar Páginas de Web Parts em bibliotecas de documentos.<br /><br /> Crie assinaturas e edite as assinaturas que você criou.|X|X||Exibir versões anteriores de um documento, inclusive instantâneos do histórico do relatório. Editar propriedades de itens para relatórios e outros documentos. Definir opções de processamento de relatórios. Definir parâmetros em um relatório. Editar propriedades de fontes de dados. Criar instantâneos de histórico de relatórios. Abrir um modelo de relatório ou um relatório baseado em modelo no Construtor de Relatórios e salvar suas alterações no arquivo. Atribuir relatórios de clique a entidades em um modelo. Substituir uma definição de relatório, uma fonte de dados compartilhados, um modelo de relatório ou um recurso por uma versão mais recente (substituir o arquivo, preservar metadados). Gerenciar itens dependentes referenciados em um relatório ou modelo. Personalizar a Web Part do Visualizador de Relatórios relativa a um relatório específico.<br /><br /> Criar, alterar e excluir assinaturas que usem as extensões de entrega do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para enviar relatórios a locais de destino. Só o proprietário da assinatura e os usuários que têm a permissão Gerenciar Alertas podem executar estas ações.|  
|Excluir Itens|Excluir itens de uma lista, documentos de uma biblioteca de documentos e comentários de discussões na Web em documentos.|X|X||Excluir relatórios, modelos de relatórios, fontes de dados compartilhados e outros documentos de uma biblioteca.|  
|Exibir Itens|Exibir itens em listas, documentos em bibliotecas de documentos e comentários de discussões na Web.|X|X|X|Abrir um relatório, modelo de relatório e outro documento e fazer com que seja processado no servidor de relatório.|  
|Abrir Itens|Exibir a origem de documentos com manipuladores de arquivo do lado do servidor.|X|X|X|Exibir uma lista de fontes de dados compartilhadas. Baixar uma cópia do arquivo de origem de uma definição de relatório ou modelo de relatório. Exibir relatórios de clickthrough que usam um modelo de relatório como fonte de dados.|  
|Exibir Versões|Exibir versões anteriores de um item de lista ou documento.|X|X|X|Exibir versões anteriores de um documento e de instantâneos de relatórios.|  
|Excluir Versões|Excluir versões anteriores de um item de lista ou documento.|X|X||Excluir versões anteriores de um documento e de instantâneos de relatórios.|  
  
> [!NOTE]  
>  Outras permissões de lista incluem Substituir Check-out, Aprovar Itens e Exibir Páginas de Aplicativo. Essas permissões não são avaliadas pelo servidor de relatório. O servidor de relatório não lida com essas operações.  
  
## <a name="site-permissions"></a>Permissões de site  
 As permissões de site determinam o acesso a operações de servidor de relatório não diretamente relacionadas a itens armazenados em uma biblioteca específica. Os exemplos incluem a criação e o gerenciamento de agendas compartilhadas, que podem ser usadas por itens em várias bibliotecas, e a configuração da Web Part do Visualizador de Relatórios, que pode ser usada em todo um site.  
  
|Permissão|Description|F|C|V|Operação do servidor de relatório|  
|----------------|-----------------|-------|-------|-------|-----------------------------|  
|Gerenciar Permissões|Criar e gerenciar níveis de permissão no site e atribuir permissões a usuários e grupos.|X|||Você pode alterar permissões para todos os itens e operações do servidor de relatório. Você pode definir a segurança de itens de modelo.|  
|Gerenciar Site|Executar todas as tarefas de administração do site, bem como gerenciar conteúdos.|X|||Criar, alterar e excluir agendas compartilhadas.|  
|Adicionar e Personalizar Páginas|Adicionar, alterar ou excluir páginas HTML ou de Web Part e editar o site usando um editor compatível com [!INCLUDE[winSPServ](../../includes/winspserv-md.md)].|X|||Adicionar ou remover uma Web Part do Visualizador de Relatórios.|  
|Procurar Informações sobre o Usuário|Exibir informações sobre os usuários do site.|X|X|X|Procurar relatórios e outros itens em sites, bibliotecas e pastas diferentes. Publicar relatórios e outros itens em uma biblioteca.|  
|Enumerar Permissões|Enumerar permissões no site, na lista, pasta, no documento ou item de lista.|X|||Ler permissões para todos os itens de servidor de relatório. Exibir um relatório de clickthrough que usa um modelo de relatório que contém configurações de segurança de item de modelo.|  
|Gerenciar Alertas|Gerenciar alertas para todos os usuários do site.|X|||Criar, alterar e excluir qualquer assinatura em um site.|  
|Usar Interfaces Remotas|Usar as interfaces SOAP, Web DAV ou SharePoint Designer para acessar o site.|X|X|X|Usado para chamar o ponto de extremidade do proxy do URL para o servidor de relatório.|  
|Abrir|Abrir um site, uma lista ou pasta para acessar itens nesse contêiner.|X|X|X|Ler propriedades de agendas e de itens.|  
  
## <a name="see-also"></a>Consulte também  
 [Comparar funções e tarefas no Reporting Services com grupos e permissões do SharePoint](../../reporting-services/security/reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)   
 [Conceder permissões para itens do servidor de relatório em um site do SharePoint](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
  
  
