---
title: "Configurar as propriedades de fonte de dados de um relatório (Gerenciador de Relatórios) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: data sources [Reporting Services], embedded
ms.assetid: 27af5195-c845-40e0-9a9c-efe569424022
caps.latest.revision: "44"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: ef7246b8413aa3010572290085a3f247e47e0430
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="configure-data-source-properties-for-a-report--report-manager"></a>Configurar propriedades de fonte de dados para um relatório (Gerenciador de Relatórios)
  Quando um relatório é executado, o servidor de relatório recupera informações de propriedade para determinar como conectar-se a uma fonte de dados. O tipo de fonte de dados, a cadeia de conexão e as informações de credenciais são especificados nas páginas de propriedade Fonte de Dados do relatório publicado. É possível definir as propriedades para variar as informações de conexão da fonte de dados com relação aos valores originais que foram especificados quando o relatório foi criado.  
  
 De maneira alternativa, se houver uma fonte de dados compartilhada predefinida que já especifica as informações de conexão que você deseja usar, você poderá especificar uma fonte de dados compartilhada. Para usar uma fonte de dados compartilhada, clique em **Fonte de Dados Compartilhada** na página de propriedades Fonte de Dados do relatório.  
  
### <a name="to-configure-an-embedded-data-source"></a>Para configurar uma fonte de dados inserida  
  
1.  Inicie o [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  No Gerenciador de Relatórios, navegue até a página **Conteúdo** . Navegue até o relatório para o qual deseja configurar uma fonte de dados específica e abra o relatório.  
  
3.  Clique na guia **Propriedades** . A página de propriedades **Geral** será aberta.  
  
4.  Clique na guia **Fontes de Dados** . A página de propriedades Fonte de Dados do relatório é exibida.  
  
5.  Clique em **Uma fonte de dados personalizada** para especificar informações de conexão de fonte de dados no relatório.  
  
6.  Na lista **Tipo de Conexão** , especifique a extensão de processamento de dados usada para processar dados da fonte de dados.  
  
7.  Em **Cadeia de Conexão**, especifique a cadeia de conexão usada pelo servidor de relatório para se conectar à fonte de dados. Recomendamos que você não especifique credenciais na cadeia de conexão.  
  
     O exemplo a seguir ilustra uma cadeia de conexão usada para conexão com o banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] local:  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
8.  Em **Conectar usando**, especifique como são obtidas as credenciais na execução do relatório:  
  
    -   Se desejar solicitar ao usuário o nome de logon e a senha, clique em **Credenciais fornecidas pelo usuário que está executando o relatório**.  
  
    -   Se você pretende usar a fonte de dados com relatórios que dão suporte a assinaturas ou a outras operações agendadas (como geração automatizada do histórico de relatórios, por exemplo), clique em **Credenciais armazenadas com segurança no servidor de relatório**.  
  
    -   Se desejar que o servidor de relatório passe as credenciais do usuário que está acessando o relatório para o servidor que está hospedando a fonte de dados externa, clique em **Segurança Integrada do Windows**. Nesse caso, não é solicitado que o usuário digite um nome de usuário ou senha.  
  
    -   Se a fonte de dados não usar credenciais (se a fonte de dados for um arquivo XML acessado pelo sistema de arquivos, por exemplo), clique em **Não são necessárias credenciais**. Você deve especificar esse tipo de credencial somente se ele for válido para a fonte de dados. Se você selecionar essa opção para uma fonte de dados que requer autenticação, a conexão falhará. Se essa opção for selecionada, certifique-se de configurar a conta de execução autônoma que permite que o servidor de relatório se conecte a outros computadores para recuperar dados ou arquivos quando as credenciais do usuário não estiverem disponíveis.  
  
 Para obter mais informações sobre como configurar as credenciais, consulte [Especificar informações de credenciais e de conexão para fontes de dados de relatório](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md). Para obter mais informações sobre a conta de execução autônoma, consulte [Configurar a conta de execução autônoma &#40; 	Gerenciador de Configurações do SSRS&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
## <a name="see-also"></a>Consulte também  
 [Página Conteúdo &#40;Gerenciador de Relatórios&#41;](http://msdn.microsoft.com/library/6b16869b-158a-4934-9c85-bee934b35378)   
 [Página Nova Fonte de Dados &#40;Gerenciador de Relatórios&#41;](http://msdn.microsoft.com/library/35563d4c-a3d5-4f95-bf46-605da9dfcbb8)   
 [Criar, modificar e excluir fontes de dados compartilhadas &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)   
 [Gerenciar fontes de dados de relatório](../../reporting-services/report-data/manage-report-data-sources.md)   
 [Criar, excluir ou modificar uma fonte de dados compartilhada &#40;Gerenciador de Relatórios&#41;](http://msdn.microsoft.com/library/cd7bace3-f8ec-4ee3-8a9f-2f217cdca9f2)   
 [Página Propriedades de Fontes de Dados &#40;Gerenciador de Relatórios&#41;](http://msdn.microsoft.com/library/f37edda0-19e6-489e-b544-8751fa6b6cfb)  
  
  
