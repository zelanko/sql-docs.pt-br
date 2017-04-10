---
title: "Carregar um arquivo ou relat&#243;rio (Gerenciador de Relat&#243;rios) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "publicando relatórios [Reporting Services], carregando arquivos"
  - "relatórios [Reporting Services], publicando"
  - "carregando relatórios [Reporting Services]"
  - "carregando arquivos [Reporting Services]"
  - "arquivos [Reporting Services], carregando"
ms.assetid: 79027e11-f4ba-4bfd-bd8c-d334e3da02a1
caps.latest.revision: 42
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 42
---
# Carregar um arquivo ou relat&#243;rio (Gerenciador de Relat&#243;rios)
  O Gerenciador de Relatórios fornece um recurso de carregamento que permite adicionar relatórios, modelos e outros arquivos a um servidor de relatório sem publicar esses itens a partir de um aplicativo cliente. Os arquivos carregados a partir do sistema de arquivos são armazenados como itens no servidor de relatório. O tipo de arquivo carregado determina o modo de armazenamento:  
  
-   Os arquivos .rdl são armazenados como relatórios.  
  
-   Os arquivos .smdl são armazenados como modelos de relatório.  
  
-   Todos os outros arquivos, incluindo os arquivos de fonte de dados compartilhada (.rds), são carregados como recursos. Os recursos não são processados por um servidor de relatório, mas podem ser exibidos no Gerenciador de Relatórios se o servidor de relatório oferecer suporte ao tipo MIME de arquivo.  
  
### Para carregar um arquivo ou relatório  
  
1.  Inicie o [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md).  
  
2.  No Gerenciador de Relatórios, navegue até a página **Conteúdo** . Navegue até a pasta à qual deseja adicionar um item.  
  
3.  Clique em **Carregar Arquivo**.  
  
4.  Clique em **Procurar** para selecionar o arquivo a ser carregado. Você pode carregar um arquivo de definição de relatório, uma imagem, um documento ou qualquer arquivo que deseje disponibilizar no servidor de relatório.  
  
5.  Digite um nome para o novo item. Um nome de item pode incluir espaços, mas não pode incluir os caracteres reservados: ; ? : @ & = + , $ / * \< > |.  
  
6.  Se desejar substituir um item existente pelo novo item, selecione **Substituir item, se existir**.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## Consulte também  
 [Criar, excluir ou modificar uma fonte de dados compartilhada &#40;Gerenciador de Relatórios&#41;](../Topic/Create,%20Delete,%20or%20Modify%20a%20Shared%20Data%20Source%20\(Report%20Manager\).md)   
 [Página Conteúdo &#40;Gerenciador de Relatórios&#41;](../Topic/Contents%20Page%20\(Report%20Manager\).md)   
 [Página Carregar Arquivo &#40;Gerenciador de Relatórios&#41;](../Topic/Upload%20File%20Page%20\(Report%20Manager\).md)   
 [Carregar arquivos em uma pasta](../../reporting-services/report-server/upload-files-to-a-folder.md)  
  
  