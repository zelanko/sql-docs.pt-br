---
Title: 'Tutorial: Using templates in SQL Server Management Studio'
description: Um Tutorial para usar modelos no SSMS.
keywords: SQL Server, SSMS, SQL Server Management Studio, Modelos
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: tutorial
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
ms.openlocfilehash: e83eea4a1f7dbcf40a4b221ca1936e823d59c86f
ms.sourcegitcommit: b3d84abfa4e2922951430772c9f86dce450e4ed1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/22/2019
ms.locfileid: "56662760"
---
# <a name="tutorial-using-templates-in-sql-server-management-studio"></a>Tutorial: usando modelos no SQL Server Management Studio
Este tutorial apresenta a você os modelos predefinidos do T-SQL (Transact-SQL) disponíveis no SSMS (SQL Server Management Studio). Neste artigo, você aprenderá como:

> [!div class="checklist"]
> * Usar o Navegador de Modelos para gerar scripts T-SQL
> * Editar um modelo existente 
> * Localizar modelos no disco
> * Criar um novo modelo
   

## <a name="prerequisites"></a>Prerequisites
Para concluir este tutorial, você precisará do SQL Server Management Studio e de acesso a um SQL Server. 

- Instalar o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
- Instalar o [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).

 

## <a name="use-template-browser"></a>Usar o Navegador de Modelos
Nesta seção, você aprende a localizar e a usar o Navegador de Modelos. 

1. Abra o SQL Server Management Studio.
2. No menu **Exibir**, selecione **Navegador de Modelos** (Ctrl+Alt+T): 

    ![Abrir o Navegador de Modelos](media/templates-ssms/templatebrowser.png)
    
    Você pode ver os modelos usados recentemente na parte inferior do navegador de modelos.

3. Expanda o nó em que você está interessado. Clique com o botão direito do mouse no modelo e, em seguida, selecione **Abrir**:

    ![Abrir um modelo](media/templates-ssms/opentemplate.png)
    
    Você também pode clicar duas vezes o nome do modelo para abri-lo.

4. Uma janela de nova consulta é aberta. O script T-SQL já está preenchido. 
5. Modifique o modelo para atender às suas necessidades e, em seguida, selecione **Executar** para executar a consulta:
    
    ![Criar um modelo de banco de dados](media/templates-ssms/createdbtemplate.png)


## <a name="edit-an-existing-template"></a>Editar um modelo existente
Você também pode editar os modelos existentes no Navegador de Modelos.  

1. No Navegador de Modelos, vá para o modelo com o qual você deseja trabalhar.
2. Clique com o botão direito do mouse no modelo e, em seguida, selecione **Editar**:

    ![Editar um modelo](media/templates-ssms/edittemplate.png)

3. Na janela de consulta que é aberta, faça as alterações que você deseja fazer.
4. Para salvar o modelo, selecione **Arquivo** > **Salvar** (Ctrl+S).
5. Fechar a janela de consulta.
6. Reabra o modelo. Suas edições devem ser exibidas.
 

## <a name="locate-templates-on-disk"></a>Localizar modelos no disco
Quando um modelo é aberto, você pode localizar os modelos que estão no disco.

1. No Navegador de Modelos, selecione um modelo e, em seguida, selecione **Editar**.
2. Clique com o botão direito do mouse **Título da Consulta** e, em seguida, selecione **Abrir a Pasta que Contém**. O Explorer deve se abrir no local em que os modelos estão armazenados no disco: 

   ![Modelos em disco](media/templates-ssms/templatesondisk.png)
  

## <a name="create-a-new-template"></a>Criar um novo modelo
Você também pode criar um novo modelo no Navegador de Modelos. As etapas a seguir mostram como criar uma nova pasta e, em seguida, criar um novo modelo nessa pasta. Você também pode usar estas etapas para criar um modelo personalizado em uma pasta existente. 

1. Abra o Navegador de Modelos.
2. Clique com o botão direito do mouse em **Modelos do SQL Server** e, em seguida, selecione **Nova** > **Pasta**.
3. Nomeie esta pasta como **Modelos Personalizados**:

    ![Criar uma pasta de modelos personalizados](media/templates-ssms/creatingcustomtemplate.png)

4. Clique com o botão direito do mouse na pasta Modelos Personalizados recém-criada e, em seguida, selecione **Novo** > **Modelo**. Insira um nome do seu modelo:
 
    ![Criar um modelo personalizado](media/templates-ssms/createnewtemplate.png)
   
5. Clique com o botão direito do mouse no modelo que você criou e, em seguida, selecione **Editar**. A janela Nova Consulta é aberta.
6. Insira o texto T-SQL que você deseja salvar. 
7. No menu **Arquivo**, selecione **Salvar**.
8. Feche a janela de consulta existente e abra seu novo modelo personalizado. 

    

## <a name="next-steps"></a>Próximas etapas
O próximo artigo apresenta mais dicas e truques para usar o SQL Server Management Studio. 

> [!div class="nextstepaction"]
> [Mais dicas e truques para usar o SSMS](ssms-tricks.md)
