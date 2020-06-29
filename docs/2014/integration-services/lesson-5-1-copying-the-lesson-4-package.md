---
title: 'Etapa 1: copiar o pacote da Lição 4 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 8aa7d690-4649-4c0a-ac6f-9504637ee426
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a2d07500e357d69ba0e07d5453ae7df7f0244360
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440423"
---
# <a name="step-1-copying-the-lesson-4-package"></a>Etapa 1: Copiar o pacote da Lição 4
  Nesta tarefa, você criará uma cópia do pacote Lesson 4.dtsx criado na Lição 4. Como alternativa, é possível adicionar o pacote concluído da Lição 4 incluído no tutorial do projeto e copiá-lo. Você usará essa cópia nova durante toda a Lição 5.  
  
### <a name="to-copy-the-lesson-4-package"></a>Para copiar o pacote da Lição 4  
  
1.  Se o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools ainda não estiver aberto, clique em **Iniciar**, aponte para **Todos os Programas**, **Microsoft SQL Server 2012**e clique em **SQL Server Data Tools**.  
  
2.  No menu **Arquivo** , clique em **Abrir**, clique em **Projeto/Solução**, selecione **Tutorial do SSIS** , clique em **Abrir**e clique duas vezes em **SSIS Tutorial.sln**.  
  
3.  No Gerenciador de Soluções, clique com o botão direito do mouse em **Lesson 4.dtsx**e clique em **Copiar**.  
  
4.  Em Gerenciador de Soluções, clique com o botão direito do mouse em **pacotes SSIS**e clique em **colar**.  
  
     Por padrão, o pacote copiado recebe o nome de Lesson 5.dtsx.  
  
5.  No Gerenciador de Soluções, clique duas vezes em **Lesson 5.dtsx** para abrir o pacote.  
  
6.  Clique com o botão direito do mouse em qualquer lugar no plano de fundo da guia **fluxo de controle** e clique em **Propriedades**.  
  
7.  Na janela Propriedades, atualize a `Name` propriedade para `Lesson 5` .  
  
8.  Clique na caixa da propriedade **ID** , clique na seta suspensa e, em seguida, clique em **\<Generate New ID>** .  
  
### <a name="to-add-the-completed-lesson-4-package"></a>Para adicionar o pacote concluído da Lição 4  
  
1.  Abra as Ferramentas de Dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e abra o projeto do Tutorial do SSIS.  
  
2.  Em Gerenciador de Soluções, clique com o botão direito do mouse em **pacotes SSIS**e clique em **Adicionar pacote existente**.  
  
3.  Na caixa de diálogo **Adicionar cópia do pacote existente** , em **local do pacote**, selecione **sistema de arquivos**.  
  
4.  Clique no botão procurar **(...)** , navegue até a **lição 4. dtsx** em seu computador e clique em **abrir**.  
  
     Para baixar todos os pacotes de lição para este tutorial, faça o seguinte.  
  
    1.  Navegue para os [Exemplos de Produtos do Integration Services](https://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Clique na guia **downloads** .  
  
    3.  Clique no arquivo SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
5.  Copie e cole o pacote da Lição 4, conforme descrito nas etapas 3 a 8 do procedimento anterior.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Etapa 2: Habilitar e configurar configurações de pacote](lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
  
