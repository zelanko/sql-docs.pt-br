---
title: SQL Server Management Studio (SSMS)
description: Descrever o que é o SSMS (SQL Server Management Studio) e o que ele pode fazer.
ms.prod: sql
ms.technology: ssms
ms.topic: overview
author: markingmyname
ms.author: maghan
ms.reviewer: ''
f1_keywords:
- sql13.ssms.viewhelp.f1
helpviewer_keywords:
- SQL Server Management Studio
- SQL Server Management Studio for Integration Services
- SQL Server Management Studio for Reporting Services
- SQL Server Management Studio for Analysis Services
ms.custom: ''
ms.date: 05/29/2019
ms.openlocfilehash: 3f80cc74cc20c2ed02e32577fadbe13a5bf7dd38
ms.sourcegitcommit: 1800fc15075bb17b50d0c18b089d8a64d87ae726
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66500338"
---
# <a name="what-is-sql-server-management-studio-ssms"></a>O que é o SSMS (SQL Server Management Studio)?

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] (SSMS) é um ambiente integrado para gerenciar qualquer infraestrutura SQL. Use o SSMS para acessar, configurar, gerenciar, administrar e desenvolver todos os componentes do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], do Banco de Dados SQL do Azure e do SQL Data Warehouse. O SSMS fornece um único utilitário abrangente que combina um amplo grupo de ferramentas gráficas com vários editores de script avançados para fornecer acesso ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para desenvolvedores e administradores de banco de dados de todos os níveis de conhecimento.

- [**Baixar o SQL Server Management Studio (SSMS)**](download-sql-server-management-studio-ssms.md)
- [**Baixar o SQL Server Developer**](https://my.visualstudio.com/Downloads?q=SQL%20Server%20Developer)
- [**Baixar o Visual Studio**](https://www.visualstudio.com/downloads/)

## <a name="sql-server-management-studio-components"></a>Componentes do SQL Server Management Studio  
  
|Descrição|Componente|  
|---------------|---------|  
|Use o **Pesquisador de Objetos** para exibir e gerenciar todos os objetos em uma ou mais instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|[Pesquisador de Objetos](../ssms/object/object-explorer.md)|  
|Como usar o **Gerenciador de Modelos** para criar e gerenciar arquivos de texto de boilerplate que você usa para acelerar o desenvolvimento de consultas e scripts.|[Explorador de Modelos](../ssms/template/template-explorer.md)|  
|Como usar o **Gerenciador de Soluções** preterido para criar projetos usados para gerenciar itens de administração como scripts e consultas.|[Gerenciador de Soluções](../ssms/solution/solution-explorer.md)|  
|Como usar as ferramentas de design visuais incluídas no [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].|[Visual Database Tools](../ssms/visual-db-tools/visual-database-tools.md)|  
|Como usar os editores de idioma do [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] para criar interativamente e depurar consultas e scripts.|[Editores de consultas e de texto (SQL Server Management Studio)](../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)|

## <a name="sql-server-management-studio-for-business-intelligence"></a>SQL Server Management Studio para Business Intelligence

Para acessar, configurar, gerenciar e administrar o [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)], o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], use o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Embora essas três tecnologias de business intelligence dependam do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], as tarefas administrativas associadas a cada tecnologia são ligeiramente diferentes.
  
> [!NOTE]
> Para criar e modificar soluções [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]e [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , use [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull_md.md)], não [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull_md.md)] é um ambiente de desenvolvimento baseado no [!INCLUDE[msCoName](../includes/msconame_md.md)][!INCLUDE[vsprvs](../includes/vsprvs-md.md)].
  
### <a name="managing-analysis-services-solutions-using-sql-server-management-studio"></a>Gerenciando as soluções do Analysis Services com o SQL Server Management Studio

[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] permite gerenciar objetos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] , como executar backups e processar objetos.
  
[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] fornece um projeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] Script no qual é possível desenvolver e salvar scripts gravados em MDX (expressões MDX), DMX (extensões DMX) e XMLA (XML for Analysis). Use os projetos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] Script para executar tarefas de gerenciamento ou recriar objetos, como bancos de dados e cubos, nas instâncias do [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] . Por exemplo, você pode desenvolver um script XMLA em um projeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] Script que cria novos objetos diretamente em uma instância existente do [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] . Os projetos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] Script podem ser salvos como parte de uma solução e integrados ao controle do código fonte.
  
Para obter mais informações sobre como usar o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], consulte [Desenvolvimento e implementação usando o SQL Server Management Studio](../analysis-services/instances/analysis-services-scripts-project-in-sql-server-management-studio.md).
  
### <a name="managing-integration-services-solutions-using-sql-server-management-studio"></a>Gerenciando as soluções do Integration Services com o SQL Server Management Studio

[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] permite usar o serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para gerenciar pacotes e monitorar os pacotes em execução. Você também pode usar o [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] para organizar os pacotes em pastas, executar pacotes, importar e exportar pacotes, migrar pacotes DTS e atualizar pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .

### <a name="managing-reporting-services-projects-using-sql-server-management-studio"></a>Gerenciando os projetos do Reporting Services com o SQL Server Management Studio

Use o SQL Server Management Studio para habilitar recursos do Reporting Services, administrar o servidor e os bancos de dados e gerenciar funções e trabalhos.

Você pode gerenciar agendas compartilhadas usando a pasta Agendas Compartilhadas e gerenciar bancos de dados do servidor de relatórios (ReportServer, ReportServerTempdb). Você também pode criar uma função RSExecRole no banco de dados Mestre do sistema ao mover um banco de dados de servidor de relatórios para um Mecanismo de Banco de Dados do SQL Server novo ou diferente ([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde_md.md)]). Para obter mais informações sobre essas tarefas, consulte os seguintes tópicos:  

- [Tópicos de instruções do Management Studio](https://msdn.microsoft.com/60685458-9108-47bf-820a-5e7db454d408)
- [Administrando um banco de dados do servidor de relatórios](../reporting-services/report-server/administer-a-report-server-database-ssrs-native-mode.md)
- [Como criar o RSExecRole](../reporting-services/security/create-the-rsexecrole.md)
  
Você também pode gerenciar o servidor habilitando e configurando vários recursos, definindo padrões de servidor e gerenciando funções e trabalhos. Para obter mais informações sobre essas tarefas, consulte os seguintes tópicos:

- [Como definir propriedades do servidor de relatório (Management Studio)](https://msdn.microsoft.com/1ed0f84b-b12a-4e49-b65c-a11a99f9093f)
- [Como criar, excluir ou modificar uma função (Management Studio)](https://msdn.microsoft.com/3d1d56e6-a283-44a7-8417-36cb4d2c74d1)
- [Habilitando e desabilitando impressão do lado do cliente para Reporting Services](https://msdn.microsoft.com/0e709c96-7517-4547-8ef6-5632f8118524)

## <a name="non-english-language-versions-of-sql-server-management-studio-ssms"></a>Versões de idioma do SSMS (SQL Server Management Studio) que não o inglês

O bloqueio na configuração de idiomas mistos foi removido. Você pode instalar o SSMS alemão em um Windows francês. Se o idioma do sistema operacional não corresponder ao idioma do SSMS, o usuário precisará alterar o idioma em Ferramentas > Opções > Configurações Internacionais. Caso contrário, o SSMS mostrará a interface do usuário em inglês.

Para obter mais informações sobre localidade diferente com as versões anteriores, confira [Instalar versões de idioma diferente do inglês do SSMS](install-other-languages.md).

## <a name="support-policy-for-ssms"></a>Política de suporte para SSMS

- Começando com o SSMS 17.0, a equipe de Ferramentas SQL adotou a [Política de Ciclo de Vida Moderna da Microsoft](https://support.microsoft.com/help/30881/modern-lifecycle-policy).
- Leia o [comunicado de Política de Ciclo de Vida Moderna](https://support.microsoft.com/help/447912/announcing-microsoft-modern-lifecycle-policy) original.
- Para obter informações adicionais, veja as [Perguntas frequentes sobre a política moderna](https://support.microsoft.com/help/30882/modern-lifecycle-policy-faq).

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

## <a name="next-steps"></a>Próximas etapas

- [Instalar versões de idioma do SSMS (SQL Server Management Studio) que não estão em inglês](install-other-languages.md)
- [Tutorial: SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [Tutorial: Gravando instruções Transact-SQL](https://msdn.microsoft.com/2addc9be-67d0-423d-a457-192fe9d7d058)
- [Desenvolvimento e implementação usando o SQL Server Data Tools](../analysis-services/multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)
- [Reporting Services no SQL Server Data Tools](../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md)
- [Tutorial: SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/tutorials/tutorial-sql-server-management-studio)

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]