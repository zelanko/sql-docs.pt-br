---
title: 'Lição 1: Criando um projeto do servidor de relatório (Reporting Services) | Microsoft Docs'
ms.custom: ''
ms.date: 11/30/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: reporting-services
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
ms.assetid: 675671ca-e6c9-48a2-82e9-386778f3a49f
caps.latest.revision: 57
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fea148cc4148b4beaf14c8b31d7bd23aad734a0b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33016523"
---
# <a name="lesson-1-creating-a-report-server-project-reporting-services"></a>Lição 1: Criando um projeto do servidor de relatórios (Reporting Services)

 > Para obter o conteúdo relacionado a versões anteriores do SQL Server, consulte [Lição 1: Criando um projeto do servidor de relatório (Reporting Services)](https://msdn.microsoft.com/en-US/library/ms167559(SQL.120).aspx).

Nesta lição, você criará um *projeto do servidor de relatórios* e um *arquivo de definição de relatório (.rdl)* [!INCLUDE[ssBIDevStudio_md](../includes/ssbidevstudio-md.md)] no Visual Studio. 

Para criar um relatório com o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], primeiro você precisa de um projeto do servidor de relatório em que possa salvar o arquivo de definição (.rdl) do relatório e outros arquivos de recursos de que precisa para o relatório. 

Nas próximas lições, você define uma fonte de dados para o relatório, define um conjunto de dados e define o layout do relatório. Quando você executa o relatório, os dados são recuperados e combinados ao layout e renderizados na tela. Depois disso, você pode exportá-los, imprimi-los ou salvá-los.  
  
  
  
## <a name="to-create-a-report-server-project"></a>Para criar um projeto do servidor de relatórios  
  
1.  Abra o [!INCLUDE[ssBIDevStudio_md](../includes/ssbidevstudio-md.md)].  
  
2.  No menu **Arquivo** > **Novo** > **Projeto**.  

    ![ssrs-ssdt-file-01-new-project](../reporting-services/media/ssrs-ssdt-file-01-new-project.png)
  
3.  Em **Instalados** > **Modelos** > **Business Intelligence**, clique em **Reporting Services**.

    ![ssrs-ssdt-01-new-rs-project](../reporting-services/media/ssrs-ssdt-01-new-rs-project.png)

5. Clique em **Projeto do Servidor de Relatório** ![ssrs_ssdt_report_server_project](../reporting-services/media/ssrs-ssdt-report-server-project.png). 

   >**Observação**: se as opções **Business Intelligence** ou **Projeto do Servidor de Relatório** não estiverem visíveis, será necessário atualizar o SSDT com os modelos de Business Intelligence. Consulte [Baixar o SSDT (SQL Server Data Tools)](../ssdt/download-sql-server-data-tools-ssdt.md)  
  
5.  Em **Nome**, digite **Tutorial**.  

    Por padrão, ele é criado na pasta Visual Studio 2015\Projects em um novo diretório.
    
    ![ssrs-ssdt-01-solution-location](../reporting-services/media/ssrs-ssdt-01-solution-location.png)
  
6.  Clique em **OK** para criar o projeto.  
  
    O projeto Tutorial é exibido no painel Gerenciador de Soluções, à direita.  
  
## <a name="to-create-a-new-report-definition-file"></a>Para criar um novo arquivo de definição de relatório  
  
1.  No painel **Gerenciador de Soluções** , clique com o botão direito do mouse em **Relatórios** > **Adicionar** > **Novo Item**. 

    >**Dica**: se você não vir o painel **Gerenciador de Soluções** , no menu **Exibir** , clique em **Gerenciador de Soluções**. 

    ![ssrs_ssdt_add_report](../reporting-services/media/ssrs-ssdt-add-report.png)
  
2.  Na janela **Adicionar Novo Item** , clique em **Relatório** ![ssrs_ssdt_report](../reporting-services/media/ssrs-ssdt-report.png).  
  
3.  Em **Nome**, digite **Sales Orders.rdl** e clique em **Adicionar**.  
  
    O Designer de Relatórios abre e exibe o novo arquivo .rdl na exibição Design.  
    
    ![ssrs-ssdt-01-new-report-designer](../reporting-services/media/ssrs-ssdt-01-new-report-designer.png)
  
     O Designer de Relatórios é um componente do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] que é executado no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Ele tem duas exibições: **Design** e **Visualização**. Clique em cada guia para alterar exibições.  
  
    Você define os dados no painel **Dados do Relatório** . Você define o layout do relatório no modo **Design** . É possível executar o relatório e ver sua aparência na exibição **Visualização** .  
  
## <a name="next-lesson"></a>Próxima lição  
Você criou um projeto de relatório chamado "Tutorial" e adicionou um arquivo de definição de relatório (.rdl) ao projeto de relatório com êxito. Em seguida, você especificará uma fonte de dados para usar para o relatório. Consulte [Lição 2: Especificando informações de conexão &#40;Reporting Services&#41;](../reporting-services/lesson-2-specifying-connection-information-reporting-services.md).  
  
## <a name="see-also"></a>Consulte Também  
[Criar um relatório de tabela básico &#40;Tutorial do SSRS&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  
  

