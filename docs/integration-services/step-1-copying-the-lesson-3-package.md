---
title: "Etapa 1: Copiando o pacote da Li&#231;&#227;o 3 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 0d053786-5203-43f3-a613-27a8dd2bc44a
caps.latest.revision: 25
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
---
# Etapa 1: Copiando o pacote da Li&#231;&#227;o 3
Nesta tarefa, você criará uma cópia do pacote Lesson 3.dtsx criado na Lição 3. Se você não tiver completado a lição 3, poderá adicionar o pacote completo da lição 3, incluído no tutorial do projeto, e então trabalhar com uma cópia. Você usará essa cópia nova durante toda a Lição 4.  
  
### Para criar o pacote da Lição 4  
  
1.  Se o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools ainda não estiver aberto, clique em **Iniciar**, aponte para **Todos os Programas**, **Microsoft SQL Server** e clique em **SQL Server Data Tools**.  
  
2.  No menu **Arquivo**, clique em **Abrir**, clique em **Projeto/Solução**, selecione **Tutorial do SSIS**, clique em **Abrir** e clique duas vezes em **SSIS Tutorial.sln**.  
  
3.  No Gerenciador de Soluções, clique com o botão direito do mouse em **Lesson 3.dtsx** e clique em **Copiar**.  
  
4.  No Gerenciador de Soluções, clique com o botão direito do mouse em **Pacotes SSIS** e clique em **Colar**.  
  
    Por padrão, o pacote copiado recebe o nome de Lesson 4.dtsx.  
  
5.  No Gerenciador de Soluções, clique duas vezes em **Lesson 4.dtsx** para abrir o pacote.  
  
6.  Clique com o botão direito do mouse em qualquer lugar da tela de fundo da guia **Fluxo de Controle** e clique em **Propriedades**.  
  
7.  Na janela Propriedades, atualize a propriedade **Name** para **Lição 4**.  
  
8.  Clique na caixa da propriedade **ID** e, na lista, clique em **<Generate New ID>**.  
  
### Para adicionar o pacote concluído da Lição 3  
  
1.  Abra o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e abra o projeto do Tutorial do SSIS.  
  
2.  No Gerenciador de Soluções, clique com o botão direito do mouse em **Pacotes SSIS** e clique em **Adicionar Pacote Existente**.  
  
3.  Na caixa de diálogo **Adicionar Cópia do Pacote Existente**, em **Local do pacote**, selecione **Sistema de arquivos**.  
  
4.  Clique no botão Procurar **(…)**, navegue até Lesson 3.dtsx no computador e clique em **Abrir**.  
  
    Para baixar todos os pacotes de lição para este tutorial, faça o seguinte.  
  
    1.  Navegue para os [Exemplos de Produtos do Integration Services](http://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Clique na guia **DOWNLOADS** .  
  
    3.  Clique no arquivo SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
5.  Copie e cole o pacote da Lição 3, conforme descrito nas etapas 3 a 8 do procedimento anterior.  
  
## Próxima tarefa da lição  
[Etapa 2: Criando um arquivo corrompido](../integration-services/step-2-creating-a-corrupted-file.md)  
  
