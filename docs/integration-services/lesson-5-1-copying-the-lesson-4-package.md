---
title: 'Etapa 1: copiar o pacote da Lição 4 | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 8aa7d690-4649-4c0a-ac6f-9504637ee426
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b52a7ec9b4c391e7dd0c35ddd51f54e579b080fd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-5-1---copying-the-lesson-4-package"></a>Lição 5-1 – copiar o pacote da Lição 4
Nesta tarefa, você criará uma cópia do pacote Lesson 4.dtsx criado na Lição 4. Como alternativa, é possível adicionar o pacote concluído da Lição 4 incluído no tutorial do projeto e copiá-lo. Você usará essa cópia nova durante toda a Lição 5.  
  
### <a name="to-copy-the-lesson-4-package"></a>Para copiar o pacote da Lição 4  
  
1.  Se o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools ainda não estiver aberto, clique em **Iniciar**, aponte para **Todos os Programas**, **Microsoft SQL Server 2012**e clique em **SQL Server Data Tools**.  
  
2.  No menu **Arquivo** , clique em **Abrir**, clique em **Projeto/Solução**, selecione **Tutorial do SSIS** , clique em **Abrir**e clique duas vezes em **SSIS Tutorial.sln**.  
  
3.  No Gerenciador de Soluções, clique com o botão direito do mouse em **Lesson 4.dtsx**e clique em **Copiar**.  
  
4.  No Gerenciador de Soluções, clique com o botão direito do mouse em **Pacotes SSIS**e clique em **Colar**.  
  
    Por padrão, o pacote copiado recebe o nome de Lesson 5.dtsx.  
  
5.  No Gerenciador de Soluções, clique duas vezes em **Lesson 5.dtsx** para abrir o pacote.  
  
6.  Clique com o botão direito do mouse em qualquer local da tela de fundo da guia **Fluxo de Controle** e clique em **Propriedades**.  
  
7.  Na janela Propriedades, atualize a propriedade **Name** para **Lição 5**.  
  
8.  Clique na caixa da propriedade **ID** , clique na seta suspensa e em **<Generate New ID>**.  
  
### <a name="to-add-the-completed-lesson-4-package"></a>Para adicionar o pacote concluído da Lição 4  
  
1.  Abra as Ferramentas de Dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e abra o projeto do Tutorial do SSIS.  
  
2.  No Gerenciador de Soluções, clique com o botão direito do mouse em **Pacotes SSIS** e clique em **Adicionar Pacote Existente**.  
  
3.  Na caixa de diálogo **Adicionar Cópia do Pacote Existente** , em **Local do pacote**, selecione **Sistema de arquivos**.  
  
4.  Clique no botão Procurar **(…)** , navegue até **Lesson 4.dtsx** no computador e clique em **Abrir**.  
  
    Para baixar todos os pacotes de lição para este tutorial, faça o seguinte.  
  
    1.  Navegue para os [Exemplos de Produtos do Integration Services](http://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Clique na guia **DOWNLOADS** .  
  
    3.  Clique no arquivo SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
5.  Copie e cole o pacote da Lição 4, conforme descrito nas etapas 3 a 8 do procedimento anterior.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Etapa 2: Configurando e habilitando configurações de pacote](../integration-services/lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
