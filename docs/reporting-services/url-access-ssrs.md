---
title: Acesso à URL (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: reporting-services
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- URL access [Reporting Services]
- links [Reporting Services], URL access
- URL access [Reporting Services], about URL access
- parameters [Reporting Services], URL access
- report servers [Reporting Services], URL access
- hyperlinks [Reporting Services]
ms.assetid: 52c3f2a3-3d6d-4fee-9c46-83f366919398
caps.latest.revision: 43
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: f0da33c47af1470c917808729ee2aee8a503fa80
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="url-access-ssrs"></a>Acesso à URL (SSRS)
  O acesso à URL do servidor de relatório do SQL Server Reporting Services (SSRS) permite enviar comandos a um servidor de relatório por meio de uma solicitação de URL. Por exemplo, você pode personalizar a renderização de um relatório em um servidor de relatório em modo nativo ou em uma biblioteca do SharePoint. Você pode exibir o relatório usando um conjunto específico de valores de parâmetros de relatório ou exibir uma página específica de interesse do relatório. Você pode encapsular essas informações na URL usando parâmetros de acesso à URL predefinidos. Você pode personalizar ainda mais como o servidor de relatório processa o relatório inserindo parâmetros de renderização de formatos ou de aparência do visualizador de relatórios. Você pode colar essa URL diretamente em um email ou página da Web para permitir que outros acessem seu relatório da mesma maneira no navegador.  
  
 Outras ações que você pode executar por acesso à URL são:  
  
-   Enviar comandos ao visualizador de HTML, como ajuste de aparência  
  
-   Listar os itens filho de uma pasta de catálogo  
  
-   Recuperar a definição de XML de um item de catálogo  
  
-   Renderizar um instantâneo de histórico de relatório específico  
  
-   Gerenciar sessões de relatório  
  
 Para conferir a lista completa de comandos e configurações disponíveis por acesso à URL, consulte [Referência de parâmetro de acesso de URL](../reporting-services/url-access-parameter-reference.md).  
  
## <a name="url-access-concepts"></a>Conceitos do acesso à URL  
 As solicitações de URL ao servidor de relatório contêm parâmetros processados pelo servidor de relatório. A forma como o servidor de relatório manipula as solicitações de URL dependerá dos parâmetros, dos prefixos de parâmetro e dos tipos de item incluídos na URL. As URLs dos servidores de relatório aderem às diretrizes de formatação de URL propostas pelo padrão de rascunho do consórcio W3C/IETF. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] é compatível com a maioria dos navegadores de Internet ou dos aplicativos que dão suporte ao endereçamento de URL padrão.  
  
### <a name="url-access-syntax"></a>Sintaxe do acesso à URL  
 As solicitações de URL podem conter vários parâmetros listados em qualquer ordem. Os parâmetros são separados por um E comercial (&) e os pares de nome/valor são separados por um sinal de igualdade (=).  
  
```  
  
rswebserviceurl  
?  
reportpath  
      [&prefix:param=value]...n]  
  
```  
  
### <a name="syntax-description"></a>Descrição da sintaxe  
 *rswebserviceurl*  
 A URL do serviço Web do servidor de relatório. No modo nativo, é a URL do serviço Web da instância do servidor de relatório configurada no Gerenciador de Configurações do Reporting Services (consulte [Configurar as URLs do Servidor de Relatório &#40; 	Gerenciador de Configurações do SSRS&#41;](../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)). Por exemplo:  
  
```  
http://myrshost/reportserver  
https://machine.adventure-works.com/reportserver_MYNAMEDINSTANCE  
```  
  
 No modo integrado do SharePoint, é a URL do proxy do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] em um site do SharePoint integrado ao [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Por exemplo:  
  
```  
http://myspsite/subsite/_vti_bin/reportserver  
```  
  
> [!TIP]  
>  É importante que a URL inclua a sintaxe do proxy `_vti_bin` para rotear a solicitação através do SharePoint e do proxy HTTP [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . O proxy adiciona qualquer contexto à solicitação HTTP, o contexto necessário para garantir a execução adequada do relatório para servidores de relatório no modo do SharePoint.  
  
 *pathinfo*  
 O nome do caminho relativo do item no banco de dados do servidor de relatório no modo nativo ou a URL totalmente qualificada do item em um catálogo do SharePoint.  
  
 O caminho do item de catálogo. No modo nativo, é o caminho relativo do item no banco de dados do servidor de relatório, que começa com uma barra (**/**). Por exemplo:  
  
```  
/AdventureWorks 2008R2/Employee_Sales_Summary_2008R2  
```  
  
 No modo integrado do SharePoint, é a URL totalmente qualificada do item na biblioteca do SharePoint, incluindo a extensão do item. Por exemplo:  
  
```  
http://myspsite/subsite/AdventureWorks 2008R2/Employee_Sales_Summary_2008R2.rdl  
```  
  
 **&**  
 Usado para separar os pares de nome e valor dos parâmetros de acesso à URL.  
  
 **prefixo**  
 Opcional. Um prefixo do parâmetro de acesso à URL (por exemplo, `rs:` ou `rc:`) que acessa um processo específico executado no servidor de relatório.  
  
> [!NOTE]  
>  Se um prefixo de um parâmetro de acesso à URL não for incluído, o parâmetro será processado pelo servidor de relatório como um parâmetro de relatório. Os parâmetros de relatório não usam um prefixo de parâmetro e diferenciam maiúsculas de minúsculas.  
  
 **param**  
 O nome do parâmetro.  
  
 *value*  
 O texto da URL correspondente ao valor do parâmetro usado.  
  
 **Observação:** para obter uma lista dos parâmetros de acesso a URL disponíveis, consulte [URL Access Parameter Reference](../reporting-services/url-access-parameter-reference.md). Para obter exemplos de como transmitir parâmetros de relatório na URL, consulte [Pass a Report Parameter Within a URL](../reporting-services/pass-a-report-parameter-within-a-url.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrições das tarefas|Links|  
|-----------------------|-----------|  
|Acessar itens do servidor de relatório, como relatórios, fontes de dados compartilhadas e recursos.|[Acessar itens do Servidor de Relatório usando o acesso à URL](../reporting-services/access-report-server-items-using-url-access.md)|  
|Transmitir parâmetros de relatório a um relatório.|[Pass a Report Parameter Within a URL](../reporting-services/pass-a-report-parameter-within-a-url.md)|  
|Definir a localidade dos parâmetros de relatório na cadeia de caracteres de acesso à URL, o que define as interpretações de datas, moedas etc. específicas da localidade.|[Definir o idioma dos parâmetros do relatório em uma URL](../reporting-services/set-the-language-for-report-parameters-in-a-url.md)|  
|Enviar configurações específicas da extensão de renderização que personalizam como o relatório é renderizado.|[Especificar configurações de informações do dispositivo em uma URL](../reporting-services/specify-device-information-settings-in-a-url.md)|  
|Exportar um relatório diretamente para um formato de arquivo sem exibi-lo no navegador.|[Exportar um relatório com acesso à URL](../reporting-services/export-a-report-using-url-access.md)|  
|Abrir um relatório e navegar diretamente ao local de uma cadeia de caracteres.|[Pesquisar um relatório com acesso à URL](../reporting-services/search-a-report-using-url-access.md)|  
|Renderizar um instantâneo de histórico de relatório específico.|[Renderizar instantâneo de histórico de relatório com o acesso à URL](../reporting-services/render-a-report-history-snapshot-using-url-access.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Pass a Report Parameter Within a URL](../reporting-services/pass-a-report-parameter-within-a-url.md)   
 [Referência de parâmetro de acesso à URL](../reporting-services/url-access-parameter-reference.md)   
 [Integrando o Reporting Services usando o acesso à URL](../reporting-services/application-integration/integrating-reporting-services-using-url-access.md)   
 [Localizando, exibindo e gerenciando relatórios &#40;Construtor de Relatórios e SSRS&#41;](../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
