---
title: "Iniciar o Assistente de Importa&#231;&#227;o e Exporta&#231;&#227;o do SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Assistente de Importação e Exportação do SQL Server"
  - "iniciando o Assistente de Importação e Exportação do SQL Server"
  - "Assistente de Importação e Exportação"
  - "iniciando o Assistente de Importação e Exportação"
ms.assetid: 5fc4f6d1-1f6f-444e-9aeb-827f85e1c405
caps.latest.revision: 130
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 112
---
# Iniciar o Assistente de Importa&#231;&#227;o e Exporta&#231;&#227;o do SQL Server
Você pode iniciar o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de uma das seguintes maneiras.
-   Do [menu Iniciar](#startStart) ou do [prompt de comando](#startCmd), para importar ou exportar para qualquer fonte de dados com suporte.
-   Do [SSMS (SQL Server Management Studio)](#startSSMS), se você estiver importando para o SQL Server ou exportando do SQL Server.
-   Do [Visual Studio com o SSDT (SQL Server Data Tools)](#startVS), se você tiver um projeto do SQL Server Integration Services aberto.

Este tópico descreve somente como **iniciar** o assistente.
-   Se você estiver procurando uma visão geral sobre o assistente, consulte [Importar e Exportar Dados com o Assistente de Importação e Exportação do SQL Server](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).
-   Se você estiver procurando informações sobre as etapas no assistente, selecione a página desejada no menu de navegação de conteúdo. Há uma página separada da documentação para cada página do assistente. Ou pressione a tecla F1 em qualquer caixa de diálogo ou página do assistente para ver a documentação da página atual.

**Obtenha o assistente.** Se você deseja executar o assistente, mas não tem o [!INCLUDE[msCoName] (../Token/msCoName_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado no computador, é possível instalar o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalando o SSDT (SQL Server Data Tools). Para obter mais informações, consulte [Baixar o SSDT (SQL Server Data Tools)](https://msdn.microsoft.com/library/mt204009.aspx).  

## <a name="a-namestartstarta-start-the-wizard-from-the-start-menu"></a><a name="startStart"></a> Inicie o assistente no menu Iniciar  
1.  No menu **Iniciar**, clique em **Todos os aplicativos**.
2.  Localize e expanda **Microsoft SQL Server 2016**.
3.  Clique em uma das opções a seguir.
  
    -   **Importar e Exportar Dados do SQL Server 2016 (64 bits)**
          
    -   **Importar e Exportar Dados do SQL Server 2016 (32 bits)**  
  
Execute a versão de 64 bits do assistente, a menos que você saiba que a fonte de dados requer um provedor de dados de 32 bits.
 
![Iniciar o assistente](../../integration-services/import-export-data/media/start-wizard-start.jpg)
  
## <a name="a-namestartcmda-start-the-wizard-from-the-command-prompt"></a><a name="startCmd"></a> Inicie o assistente do prompt de comando  
Em uma janela de Prompt de comando, execute **DTSWizard.exe** de um dos seguintes locais.  
  
-   **C:\Arquivos de Programas\Microsoft SQL Server\130\DTS\Binn** para a versão de 64 bits.  
  
-   **C:\Arquivos de Programas (x86)\Microsoft SQL Server\130\DTS\Binn** para a versão de 32 bits.  
  
Execute a versão de 64 bits do assistente, a menos que você saiba que a fonte de dados requer um provedor de dados de 32 bits.

![Inicie o Assistente cmd](../../integration-services/import-export-data/media/start-wizard-cmd.jpg)  
  
## <a name="a-namestartssmsa-start-the-wizard-from-sql-server-management-studio-ssms"></a><a name="startSSMS"></a> Inicie o assistente do SSMS (SQL Server Management Studio)  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)].
2.  Expanda os **Bancos de dados**.
3.  Clique com o botão direito do mouse em um banco de dados.
4.  Aponte para **Tarefas**.
5.  Clique em uma das opções a seguir.
  
    -   **Importar dados**
      
    -   **Exportar dados**  

![Inicie o Assistente SSMS](../../integration-services/import-export-data/media/start-wizard-ssms.jpg) 

Se você não tem o SQL Server instalado, ou se tem o SQL Server, mas não tem o SQL Server Management Studio instalado, consulte [Baixar o SSMS (SQL Server Management Studio)](https://msdn.microsoft.com/library/mt238290.aspx).
    
## <a name="a-namestartvsa-start-the-wizard-from-visual-studio-with-sql-server-data-tools-ssdt"></a><a name="startVS"></a> Inicie o assistente do Visual Studio com o SSDT (SQL Server Data Tools)  
 No Visual Studio com o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], com um projeto do Integration Services aberto, faça um dos itens a seguir.  
  
-   No menu **Projeto**, clique em **Assistente de Importação e Exportação do SSIS**. 

    ![Inicie o projeto do assistente](../../integration-services/import-export-data/media/start-wizard-project.jpg) 
    
    \- ou –
    
-   No Gerenciador de Soluções, clique com o botão direito do mouse na pasta **Pacotes SSIS** e clique em **Assistente de Importação e Exportação do SSIS**.

    ![Inicie pacotes do assistente](../../integration-services/import-export-data/media/start-wizard-packages.jpg)

Se você não tem o Visual Studio instalado ou se tem o Visual Studio, mas não tem o SQL Server Data Tools instalado, consulte [Baixar o SSDT (SQL Server Data Tools)](https://msdn.microsoft.com/library/mt204009.aspx). 

## <a name="get-help-while-the-wizard-is-running"></a>Obter ajuda enquanto o assistente está em execução
> [!TIP] Pressione a tecla F1 em qualquer caixa de diálogo ou página do assistente para ver a documentação da página atual.   

 ## <a name="whats-next"></a>O que vem a seguir?  
 Quando você iniciar o assistente, a primeira página será **Bem-vindo ao Assistente de Importação e Exportação do SQL Server**. Você não precisa realizar nenhuma ação nesta página. Para obter mais informações, consulte [Bem-vindo ao Assistente de Importação e Exportação do SQL Server](../../integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md).  
  
  