---
title: "Acesso offline da documenta&#231;&#227;o do SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "08/22/2016"
ms.prod: "sql-non-specified"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "server-general"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 257ed357-8cbb-43bd-b042-254be5fbb977
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# Acesso offline da documenta&#231;&#227;o do SQL Server

Exiba a documentação técnica offline do SQL Server 2016.
  
## Pré-requisitos
Para exibir a documentação técnica offline do SQL Server 2016, é necessário ter o HelpViewer 2.2, que é instalado com: 
- [Visual Studio 2015 (qualquer edição, incluindo Community)](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) ou
- [SSMS (SQL Server Management Studio) Visualização de abril de 2016 (13.0.12500.29) ou posterior](https://msdn.microsoft.com/library/mt238290.aspx)

Instale um desses antes de continuar com as etapas abaixo.
  
## Instalar a documentação técnica offline do SQL Server 

1. Instale qualquer edição do Visual Studio 2015 ou SSMS com build de Visualização de abril de 2016 ou posterior. 
2. Inicie o SSMS ou o Visual Studio.
3. No menu **Ajuda** na barra de navegação superior, selecione **Adicionar e Remover Conteúdo da Ajuda**. 

#### (Essa ação inicia o HelpViewer)

4. No HelpViewer, escolha a Fonte de Instalação padrão: **Online** 
5. Clique em **Adicionar** ao lado de toda a documentação a ser instalada.
6. Clique no botão **Atualizar** no lado inferior direito da tela para baixar e instalar a documentação selecionada.
![carregar conteúdo offline](../sql-server/media/load-offline-content.png) 

 >** IMPORTANTE:** Depois de clicar em Atualizar, o HelpViewer, eventualmente, congelará ou parará de responder. Ele ainda baixa e instala suas escolhas de documentação. **Para resolver esse problema**, encerre o HelpViewer no Gerenciador de Tarefas e reinicie-o seguindo a etapa 3 acima. Na primeira vez em que o HelpViewer congelar/parar de responder, execute [estas etapas](https://msdn.microsoft.com/library/mt654096.aspx) também. Você só precisa realizar estas etapas uma vez, mas provavelmente, precisará encerrar o HelpViewer no Gerenciador de Tarefas sempre que atualizar o conteúdo.  
6. Reinicie o HelpViewer selecionando novamente Ajuda/Adicionar e Remover Conteúdo. A documentação offline agora está pronta para uso!



   ![Offline e pronta para uso](../sql-server/media/offline-ready-to-use.png)


