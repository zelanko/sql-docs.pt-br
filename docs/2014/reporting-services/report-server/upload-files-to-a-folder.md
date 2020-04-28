---
title: Carregar arquivos em uma pasta | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- publishing reports [Reporting Services], uploading files
- reports [Reporting Services], publishing
- uploading reports [Reporting Services]
- uploading files [Reporting Services]
- files [Reporting Services], uploading
- files [Reporting Services]
- folders [Reporting Services], uploading files to
ms.assetid: 2f99a288-d4aa-4c64-b310-e457a2aef2c5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e0bb599b49235cc68fdc7cfa2c74e7b15f6c1c4d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78177161"
---
# <a name="upload-files-to-a-folder"></a>Carregar arquivos em uma pasta
  Você pode carregar arquivos do sistema de arquivos e armazená-los como itens gerenciados em um banco de dados do servidor de relatório. O que acontece quando o arquivo é carregado depende do tipo de arquivo.

-   Carregar um arquivo .rdl é equivalente a publicar um relatório.

-   O carregamento de qualquer outro arquivo adiciona esse arquivo ao banco de dados do servidor de relatório como um único objeto binário. Esses arquivos são publicados em um servidor de relatório como um recurso. Os recursos podem ser qualquer tipo de arquivo. Se a extensão do arquivo corresponder com um tipo MIME conhecido, um ícone desse tipo MIME será usado para identificar o tipo de recurso. Caso contrário, um ícone de arquivo genérico indica um recurso.

> [!NOTE]
>  Você não pode carregar um arquivo de fonte de dados de relatório (.rds) para criar uma fonte de dados compartilhada. Um arquivo .rds só é usado no Designer de Relatórios. Esse arquivo não pode fornecer o conteúdo para um item de fonte de dados compartilhada definido e gerenciado pelo Gerenciador de Relatórios. Como alternativa do carregamento, é possível gravar um script que cria uma fonte de dados compartilhada com base em um arquivo .rds.

 O tamanho de arquivo máximo para itens carregados é determinado por [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]. Por padrão, o tamanho máximo é de 4 megabytes (MB).

 Visualmente, os arquivos carregados em um banco de dados do servidor de relatório são representados na hierarquia de pastas com os seguintes ícones.

 Ícone do relatório de ![ícone de relatório](../media/hlp-16doc.gif "Ícone do relatório")

 Ícone ![modelo modelo de relatório ícone](../media/model-icon.gif "Ícone de modelo")

 ícone de ![recurso genérico](../media/hlp-16file.gif "ícone de recurso genérico") ícone de recurso genérico

 Ao ser carregado, o arquivo sempre é colocado na pasta que está selecionada atualmente. Você pode navegar até a pasta na qual deseja incluir o item primeiro ou carregar um arquivo e, em seguida, movê-lo para um local final posteriormente.

 Para carregar um arquivo, use o Gerente de Relatórios. O carregamento de arquivos em um servidor de relatório depende das tarefas que fazem parte de sua atribuição de função. Se a segurança padrão for usada, os administradores locais poderão adicionar itens a um servidor de relatório. Se Meus Relatórios estiver habilitado, qualquer usuário que tiver uma pasta Meus Relatórios terá permissão para carregar itens nessa pasta. Se atribuições de função personalizadas forem utilizadas, a atribuição de função deve incluir tarefas que ofereçam suporte para o gerenciamento de pastas.

|Para fazer isto|Inclua estas tarefas|
|----------------|-------------------------|
|Carregar um arquivo .rdl em uma pasta|Gerenciar relatórios|
|Carregar qualquer arquivo como um objeto binário|Gerenciar recursos|
|Exibir o conteúdo de uma pasta|Exibir recursos, exibir relatórios|

## <a name="see-also"></a>Consulte Também
 [Report Manager &#40;modo nativo do SSRS&#41;].. /report-manager-ssrs-native-mode.md) [conceder permissões em](../security/granting-permissions-on-a-native-mode-report-server.md) [tarefas e permissões](../security/tasks-and-permissions.md) do servidor de relatório no modo nativo [carregar um arquivo ou relatório &#40;Report Manager&#41;](../reports/upload-a-file-or-report-report-manager.md)


