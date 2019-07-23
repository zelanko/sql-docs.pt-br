---
title: 'Etapa 1: Copiar o pacote da Lição 1 | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 7f1616c2-2b4e-4010-be50-27d7b897403a
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 421655cb190ac175b7e6c65cf6b296279efe25ba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086605"
---
# <a name="lesson-2-1-copy-the-lesson-1-package"></a>Lição 2-1: Copiar o pacote da Lição 1

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Nesta tarefa, você pode criar uma cópia do pacote **Lesson 1.dtsx**. Se você não tiver concluído a Lição 1, poderá usar o pacote concluído da Lição 1 incluído neste tutorial. Você usa a nova cópia durante o restante da Lição 2.  
  
## <a name="create-the-lesson-2-package"></a>Criar o pacote da Lição 2  

Use este procedimento se você estiver copiando a Lição 1 concluída.  Para copiar a Lição 1 de exemplo, confira a próxima seção.
  
1.  Se as Ferramentas de Dados [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ainda não estiverem abertas, selecione **Iniciar** > **Todos os Programas** > **Microsoft SQL Server 2017** e, em seguida, selecione **SQL Server Data Tools**.  
  
2.  No menu **Arquivo**, selecione **Abrir** > **Projeto/Solução**, selecione a pasta **Tutorial SSIS** e **Abrir**, então clique duas vezes em **SSIS Tutorial.sln**.  
  
3.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Lesson 1.dtsx** e, em seguida, selecione **Copiar**.  
  
4.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Pacotes SSIS** e selecione **Colar**.  
  
    Por padrão, o pacote copiado recebe o nome de **Lesson 2.dtsx**.  
  
5.  No **Gerenciador de Soluções**, clique duas vezes em **Lesson 2.dtsx** para abrir o pacote  
  
6.  Clique com o botão direito do mouse em qualquer lugar da tela de fundo da superfície de design **Fluxo de Controle** e selecione em **Propriedades**.  
  
7.  Na janela **Propriedades**, atualize a propriedade **Nome** para **Lição 2**.  
  
8.  Marque a caixa para a propriedade **ID**, selecione a seta suspensa e, em seguida, selecione **\<Gerar Nova ID>** .  
  
## <a name="use-the-sample-lesson-1-package"></a>Usar o pacote da Lição 1 de exemplo  
  
1.  Abra as Ferramentas de Dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e abra o projeto do Tutorial do SSIS.  
  
2.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Pacotes SSIS** e clique em **Adicionar Pacote Existente**.  
  
3.  Na caixa de diálogo **Adicionar Cópia do Pacote Existente**, em **Localização do pacote**, selecione **Sistema de arquivos**.  
  
4.  Selecione o botão Procurar **(…)** , navegue até **Lesson 1.dtsx** no computador e selecione **Abrir**.  
  
5.  Copie e cole o pacote da Lição 1 conforme descrito nas etapas de 3 a 8 da seção anterior.  
  
## <a name="go-to-next-task"></a>Ir para a próxima tarefa

[Etapa 2: Adicionar e configurar o contêiner Loop Foreach](../integration-services/lesson-2-2-adding-and-configuring-the-foreach-loop-container.md)  
  
