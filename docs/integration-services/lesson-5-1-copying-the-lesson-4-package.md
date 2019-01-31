---
title: 'Etapa 1: Copiar o pacote da Lição 4 | Microsoft Docs'
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 8aa7d690-4649-4c0a-ac6f-9504637ee426
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f6e3f2999bb686d0e6242ec8a6eea9d926cc787c
ms.sourcegitcommit: 5ca813d045e339ef9bebe0991164a5d39c8c742b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54880439"
---
# <a name="lesson-5-1-copy-the-lesson-4-package"></a>Lição 5-1: Copiar o pacote da Lição 4

Nesta tarefa, você pode criar uma cópia do pacote **Lesson 4.dtsx** da Lição 4. Se você não tiver completado a lição 4, poderá adicionar o pacote completo da lição 4, incluído no tutorial do projeto e então trabalhar com uma cópia. Você usa esta cópia nova ao longo de toda a lição 5.  
  
## <a name="create-the-lesson-5-package"></a>Criar o pacote da Lição 5  
  
Use este procedimento se você estiver copiando a Lição 4 concluída.  Para copiar a Lição 4 de exemplo, confira a próxima seção.

1.  Se as Ferramentas de Dados [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ainda não estiverem abertas, selecione **Iniciar** > **Todos os Programas** > **Microsoft SQL Server 2017** e, em seguida, selecione **SQL Server Data Tools**.

2.  No menu **Arquivo**, selecione **Abrir** > **Projeto/Solução**, selecione a pasta **Tutorial do SSIS** e selecione **Abrir**.  Em seguida, clique duas vezes **SSIS Tutorial.sln**.

3.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Lesson 4.dtsx** e, em seguida, selecione **Copiar**.

4.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Pacotes SSIS** e selecione **Colar**.

    Por padrão, o nome do pacote copiado é **Lesson 4.dtsx**.

5.  No **Gerenciador de Soluções**, clique duas vezes em **Lesson 4.dtsx** para abrir o pacote.

6.  Clique com o botão direito do mouse em qualquer lugar da tela de fundo da superfície de design **Fluxo de Controle** e selecione em **Propriedades**.

7.  Na janela **Propriedades**, atualize a propriedade **Nome** para **Lição 5**.

8.  Marque a caixa para a propriedade **ID**, selecione a seta suspensa e, em seguida, selecione **\<Gerar Nova ID>**.

## <a name="add-the-completed-lesson-4-package"></a>Adicionar o pacote concluído da Lição 4

1.  Abra as Ferramentas de Dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e abra o projeto do Tutorial do SSIS.

2.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Pacotes SSIS** e clique em **Adicionar Pacote Existente**.

3.  Na caixa de diálogo **Adicionar Cópia do Pacote Existente** , em **Local do pacote**, selecione **Sistema de arquivos**.

4.  Selecione o botão Procurar **(…)**, navegue até **Lesson 4.dtsx** no computador e selecione **Abrir**.

5.  Copie e cole o pacote da Lição 4 conforme descrito nas etapas de 3 a 8 da seção anterior.
  
## <a name="go-to-next-task"></a>Ir para a próxima tarefa  
[Etapa 2: Habilitar e configurar as configurações do pacote](../integration-services/lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
