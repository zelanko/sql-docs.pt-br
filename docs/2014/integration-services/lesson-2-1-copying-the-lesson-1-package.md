---
title: 'Etapa 1: Copiando o pacote da lição 1 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7f1616c2-2b4e-4010-be50-27d7b897403a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d473cdf45eebeb0a5bd6268ed79c071741e74e8c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62891669"
---
# <a name="step-1-copying-the-lesson-1-package"></a>Etapa 1: Copiar o pacote da Lição 1
  Nesta tarefa, você criará uma cópia do pacote Lesson 1.dtsx criado na Lição 1. Se você não completou a lição 1, poderá adicionar o pacote completo da lição 1 incluído com o tutorial do projeto e, então, copiar esse pacote. Você usará essa cópia nova durante toda a Lição 2.  
  
### <a name="to-create-the-lesson-2-package"></a>Para criar o pacote da lição 2  
  
1.  Se o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools ainda não estiver aberto, clique em **Iniciar**, aponte para **Todos os Programas**, **Microsoft SQL Server 2012**e clique em **SQL Server Data Tools**.  
  
2.  No menu **Arquivo** , clique em **Abrir**, clique em **Projeto/Solução**, clique na pasta **Tutorial do SSIS** , clique em **Abrir**e clique duas vezes em **SSIS Tutorial.sln**.  
  
3.  No Gerenciador de Soluções, clique com o botão direito do mouse em **Lesson 1.dtsx**e clique em **Copiar**.  
  
4.  No Gerenciador de Soluções, clique com o botão direito do mouse em **Pacotes SSIS**e clique em **Colar**.  
  
     Por padrão, o pacote copiado receberá o nome de Lesson 2.dtsx.  
  
5.  No Gerenciador de Soluções, clique duas vezes em **Lesson 2.dtsx** para abrir o pacote  
  
6.  Clique com o botão direito do mouse em qualquer lugar da tela de fundo da superfície de design **Fluxo de Controle** e clique em **Propriedades**.  
  
7.  Na janela Propriedades, atualize o `Name` propriedade para `Lesson 2`.  
  
8.  Clique na caixa para o **identificação** propriedade, clique na seta suspensa e, em seguida, clique em  **\<gerar nova ID >**.  
  
### <a name="to-add-the-completed-lesson-1-package"></a>Para adicionar o pacote concluído da Lição 1  
  
1.  Abra as Ferramentas de Dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e abra o projeto do Tutorial do SSIS.  
  
2.  No Gerenciador de Soluções, clique com o botão direito do mouse em **Pacotes SSIS** e clique em **Adicionar Pacote Existente**.  
  
3.  Na caixa de diálogo **Adicionar Cópia do Pacote Existente** , em **Local do pacote**, selecione **Sistema de arquivos**.  
  
4.  Clique no botão Procurar **(…)**, navegue até **Lesson 1.dtsx** no computador e clique em **Abrir**.  
  
     Para baixar todos os pacotes de lição para este tutorial, faça o seguinte.  
  
    1.  Navegue para os [Exemplos de Produtos do Integration Services](https://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Clique na guia **DOWNLOADS** .  
  
    3.  Clique no arquivo SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
5.  Copie e cole o pacote da Lição 1, conforme descrito nas etapas 3 a 8 do procedimento anterior.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Etapa 2: Adicionando e configurando o contêiner Loop Foreach](lesson-2-2-adding-and-configuring-the-foreach-loop-container.md)  
  
  
