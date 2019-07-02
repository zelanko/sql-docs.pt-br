---
title: Carregar arquivos em uma pasta | Microsoft Docs
ms.date: 06/17/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
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
ms.openlocfilehash: d93840b2b1b7354238ccae12ba3a540889038fb2
ms.sourcegitcommit: 1bbbbb8686745a520543ac26c4d4f6abe1b167ea
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2019
ms.locfileid: "67228683"
---
# <a name="upload-files-to-a-folder"></a>Carregar arquivos em uma pasta
  Você pode carregar arquivos do sistema de arquivos e armazená-los como itens gerenciados em um banco de dados do servidor de relatório. O que acontece quando o arquivo é carregado depende do tipo de arquivo.  
  
-   Carregar um arquivo .rdl é equivalente a publicar um relatório.  
  
-   O carregamento de qualquer outro arquivo adiciona esse arquivo ao banco de dados do servidor de relatório como um único objeto binário. Esses arquivos são publicados em um servidor de relatório como um recurso. Os recursos podem ser qualquer tipo de arquivo. Se a extensão do arquivo corresponder com um tipo MIME conhecido, um ícone desse tipo MIME será usado para identificar o tipo de recurso. Caso contrário, um ícone de arquivo genérico indica um recurso.  
  
    >[!NOTE]  
    >Você não pode carregar um arquivo de fonte de dados de relatório (.rds) para criar uma fonte de dados compartilhada. Um arquivo .rds só é usado no Designer de Relatórios. Esse arquivo não pode fornecer o conteúdo para um item de fonte de dados compartilhada definido e gerenciado pelo portal da Web. Como alternativa do carregamento, é possível gravar um script que cria uma fonte de dados compartilhada com base em um arquivo .rds.  
  
 O tamanho máximo para itens carregados é de 2 GB e pode ser definido usando a propriedade MaxFileSizeMb em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
 Visualmente, os arquivos carregados em um banco de dados do servidor de relatório são representados na hierarquia de pastas com os seguintes ícones.  
  
  ![Ícones de arquivo uploadable do servidor de relatório](../../reporting-services/report-server/media/upload-files-to-a-folder/report-server-uploadable-file-icons.png)
  
 Ao ser carregado, o arquivo sempre é colocado na pasta que está selecionada atualmente. Você pode navegar até a pasta na qual deseja incluir o item primeiro ou carregar um arquivo e, em seguida, movê-lo para um local final posteriormente.  
  
 Para carregar um arquivo, use o portal da web. O carregamento de arquivos em um servidor de relatório depende das tarefas que fazem parte de sua atribuição de função. Se a segurança padrão for usada, os administradores locais poderão adicionar itens a um servidor de relatório. Se Meus Relatórios estiver habilitado, qualquer usuário que tiver uma pasta Meus Relatórios terá permissão para carregar itens nessa pasta. Se atribuições de função personalizadas forem utilizadas, a atribuição de função deve incluir tarefas que ofereçam suporte para o gerenciamento de pastas.  
  
|Para fazer isso|Inclua estas tarefas|  
|----------------|-------------------------|  
|Carregar um arquivo .rdl em uma pasta|Gerenciar relatórios|  
|Carregar qualquer arquivo como um objeto binário|Gerenciar recursos|  
|Exibir o conteúdo de uma pasta|Exibir recursos, exibir relatórios|  
  
## <a name="see-also"></a>Confira também  
 [O portal da Web de um servidor de relatório (modo nativo do SSRS)](../../reporting-services/web-portal-ssrs-native-mode.md)  
 [Concedendo permissões em um servidor de relatório no modo nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [Tarefas e permissões](../../reporting-services/security/tasks-and-permissions.md)   
 [Carregar um arquivo ou relatório no servidor de relatório](../../reporting-services/reports/upload-a-file-or-report-report-manager.md)   
  