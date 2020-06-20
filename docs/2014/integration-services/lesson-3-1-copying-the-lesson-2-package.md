---
title: 'Etapa 1: copiar o pacote da Lição 2 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4bd91402-4e37-41de-ab78-8ca5a1948a37
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 3ae62c014baffec44c856587b99410b9c7228e6a
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965266"
---
# <a name="step-1-copying-the-lesson-2-package"></a>Etapa 1: Copiar o pacote da Lição 2
  Nesta tarefa, você criará uma cópia do pacote Lesson 2.dtsx criado na Lição 2. Como alternativa, é possível adicionar o pacote concluído da Lição 2 incluído no tutorial do projeto e copiá-lo. Você usará essa cópia nova durante toda a Lição 3.  
  
### <a name="to-create-the-lesson-3-package"></a>Para criar o pacote da Lição 3  
  
1.  Se o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools ainda não estiver aberto, clique em **Iniciar**, aponte para **Todos os Programas**, **Microsoft SQL Server 2012**e clique em **SQL Server Data Tools**.  
  
2.  No menu **Arquivo** , clique em **Abrir**, clique em **Projeto/Solução**, selecione **Tutorial do SSIS** , clique em **Abrir**e clique duas vezes em **SSIS Tutorial.sln**.  
  
3.  No Gerenciador de Soluções, clique com o botão direito do mouse em **Lesson 2.dtsx**e clique em **Copiar**.  
  
4.  Em Gerenciador de Soluções, clique com o botão direito do mouse em **pacotes SSIS**e clique em **colar**.  
  
     Por padrão, o pacote copiado recebe o nome de Lesson 3.dtsx.  
  
5.  Em Gerenciador de Soluções, clique duas vezes na **lição 3. dtsx** para abrir o pacote.  
  
6.  Clique com o botão direito do mouse em qualquer lugar da tela de fundo da guia **Fluxo de Controle** e clique em **Propriedades**.  
  
7.  Na janela Propriedades, atualize a `Name` propriedade para `Lesson 3` .  
  
8.  Clique na caixa da propriedade **ID** e, na lista, clique em **\<Generate New ID>**.  
  
### <a name="to-add-the-completed-lesson2-package"></a>Para adicionar o pacote concluído da lição 2  
  
1.  Abra o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e abra o projeto do Tutorial do SSIS.  
  
2.  Em Gerenciador de Soluções, clique com o botão direito do mouse em **pacotes SSIS**e clique em **Adicionar pacote existente**.  
  
3.  Na caixa de diálogo **Adicionar cópia do pacote existente** , em **local do pacote**, selecione **sistema de arquivos**.  
  
4.  Clique no botão Procurar **(…)**, navegue até **Lesson 2.dtsx** no computador e clique em **Abrir**.  
  
     Para baixar todos os pacotes de lição para este tutorial, faça o seguinte.  
  
    1.  Navegue para os [Exemplos de Produtos do Integration Services](https://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Clique na guia **downloads** .  
  
    3.  Clique no arquivo SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
5.  Copie e cole o pacote da Lição 3, conforme descrito nas etapas 3 a 8 do procedimento anterior.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Etapa 2: Adicionar e configurar registro em log](lesson-3-2-adding-and-configuring-logging.md)  
  
  
