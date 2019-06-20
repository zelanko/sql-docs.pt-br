---
title: Configurações de informações de dispositivo XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- XML [Reporting Services], rendering
- device information settings [Reporting Services], PDF rendering
ms.assetid: a32e83fe-c10e-4ebd-8975-5be7dcc422e7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e642034d445e52485874c71df110bff81b9c1aaf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66096941"
---
# <a name="xml-device-information-settings"></a>Configurações de informações do dispositivo XML
  A tabela a seguir lista as configurações de informações de dispositivo para renderização no formato XML.  
  
|Configuração|Valor|  
|-------------|-----------|  
|`XSLT`|O caminho no namespace do servidor de relatório de um XSLT a ser aplicado ao arquivo XML, por exemplo, `/Transforms/myxslt`. O arquivo xsl deve ser um recurso publicado no servidor de relatório e você deve acessá-lo por meio de um caminho de item do servidor de relatório. O valor dessa configuração é aplicado depois de qualquer XSLT especificado no relatório. Se a configuração `XSLT` for aplicada, a configuração `OmitSchema`será ignorada.|  
|**MIMEType**|O tipo MIME (Multipurpose Internet Mail Extensions) do arquivo XML.|  
|**UseFormattedValues**|Indica se será preciso renderizar o valor formatado de uma caixa de texto durante a geração dos dados XML. Um valor falso indica que o valor subjacente da caixa de texto será usado.|  
|**Indented**|Indica se será preciso gerar XML recuado. O valor padrão `false` gera XML não recuado e compactado.|  
|`OmitNamespace`|Indica se será preciso omitir o namespace padrão do XML.<br /><br /> Se true, o XML não especifica um namespace padrão.<br /><br /> Se false, o XML especifica um namespace padrão com o valor da propriedade DataSchema do relatório. A propriedade DataSchema usa como padrão o nome do relatório.<br /><br /> O valor padrão é `false`.|  
|`OmitSchema`|Indica se será preciso omitir o local de esquema do XML. O local é o atributo SchemaLocation. O valor padrão de OmitSchema depende do valor de OmitNamespace:<br /><br /> Se OmitNamespace = False, OmitSchema = `False` por padrão. O usuário pode substituir o padrão definindo OmitSchema = True.<br /><br /> Se OmitNamespace = True, OmitSchema funcionará como `True`, independentemente do valor explicitamente configurado para OmitShema.|  
|**Codificação**|O nome da IANA (Internet Assigned Numbers Authority) de uma codificação de caracteres com suporte do .NET Framework. O valor padrão é `UTF-8`. Exemplos de outros valores incluem ASCII, UTF-7 e UTF-16.|  
|**FileExtension**|A extensão de arquivo a ser usada para o arquivo gerado.|  
|**Esquema**|Indica se será preciso renderizar o XSD (XML schema definition) ou se os dados XML reais serão renderizados. Um valor `true` indica que um esquema XML será renderizado. O valor padrão é `false`.|  
  
## <a name="see-also"></a>Consulte também  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Passando configurações de informações de dispositivos para extensões de renderização](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar parâmetros de extensão de renderização em RSReportServer.config](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referência técnica &#40;SSRS&#41;](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
