---
title: Usando Meus Relatórios (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-builder
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: 49c3c1da-b106-41f6-9173-16ff225bade8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 97ff26393b97c215efc429b55ba6a3ae0f4d21c3
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43277888"
---
# <a name="using-my-reports-report-builder-and-ssrs"></a>Usando Meus Relatórios (Construtor de Relatórios e SSRS)
  Em um servidor de relatório configurado em modo nativo, a pasta Meus Relatórios é um espaço de trabalho individual que você pode usar para armazenar e trabalhar com seus próprios relatórios. Outras pastas do servidor de relatórios são públicas e geralmente exigem que os usuários tenham permissões avançadas para adicionar ou modificar o conteúdo de pasta. Em contraste, a pasta Meus Relatórios é uma área de trabalho gerenciada pelo usuário. Você pode adicionar ou remover relatórios e pastas e salvar relatórios vinculados com configurações personalizadas.  
  
 Conceitualmente, a pasta Meus Relatórios é semelhante à pasta Meus Documentos no sistema de arquivos do Windows. Embora cada usuário tenha uma pasta chamada Meus Relatórios, a pasta que cada um acessa é diferente de todos os outros usuários. Exceto para os administradores do servidor de relatórios, outros usuários não podem acessar o conteúdo da pasta Meus Relatórios que pertence a você.  
  
 O recurso Meus Relatórios é opcional e pode ser desabilitado por um administrador de servidor de relatório. Se estiver habilitado, você verá uma pasta Meus Relatórios na pasta Base, que você pode acessar usando o Gerenciador de Relatórios em uma janela da Web. Para obter mais informações, consulte [Localizando e exibindo relatórios no Gerenciador de Relatórios &#40;Construtor de Relatórios e SSRS&#41;](finding-and-viewing-reports-with-a-browser-report-builder-and-ssrs.md).  
  
 Em um servidor de relatório configurado em modo integrado do SharePoint, não existe um equivalente à pasta Meus Relatórios. Para obter mais informações, consulte [Localizando, exibindo e gerenciando relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="ways-to-use-my-reports"></a>Maneiras de usar Meus Relatórios  
 A pasta Meus Relatórios permanecerá vazia até que você adicione relatórios, pastas e outros itens. Aqui estão algumas maneiras de adicionar conteúdo em Meus Relatórios.  
  
-   Crie um relatório pessoal vinculado e armazene-o em Meus Relatórios. Nem todos os relatórios estão disponíveis para serem vinculados. Para obter mais informações, consulte [Criar um relatório vinculado](../../reporting-services/reports/create-a-linked-report.md).  
  
-   Carregue um arquivo de definição de relatório (.rdl), arquivo de modelo de relatório (.smdl) ou outros arquivos do sistema de arquivos. Você pode carregar qualquer arquivo, mas o servidor de relatório só processa os arquivos de relatórios com uma extensão .rdl ou .smdl. Para obter mais informações, consulte “Definições de relatório” na [documentação do Reporting Services](http://go.microsoft.com/fwlink/?linkid=121312) nos Manuais Online do SQL Server e em [Carregar um arquivo ou relatório &#40;Gerenciador de Relatórios&#41;](../../reporting-services/reports/upload-a-file-or-report-report-manager.md).  
  
-   Crie e publique seus próprios relatórios em Meus Relatórios. Para obter mais informações, consulte [Modo de exibição de Design de relatório &#40;Construtor de Relatórios&#41;](../../reporting-services/report-builder/report-design-view-report-builder.md).  
  
 Normalmente, as permissões em Meus Relatórios permitem que você mesmo gerencie a pasta. No entanto, o administrador do servidor de relatório determina finalmente quais tarefas os usuários podem executar. Se permissões insuficientes lhe impedirem de trabalhar com Meus Relatórios, consulte seu administrador de servidor de relatório.  
  
## <a name="searching-my-reports"></a>Pesquisando em Meus Relatórios  
 Quando você pesquisa em um banco de dados do servidor de relatório, o conteúdo da sua pasta Meus Relatórios é incluído na pesquisa, enquanto o conteúdo das outras pastas Meus Relatórios é excluído. Os resultados da pesquisa listam apenas os relatórios para os quais você tem acesso.  
  
## <a name="see-also"></a>Consulte Também  
 [Localizando, exibindo e gerenciando relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
