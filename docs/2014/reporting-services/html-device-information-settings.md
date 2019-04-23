---
title: Configurações de informações do dispositivo HTML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- HTML [Reporting Services], rendering
- device information settings [Reporting Services], HTML rendering
ms.assetid: f505f478-dd6d-444a-957c-34f7cfb98911
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8e5f34ac12dd76de22e53be72e04d51d0cef8be1
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59946716"
---
# <a name="html-device-information-settings"></a>Configurações de informações do dispositivo HTML
  A tabela a seguir lista as configurações de informações de dispositivos para renderização no formato HTML.  
  
> [!IMPORTANT]  
>  As configurações de informações de dispositivo listadas na tabela abaixo com um **(\*)** foram preteridas e não devem ser usadas em novos aplicativos. Para obter mais informações, consulte [recursos preteridos no SQL Server Reporting Services no SQL Server 2014](deprecated-features-in-sql-server-reporting-services-ssrs.md).  
  
|Configuração|Valor|  
|-------------|-----------|  
|`AccessibleTablix`|Indica se a renderização será realizada com metadados de acessibilidade adicionais para uso com leitores de tela. Este parâmetro só se aplica a relatórios que contenham estruturas simples de tabela ou matriz com agrupamento simples. O valor padrão é `false`. Os metadados de acessibilidade adicionais tornam o relatório renderizado em conformidade com os seguintes padrões técnicos da seção "Informações e Aplicativos de Intranet e Internet na Web" (1194.22) do documento de Normas de Acessibilidade Eletrônica e de Tecnologia da Informação (Seção 508):<br /><br /> (g) Os cabeçalhos de linhas e colunas das tabelas de dados serão identificados.<br /><br /> (h) A marcação será usada para associar células de dados e células de cabeçalho de tabelas de dados que tenham dois ou mais níveis lógicos de cabeçalhos de linha ou coluna.<br /><br /> (i) Os quadros levarão um título cujo texto facilite a identificação e a navegação do quadro.<br /><br /> Este parâmetro tem suporte no [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[SPS2010](../includes/sps2010-md.md)], mas não no [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[SPS2007](../includes/sps2007-md.md)].|  
|**ActionScript(\*)**|Especifica o nome da função JavaScript a usar quando um evento de ação ocorre, como detalhar ou clicar no indicador. Se esse parâmetro for especificado, um evento de ação disparará a função JavaScript nomeada em vez de um postback para o servidor.|  
|**BookmarkID**|A ID de indicador para ir para o relatório.|  
|**DocMap**|Indica se você deve mostrar ou ocultar o mapa do documento do relatório. O valor padrão desse parâmetro é `true`.|  
|`ExpandContent`|Indica se o relatório deve ser incluído em uma estrutura de tabela que compacta o tamanho horizontal.|  
|**FindString**|O texto a ser pesquisado no relatório. O valor padrão desse parâmetro é uma cadeia de caracteres vazia.|  
|**GetImage (\*)**|Obtém um ícone específico para a interface de usuário do Visualizador de HTML.|  
|`HTMLFragment`|Indica se um fragmento de HTML é criado no lugar de um documento HTML completo. Um fragmento de HTML inclui o conteúdo do relatório em um elemento TABLE e omite os elementos HTML e BODY. O valor padrão é `false`. A renderização usando SOAP com o conjunto de propriedade `HTMLFragment` definido como `true` cria URLs contendo informações da sessão que podem ser usadas para solicitar imagens corretamente. As imagens devem ser recursos carregados no banco de dados do servidor de relatório.|  
|`ImageConsolidation`|Indica se o gráfico renderizado, mapa, medidor e imagens de medidor serão consolidados em uma única imagem grande. A consolidação de imagens ajuda a melhorar o desempenho do relatório no navegador do cliente quando o relatório contém muitos itens de visualização de dados. O valor padrão é `true` para a maioria dos navegadores modernos.|  
|**JavaScript**|Indica se JavaScript é compatível com o relatório renderizado. O valor padrão é `true`.|  
|`LinkTarget`|O destino de hiperlinks no relatório. Você pode direcionar uma janela ou quadro fornecendo o nome da janela, como `LinkTarget` = *window_name*, ou você pode destinar uma nova janela usando `LinkTarget`= blank. Outros nomes de destino válidos incluem _self, _parent e _top.|  
|**OnlyVisibleStyles(\*)**|Indica se somente os estilos compartilhados são gerados para a página renderizada atualmente.|  
|`OutlookCompat`|Indica se ocorrerá renderização com metadados extras que melhoram a aparência do relatório no Outlook. Para os demais, o valor padrão é `false`.|  
|**Parâmetros**|Indica se deve mostrar ou ocultar a área de parâmetros da barra de ferramentas. Se você definir esse parâmetro como um valor `true`, a área de parâmetros da barra de ferramentas será exibida. O valor padrão desse parâmetro é `true`.|  
|`PrefixId`|Quando usado com `HTMLFragment`, ele adiciona o prefixo especificado a todos os atributos `ID` no fragmento HTML que é criado.|  
|**ReplacementRoot(\*)**|A cadeia de caracteres que precede todos os links de detalhamento, alternância e indicadores no relatório quando forem renderizados fora do controle ReportViewer. Por exemplo, este é usado para redirecionar um clique do usuário a uma página personalizada.|  
|**ResourceStreamRoot(\*)**|A cadeia de caracteres a ser pré-demarcada na URL para todos os recursos de imagem, como imagens para alternância ou classificação.|  
|**Seção**|O número da página do relatório para renderizar. Um valor `0` indica que todas as seções do relatório serão renderizadas. O valor padrão é `1`.|  
|**StreamRoot (\*)**|O caminho usado para prefixar o valor do atributo **src** do elemento IMG no relatório de HTML retornado pelo servidor de relatório. Por padrão, o servidor de relatório fornece o caminho. Você pode usar essa configuração para especificar um caminho raiz para as imagens em um relatório (por exemplo, **http://\<servername>/resources/companyimages**).|  
|**StyleStream**|Indica se os estilos e scripts são criados como um fluxo separado em vez de no documento. O valor padrão é `false`.|  
|`Toolbar`|Indica se deve mostrar ou ocultar a barra de ferramentas. O padrão desse parâmetro é `true`. Se o valor desse parâmetro for `false`, todas as demais opções (menos o mapa do documento) serão ignoradas. Se você omitir esse parâmetro, a barra de ferramentas será exibida automaticamente para renderizar formatos que dão suporte a ele.<br /><br /> A barra de ferramentas do Visualizador de Relatório é renderizada quando você usa o acesso de URL para renderizar um relatório. A barra de ferramentas não é renderizada por meio da API SOAP. Entretanto, a configuração de informações de dispositivo `Toolbar` afeta o modo como o relatório é exibido ao usar o método de SOAP `Render`. Se o valor desse parâmetro for `true` ao usar o SOAP para renderizar para HTML, somente a primeira seção do relatório será renderizada. Se o valor for `false`, o relatório HTML inteiro será renderizado como uma única página HTML.|  
|`UserAgent`|A cadeia de caracteres `user-agent` do navegador que faz a solicitação, a qual é encontrada na solicitação HTTP.|  
|**Zoom (\*)**|O valor de zoom do relatório como uma porcentagem de número inteiro ou uma constante de cadeia de caracteres. Os valores de cadeia de caracteres padrão incluem `Page Width` e `Whole Page`. Esse parâmetro é ignorado pelas versões do [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Explorer anteriores ao Internet Explorer 5.0 e por todos os navegadores que não são da[!INCLUDE[msCoName](../includes/msconame-md.md)] . O valor padrão desse parâmetro é `100`.|  
|**DataVisualizationFitSizing**|Indica comportamento de ajuste de visualização de dados quando dentro de um tablix. Isso inclui gráfico, medidor e mapa.<br /><br /> Os valores possíveis são **Aproximado** e **Exato**.<br /><br /> O valor padrão é **Aproximado**. Se a configuração for removida do arquivo **rsreportserver.config** , o comportamento padrão será **Exato**.<br /><br /> Habilitar **Exato** pode ter impacto de desempenho porque o processamento para determinar o tamanho exato pode levar mais tempo.|  
  
## <a name="see-also"></a>Consulte também  
 [Passando configurações de informações de dispositivos para extensões de renderização](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar parâmetros de extensão de renderização em RSReportServer.config](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referência técnica &#40;SSRS&#41;](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
