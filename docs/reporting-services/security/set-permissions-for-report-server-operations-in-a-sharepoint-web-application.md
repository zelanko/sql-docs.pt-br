---
title: Definir permissões para operações do servidor de relatório em um aplicativo Web do SharePoint | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
- SharePoint integration [Report Builder]
- security [Reporting Services], SharePoint integrated mode
- Report Builder 1.0, SharePoint integration
- model item security [Reporting Services]
ms.assetid: 9ea71f1a-ee9e-4337-95ff-d7cef79946e7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ce5ddca1cb39d7d4f375232e3588900b5b1ebe6a
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "65570594"
---
# <a name="set-permissions-for-report-server-operations-in-a-sharepoint-web-application"></a>Definir permissões para operações do servidor de relatório em um aplicativo Web do SharePoint
  Para um servidor de relatório executado no modo integrado do SharePoint, as configurações de segurança no site do SharePoint determinam como exibir e gerenciar os relatórios, modelos de relatório e fontes de dados compartilhadas. Se você estiver usando os grupos, níveis de permissão e atribuições de permissão do SharePoint padrão, será possível trabalhar com relatórios e outros documentos usando as configurações de segurança atuais.  
  
 Se as configurações de segurança padrão não fornecerem o nível de acesso desejado, você poderá usar as informações nas seguintes seções para saber quais permissões são necessárias para operações específicas.  
  
-   [Permissões para exibir e gerenciar relatórios](#permissionReports)  
  
-   [Permissões para criar e gerenciar relatórios com o uso do Construtor de Relatórios](#permissionReportBuilder)  
  
-   [Permissões para criar e gerenciar agendas compartilhadas](#permissionSharedSchedules)  
  
-   [Permissões para criar e gerenciar assinaturas](#permissionSubscriptions)  
  
-   [Permissões para criar e gerenciar fontes de dados compartilhadas e modelos de relatórios](#permissionDataSources)  
  
 São necessárias alguns permissões chave para completar quase qualquer operação em um site do SharePoint. Essas permissões não são listadas nas tabelas de tarefas e permissões abaixo, mas você deve incluí-las se estiver criando níveis permissão personalizados:  
  
-   Procurar Informações sobre o Usuário  
  
-   Usar Interfaces Remotas  
  
-   Aberto  
  
-   Exibir Páginas de Aplicativo  
  
 Se você estiver usando níveis de permissão predefinidos, nenhuma ação será necessária porque as permissões anteriores já estarão incluídas em Controle Total, Criação, Colaboração, Leitura e Acesso Limitado. No entanto, se você estiver usando níveis de permissão personalizados ou se estiver editando as permissões atribuídas a um usuário ou grupo específico, adicione a permissão manualmente.  
  
 A permissão "Procurar Informações sobre o Usuário" permite que o servidor de relatório retorne informações sobre o criador do item e o último usuário que o modificou. Sem essa permissão, o servidor de relatório retornará os erros a seguir. Para operações de procura, o erro é: "O Report Server encontrou um erro de SharePoint. ---> System.UnauthorizedAccessException: acesso negado." Para operações de publicação, o erro é: "As permissões concedidas ao usuário '\<domínio>\\<usuário\>' não são suficientes para realizar esta operação".  
  
##  <a name="permissionReports"></a> Permissões para exibir e gerenciar relatórios  
 As permissões de definição são estabelecidas através de permissões de Lista na biblioteca que contém o relatório, mas é possível definir permissões em relatórios individuais, se você desejar restringir o acesso. A tabela a seguir fornece uma lista de tarefas e as permissões que oferecem suporte a cada uma.  
  
|Tarefa|Permissão|  
|----------|----------------|  
|Exibir um relatório.|**Exibir Itens** na biblioteca que contém os arquivos ou no relatório individual.|  
|Exibir um relatório de clickthrough que use um modelo de relatório como fonte de dados.|**Exibir Itens** na biblioteca que contém o relatório e o modelo de relatório ou no relatório ou modelo individual. Se você não tiver permissões de exibição no modelo, ainda assim poderá abrir o relatório, mas não executar exploração ad hoc nos dados.<br /><br /> Se o modelo de relatório usar a segurança de item do modelo, o usuário também deverá ter a permissão **Enumerar Permissões** no modelo de relatório.|  
|Exibir instantâneos no histórico de relatórios.|**Editar Itens** para a biblioteca com os arquivos ou para o relatório individual. No caso de relatórios específicos, você pode exibir todos ou nenhum histórico de relatórios. Não é possível definir permissões em instantâneos individuais no histórico de relatórios.|  
|Carregar ou publicar um relatório em uma biblioteca.|**Adicionar Itens** na biblioteca que conterá o relatório.|  
|Definir propriedades em um relatório, inclusive opções de processamento, propriedades de parâmetros e informações de conexão da fontes de dados.|**Editar Itens** na biblioteca que contém o relatório ou no relatório individual. Você também deve ter permissões de exibição para a fonte de dados compartilhada (.rsds) para selecioná-la para uso com o relatório.|  
|Agendar processamento de relatórios.|Para selecionar uma agenda compartilhada, você deve ter a permissão **Abrir** para o site que contém a biblioteca onde se encontra o relatório. Para agendar o processamento de dados ou uma expiração de cache, você deve ter a permissão **Editar Itens** na biblioteca que contém o relatório ou no relatório individual.|  
|Excluir um relatório.|**Excluir Itens** para a biblioteca que contém o relatório ou para o relatório individual.|  
|Substituir uma definição de relatório (sem afetar propriedades, permissões, histórico ou assinaturas) por uma nova versão.|**Editar Itens** na biblioteca que contém o relatório ou no relatório individual.|  
|Criar instantâneos em um histórico de relatórios.|**Adicionar Itens** na biblioteca que contém o relatório para o qual você está criando um histórico de relatórios.|  
|Criar instantâneos em um histórico de relatórios.|**Adicionar Itens** na biblioteca que contém o relatório para o qual você está criando um histórico de relatórios.|  
|Excluir instantâneos em um histórico de relatórios e excluir versões específicas de definições de relatórios que tenham sofrido check out e sido modificadas com o decorrer do tempo.|**Excluir Versões** para a biblioteca que contém o relatório do qual você está excluindo um histórico de relatórios.|  
|Exibir instantâneos em um histórico de relatórios e exibir versões específicas de definições de relatórios que tenham sofrido check out e sido modificadas com o decorrer do tempo.|**Exibir Versões** na biblioteca que contém o relatório.|  
  
##  <a name="permissionReportBuilder"></a> Permissões para criar e gerenciar relatórios com o uso do Construtor de Relatórios  
 O Construtor de Relatórios é uma ferramenta de criação de relatórios que você pode usar para criar relatórios ad hoc. O Construtor de Relatórios usa modelos de relatórios como fonte de dados para oferecer suporte à exploração de dados ad hoc. Você pode carregar um modelo no Construtor de Relatórios para criar um relatório, executá-lo, clicar em dados do modelo e, opcionalmente, salvar o relatório em uma biblioteca. Os usuários com permissões suficientes podem, em seguida, abrir o mesmo relatório e também executar exploração de dados ad hoc.  
  
> [!NOTE]  
>  O acesso ao Construtor de Relatórios pode ser determinado por outros fatores além das permissões. Um administrador de site pode desabilitar a criação de relatórios ad hoc definindo propriedades do servidor ou limitar a disponibilidade do Construtor de Relatórios adicionando o tipo de conteúdo do relatório do Construtor de Relatórios a uma biblioteca, o que impede que os usuários criem novos relatórios no menu **Novo** de uma biblioteca. Além disso, um administrador de servidor de relatório pode tornar o Construtor de Relatórios indisponível definindo propriedades no servidor de relatório. Se qualquer uma dessas condições for verdadeira no seu servidor, você não poderá usar o Construtor de Relatórios, mesmo que possua as permissões necessárias.  
  
 A tabela a seguir fornece uma lista de tarefas para a criação de relatórios e o uso do Construtor de Relatórios, além das permissões que oferecem suporte a cada uma.  
  
|Tarefa|Permissão|  
|----------|----------------|  
|Iniciar o Construtor de Relatórios.|Não há permissões explicitamente usadas para controlar o acesso ao uso do Construtor de Relatórios. O Construtor de Relatórios estará disponível se a integração com o servidor de relatórios estiver configurada e se você tiver permissão para adicionar itens a uma biblioteca. Para iniciar o Construtor de Relatórios no menu **Novo** da biblioteca, você deverá registrar o tipo de conteúdo do Construtor de Relatórios. Para obter mais informações, veja [Adicionar os tipos de conteúdo do Reporting Services à sua biblioteca do SharePoint](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md).|  
|Carregar um modelo ou uma fonte de dados compartilhados.|**Adicionar Itens** na biblioteca que conterá os arquivos.|  
|Exibir um modelo ou uma fonte de dados compartilhados dependente.|**Exibir Itens** para a biblioteca que contém os arquivos.<br /><br /> Se o modelo contiver configurações de segurança de item de modelo, o usuário também deverá ter a permissão **Enumerar Permissões** para o modelo.|  
|Gerar um modelo com base em uma fonte de dados compartilhados.|**Adicionar Itens** na biblioteca que contém o arquivo de fonte de dados compartilhada (.rsds) usado para a criação do modelo.|  
|Definir permissões de itens de modelo específicos presentes em um modelo.|**Gerenciar Permissões** no site que contém a biblioteca e o arquivo de modelo de relatório (.smdl).|  
|Carregar um modelo no Construtor de Relatórios.|**Editar Itens** para o arquivo de modelo de relatório (.smdl).|  
|Criar uma definição de relatório no Construtor de Relatórios e salvar um relatório em uma biblioteca.|**Adicionar Itens** para salvar o arquivo em uma biblioteca.|  
|Editar um relatório no Construtor de Relatórios.|**Editar Itens** no arquivo de definição do relatório.|  
  
 As permissões para criar e usar assinaturas, histórico de relatórios e também para definir opções de processamento de relatórios ou de dados em um relatório do Construtor de Relatórios são as mesmas usadas para executar ações idênticas em arquivos de definição de relatório padrão.  
  
##  <a name="permissionSharedSchedules"></a> Permissões para criar e gerenciar agendas compartilhadas  
 As agendas compartilhadas não são documentos armazenados em uma biblioteca. Por esse motivo, a criação e o gerenciamento dessas agendas requerem permissões do site. Não é possível restringir o acesso a agendas compartilhadas específicas. Qualquer agenda compartilhada criada por você estará disponível para qualquer usuário com permissão Abrir, em todo o site.  
  
 A tabela a seguir fornece uma lista de tarefas e permissões para criar, gerenciar e usar agendas compartilhadas.  
  
|Tarefa|Permissão|  
|----------|----------------|  
|Criar, editar ou excluir uma agenda compartilhada.|**Gerenciar Site** no site.|  
|Selecione uma agenda compartilhada para processamento de assinaturas ou recuperação de dados.|**Abrir** no site que contém a biblioteca.|  
  
##  <a name="permissionSubscriptions"></a> Permissões para criar e gerenciar assinaturas  
 O SharePoint impõe uma dependência entre as permissões de assinatura e de exibição. Não é possível fazer assinatura em um relatório que você não tem permissão para exibir. Se você conceder permissões para fazer a assinatura em um relatório, as permissões para exibição serão concedidas automaticamente.  
  
 A tabela a seguir fornece uma lista de tarefas e permissões para criar, gerenciar e usar assinaturas.  
  
|Tarefa|Permissão|  
|----------|----------------|  
|Criar, editar ou excluir uma assinatura de propriedade de um usuário para um relatório específico.|**Editar Itens** na biblioteca que contém o relatório ou no próprio relatório. Exibir Itens é uma permissão dependente e será automaticamente incluída no nível da permissão. Os usuários que podem criar uma assinatura também podem criar agendas personalizadas para executar essa assinatura.|  
|Selecione uma agenda compartilhada para usar com a assinatura.|**Abrir** no site que contém a biblioteca.|  
|Criar, editar ou excluir qualquer assinatura em todo o site.|**Gerenciar Alertas** no site.|  
  
##  <a name="permissionDataSources"></a> Permissões para criar e gerenciar fontes de dados compartilhadas e modelos de relatórios  
 Um arquivo de fonte de dados compartilhados (.rsds) contém informações de conexão da fontes de dados que podem ser usadas por vários relatórios e modelos. No caso de relatórios padrão, o uso de um arquivo .rsds para especificar informações de conexão da fonte de dados é opcional. No caso de relatórios controlados por modelos, o uso de um arquivo .rsds é obrigatório. Um modelo de relatório sempre usa um arquivo .rsds para conectar-se a fontes de dados externas.  
  
 Você pode definir propriedades em fontes de dados compartilhados que determinam se os usuários individuais podem exibir ou gerenciar fontes de dados compartilhados. As permissões para exibir ou gerenciar uma fonte de dados compartilhados diferem daquelas para exibição de relatórios; você pode exibir um relatório que use um arquivo .rsds sem possuir permissão para exibição no próprio arquivo .rsds.  
  
|Tarefas|Permissão|  
|-----------|----------------|  
|Criar uma fonte de dados compartilhados.|**Adicionar Itens** na biblioteca que contém a fonte de dados compartilhada. Você pode criar novas fontes de dados compartilhadas no menu Novo em uma biblioteca. Para isso, você deverá registrar o tipo de conteúdo da Fonte de Dados de Relatório na biblioteca. Para obter mais informações, veja [Adicionar os tipos de conteúdo do Reporting Services à sua biblioteca do SharePoint](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md).|  
|Editar uma fonte de dados compartilhados.|**Editar Itens** na biblioteca que contém a fonte de dados compartilhada ou na própria fonte de dados compartilhada.|  
|Excluir uma fonte de dados compartilhados.|**Excluir Itens** na biblioteca que contém a fonte de dados compartilhada ou na própria fonte de dados compartilhada.|  
|Usar uma fonte de dados compartilhados (.rsds) com um relatório.|**Editar Itens** no relatório ou na biblioteca que contém o relatório. A seleção de uma fonte de dados compartilhados é parte da definição de propriedades de fonte de dados de um relatório.|  
|Gerar um modelo de relatório com base em uma fonte de dados compartilhados.|**Adicionar Itens** na biblioteca que conterá o modelo de relatório.|  
|Excluir um modelo de relatório.|**Excluir Itens** na biblioteca que contém o modelo de relatório ou no próprio modelo de relatório.|  
|Definir permissões de itens de modelo específicos presentes em um modelo.|**Gerenciar Permissões** no site que contém a biblioteca e o arquivo de modelo de relatório (.smdl).|  
  
> [!NOTE]  
>  Não há permissões para editar modelos de relatório. Embora seja possível gerar ou excluir modelos de relatórios, não é possível editá-los em um site do SharePoint. A edição de modelos de relatório requer o Designer de Modelos, uma ferramenta de criação de clientes que não é afetada por permissões definidas no SharePoint.  
  
## <a name="see-also"></a>Consulte Também  
 [Concedendo permissões para itens do servidor de relatório em um site do SharePoint](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Comparar funções e tarefas no Reporting Services com grupos e permissões do SharePoint](../../reporting-services/security/reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)   
 [Concedendo permissões para itens do servidor de relatório em um site do SharePoint](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Usar a segurança interna no Windows SharePoint Services para itens do servidor de relatório](../../reporting-services/security/use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)  
  
  
