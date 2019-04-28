---
title: Visão geral das extensões de renderização | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- formats [Reporting Services], rendering extensions
- rendering extensions [Reporting Services], about extensions
ms.assetid: 909356a0-4709-43e5-b597-33bd9bb22882
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5386c8db5c3d240533b21311794779905039e70a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62985809"
---
# <a name="rendering-extensions-overview"></a>Visão geral das extensões de renderização
  Uma extensão de renderização é um componente ou um módulo de um servidor de relatório que transforma dados de relatório e informações de layout para um formato específico do dispositivo. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] inclui sete extensões de renderização: HTML, Excel, Word, CSV ou texto, XML, imagem e PDF. Você pode criar extensões de renderização adicionais para gerar relatórios em outros formatos.  
  
> [!NOTE]  
>  Para determinar quais extensões de renderização estão disponíveis, exiba a lista das extensões instaladas no arquivo RSReportServer.config.  
  
 A tabela a seguir descreve as extensões de renderização incluídas no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
|Nome da Extensão|Descrição|  
|--------------------|-----------------|  
|`XML`|Renderiza um relatório em XML. O relatório é aberto em um navegador. Transformações adicionais aplicadas a esta saída XML podem ser uma forma econômica de evitar o desenvolvimento de sua própria extensão de renderização.|  
|`CSV`|Renderiza um relatório em um formato delimitado por vírgula. O relatório é aberto em uma ferramenta de visualização associada a formatos de arquivo CSV.|  
|`IMAGE`|Renderiza um relatório em um formato orientado para páginas. O formato é mostrado como **TIFF** na lista suspensa Exportar da barra de ferramentas de relatório.|  
|`PDF`|Renderiza um relatório no Adobe Acrobat Reader. O formato é mostrado como **Arquivo Acrobat (PDF)** na lista suspensa Exportar da barra de ferramentas de relatório.|  
|`EXCEL`|Renderiza um relatório no [!INCLUDE[ofprexcel](../../../includes/ofprexcel-md.md)].|  
|`WORD`|Renderizar um relatório no [!INCLUDE[ofprword](../../../includes/ofprword-md.md)].|  
|`HTML 4.0` (parte da extensão de renderização HTML)|HTML é o formato usado para renderizar inicialmente o relatório. Se o seu navegador der suporte a HTML 4.0, esse será o formato usado. Caso contrário, o HTML 3.2 será usado.|  
|`MHTML` (parte da extensão de renderização HTML)|Renderiza um relatório em MHTML. O relatório é aberto no Internet Explorer. O formato é mostrado como **Arquivo Web** na lista suspensa Exportar da barra de ferramentas de relatório.|  
|`NULL`|Não renderiza um relatório para um formato específico. Essa extensão de renderização é útil para colocar relatórios em cache. A renderização nula deve ser usada em conjunto com uma execução ou entrega agendada.|  
  
 Para obter mais informações sobre os formatos recomendados e seus usos, consulte [Exportando relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../report-builder/export-reports-report-builder-and-ssrs.md).  
  
 Cada uma das extensões de renderização implementadas pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] e enviadas com o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] usa um conjunto comum de interfaces. Isso garante que cada extensão implemente funcionalidade comparável e reduz a complexidade do código de renderização no núcleo do servidor de relatório.  
  
## <a name="rendering-object-model"></a>Modelo de objeto de renderização  
 Quando um relatório é processado, o resultado é um modelo de objeto publicamente exposto conhecido como ROM (Modelo de Objeto de Renderização). O Modelo de Objeto de Renderização é uma coleção de classes que definem os conteúdos, o layout e os dados de um relatório que foi processado. O ROM está disponível para desenvolvedores que queiram criar, desenvolver e implantar extensões de renderização personalizadas para o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. O ROM é gerado quando o servidor de relatório processa a definição XML de um relatório junto com os dados de relatório definidos pelo usuário. Quando o processamento é concluído, o modelo de objeto público é usado por uma extensão de renderização para definir a saída do relatório. As classes públicas disponíveis de ROM são definidas no namespace `Microsoft.ReportingServices.OnDemandReportRendering`.  
  
## <a name="writing-custom-rendering-extensions"></a>Escrevendo extensões de renderização personalizadas  
 Antes de decidir criar uma extensão de renderização personalizada, avalie alternativas mais simples. Você pode:  
  
-   Personalizar a saída renderizada especificando configurações de informações de dispositivo para extensões existentes.  
  
-   Adicione formatação personalizada e recursos de apresentação combinando XSLT (Transformações XSL) com a saída do formato de renderização XML.  
  
 Escrever uma extensão de renderização personalizada é difícil. Normalmente, uma extensão de renderização deve dar suporte a todas as combinações possíveis de elementos de relatório e exige que você implemente centenas de classes, de interfaces, de métodos e de propriedades. Se você tiver de renderizar um relatório em um formato não incluído no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] e decidir escrever a sua própria implementação de código gerenciado de uma extensão de renderização, o código da extensão de renderização deve implementar a interface `Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension`, exigida pelo servidor de relatório.  
  
 Para obter a documentação e whitepapers suplementares sobre o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], consulte os últimos recursos técnicos no [site do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=19951).  
  
## <a name="see-also"></a>Consulte também  
 [Implementando uma extensão de renderização](implementing-a-rendering-extension.md)   
 [Biblioteca de extensões do Reporting Services](../reporting-services-extension-library.md)  
  
  
