---
title: Visualizando relatórios | Microsoft Docs
ms.custom: ''
ms.date: 05/05/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: reports
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Report Designer [Reporting Services], previewing reports
- previewing reports [Reporting Services]
- printing previews
- test servers [Reporting Services]
ms.assetid: 85117f6c-828e-45c9-810f-e700d9bfba67
caps.latest.revision: 44
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 2cdd46a01c2151a828d58f851e3a4bdcb02e7483
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="previewing-reports"></a>Visualizando relatórios
  Ao criar um relatório do     [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , convém vê-lo antes da publicação em um ambiente de produção. Há várias formas de se fazer isso: você pode alternar para o modo de Visualização no Designer de Relatórios, usar a janela de visualização do Designer de Relatórios e publicar o relatório em um servidor de relatórios em um ambiente de teste.  
  
> [!NOTE]  
>  Quando você visualizar um relatório, seus dados serão armazenados em cache em um arquivo no computador local. Ao visualizar novamente o mesmo relatório usando a mesma consulta, os mesmos parâmetros e as mesmas credenciais, o Designer de Relatórios recuperará a cópia em cache em vez de executar a consulta mais uma vez. O arquivo de dados será salvo como *\<nomedorelatório>*.rdl.data no mesmo diretório do arquivo de definição de relatório. Ele não será excluído quando você fechar o Designer de Relatórios.  
  
## <a name="preview-mode"></a>Modo de Visualização  
 É possível visualizar um relatório no Designer de Relatórios clicando em ![ssrs_ssdt_preview](../../reporting-services/media/ssrs-ssdt-preview.png "ssrs_ssdt_preview"). Isso executará o relatório localmente, usando a mesma funcionalidade de processamento e renderização de relatório do servidor de relatórios. O relatório será exibido como uma imagem interativa: é possível selecionar parâmetros, clicar em links, exibir o mapa do documento e expandir e recolher áreas ocultas do relatório. Também é possível exportar o relatório para qualquer formato de renderização instalado.  
  
## <a name="standalone-preview"></a>Visualização autônoma  
 Outra forma de visualizar um relatório é executar seu projeto em uma configuração de depuração, por exemplo, para depurar assemblies personalizados que você criou. O relatório é aberto no navegador padrão. Há três maneiras de executar um projeto:  
  
-   Clicando em **Iniciar Depuração** no menu **Depurar** .  
  
-   Ao clicar no botão **Iniciar** na barra de ferramentas padrão [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ![ssrs_ssdt_startdebug](../../reporting-services/reports/media/ssrs-ssdt-startdebug.png "ssrs_ssdt_startdebug").  
  
-   Pressionando **F5**.  
  
 Se você usar a configuração de projeto que cria um relatório mas não o implanta, o relatório especificado na propriedade **StartItem** da configuração atual será aberto em outra janela de visualização. A janela de visualização exibirá o relatório da mesma forma e terá a mesma funcionalidade do modo de Visualização.  
  
> [!NOTE]  
>  Antes de depurar um relatório, defina um item inicial. Por exemplo, se você executar o modo de depuração e o navegador abrir a página do servidor de relatório principal e não o relatório no modo de visualização. Para definir um item inicial no Gerenciador de Soluções, clique com o botão direito do mouse no projeto de relatório, clique em **Propriedades**, **StartItem**e selecione o nome do relatório que será exibido.  
  
 Se quiser visualizar um relatório específico que não é o item inicial do projeto, selecione uma configuração que cria o relatório, mas que não o implanta (por exemplo, a configuração DebugLocal), clique com o botão direito do mouse no relatório e clique em **Executar**. Escolha uma configuração que não implante o relatório, caso contrário, o relatório será publicado no servidor de relatórios em vez de ser exibido localmente na janela de visualização.  
  
## <a name="publishing-to-a-test-server"></a>Publicando em um servidor de teste  
 Também é possível testar os relatórios publicando-os em um servidor de teste, navegar para o relatório e visualizá-lo. A publicação do relatório em um servidor de teste é igual à publicação em um servidor de produção. Para obter informações sobre como publicar um relatório, consulte [Publicando relatórios em um servidor de relatório](../../reporting-services/reports/publishing-reports-to-a-report-server.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Imprimir relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)   
 [Imprimir um relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/print-a-report-report-builder-and-ssrs.md)   
 [Publicar Relatórios](http://msdn.microsoft.com/library/ef5a514e-e818-4041-a8b0-15835f9a046b)   
 [Usar assemblies personalizados com relatórios](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
