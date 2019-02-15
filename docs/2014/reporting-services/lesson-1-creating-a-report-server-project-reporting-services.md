---
title: 'Lição 1: Criando um projeto de servidor de relatório (Reporting Services) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 675671ca-e6c9-48a2-82e9-386778f3a49f
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 48ad3fd25dd842ca1f4979a6875887d6ad656508
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56286464"
---
# <a name="lesson-1-creating-a-report-server-project-reporting-services"></a>Lição 1: Criando um projeto do servidor de relatório (Reporting Services)
  Para criar um relatório no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], primeiro crie um projeto de servidor de relatório em que o arquivo de definição de relatório (.rdl) e qualquer outro arquivo de recursos que seja necessário sejam salvos para o relatório. Em seguida, você criará o arquivo de definição do relatório real, definirá uma fonte de dados para o relatório, um conjunto de dados e o layout do relatório. Quando você executar o relatório, os dados reais serão recuperados e combinados com o layout e renderizados na tela, de onde ele poderá ser exportado, impresso ou salvo.  
  
 Nesta lição, você obterá informações sobre como criar um projeto de servidor de relatório no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Um projeto de servidor de relatório é usado para criar relatórios que são executados em um servidor de relatório.  
  
### <a name="to-create-a-report-server-project"></a>Para criar um projeto do servidor de relatórios  
  
1.  Clique em **inicie**, aponte para **todos os programas**, aponte para [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]e, em seguida, clique em **SQL Server Data Tools**. Se esta for a primeira vez que você abriu [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique em **configurações do Business Intelligence** para as configurações de ambiente padrão.  
  
2.  No menu **Arquivo** , aponte para **Novo**e clique em **Projeto**.  
  
3.  Na lista **Modelos Instalados** , clique em **Business Intelligence**.  
  
4.  Clique em **projeto de servidor de relatório**.  
  
5.  Em **Nome**, digite **Tutorial**.  
  
6.  Clique em **OK** para criar o projeto.  
  
     O projeto Tutorial é exibido no Gerenciador de Soluções.  
  
### <a name="to-create-a-new-report-definition-file"></a>Para criar um novo arquivo de definição de relatório  
  
1.  No Gerenciador de soluções, clique com botão direito **relatórios**, aponte para **Add**e clique em **Novo Item**.  
  
    > [!NOTE]  
    >  Se a janela **Gerenciador de Soluções** não estiver visível, no menu **Exibir** , clique em **Gerenciador de Soluções**.  
  
2.  No **Adicionar Novo Item** caixa de diálogo **modelos**, clique em **relatório**.  
  
3.  Em **Nome**, digite **Sales Orders.rdl** e clique em **Adicionar**.  
  
     O Designer de Relatórios abre e exibe o novo arquivo .rdl na exibição Design.  
  
 O Designer de Relatórios é um componente do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] que é executado no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Ele tem dois modos de exibição: **Design** e **visualização**. Clique em cada guia para alterar exibições.  
  
 Você define os dados no painel **Dados do Relatório** . Você define o layout do relatório no modo **Design** . É possível executar o relatório e ver sua aparência na exibição **Visualização** .  
  
## <a name="next-task"></a>Próxima tarefa  
 Você criou um projeto de relatório chamado "Tutorial" e adicionou um arquivo de definição de relatório (.rdl) ao projeto de relatório com êxito. Em seguida, você especificará uma fonte de dados para usar para o relatório. Consulte [lição 2: Especificar informações de Conexão &#40;Reporting Services&#41;](lesson-2-specifying-connection-information-reporting-services.md).  
  
## <a name="see-also"></a>Consulte também  
 [Criar um relatório de tabela básico &#40;Tutorial do SSRS&#41;](create-a-basic-table-report-ssrs-tutorial.md)  
  
  
