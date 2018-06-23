---
title: Implantar políticas agendadas em várias instâncias | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f551b8e8-3668-4ed4-852f-bae826254f4f
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8331f0f33874c5bfbd0811231dc2cacf494b1d89
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117775"
---
# <a name="deploy-scheduled-policies-to-multiple-instances"></a>Implantar diretivas agendadas em várias instâncias
  Usando Servidores Registrados, você poderá implantar políticas agendadas em servidores gerenciados a partir de um local central. Você poderá implantar diretivas agendadas a partir de um grupo de servidores local ou de um Servidor Central de Gerenciamento.  
  
 Nesta tarefa, você fará o seguinte:  
  
1.  Exportar as diretivas agendadas na tarefa anterior em uma pasta.  
  
2.  Implantar as diretivas agendadas nas instâncias de destino que são gerenciadas por meio de Servidores Registrados.  
  
 Você executará essas tarefas no computador em que concluiu as tarefas anteriores desta lição.  
  
## <a name="prerequisites"></a>Prerequisites  
 Esta tarefa tem os seguintes pré-requisitos:  
  
-   Você deve ter concluído as tarefas anteriores desta lição.  
  
-   As instâncias em que você implantará as diretivas agendadas deve estar executando o [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] ou uma versão posterior. A automação requer que as diretivas sejam armazenadas localmente, o que não tem suporte em versões do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)].  
  
-   Os servidores em que você deseja implantar as diretivas agendadas devem ser registrados em servidores registrados no **Local Server Groups** ou **servidores centrais de gerenciamento** nó. Para obter mais informações, consulte os tópicos a seguir:  
  
    -   [Criar ou editar um grupo de servidores &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-or-edit-a-server-group-sql-server-management-studio.md)  
  
    -   [Registrar um servidor conectado &#40;SQL Server Management Studio&#41;](../ssms/register-servers/register-a-connected-server-sql-server-management-studio.md).  
  
    -   [Criar um servidor de gerenciamento central e um grupo de servidores &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-a-central-management-server-and-server-group.md)  
  
### <a name="to-export-the-scheduled-policies-as-xml-files"></a>Para exportar as diretivas agendadas como arquivos .xml  
  
1.  No servidor em que você configurou políticas agendadas na tarefa anterior, expanda **gerenciamento**, expanda **gerenciamento de política de**e, em seguida, clique em **políticas**.  
  
2.  No menu **Exibir** , clique em **Detalhes do Pesquisador de Objetos**.  
  
3.  No **detalhes do Pesquisador** painel, selecione todas as práticas recomendadas agendadas a políticas que você deseja implantar para outros servidores através de servidores registrados.  
  
    > [!NOTE]  
    >  Você pode clicar no **categoria** título para classificar as diretivas por categoria.  
  
4.  Clique com botão direito a seleção e, em seguida, clique em **exportar política**.  
  
5.  Se você selecionou várias diretivas para exportar, o **Procurar pasta** caixa de diálogo, selecione uma pasta de destino ou crie uma nova pasta. Nesta lição, crie uma nova pasta com o caminho **C:\Scheduled_BP_Policies**e, em seguida, clique em **Okey**.  
  
     Se você selecionou apenas uma diretiva para exportar, o **exportar política** caixa de diálogo caixa, crie uma nova pasta com o caminho **C:\Scheduled_BP_Policies**, clique em **abrir**e, em seguida, clique em **Salvar**.  
  
     Os arquivos de diretivas .xml são criados no local da pasta.  
  
### <a name="to-deploy-the-scheduled-policies-to-servers-that-are-managed-through-registered-servers"></a>Para implantar as diretivas agendadas em servidores que são gerenciados por meio de Servidores Registrados  
  
1.  No menu **Exibir** , clique em **Servidores Registrados**.  
  
2.  Expanda **mecanismo de banco de dados**, expanda **Local Server Groups** ou **servidores centrais de gerenciamento**, com o botão direito no nó que você deseja implantar as políticas e, em seguida, Clique em **importar diretivas**.  
  
    > [!NOTE]  
    >  Se clicar **Local Server Groups** ou o servidor de gerenciamento Central, as diretivas serão implantadas para todos os servidores gerenciados. Se você clicar com o botão direito do mouse em um grupo específico de servidores, as diretivas serão implantadas somente nos servidores desse grupo. Se você clicar com o botão direito do mouse em um servidor registrado específico, as políticas serão implantadas nesse servidor.  
  
3.  Ao lado de **arquivos a importar**, clique no botão de reticências (**...** ).  
  
4.  No **Selecionar política** caixa de diálogo, navegue até o local da pasta onde você salvou as políticas agendadas. Neste exemplo, navegue até o local **C:\Scheduled_BP_Policies**.  
  
5.  Selecione as diretivas que você deseja importar para a instância de destino e, em seguida, clique em **abrir**.  
  
6.  No **importação** na caixa de **estado da política** , selecione o estado desejado. Você poderá optar por preservar o estado da diretiva, habilitar ou desabilitar as diretivas na importação. Lembre-se de que as diretivas devem ser habilitadas para execução em um agendamento.  
  
7.  Clique em **Okey** para importar as políticas para todas as instâncias de destino.  
  
    > [!NOTE]  
    >  Se houver erros, o **importação** caixa de diálogo não desaparecerá. Clique o **Log** página para examinar as mensagens. Clique em **Cancelar** para fechar a caixa de diálogo.  
  
8.  Para exibir as políticas de uma instância de destino, conecte-se à instância, abra o Pesquisador de objetos, expanda **gerenciamento**e, em seguida, expanda **políticas**. Você deve ver as diretivas importadas no **políticas** nó. Se você clicar duas vezes em cada diretiva, poderá ver a agenda ou alterar as configurações.  
  
    > [!NOTE]  
    >  Para exibir os resultados da avaliação após a execução de uma diretiva agendada, abra o log Histórico da Diretiva na instância de destino. Para abrir o log, clique com botão direito **gerenciamento de política de**e, em seguida, clique em **Exibir histórico**.  
  
## <a name="summary"></a>Resumo  
 Este tutorial mostrou como executar avaliações sob demanda e planejadas das diretivas de práticas recomendadas em uma ou mais instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="next"></a>Próximo  
 Este tutorial está concluído. Para retornar ao início, consulte [Tutorial: avaliando práticas recomendadas pelo gerenciamento baseado em políticas](../../2014/tutorials/tutorial-evaluating-best-practices-by-using-policy-based-management.md).  
  
 Para ver uma lista de [!INCLUDE[ssDE](../includes/ssde-md.md)] tutoriais, clique em [tutoriais do mecanismo de banco de dados](../relational-databases/database-engine-tutorials.md).  
  
## <a name="see-also"></a>Consulte também  
 [Administrar servidores com Gerenciamento Baseado em Políticas](../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  