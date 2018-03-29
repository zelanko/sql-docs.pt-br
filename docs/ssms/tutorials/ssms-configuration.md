---
Title: 'Tutorial: SQL Server Management Studio Components and Configuration'
description: Um tutorial que descreve os componentes e opções de configuração básicas para seu ambiente do SQL Server Management Studio.
keywords: SQL Server, SSMS, SQL Server Management Studio
author: MashaMSFT
ms.author: mathoma
ms.date: 03/16/2018
ms.topic: Tutorial
ms.suite: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
ms.openlocfilehash: 8cdb4f258f62b425be78e9f6b4628d69e304c7ba
ms.sourcegitcommit: ccb05cb5a4cccaf7ffa9e85a4684fa583bab914e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2018
---
# <a name="tutorial-sql-server-management-studio-components-and-configuration"></a>Tutorial: componentes e configuração do SQL Server Management Studio
Este Tutorial descreve os diferentes componentes de janela no SSMS (SQL Server Management Studio) e algumas opções de configuração básicas para seu espaço de trabalho. Neste artigo, você aprenderá sobre como: 

> [!div class="checklist"]
> * Os diferentes componentes que formam o ambiente de SSMS
> * Alterar o layout do ambiente e redefini-lo para o padrão
> * Maximizar o editor de consultas
> * Alterar a fonte 
> * Configurar as opções de inicialização 
> * Redefinir a configuração de volta ao padrão 

## <a name="prerequisites"></a>Prerequisites
Para concluir este Tutorial, você precisará do SQL Server Management Studio.  

- Instalar o [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="sql-server-management-studio-components"></a>Componentes do SQL Server Management Studio
Esta seção aborda os diferentes componentes de janela disponíveis no espaço de trabalho e sua finalidade. 

- Cada componente de janela pode ser fechado clicando no X no canto superior da barra de título e reaberto na lista suspensa **Exibir** no menu principal. 

    ![Menu Exibir](media/ssms-configuration/viewmenu.png)

- **Pesquisador de Objetos** (F8): o Pesquisador de Objetos é um modo de exibição de árvore de todos os objetos de banco de dados em um servidor. Isso pode incluir bancos de dados do Mecanismo de Banco de Dados do SQL Server, Analysis Services, Reporting Services e Integration Services. O Pesquisador de Objetos inclui informações de todos os servidores aos quais está conectado. 
    
    ![Pesquisador de Objetos](media/ssms-configuration/objectexplorer.png)
- **Janela de Consulta** (Ctrl+N): depois de clicar em **Nova Consulta**, esta é a janela onde você digitará em suas consultas T-SQL (Transact-SQL). Os resultados das consultas também serão exibidos aqui.
    
    ![Janela Nova Consulta](media/ssms-configuration/newquery.png)

- **Propriedades** (F4): isso fica visível depois que a **Janela de Consulta** é aberta e exibe as propriedades básicas da consulta. Por exemplo, ela mostrará a hora de início de uma consulta, o número de linhas retornado e os detalhes da conexão.  

    ![Propriedades](media/ssms-configuration/properties.png)

- **Navegador de Modelos** (Ctrl+Alt+T): há diversos modelos predefinidos do T-SQL que podem ser encontrados no navegador de modelos. Esses modelos permitem que você execute várias funções, como criar ou fazer backup de um banco de dados. 

    ![Navegador de Modelos](media/ssms-configuration/templates.png)

- **Detalhes do Pesquisador de Objetos**(F7): esta é uma exibição mais granular do que está visível no Pesquisador de Objetos, e permite que você manipule vários objetos ao mesmo tempo. Por exemplo, a janela de Detalhes do Pesquisador de Objetos permite que você selecione vários bancos de dados simultaneamente e os exclua ou gere o script deles. 

    ![Detalhes do Pesquisador de Objetos](media/ssms-configuration/objectexplorerdetails.PNG) 
 

    

## <a name="change-the-environmental-layout"></a>Alterar o layout do ambiente 
Esta seção aborda como manipular o layout do ambiente, tal como mover as diversas janelas. 

-  Cada componente da janela pode ser movido mantendo pressionado o título e arrastando a janela. 
- Cada componente da janela pode ser fixado e desafixado selecionando o ícone de pino na barra de título:
    
    ![Fixar objetos](media/ssms-configuration/pushpin.png)

- Cada componente de janela tem uma seta suspensa que permite que a janela ser manipulada de diversas maneiras: 

    ![Opções de janela](media/ssms-configuration/windowoptions.png)

- Quando você tiver duas ou mais janelas de consulta abertas, elas podem ser navegadas verticalmente ou horizontalmente, para que ambas as janelas de consulta fiquem visíveis ao mesmo tempo. Para fazer isso, clique com o botão direito do mouse no título da consulta e selecione a opção de navegação pelas guias desejada. 
 
    ![Opções de guia de consulta](media/ssms-configuration/querytabbedoptions.png)

    - Este é o **Agrupamento de guias horizontal**: ![Agrupamento de guias horizontal](media/ssms-configuration/horizontaltab.png)     
    
    - Este é o **Agrupamento de guias vertical**:  
        ![Agrupamento de guias horizontal](media/ssms-configuration/verticaltabgroup.png)
        

    - Para mesclar as guias novamente, clique com o botão direito do mouse no título da consulta novamente e em **Mover para o próximo grupo de guias** ou **Mover para o grupo de guias anterior**:
    
        ![Mesclar guias de consulta](media/ssms-configuration/mergetabgroups.png)

- Para restaurar o layout do ambiente padrão, clique no **Menu de Janela** > **Redefinir Layout da Janela**:
 
    ![Restaurar Layout de Janela](media/ssms-configuration/resetwindowlayout.png)
    
## <a name="maximize-query-editor"></a>Maximizar o Editor de Consultas
O editor de consultas pode ser maximizado para o modo de tela inteira.

1. Clique em qualquer lugar na Janela do Editor de Consultas.
2. Pressione SHIFT + ALT + ENTER para alternar entre o modo de tela inteira e o modo comum. 

Esse atalho de teclado funciona com qualquer janela de documentos. 



## <a name="change-basic-settings"></a>Alterar as configurações básicas
Esta seção descreve como modificar algumas configurações básicas no SSMS. Essas opções encontram-se a opções do menu **Ferramentas**:

  ![Menu Ferramentas](media/ssms-configuration/tools.png)


- A barra de ferramentas realçada pode ser modificada acessando o menu: **Ferramentas** > **Personalizar**:

    ![Personalizar Barra de Ferramentas](media/ssms-configuration/toolbar.png)

### <a name="change-the-font"></a>Alterar fonte
- A fonte pode ser alterada no menu: **Ferramentas** > **Opções** > **Fontes e Cores**:

     ![Fontes e Cores](media/ssms-configuration/fontsandcolors.png)

### <a name="change-the-startup-options"></a>Alterar as opções de inicialização
- As opções de inicialização determinam como seu espaço de trabalho aparece ao abrir o SSMS pela primeira vez. Elas podem ser configuradas no menu: **Ferramentas** > **Opções** > **Inicialização**:
 
    ![Opções de inicialização](media/ssms-configuration/startup.png)

### <a name="reset-settings-to-default"></a>Redefinir as configurações como o padrão
- Todas essas configurações podem ser exportadas e importadas no menu: **Ferramentas** > **Importar e Exportar Configurações** 

    ![Importar + Exportar Configurações](media/ssms-configuration/settings.png)
    - Também é aqui que você pode redefinir todas as suas configurações para o padrão. 


## <a name="next-steps"></a>Próximas etapas
O próximo artigo apresentará dicas e truques adicionais para usar o SSMS, como localizar o log de erros do SQL Server e o nome da instância SQL. 

Prossiga para o próximo artigo para saber mais
> [!div class="nextstepaction"]
> [Botão Próximas etapas](ssms-tricks.md)
 
 




