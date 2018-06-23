---
title: Exportando para um arquivo de imagem (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 020d8ea2-de07-4212-a2bb-2ed0df2c8db8
caps.latest.revision: 10
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: e89c4b2b2026be6e90d02f38453f6e7ddd367226
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008358"
---
# <a name="exporting-to-an-image-file-report-builder-and-ssrs"></a>Exportando para um arquivo de imagem (Construtor de Relatórios e SSRS)
  A extensão de renderização da Imagem renderiza um relatório para um bitmap ou metarquivo. Por padrão, a extensão de renderização da Imagem produz um arquivo TIFF do relatório, que pode ser exibido em várias páginas. Quando o cliente receber a imagem, ela pode ser exibida em um visualizador de imagem e impressa. Este tópico fornece as informações específicas do processador de Imagem e descreve as exceções às regras de renderização.  
  
 A extensão de renderização de Imagem pode gerar arquivos em qualquer um dos formatos que tenham o suporte do [!INCLUDE[ndptecgdiplus](../../includes/ndptecgdiplus-md.md)]: BMP, EMF, EMFPlus, GIF, JPEG, PNG e TIFF. Para o formato TIFF, o nome de arquivo do fluxo primário é *NomedoRelatório*.tif. Para todos os outros formatos, que renderizam como uma página única por arquivo, o nome do arquivo é *ReportName_Page.ext* . *ext* é a extensão do arquivo para o formato selecionado. Para gerar um arquivo em outro formato com suporte da Imagem, especifique qualquer uma das cadeias de caracteres listadas anteriormente na configuração **OutputFormatDeviceInfo** .  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="SupportedImageFormats"></a> Formatos de imagem com suporte  
 A tabela a seguir mostra a extensão de arquivo e MimeType para cada formato do processador de Imagem.  
  
|**Tipo**|**Extensão**|**MIMEType**|  
|--------------|-------------------|------------------|  
|BMP|BMP|image/bmp|  
|GIF|GIF|image/gif|  
|JPEG|jpeg|image/jpeg|  
|PNG|png|image/png|  
|TIFF|tif|imagem/tiff|  
|EMF|EMF|imagem/emf|  
|EMFPlus|EMF|imagem/emf|  
  
  
##  <a name="RenderingMultiplePages"></a> Renderizando várias páginas  
 TIFF é o único formato que dá suporte a documentos de várias páginas em um único arquivo. Os demais formatos, como JPG ou PNG, emitem uma página por vez e requerem uma chamada separada para a extensão de renderização de cada página.  
  
  
##  <a name="Interactivity"></a> Interatividade  
 A interatividade não tem suporte em formatos de Imagem gerados por esse renderizador. Os elementos interativos a seguir não são renderizados:  
  
-   Hiperlinks  
  
-   Mostrar ou ocultar  
  
-   Mapa do documento  
  
-   Links de detalhamento ou de clique  
  
-   Classificação de usuário final  
  
-   Cabeçalhos fixos  
  
-   Indicadores  
  
  
##  <a name="DeviceInfo"></a> Configurações de informações de dispositivo  
 Você pode alterar algumas configurações padrão desse renderizador alterando as configurações de informações de dispositivo. Para obter mais informações, consulte [Image Device Information Settings](../image-device-information-settings.md).  
  
  
## <a name="see-also"></a>Consulte também  
 [Paginação no Reporting Services &#40;Construtor de Relatórios e SSRS&#41;](../report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Comportamentos de renderização &#40;Construtor de Relatórios e SSRS&#41;](../report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [Funcionalidade interativa para extensões de renderização de relatório diferentes &#40;SSRS e construtor de relatórios&#41;](interactive-functionality-different-report-rendering-extensions.md)   
 [Renderizando itens de relatório &#40;Construtor de Relatórios e SSRS&#41;](../report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
  
  