---
Title: 'Tutorial: Using Templates in SQL Server Management Studio'
description: Um Tutorial para usar Modelos no SSMS. para obter informações sobre a ferramenta de configuração e recursos adicionais.
keywords: SQL Server, SSMS, SQL Server Management Studio, Modelos
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: Tutorial
ms.suite: sql
ms.prod: sql
ms.technology: ssms
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
helpviewer_keywords:
- templates [SQL Server], SQL Server Management Studio
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- SQL Server Management Studio [SQL Server], tutorials
- scripts [SQL Server], SQL Server Management Studio
ms.openlocfilehash: c4ddbf149048b7cb7f89be24369c60afc47bdb4a
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="tutorial-using-templates-within-sql-server-management-studio"></a>Tutorial: usando Modelos no SQL Server Management Studio
Este tutorial apresentará a você os modelos predefinidos do T-SQL (Transact-SQL) que estão disponíveis no SSMS (SQL Server Management Studio). Neste artigo, você aprenderá como:

> [!div class="checklist"]
> * Usar o Navegador de Modelos para gerar scripts T-SQL
> * Editar um Modelo existente 
> * Localizar os modelos no disco
> * Criar um novo Modelo
   

## <a name="prerequisites"></a>Prerequisites
Para concluir este Tutorial, você precisará do SQL Server Management Studio, bem como acesso a um SQL Server. 

- Instalar o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
- Instalar o [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).

 

## <a name="using-the-template-browser"></a>Usar o Navegador de Modelos
Nesta seção, você aprenderá como localizar e usar o **Navegador de Modelos**. 

1. Inicie o SQL Server Management Studio.
2. No Menu **Exibir** > **Navegador de Modelos** (Ctrl + Alt + T): 

    ![Navegador de Modelos](media/templates-ssms/templatebrowser.png)
    - Também é possível ver os modelos recém-usados na parte inferior do **Navegador de Modelos**.

3. Expanda o nó de seu interesse > clique com botão direito do mouse no Modelo > Abrir:

    ![Abrir Modelo](media/templates-ssms/opentemplate.png)
    - Clicar duas vezes no modelo terá o mesmo efeito.

4. Isso abrirá uma nova janela de consulta com o T-SQL já populado. 
5. Modifique o modelo para atender às suas necessidades e **Execute** a consulta:
    
    ![Criar modelo de BD](media/templates-ssms/createdbtemplate.png)


## <a name="edit-an-existing-template"></a>Editar um Modelo existente
Você também pode editar os modelos existentes em **Navegador de Modelo**.  

1. Localize o modelo de seu interesse no **Navegador de Modelos**.
2. Clique com o botão direito do mouse no modelo > **Editar**:

    ![Editar Modelo](media/templates-ssms/edittemplate.png)

3. Faça as alterações desejadas na janela de consulta que se abre.
4. Salve o modelo acessando **Arquivo** > **Salvar** (Ctrl+S).
5. Fechar a janela de consulta.
6. Reabra o Modelo que você salvou e suas novas edições deverão aparecer nele.
 

## <a name="locate-the-templates-on-disk"></a>Localizar os modelos no disco
Quando um modelo é aberto, é possível localizá-lo no disco.

1. Selecione um modelo no **Navegador de Modelos** > **Edições**.
2. Clique com o botão direito do mouse em **Título da Consulta** > **Abrir pasta de origem**. Isso deverá abrir o navegador no local onde os modelos são armazenados no disco: 

    ![Modelos em disco](media/templates-ssms/templatesondisk.png)
  

## <a name="create-a-new-template"></a>Criar um novo modelo
Dentro do **Navegador de Modelos**, também é possível criar novos modelos. Essas etapas ensinarão você a criar uma nova pasta e um novo modelo dentro dessa pasta. No entanto, com estas etapas, você também pode criar um modelo personalizado dentro das pastas existentes. 

1. Abra o **Navegador de Modelos**.
2. Clique com o botão direito do mouse em Modelos do SQL Server > **Novo** > **Pasta**.
3. Nomeie esta pasta como **Modelos Personalizados**:

    ![Criando modelos personalizados](media/templates-ssms/creatingcustomtemplate.png)

4. Clique com o botão direito do mouse na pasta **Modelos Personalizados** recém-criada > **Novo** > **Modelo** > nomeie seu modelo:
 
    ![Criar modelo personalizado](media/templates-ssms/createnewtemplate.png)
   
5. Clique com o botão direito do mouse no modelo que você acabou de criar > **Editar**. Isso abrirá uma **Nova Janela de Consulta**.
6. Digite o texto de T-SQL que você deseja salvar. 
7. Salve o arquivo acessando o menu **Arquivo** > **Salvar**.
8. Feche a **Janela de Consulta** existente e abra seu novo modelo personalizado. 

    

## <a name="next-steps"></a>Próximas etapas
O próximo artigo fornecerá algumas outras dicas e truques para usar o SQL Server Management Studio. 

Prossiga para o próximo artigo para saber mais
> [!div class="nextstepaction"]
> [Botão Próximas etapas](ssms-tricks.md)
