---
title: Criar um projeto | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-solutions
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vs.newproject
- vs.addnewproject
helpviewer_keywords:
- projects [SQL Server Management Studio], creating
ms.assetid: 7897be19-365b-4b06-bcf0-8a669f67a673
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7b9549bfce672b3ddf5c67ddb8a6a4968e87a5b7
ms.sourcegitcommit: b70b99c2e412b4d697021f3bf1a92046aafcbe37
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2018
ms.locfileid: "42773902"
---
# <a name="create-a-project"></a>Criar um projeto
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Você pode criar um ou mais projetos dentro de uma solução existente.  
  
### <a name="to-create-a-new-project-and-add-it-to-a-solution"></a>Para criar um novo projeto e adicioná-lo a uma solução  
  
1.  No Gerenciador de Soluções, selecione a solução.  
  
2.  No menu **Arquivo** , aponte para **Adicionar**e clique em **Novo Projeto**.  
  
3.  Na caixa de diálogo  **Novo Projeto** , clique em um tipo de projeto.  
  
    **Modelos**  
    Na caixa **Modelos** , selecione um modelo. Uma breve descrição do modelo de projeto selecionado aparece abaixo da caixa **Modelos** .  
  
    **Nome**  
    Digite o nome do projeto de script que deseja criar. Também é criada uma pasta com o mesmo nome do projeto no local exibido no campo **Local** . Para alguns projetos, o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] cria fonte e outros arquivos de suporte e os adiciona à pasta de projeto nova.  
  
    > [!NOTE]  
    > Para alguns tipos de projeto, a caixa de texto **Nome** fica indisponível, pois especificar o local define o nome. Por exemplo, aplicativos e serviços Web estão localizados em um servidor Web e extraem seus nomes de diretórios virtuais especificados nesse servidor.  
  
    Nomes não podem conter os seguintes caracteres:  
  
    -   Cerquilha (#)  
  
    -   Porcentagem (%)  
  
    -   E comercial (&)  
  
    -   Asterisco (*)  
  
    -   Barra vertical (|)  
  
    -   Barra invertida (\\)  
  
    -   Dois-pontos (:)  
  
    -   Aspas (")  
  
    -   Menor que (\<)  
  
    -   Maior que (>)  
  
    -   Ponto de interrogação (?)  
  
    -   Barra (/)  
  
    -   Espaços iniciais ou finais (' ')  
  
    -   Nomes reservados para o Microsoft Windows ou MS-DOS, como ("nul", "aux", "con", "com1", "lpt1" e assim por diante)  
  
    **Local**  
    Insira o local onde deseja criar seu projeto ou escolha um na lista.  
  
    **Procurar**  
    Exibe a caixa de diálogo **Local do Projeto** , permitindo que você navegue até um novo diretório no qual salvar o projeto.  
  
    **Solução**  
    Selecione **Criar Nova Solução** para criar uma solução no Gerenciador de Soluções. Selecione **Adicionar à Solução** para adicionar o novo projeto à solução atualmente aberta no Gerenciador de Soluções.  
  
    **Criar diretório para a solução**  
    Selecione para habilitar a caixa de texto **(Solução) Nome** . Esta opção cria um novo diretório do nome escolhido para seu projeto e solução.  
  
    **Nome da Solução**  
    Digite o nome da nova solução em que você deseja que seu projeto seja criado. Por padrão, este campo usa o mesmo nome digitado no campo **Nome** .  
  
    **Observação** Para acessar essa opção, você deve marcar as caixas de seleção **Criar Nova Solução** em **Solução** e **Criar diretório para a solução** . Alguns modelos de projeto não oferecem suporte a esta opção, como aplicativos Web.  
  
    **Adicionar ao Controle do Código Fonte**  
    Quando esta caixa de seleção é marcada, seu aplicativo de controle do código-fonte é aberto quando você clica em **OK**. Preencha qualquer informação solicitada por seu aplicativo de controle do código fonte para continuar. Você deve ter um aplicativo cliente de controle do código-fonte instalado para usar esta opção.  
  
4.  Clique em **OK**.  
  
Você pode definir um nome para o projeto de script, mas os nomes de pastas são definidos pelo [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e não podem ser alterados. Você pode configurar a unidade e a especificação do caminho do conjunto comum de pastas usando a caixa de diálogo **Adicionar Novo Projeto** . No **Gerenciador de Soluções**, clique com o botão direito do mouse no ícone da solução e clique em **Adicionar**. O local padrão para pastas de projeto de script é: C:\Documents and Settings\\*username*\My Documents\SQL Server Management Studio\Projects\\.  
  
## <a name="see-also"></a>Consulte Também  
[Gerenciador de Soluções](../../ssms/solution/solution-explorer.md)  
[Adicionar um projeto existente a uma solução](../../ssms/solution/add-an-existing-project-to-a-solution.md)  
[Adicionar novos itens a um projeto](../../ssms/solution/add-new-items-to-a-project.md)  
[Adicionar itens existentes a um projeto](../../ssms/solution/add-existing-items-to-a-project.md)  
[Alterar o local padrão dos projetos](../../ssms/solution/change-the-default-location-for-projects.md)  
[Remover ou excluir um item ou projeto](../../ssms/solution/remove-or-delete-an-item-or-project.md)  
[Excluir uma solução](../../ssms/solution/delete-a-solution.md)  
  
