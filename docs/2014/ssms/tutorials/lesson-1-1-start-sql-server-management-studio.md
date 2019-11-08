---
title: Iniciar o SQL Server Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 25ffaea6-0eee-4169-8dd0-1da417c28fc6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bd7fed6fff4ddd55ef56e4c5b342c56b6c2f462f
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632794"
---
# <a name="start-sql-server-management-studio"></a>Iniciar o SQL Server Management Studio
  Para iniciar este tutorial, vamos olhar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="opening-sql-server-management-studio"></a>Abrindo o SQL Server Management Studio  
  
#### <a name="to-open-sql-server-management-studio"></a>Para abrir o SQL Server Management Studio  
  
1.  No menu **Iniciar** , aponte para **Todos os Programas**, aponte para [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]e clique em **SQL Server Management Studio**.  
  
    > [!NOTE]  
    >  O [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] não é instalado por padrão. Se o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] não estiver disponível, instale-o executando a Instalação. O [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] não está disponível com o [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] Express está disponível como um download gratuito no [centro de download da Microsoft](https://www.microsoft.com/download/details.aspx?id=7593), mas tem uma interface do usuário diferente da descrita neste tutorial.  
  
2.  Na caixa de diálogo **Conectar ao Servidor** , verifique as configurações padrão e clique em **Conectar**. Para se conectar, a caixa **nome do servidor** deve conter o nome do computador em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado. Se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] for uma instância nomeada, a caixa **nome do servidor** também deverá conter o nome da instância no formato \<*computer_name*>\\ *<instance_name*>.  
  
## <a name="management-studio-components"></a>Componentes do Management Studio  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] apresenta informações em janelas dedicadas a tipos específicos de informações. Informações de banco de dados são exibidas no Pesquisador de Objetos e janelas de documentos.  
  
-   Pesquisador de Objetos é uma exibição de árvore de todos os objetos de banco de dados em um servidor. Isso pode incluir os bancos de dados do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]e [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. O Pesquisador de Objetos inclui informações de todos os servidores aos quais está conectado. Ao abrir o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], você é solicitado a conectar o Pesquisador de Objetos às configurações utilizadas na última vez. Você pode clicar duas vezes em qualquer componente de Servidores Registrados e conectar-se a ele, mas não é necessário registrar um servidor para fazer a conexão.  
  
-   A janela de documentos é a maior parte do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. As janelas de documentos podem conter editores de consulta e janelas de navegador. Por padrão, é exibida a página de Resumo, conectada à instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] no computador atual.  
  
## <a name="showing-additional-windows"></a>Exibindo janelas adicionais  
  
#### <a name="to-show-the-registered-servers-window"></a>Para exibir a janela de Servidores Registrados  
  
1.  No menu **Exibir** , clique em **Servidores Registrados**.  
  
     A janela de Servidores Registrados será exibida acima do Pesquisador de Objetos. Servidores Registrados relaciona servidores gerenciados frequentemente. Você pode adicionar ou remover servidores dessa lista. Os únicos servidores relacionados serão as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no computador em que você estiver executando o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
2.  Se o servidor não aparecer, em servidores registrados, clique com o botão direito do mouse em **mecanismo de banco de dados**e clique em **Atualizar Registro do servidor local**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Conectar com os Servidores Registrados e o Pesquisador de Objetos](../object/object-explorer.md)  
  
  
