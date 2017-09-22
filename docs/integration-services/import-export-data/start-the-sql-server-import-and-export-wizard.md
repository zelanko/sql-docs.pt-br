---
title: "Inicie o SQL Server de importação e exportação Assistente | Microsoft Docs"
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Import and Export Wizard
- starting SQL Server Import and Export Wizard
- Import and Export Wizard
- starting Import and Export Wizard
ms.assetid: 5fc4f6d1-1f6f-444e-9aeb-827f85e1c405
caps.latest.revision: 130
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: ada9817d628b9c146899807bba35a6651842afa3
ms.contentlocale: pt-br
ms.lasthandoff: 09/21/2017

---
# <a name="start-the-sql-server-import-and-export-wizard"></a>Iniciar o Assistente de Importação e Exportação do SQL Server

 > Para conteúdo relacionado a versões anteriores do SQL Server, consulte [executar o Assistente de exportação e importação do SQL Server](https://msdn.microsoft.com/en-US/library/ms140052(SQL.120).aspx).

Iniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assistente de importação e exportação de uma das maneiras descritas neste tópico para importar dados e exportar dados para qualquer fonte de dados com suporte.

> [!IMPORTANT]
> Este tópico descreve somente como **iniciar** o assistente. Se você estiver procurando por alguma outra coisa, consulte [relacionadas a tarefas e conteúdo](#related).

Você pode iniciar o Assistente:
-   Do [menu Iniciar](#startStart).
-   Do [prompt de comando](#startCmd). 
-   Do [SSMS (SQL Server Management Studio)](#startSSMS).
-   Do [Visual Studio com o SSDT (SQL Server Data Tools)](#startVS).

## <a name="prerequisite---is-the-wizard-installed-on-your-computer"></a>Pré - é o assistente instalado em seu computador?
Se você deseja executar o assistente, mas você não tiver [! INCLUIR[msCoName](/sql-docs/docs/ssdt/download-sql-server-data-tools-ssdt).

> [!NOTE]
> Para usar a versão de 64 bits do SQL Server Assistente de importação e exportação, você precisa instalar o SQL Server. SQL Server Data Tools (SSDT) e SQL Server Management Studio (SSMS) são aplicativos de 32 bits, somente instalar os arquivos de 32 bits, incluindo a versão de 32 bits do assistente.

## <a name="startStart"></a> menu Iniciar  
### <a name="start-the-sql-server-import-and-export-wizard-from-the-start-menu"></a>Iniciar o Assistente para exportação e importação do SQL Server no menu Iniciar
1.  Sobre o **iniciar** menu, localize e expanda **Microsoft SQL Server 2016**.
3.  Clique em uma das opções a seguir.
  
    -   **Importar e Exportar Dados do SQL Server 2016 (64 bits)**
          
    -   **Importar e Exportar Dados do SQL Server 2016 (32 bits)**  
  
    Execute a versão de 64 bits do assistente, a menos que você saiba que a fonte de dados requer um provedor de dados de 32 bits.
 
    ![Iniciar o assistente](../../integration-services/import-export-data/media/start-wizard-start.jpg)
  
## <a name="startCmd"></a> Command prompt
### <a name="start-the-sql-server-import-and-export-wizard-from-the-command-prompt"></a>Iniciar o Assistente para exportação e importação do SQL Server do prompt de comando  
Em uma janela de Prompt de comando, execute **DTSWizard.exe** de um dos seguintes locais.  
  
-   **C:\Arquivos de Programas\Microsoft SQL Server\130\DTS\Binn** para a versão de 64 bits.  
  
-   **C:\Arquivos de Programas (x86)\Microsoft SQL Server\130\DTS\Binn** para a versão de 32 bits.  
  
Execute a versão de 64 bits do assistente, a menos que você saiba que a fonte de dados requer um provedor de dados de 32 bits.

![Inicie o Assistente cmd](../../integration-services/import-export-data/media/start-wizard-cmd.jpg)  
  
## <a name="startSSMS"></a> SSMS (SQL Server Management Studio)
### <a name="start-the-sql-server-import-and-export-wizard-from-sql-server-management-studio-ssms"></a>Iniciar o SQL Server Assistente de importação e exportação do SQL Server Management Studio (SSMS)    
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)].
    
2.  Expanda os **Bancos de dados**.
3.  Clique com o botão direito do mouse em um banco de dados.
4.  Aponte para **Tarefas**.
5.  Clique em uma das opções a seguir.
  
    -   **Importar dados**
      
    -   **Exportar dados**  

    ![Inicie o Assistente SSMS](../../integration-services/import-export-data/media/start-wizard-ssms.jpg) 

Se você não tem o SQL Server instalado, ou se tem o SQL Server, mas não tem o SQL Server Management Studio instalado, consulte [Baixar o SSMS (SQL Server Management Studio)](/sql-docs/docs/ssms/download-sql-server-management-studio-ssms).
  
## <a name="startVS"></a>O Visual Studio
### <a name="start-the-sql-server-import-and-export-wizard-from-visual-studio-with-sql-server-data-tools-ssdt"></a>Iniciar o SQL Server Assistente de importação e exportação do Visual Studio com SQL Server Data Tools (SSDT) 
 No Visual Studio com o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], com um projeto do Integration Services aberto, faça um dos itens a seguir. 
  
-   No menu **Projeto** , clique em **Assistente de Importação e Exportação do SSIS**. 

    ![Inicie o projeto do assistente](../../integration-services/import-export-data/media/start-wizard-project.jpg) 
    
    \- ou –
    
-   No Gerenciador de Soluções, clique com o botão direito do mouse na pasta **Pacotes SSIS** e clique em **Assistente de Importação e Exportação do SSIS**.

    ![Inicie pacotes do assistente](../../integration-services/import-export-data/media/start-wizard-packages.jpg)

Se você não tem o Visual Studio instalado ou se tem o Visual Studio, mas não tem o SQL Server Data Tools instalado, consulte [Baixar o SSDT (SQL Server Data Tools)](/sql-docs/docs/ssdt/download-sql-server-data-tools-ssdt).

## <a name="get-the-wizard"></a>Obter o Assistente
Se você deseja executar o assistente, mas você não tiver [! INCLUIR[msCoName](/sql-docs/docs/ssdt/download-sql-server-data-tools-ssdt).

## <a name="get-help-while-the-wizard-is-running"></a>Obter ajuda enquanto o assistente está em execução
> [!TIP]
> Pressione a tecla F1 em qualquer caixa de diálogo ou página do assistente para ver a documentação da página atual.   

 ## <a name="whats-next"></a>O que vem a seguir?  
 Quando você iniciar o assistente, a primeira página será **Bem-vindo ao Assistente de Importação e Exportação do SQL Server**. Você não precisa realizar nenhuma ação nesta página. Para obter mais informações, consulte [Bem-vindo ao Assistente de Importação e Exportação do SQL Server](../../integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md).  
  
## <a name="related"></a>Conteúdo e tarefas relacionadas  
 Aqui estão algumas outras tarefas básicas.
-   **Veja um exemplo rápido de como funciona o assistente.**

    -   **Se preferir ver capturas de tela.** Veja este exemplo de ponta a ponta simples em uma única página - [começar com esse exemplo simples de Assistente de importação e exportação](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md).

    -   **Se você preferir assistir um vídeo.** Assista a este vídeo de quatro minutos do YouTube que demonstra o assistente e explica claramente e simplesmente como exportar dados para Excel - [usando o SQL Server Assistente de importação e exportação para exportar para Excel](https://go.microsoft.com/fwlink/?linkid=829049).

-   **Saiba mais sobre como funciona o assistente.**

    -   **Saiba mais sobre o assistente.** Se você estiver procurando uma visão geral sobre o assistente, consulte [Importar e Exportar Dados com o Assistente de Importação e Exportação do SQL Server](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).

    -   **Saiba mais sobre as etapas no assistente.** Se você estiver procurando informações sobre as etapas no assistente, consulte [as etapas no Assistente para exportação e do SQL Server Import](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md). Também é uma página separada da documentação de cada página do assistente.

    -   **Saiba como se conectar a fontes de dados e destinos.** Se você estiver procurando informações sobre como conectar-se aos seus dados, selecione a página que você deseja na lista aqui - [conectar-se a fontes de dados com o SQL Server Assistente de importação e exportação](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md). Há uma página separada da documentação para cada uma das várias fontes de dados usadas com frequência.



