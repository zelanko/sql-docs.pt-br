---
title: 'Etapa 1: copiar o pacote da Lição 3 | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2016
ms.assetid: 0d053786-5203-43f3-a613-27a8dd2bc44a
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 35cf58153bff50754c04447073af2aa54ac2bd46
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35411968"
---
# <a name="lesson-4-1---copying-the-lesson-3-package"></a>Lição 4-1 – copiar o pacote da Lição 3
Nesta tarefa, você criará uma cópia do pacote Lesson 3.dtsx criado na Lição 3. Se você não tiver completado a lição 3, poderá adicionar o pacote completo da lição 3, incluído no tutorial do projeto, e então trabalhar com uma cópia. Você usará essa cópia nova durante toda a Lição 4.  
  
### <a name="to-create-the-lesson-4-package"></a>Para criar o pacote da Lição 4  
  
1.  Se o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools ainda não estiver aberto, clique em **Iniciar**, aponte para **Todos os Programas**, **Microsoft SQL Server**e clique em **SQL Server Data Tools**.  
  
2.  No menu **Arquivo** , clique em **Abrir**, clique em **Projeto/Solução**, selecione **Tutorial do SSIS** , clique em **Abrir**e clique duas vezes em **SSIS Tutorial.sln**.  
  
3.  No Gerenciador de Soluções, clique com o botão direito do mouse em **Lesson 3.dtsx**e clique em **Copiar**.  
  
4.  No Gerenciador de Soluções, clique com o botão direito do mouse em **Pacotes SSIS**e clique em **Colar**.  
  
    Por padrão, o pacote copiado recebe o nome de Lesson 4.dtsx.  
  
5.  No Gerenciador de Soluções, clique duas vezes em **Lesson 4.dtsx** para abrir o pacote.  
  
6.  Clique com o botão direito do mouse em qualquer lugar da tela de fundo da guia **Fluxo de Controle** e clique em **Propriedades**.  
  
7.  Na janela Propriedades, atualize a propriedade **Name** para **Lição 4**.  
  
8.  Clique na caixa da propriedade **ID** e, na lista, clique em **<Generate New ID>**.  
  
### <a name="to-add-the-completed-lesson-3-package"></a>Para adicionar o pacote concluído da Lição 3  
  
1.  Abra o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e abra o projeto do Tutorial do SSIS.  
  
2.  No Gerenciador de Soluções, clique com o botão direito do mouse em **Pacotes SSIS**e clique em **Adicionar Pacote Existente**.  
  
3.  Na caixa de diálogo **Adicionar Cópia do Pacote Existente**, em **Local do pacote**, selecione **Sistema de arquivos**.  
  
4.  Clique no botão Procurar **(…)** , navegue até Lesson 3.dtsx no computador e clique em **Abrir**.  
  
    Para baixar todos os pacotes de lição para este tutorial, faça o seguinte.  
  
    1.  Navegue para os [Exemplos de Produtos do Integration Services](http://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Clique na guia **DOWNLOADS** .  
  
    3.  Clique no arquivo SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
5.  Copie e cole o pacote da Lição 3, conforme descrito nas etapas 3 a 8 do procedimento anterior.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Etapa 2: Criando um arquivo corrompido](../integration-services/lesson-4-2-creating-a-corrupted-file.md)  
  
