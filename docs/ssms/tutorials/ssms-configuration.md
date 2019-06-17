---
title: 'Tutorial: componentes e configuração do SQL Server Management Studio'
description: Um tutorial descrevendo os componentes e as opções de configuração básica para seu ambiente do SQL Server Management Studio.
keywords: SQL Server, SSMS, SQL Server Management Studio
author: MashaMSFT
ms.author: mathoma
ms.date: 03/16/2018
ms.topic: tutorial
ms.prod: sql
ms.technology: ssms
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
ms.openlocfilehash: 10be7a0bcc588961321713e365819a5f699bcbc9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66822275"
---
# <a name="tutorial-sql-server-management-studio-components-and-configuration"></a>Tutorial: componentes e configuração do SQL Server Management Studio

Este tutorial descreve os diversos componentes de janela no SSMS (SQL Server Management Studio) e algumas opções de configuração básicas para seu workspace. Neste artigo, você aprenderá como: 

> [!div class="checklist"]
> * Identificar os componentes que formam o ambiente de SSMS
> * Alterar o layout do ambiente e redefini-lo para o padrão
> * Maximizar o editor de consultas
> * Alterar fonte 
> * Configurar as opções de inicialização 
> * Redefinir a configuração para o padrão 

## <a name="prerequisites"></a>Prerequisites
Para concluir este tutorial, você precisará do SQL Server Management Studio.  

- Instalar o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="sql-server-management-studio-components"></a>Componentes do SQL Server Management Studio
Esta seção descreve os vários componentes de janela que estão disponíveis no workspace e como usá-los. 

- Para fechar uma janela, selecione o **X** no canto direito da barra de título. 
- Para reabrir uma janela, selecione a janela no menu **Exibir**. 

    ![No menu Exibir](media/ssms-configuration/viewmenu.png)

- **Pesquisador de Objetos** (F8): Pesquisador de Objetos é uma exibição de árvore de todos os objetos de banco de dados em um servidor. Essa exibição inclui os bancos de dados do Mecanismo de Banco de Dados do SQL Server, SQL Server Analysis Services, SQL Server Reporting Services e SQL Server Integration Services. O Pesquisador de Objetos inclui informações de todos os servidores conectados a ele. 
    
    ![Pesquisador de Objetos](media/ssms-configuration/objectexplorer.png)
- **Janela de Consulta** (Ctrl+N): depois de selecionar **Nova Consulta**, insira suas consultas T-SQL (Transact-SQL) nesta janela. Os resultados das suas consultas também são exibidos aqui.
    
    ![Janela Nova Consulta](media/ssms-configuration/newquery.png)

- **Propriedades** (F4): você pode ver a exibição Propriedades quando a Janela de Consulta está aberta. A exibição mostra as propriedades básicas da consulta. Por exemplo, mostra a hora em que uma consulta começou, o número de linhas retornadas e os detalhes da conexão.  

    ![Propriedades](media/ssms-configuration/properties.png)

- **Navegador de Modelos** (Ctrl+Alt+T): o Navegador de Modelos tem vários modelos T-SQL predefinidos. Você pode usar esses modelos para executar várias funções, como criar ou fazer backup de um banco de dados. 

    ![Navegador de Modelos](media/ssms-configuration/templates.png)

- **Detalhes do Pesquisador de Objetos** (F7): essa exibição é mais granular do que a exibição no Pesquisador de Objetos. Você pode usar os Detalhes do Pesquisador de Objetos para manipular vários objetos ao mesmo tempo. Por exemplo, nesta janela, você pode selecionar vários bancos de dados e excluí-los ou criar o script deles simultaneamente. 

    ![Detalhes do Pesquisador de Objetos](media/ssms-configuration/objectexplorerdetails.PNG) 
 
    

## <a name="change-the-environment-layout"></a>Alterar o layout do ambiente 
Esta seção descreve como alterar o layout do ambiente, por exemplo, como mover várias janelas. 

- Para mover uma janela, pressione e segure o título e, em seguida, arraste a janela. 
- Para fixar ou desafixar uma janela, selecione o ícone de alfinete na barra de título:
    
    ![Fixar um objeto](media/ssms-configuration/pushpin.png)

- Cada componente de janela tem um menu suspenso que você pode usar para manipular a janela de várias maneiras: 

    ![Opções de janela](media/ssms-configuration/windowoptions.png)

- Quando duas ou mais janelas de consulta estão abertas, elas podem ser colocadas em guias vertical ou horizontalmente para que ambas as janelas de consulta fiquem visíveis. Para exibir janelas com guias, clique com o botão direito do mouse no título da consulta e, em seguida, selecione a opção com guias que você deseja: 
 
    ![Opções de guia de consulta](media/ssms-configuration/querytabbedoptions.png)

    - Aqui está um Grupo de Guias Horizontais:

      ![Um exemplo de Grupo de Guias Horizontais](media/ssms-configuration/horizontaltab.png)     
    
    - Aqui está um Grupo de Guias Verticais:

      ![Um exemplo de Grupo de Guias Verticais](media/ssms-configuration/verticaltabgroup.png)
        
    - Para mesclar as guias, clique com o botão direito do mouse no título da consulta e selecione **Mover para o Grupo de Guias Seguinte** ou **Mover para o Grupo de Guias Anterior**:
    
      ![Mesclar guias de consulta](media/ssms-configuration/mergetabgroups.png)

- Para restaurar o layout do ambiente padrão, no menu **Janela**, selecione **Redefinir Layout da Janela**:
 
    ![Restaurar o layout da janela](media/ssms-configuration/resetwindowlayout.png)
    
## <a name="maximize-query-editor"></a>Maximizar o Editor de Consultas
Você pode maximizar o Editor de Consultas para o modo de tela inteira:

1. Clique em qualquer lugar na janela do Editor de Consultas.
2. Pressione Shift+Alt+Enter para alternar entre o modo de tela inteira e o modo comum. 

Esse atalho de teclado funciona com qualquer janela de documentos. 



## <a name="change-basic-settings"></a>Alterar configurações básicas
Esta seção descreve como modificar algumas configurações básicas no SSMS usando o menu **Ferramentas**.

  ![menu Ferramentas](media/ssms-configuration/tools.png)


- Para modificar a barra de ferramentas realçada, selecione **Ferramentas** > **Personalizar**:

    ![Personalizar uma barra de ferramentas](media/ssms-configuration/toolbar.png)

### <a name="change-the-font"></a>Alterar fonte
- Para alterar a fonte, selecione **Ferramentas** > **Opções** > **Fontes e Cores**:

     ![Alterar fontes e cores](media/ssms-configuration/fontsandcolors.png)

### <a name="change-startup-options"></a>Alterar opções de inicialização
- As opções de inicialização determinam como seu workspace aparece ao abrir o SSMS pela primeira vez. Para alterar as opções de inicialização, selecione **Ferramentas** > **Opções** > **Inicialização**:
 
    ![Alterar opções de inicialização](media/ssms-configuration/startup.png)

### <a name="reset-settings-to-the-default"></a>Redefinir as configurações para o padrão
- Você pode exportar e importar todas essas configurações do menu. Para importar ou exportar as configurações ou para restaurar as configurações padrão, selecione **Ferramentas** > **Importar e Exportar Configurações** 

    ![Importar e exportar configurações](media/ssms-configuration/settings.png)



## <a name="next-steps"></a>Próximas etapas
O próximo artigo ensina mais algumas dicas e truques para usar o SSMS, como localizar o log de erros do SQL Server e o nome da instância SQL. 

> [!div class="nextstepaction"]
> [Mais dicas e truques para usar o SSMS](ssms-tricks.md)
 
 




