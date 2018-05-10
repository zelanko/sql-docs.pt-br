---
title: Carregar um arquivo ou relatório (Gerenciador de Relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: reports
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- publishing reports [Reporting Services], uploading files
- reports [Reporting Services], publishing
- uploading reports [Reporting Services]
- uploading files [Reporting Services]
- files [Reporting Services], uploading
ms.assetid: 79027e11-f4ba-4bfd-bd8c-d334e3da02a1
caps.latest.revision: 42
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: d5485f3c29c394655371ff42b690ccbacdcdd53d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="upload-a-file-or-report-report-manager"></a>Carregar um arquivo ou relatório (Gerenciador de Relatórios)
  O Gerenciador de Relatórios fornece um recurso de carregamento que permite adicionar relatórios, modelos e outros arquivos a um servidor de relatório sem publicar esses itens a partir de um aplicativo cliente. Os arquivos carregados a partir do sistema de arquivos são armazenados como itens no servidor de relatório. O tipo de arquivo carregado determina o modo de armazenamento:  
  
-   Os arquivos .rdl são armazenados como relatórios.  
  
-   Os arquivos .smdl são armazenados como modelos de relatório.  
  
-   Todos os outros arquivos, incluindo os arquivos de fonte de dados compartilhada (.rds), são carregados como recursos. Os recursos não são processados por um servidor de relatório, mas podem ser exibidos no Gerenciador de Relatórios se o servidor de relatório oferecer suporte ao tipo MIME de arquivo.  
  
### <a name="to-upload-a-file-or-report"></a>Para carregar um arquivo ou relatório  
  
1.  Inicie o [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  No Gerenciador de Relatórios, navegue até a página **Conteúdo** . Navegue até a pasta à qual deseja adicionar um item.  
  
3.  Clique em **Carregar Arquivo**.  
  
4.  Clique em **Procurar** para selecionar o arquivo a ser carregado. Você pode carregar um arquivo de definição de relatório, uma imagem, um documento ou qualquer arquivo que deseje disponibilizar no servidor de relatório.  
  
5.  Digite um nome para o novo item. Um nome de item pode incluir espaços, mas não pode incluir os caracteres reservados: ; ? : @ & = + , $ / * < > |.  
  
6.  Se desejar substituir um item existente pelo novo item, selecione **Substituir item, se existir**.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Criar, excluir ou modificar uma fonte de dados compartilhada &#40;Gerenciador de Relatórios&#41;](http://msdn.microsoft.com/library/cd7bace3-f8ec-4ee3-8a9f-2f217cdca9f2)   
 [Página Conteúdo &#40;Gerenciador de Relatórios&#41;](http://msdn.microsoft.com/library/6b16869b-158a-4934-9c85-bee934b35378)   
 [Página Carregar Arquivo &#40;Gerenciador de Relatórios&#41;](http://msdn.microsoft.com/library/7bb3166f-9374-4449-b66a-ffb77298507d)   
 [Carregar arquivos em uma pasta](../../reporting-services/report-server/upload-files-to-a-folder.md)  
  
  
