---
title: 'Etapa 1: copiar o pacote da Lição 3 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 0d053786-5203-43f3-a613-27a8dd2bc44a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1645a1dee923da3913d12e36bdd60829918bbf7b
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440473"
---
# <a name="step-1-copying-the-lesson-3-package"></a>Etapa 1: Copiar o pacote da Lição 3
  Nesta tarefa, você criará uma cópia do pacote Lesson 3.dtsx criado na Lição 3. Se você não tiver completado a lição 3, poderá adicionar o pacote completo da lição 3, incluído no tutorial do projeto, e então trabalhar com uma cópia. Você usará essa cópia nova durante toda a Lição 4.  
  
### <a name="to-create-the-lesson-4-package"></a>Para criar o pacote da Lição 4  
  
1.  Se o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools ainda não estiver aberto, clique em **Iniciar**, aponte para **Todos os Programas**, **Microsoft SQL Server**e clique em **SQL Server Data Tools**.  
  
2.  No menu **Arquivo** , clique em **Abrir**, clique em **Projeto/Solução**, selecione **Tutorial do SSIS** , clique em **Abrir**e clique duas vezes em **SSIS Tutorial.sln**.  
  
3.  No Gerenciador de Soluções, clique com o botão direito do mouse em **Lesson 3.dtsx**e clique em **Copiar**.  
  
4.  Em Gerenciador de Soluções, clique com o botão direito do mouse em **pacotes SSIS**e clique em **colar**.  
  
     Por padrão, o pacote copiado recebe o nome de Lesson 4.dtsx.  
  
5.  Em Gerenciador de Soluções, clique duas vezes na **lição 4. dtsx** para abrir o pacote.  
  
6.  Clique com o botão direito do mouse em qualquer lugar da tela de fundo da guia **Fluxo de Controle** e clique em **Propriedades**.  
  
7.  Na janela Propriedades, atualize a `Name` propriedade para `Lesson 4` .  
  
8.  Clique na caixa da propriedade **ID** e, na lista, clique em **\<Generate New ID>**.  
  
### <a name="to-add-the-completed-lesson-3-package"></a>Para adicionar o pacote concluído da Lição 3  
  
1.  Abra o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e abra o projeto do Tutorial do SSIS.  
  
2.  Em Gerenciador de Soluções, clique com o botão direito do mouse em **pacotes SSIS**e clique em **Adicionar pacote existente**.  
  
3.  Na caixa de diálogo **Adicionar cópia do pacote existente** , em **local do pacote**, selecione **sistema de arquivos**.  
  
4.  Clique no botão procurar **(...)** , navegue até a lição 3. dtsx em seu computador e clique em **abrir**.  
  
     Para baixar todos os pacotes de lição para este tutorial, faça o seguinte.  
  
    1.  Navegue para os [Exemplos de Produtos do Integration Services](https://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Clique na guia **downloads** .  
  
    3.  Clique no arquivo SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
5.  Copie e cole o pacote da Lição 3, conforme descrito nas etapas 3 a 8 do procedimento anterior.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Etapa 2: Criar um arquivo corrompido](lesson-4-2-creating-a-corrupted-file.md)  
  
  
