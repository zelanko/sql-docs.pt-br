---
title: 'Etapa 1: Copiar o pacote da Lição 3 | Microsoft Docs'
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 0d053786-5203-43f3-a613-27a8dd2bc44a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a5d6eec55e339d8aaf23d04b88d14fc945e8f0c7
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86922142"
---
# <a name="lesson-4-1-copy-the-lesson-3-package"></a>Lição 4-1: Copiar o pacote da Lição 3

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



Nesta tarefa, você pode criar uma cópia do pacote Lesson 3.dtsx da Lição 3. Se você não tiver completado a lição 3, poderá adicionar o pacote completo da lição 3, incluído no tutorial do projeto e então trabalhar com uma cópia. Você usa esta cópia nova ao longo de toda a lição 4.  
  
## <a name="create-the-lesson-4-package"></a>Criar o pacote da Lição 4  
  
Use este procedimento se você estiver copiando a Lição 3 concluída.  Para copiar a Lição 3 de exemplo, confira a próxima seção.

1.  Se as Ferramentas de Dados [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ainda não estiverem abertas, selecione **Iniciar** > **Todos os Programas** > **Microsoft SQL Server 2017** e, em seguida, selecione **SQL Server Data Tools**.

2.  No menu **Arquivo**, selecione **Abrir** > **Projeto/Solução**, selecione a pasta **Tutorial SSIS** e **Abrir**, então clique duas vezes em **SSIS Tutorial.sln**.

3.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Lesson 3.dtsx** e, em seguida, selecione **Copiar**.

4.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Pacotes SSIS** e selecione **Colar**.

    Por padrão, o nome do pacote copiado é **Lesson 4.dtsx**.

5.  No **Gerenciador de Soluções**, clique duas vezes em **Lesson 4.dtsx** para abrir o pacote

6.  Clique com o botão direito do mouse em qualquer lugar da tela de fundo da superfície de design **Fluxo de Controle** e selecione em **Propriedades**.

7.  Na janela **Propriedades**, atualize a propriedade **Nome** para **Lição 4**.

8.  Marque a caixa correspondente à propriedade **ID**, selecione a seta da lista suspensa e escolha **\<Generate New ID>** .

## <a name="add-the-completed-lesson-3-package"></a>Adicionar o pacote concluído da Lição 3

1.  Abra as Ferramentas de Dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e abra o projeto do Tutorial do SSIS.

2.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Pacotes SSIS** e clique em **Adicionar Pacote Existente**.

3.  Na caixa de diálogo **Adicionar Cópia do Pacote Existente** , em **Local do pacote**, selecione **Sistema de arquivos**.

4.  Selecione o botão Procurar **(…)** , navegue até **Lesson 3.dtsx** no computador e selecione **Abrir**.

5.  Copie e cole o pacote da Lição 3 conforme descrito nas etapas de 3 a 8 da seção anterior.

  
## <a name="go-to-next-task"></a>Ir para a próxima tarefa  
[Etapa 2: Criar um arquivo corrompido](../integration-services/lesson-4-2-creating-a-corrupted-file.md)  
  
