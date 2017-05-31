---
title: "Adicionar um relatório personalizado ao Management Studio | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], custom reports
ms.assetid: 3cf8d726-0a90-4f80-98d0-352a2a59be0f
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 04726d3d8f01dbb667ab728abd56fce8e7ce3933
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="add-a-custom-report-to-management-studio"></a>adicionar um relatório personalizado ao Management Studio
Esse tópico descreve como criar um relatório simples do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion_md.md)] que é salvo como um arquivo .rdl e, em seguida, adicionar esse arquivo rdl ao [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] como um relatório personalizado. [!INCLUDE[ssRS](../../includes/ssrs_md.md)] pode criar um ampla variedade de relatórios sofisticados. Para criar um relatório com o uso desse tópico, o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull_md.md)] deve estar instalado no computador. Não é necessário instalar o [!INCLUDE[ssRS](../../includes/ssrs_md.md)] no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para executar um relatório personalizado com o [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)].  
  
 
### <a name="to-create-a-simple-report-saved-as-an-rdl-file"></a>Para criar um relatório simples salvo como um arquivo .rdl  
  
1.  Clique em **Iniciar**, aponte para **Programas**, **Microsoft SQL Server**e clique em **Ferramentas de Dados do SQL Server**.  
  
2.  No menu **Arquivo** , aponte para **Novo**e clique em **Projeto**.  
  
3.  Na lista **Tipos de Projeto** , clique em **Projetos de Business Intelligence**.  
  
4.  Na lista **Modelos** , clique em **Assistente de Projeto do Servidor de Relatório**.  
  
5.  Em **Nome**, digite **ConnectionsReport**e clique em **OK**.  
  
6.  Na página de introdução do **Assistente de Relatório** , clique em **Avançar**.  
  
7.  Na página **Selecionar Fonte de Dados** , na caixa Nome, digite um nome para essa conexão com o [!INCLUDE[ssDE](../../includes/ssde_md.md)]e clique em **Editar**.  
  
8.  Na caixa de diálogo **Propriedades da Conexão** , na caixa **Nome do servidor** , digite o nome da sua instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
9. Na caixa **Selecionar ou digitar um nome de banco de dados** , digite o nome de qualquer banco de dados no seu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], como [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject_md.md)], e depois clique em **OK**.  
  
10. Na página **Selecionar Fonte de Dados** , clique em **Avançar**.  
  
11. Na página **Criar Consulta** , na caixa **Cadeia de caracteres de consulta** , digite a instrução [!INCLUDE[tsql](../../includes/tsql_md.md)] a seguir que lista as conexões atuais com o [!INCLUDE[ssDE](../../includes/ssde_md.md)]e clique em **Avançar**. A caixa de cadeia de caracteres de Consulta do Assistente de Relatório não aceita parâmetros de relatório. Relatórios personalizados mais complexos devem ser criados manualmente.  
  
    **SELECT session_id, net_transport FROM sys.dm_exec_connections;**  
  
12. Na página **Selecionar Tipo de Relatório** , selecione **Tabular**e clique em **Concluir**.  
  
13. Na página **Concluindo o Assistente** , na caixa **Nome do relatório** , digite **ConnectionsReport**e clique em **Concluir** para criar e salvar o relatório.  
  
14. Feche o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio_md.md)].  
  
15. Copie **ConnectionsReport.rdl** para uma pasta que você criou no servidor de banco de dados para relatórios personalizados.  
  
### <a name="to-add-a-report-to-management-studio"></a>Para adicionar um relatório ao Management Studio  
  
-   No [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)], clique com o botão direito do mouse em um nó no Pesquisador de Objetos, aponte para **Relatórios**e clique em **Relatórios Personalizados**. Na caixa de diálogo **Abrir Arquivo** , localize a pasta de relatórios personalizados, selecione o arquivo **ConnectionsReport.rdl** e clique em **Abrir**.  
  
    Quando um novo relatório personalizado é aberto pela primeira vez de um nó do Pesquisador de Objetos, esse relatório é adicionado à lista dos relatórios usados mais recentemente, em **Relatórios Personalizados** no menu de atalho desse nó. Quando um relatório padrão é aberto pela primeira vez, ele também é exibido nessa lista, em **Relatórios Personalizados**. Se um relatório personalizado for excluído, na próxima vez que ele for selecionado, será exibido um prompt para excluir o item da lista de relatórios usados mais recentemente.  
  
    1.  Para alterar o número de arquivos exibidos na lista de itens usados recentemente, no menu **Ferramentas** , clique em **Opções** , expanda a pasta **Ambiente** e clique em **Geral**.  
  
    2.  Ajuste o número para **Exibir arquivos na lista dos usados recentemente**.  
  
## <a name="see-also"></a>Consulte também  
[Relatórios personalizados no Management Studio](../../ssms/object/custom-reports-in-management-studio.md)  
[Usar relatórios personalizados com propriedades de nó do Pesquisador de Objetos](../../ssms/object/use-custom-reports-with-object-explorer-node-properties.md)  
[Cancelar supressão da execução de avisos de relatório personalizado](../../ssms/object/unsuppress-run-custom-report-warnings.md)  
[SQL Server Reporting Services](http://msdn.microsoft.com/en-us/b8d18d3d-9db0-43e7-8286-7b46cc3a37ed)  
  

