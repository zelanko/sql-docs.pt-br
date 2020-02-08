---
title: 'Etapa 1: Copiar o pacote da Lição 5 | Microsoft Docs'
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: a25fcc13-987e-4f3d-8f0c-76f7e6e59920
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2c4c895e71da13d7de38bf5dfc64f27829206d25
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71283121"
---
# <a name="lesson-6-1-copy-the-lesson-5-package"></a>Lição 6-1: Copiar o pacote da Lição 5

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Nesta tarefa, você pode criar uma cópia do pacote **Lesson 5.dtsx** da Lição 5. Se você não tiver completado a Lição 5, poderá adicionar o pacote completo da Lição 5 incluído no tutorial do projeto e então trabalhar com uma cópia. Você usa esta cópia nova ao longo de toda a lição 6. 

> [!IMPORTANT]
> Depois de copiar o pacote da lição 5, se você tiver atualmente os pacotes das lições anteriores em sua solução, clique com o botão direito do mouse em cada pacote das lições de 1 a 5 e selecione **Excluir do Projeto**. Ao terminar, você deve ter apenas **Lesson 6.dtsx** em sua solução.   
  
## <a name="create-the-lesson-6-package"></a>Criar o pacote da Lição 6  
  
Use este procedimento se você estiver copiando a Lição 5 concluída.  Para copiar a Lição 5 de exemplo, confira a próxima seção.

1.  Se as Ferramentas de Dados [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ainda não estiverem abertas, selecione **Iniciar** > **Todos os Programas** > **Microsoft SQL Server 2017** e, em seguida, selecione **SQL Server Data Tools**.

2.  No menu **Arquivo**, selecione **Abrir** > **Projeto/Solução**, selecione a pasta **Tutorial SSIS** e **Abrir**, então clique duas vezes em **SSIS Tutorial.sln**.

3.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Lesson 5.dtsx** e, em seguida, selecione **Copiar**.

4.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Pacotes SSIS** e selecione **Colar**.

    Por padrão, o nome do pacote copiado é **Lesson 5.dtsx**.

5.  No **Gerenciador de Soluções**, clique duas vezes em **Lesson 5.dtsx** para abrir o pacote

6.  Clique com o botão direito do mouse em qualquer lugar da tela de fundo da superfície de design **Fluxo de Controle** e selecione em **Propriedades**.

7.  Na janela **Propriedades**, atualize a propriedade **Nome** para **Lição 6**.

8.  Marque a caixa para a propriedade **ID**, selecione a seta suspensa e, em seguida, selecione **\<Gerar Nova ID>** .

## <a name="add-the-completed-lesson-5-package"></a>Adicionar o pacote concluído da Lição 5

1.  Abra as Ferramentas de Dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e abra o projeto do Tutorial do SSIS.

2.  No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Pacotes SSIS** e clique em **Adicionar Pacote Existente**.

3.  Na caixa de diálogo **Adicionar Cópia do Pacote Existente** , em **Local do pacote**, selecione **Sistema de arquivos**.

4.  Selecione o botão Procurar **(…)** , navegue até **Lesson 5.dtsx** no computador e selecione **Abrir**.

5.  Copie e cole o pacote da Lição 5 conforme descrito nas etapas de 3 a 8 da seção anterior.

## <a name="go-to-next-task"></a>Ir para a próxima tarefa
[Etapa 2: Converter o projeto no Modelo de Implantação de Projeto](../integration-services/lesson-6-2-converting-the-project-to-the-project-deployment-model.md)  
  
