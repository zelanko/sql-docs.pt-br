---
title: 'Etapa 1: Copiar o pacote da Lição 2 | Microsoft Docs'
ms.custom: ''
ms.date: 01/04/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 4bd91402-4e37-41de-ab78-8ca5a1948a37
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 75a1cd07710bb95c041d0de8a00cb23f7354eb91
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65722404"
---
# <a name="lesson-3-1-copy-the-lesson-2-package"></a>Lição 3-1: Copiar o pacote da Lição 2

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Nesta tarefa, você pode criar uma cópia do pacote Lesson 2.dtsx da Lição 2. Se você não tiver concluído a Lição 2, poderá adicionar o pacote completo da Lição 2 incluído com o tutorial do projeto e então copiar esse pacote. Você usa esta cópia nova ao longo de toda a lição 3.

## <a name="create-the-lesson-3-package"></a>Criar o pacote da Lição 3

Use este procedimento se você estiver copiando a Lição 2 concluída.  Para copiar a Lição 2 de exemplo, confira a próxima seção.

1.  Se as Ferramentas de Dados [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ainda não estiverem abertas, selecione **Iniciar** > **Todos os Programas** > **Microsoft SQL Server 2017** e, em seguida, selecione **SQL Server Data Tools**.

2.  No menu **Arquivo**, selecione **Abrir** > **Projeto/Solução**, selecione a pasta **Tutorial SSIS** e **Abrir**, então clique duas vezes em **SSIS Tutorial.sln**.

3.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Lesson 2.dtsx** e, em seguida, selecione **Copiar**.

4.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Pacotes SSIS** e selecione **Colar**.

    Por padrão, o nome do pacote copiado é Lesson 3.dtsx.

5.  No **Gerenciador de Soluções**, clique duas vezes em **Lesson 3.dtsx** para abrir o pacote

6.  Clique com o botão direito do mouse em qualquer lugar da tela de fundo da superfície de design **Fluxo de Controle** e selecione em **Propriedades**.

7.  Na janela **Propriedades**, atualize a propriedade **Nome** para **Lição 3**.

8.  Marque a caixa para a propriedade **ID**, selecione a seta suspensa e, em seguida, selecione **\<Gerar Nova ID>**.

## <a name="add-the-completed-lesson-2-package"></a>Adicionar o pacote concluído da Lição 2

1.  Abra as Ferramentas de Dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e abra o projeto do Tutorial do SSIS.

2.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Pacotes SSIS** e clique em **Adicionar Pacote Existente**.

3.  Na caixa de diálogo **Adicionar Cópia do Pacote Existente**, em **Localização do pacote**, selecione **Sistema de arquivos**.

4.  Selecione o botão Procurar **(…)**, navegue até **Lesson 2.dtsx** no computador e selecione **Abrir**.

5.  Copie e cole o pacote da Lição 3 conforme descrito nas etapas de 3 a 8 da seção anterior.  
  
## <a name="go-to-next-task"></a>Ir para a próxima tarefa
[Etapa 2: Adicionar e configurar o registro em log](../integration-services/lesson-3-2-adding-and-configuring-logging.md)  
  
