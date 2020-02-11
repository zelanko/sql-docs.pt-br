---
title: Usar a segurança interna no Windows SharePoint Services para itens de servidor de relatório | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
- security [Reporting Services], SharePoint integrated mode
ms.assetid: 9577e88d-c22b-4934-936f-e0f1400cedf5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 622fbdf67d33972500a5047c3886830ba802796a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66101453"
---
# <a name="use-built-in-security-in-windows-sharepoint-services-for-report-server-items"></a>Usar a segurança interna no Windows SharePoint Services para itens do servidor de relatório
  O SharePoint fornece recursos de segurança interna que você pode usar para acessar itens do servidor de relatório nos sites e bibliotecas do SharePoint. Se você já tiver atribuído permissões de site e de lista aos usuários, esses mesmos usuários terão acesso a itens e operações do servidor de relatórios assim que você configurar a integração entre o SharePoint e um servidor de relatório.  
  
## <a name="securable-items"></a>Itens protegíveis  
 As permissões definidas no site ou na biblioteca podem ser usadas para conceder acesso a itens do servidor de relatórios. Entretanto, se você quiser proteger itens individuais, pode definir permissões nos seguintes tipos de conteúdo:  
  
|Tipo de arquivo|DESCRIÇÃO|  
|---------------|-----------------|  
|.rdl|Um arquivo de definição de relatório que define o layout do relatório e os comandos usados para recuperar dados. Uma definição de relatório usa informações de conexão da fontes de dados para recuperar dados quando o relatório é processado. Se a definição do relatório determinar um relatório ad hoc criado no Construtor de Relatórios, o relatório fará par com um arquivo de modelo de relatório (.smdl) que define o escopo na exploração de dados do relatório renderizado.|  
|.smdl|Um arquivo de modelo de relatório que descreve estruturas de dados e como elas se relacionam. Ele é usado para criar e executar relatórios do Construtor de Relatórios.|  
|.rsds|Um arquivo de fonte de dados compartilhada que especifica informações de conexão com uma fonte de dados externa. Ele é usado por arquivos de definição de relatório (.rdl) e de modelo de relatório (.smdl). Os modelos de relatórios sempre usam arquivos .rsds para obter informações de conexão com uma fonte de dados subjacente. As definições de relatórios podem usar arquivos .rsds ou informações de conexão definidas em propriedades de fonte de dados no relatório.|  
|.rsc|Uma parte de relatório que define o layout e a estrutura de um item de relatório ou região de dados. É usado para publicar a parte de relatório em um servidor de modo que o item possa ser usado novamente por outros autores de relatório da Galeria de Partes de Relatório.|  
|.rsd|Um arquivo de conjunto de dados compartilhado que define a sintaxe de consulta e as propriedades para um conjunto de dados. Conjuntos de dados compartilhados podem ser compartilhados, armazenados, processados e armazenados em cache externo a partir de um relatório.|  
  
 Agendas, assinaturas e histórico de relatórios não são itens de segurança. Você pode definir permissões no site ou na biblioteca que determinem se um usuário poderá criar ou usar agendas, assinaturas e histórico de relatórios, mas não pode proteger esses itens diretamente.  
  
 Para proteger itens individuais, selecione o item na biblioteca, clique na seta para baixo e selecione **Gerenciar Permissões**. No menu **Ações** , selecione **Editar Permissões**.  
  
## <a name="using-built-in-groups-and-permission-levels-to-access-report-server-items"></a>Usando grupos internos e níveis de permissão para acessar itens do servidor de relatório  
 Quando você usa herança de permissões e grupos do SharePoint padrão, pode acessar a maioria das operações do servidor de relatório assim que configura a integração no servidor de relatório e nas instâncias do SharePoint.  
  
 O SharePoint fornece grupos padrão mapeados para níveis de permissão predefinidos que determinam como você acessa documentos e páginas em um site do SharePoint. Se você estiver usando grupos e níveis de permissão padrão e se seus sites forem configurados para herdar permissões, será possível trabalhar com recursos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] dos seguintes modos:  
  
|**Grupos do SharePoint**|**Nível de permissão**|**Resumo**|**Acesso ao servidor de relatório**|  
|---------------------------|--------------------------|-----------------|------------------------------|  
|**Proprietários**|Controle Total|Os proprietários têm permissão total para criar, gerenciar e proteger itens e operações do servidor de relatório.|Definir permissões que controlam o acesso a todos os itens do servidor de relatórios armazenados em bibliotecas em todo o site. Definir permissões em um modelo de relatório (também chamado de segurança de item de modelo). Personalizar uma Web Part do Visualizador de Relatórios. Adicionar relatórios e outros itens a bibliotecas. Editar propriedades de itens para relatórios e outros documentos. Excluir relatórios e outros itens. Exibir relatórios, inclusive aqueles que usam modelos de relatórios para exploração de dados. Definir parâmetros em relatórios. Definir opções de processamento em um relatório. Gerar modelos de relatórios. Criar relatórios no Construtor de Relatórios. Criar e gerenciar fontes de dados compartilhados. Criar, alterar e excluir assinaturas de propriedade de qualquer usuário. Criar e gerenciar agendamentos compartilhados usadas em todo o site. Criar e gerenciar versões de um documento, inclusive o histórico de relatórios. Baixar o arquivo de origem de uma definição de relatório ou de um modelo de relatório. Substituir uma definição de relatório, modelo de relatório, fonte de dados compartilhados ou recursos (preservando propriedades e permissões de itens).|  
|**Membros**|Contribuir|Os membros podem criar novos itens e publicar relatórios de itens e modelos usando ferramentas de criação em uma biblioteca do SharePoint.|Adicionar relatórios e outros itens a bibliotecas. Editar propriedades de itens para relatórios e outros documentos. Excluir relatórios e outros itens. Exibir relatórios, inclusive aqueles que usam modelos de relatórios para exploração de dados. Exibir versões anteriores de um documento, inclusive instantâneos em um histórico de relatórios (exige que o usuário tenha permissão de abrir o relatório para o qual foi criado o histórico de relatórios). Definir parâmetros em relatórios. Definir opções de processamento em um relatório. Gerar modelos de relatórios. Criar relatórios no Construtor de Relatórios. Criar e gerenciar fontes de dados compartilhados. Criar, alterar e excluir assinaturas de propriedade do usuário. Usar agendamentos compartilhados com assinatura. Criar e gerenciar versões de um documento, inclusive o histórico de relatórios. Baixar o arquivo de origem de uma definição de relatório ou de um modelo de relatório. Substituir uma definição de relatório, modelo de relatório, fonte de dados compartilhados ou recursos (preservando propriedades e permissões de itens).|  
|**Visitantes** e **Visualizadores**|Ler|Os visitantes podem exibir relatórios|Exibir relatórios, inclusive aqueles que usam modelos de relatórios para exploração de dados.|  
  
 Se você não estiver usando os grupos internos e níveis de permissão, inclua permissões específicas para acessar recursos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações, consulte [Definir permissões para operações do servidor de relatório em um aplicativo Web do SharePoint](set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Concedendo permissões para itens do servidor de relatório em um site do SharePoint](granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Comparar funções e tarefas no Reporting Services com grupos e permissões do SharePoint](../reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)   
 [Definir permissões para operações do servidor de relatório em um aplicativo Web do SharePoint](set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)   
 [Conceder permissões para itens do servidor de relatório em um site do SharePoint](granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
  
  
