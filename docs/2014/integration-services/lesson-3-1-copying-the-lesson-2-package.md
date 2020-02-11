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
manager: craigg
ms.openlocfilehash: b4458f8fe198ba3d052bcb21bef38975738b2c23
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62767458"
---
# <a name="step-1-copying-the-lesson-2-package"></a>Etapa 1: Copiando o pacote da Lição 2
  Nesta tarefa, você criará uma cópia do pacote Lesson 2.dtsx criado na Lição 2. Como alternativa, é possível adicionar o pacote concluído da Lição 2 incluído no tutorial do projeto e copiá-lo. Você usará essa cópia nova durante toda a Lição 3.  
  
### <a name="to-create-the-lesson-3-package"></a>Para criar o pacote da Lição 3  
  
1.  Se o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools ainda não estiver aberto, clique em **Iniciar**, aponte para **Todos os Programas**, **Microsoft SQL Server 2012**e clique em **SQL Server Data Tools**.  
  
2.  No menu **arquivo** , clique em **abrir**, clique em **projeto/solução**, selecione **tutorial do SSIS** , clique em **abrir**e clique duas vezes em **SSIS tutorial. sln**.  
  
3.  No Gerenciador de Soluções, clique com o botão direito do mouse em **Lesson 2.dtsx**e clique em **Copiar**.  
  
4.  No Gerenciador de Soluções, clique com o botão direito do mouse em **Pacotes SSIS**e clique em **Colar**.  
  
     Por padrão, o pacote copiado recebe o nome de Lesson 3.dtsx.  
  
5.  Em Gerenciador de Soluções, clique duas vezes na **lição 3. dtsx** para abrir o pacote.  
  
6.  Clique com o botão direito do mouse em qualquer lugar da tela de fundo da guia **Fluxo de Controle** e clique em **Propriedades**.  
  
7.  Na janela Propriedades, atualize a `Name` propriedade para. `Lesson 3`  
  
8.  Clique na caixa da propriedade **ID** e, na lista, clique em ** \<gerar nova ID>**.  
  
### <a name="to-add-the-completed-lesson2-package"></a>Para adicionar o pacote concluído da lição 2  
  
1.  Abra o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e abra o projeto do Tutorial do SSIS.  
  
2.  No Gerenciador de Soluções, clique com o botão direito do mouse em **Pacotes SSIS**e clique em **Adicionar Pacote Existente**.  
  
3.  Na caixa de diálogo **Adicionar Cópia do Pacote Existente** , em **Local do pacote**, selecione **Sistema de arquivos**.  
  
4.  Clique no botão Procurar **(…)**, navegue até **Lesson 2.dtsx** no computador e clique em **Abrir**.  
  
     Para baixar todos os pacotes de lição para este tutorial, faça o seguinte.  
  
    1.  Navegue para os [Exemplos de Produtos do Integration Services](https://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Clique na guia **DOWNLOADS** .  
  
    3.  Clique no arquivo SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
5.  Copie e cole o pacote da Lição 3, conforme descrito nas etapas 3 a 8 do procedimento anterior.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Etapa 2: Adicionando e configurando registro em log](lesson-3-2-adding-and-configuring-logging.md)  
  
  
