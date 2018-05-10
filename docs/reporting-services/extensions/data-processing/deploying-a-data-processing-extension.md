---
title: Implantando uma extensão de processamento de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/18/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: extensions
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- data processing extensions [Reporting Services], deploying
- Extension element
- deploying [Reporting Services], extensions
ms.assetid: e5c0b5a9-1386-47cb-aade-96653ecfaa54
caps.latest.revision: 34
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: bd41f79d89e1514736b3453a4f6f038488b1200f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="deploying-a-data-processing-extension"></a>Implantando uma extensão de processamento de dados
  Depois de gravar e compilar a extensão de processamento de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] em uma biblioteca do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], você precisa torná-la detectável pelo servidor de relatório e pelo Designer de Relatórios. Isso é tão fácil quanto copiar a extensão para os diretórios adequados e adicionar entradas aos arquivos de configuração do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] adequados.  
  
## <a name="configuration-file-extension-element"></a>Elemento de extensão do arquivo de configuração  
 As extensões de processamento de dados implantadas no servidor de relatório ou no Designer de Relatórios devem ser inseridas como elementos **Extension** nos arquivos de configuração. Esses arquivos são o RSReportServer.config para o servidor de relatório e o RSReportDesigner.config para Designer de Relatórios.  
  
 A tabela a seguir descreve os atributos do elemento **Extension** das extensões de processamento de dados.  
  
|attribute|Description|  
|---------------|-----------------|  
|**Nome**|Um nome exclusivo para a extensão, por exemplo, o "SQL" para a extensão de processamento de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou "OLEDB" para a extensão de processamento de dados OLE DB. O comprimento máximo do atributo **Name** é de 255 caracteres. O nome deve ser exclusivo entre todas as entradas dento do elemento **Extension** de um arquivo de configuração.|  
|**Tipo**|Uma lista separada por vírgulas que inclui o namespace totalmente qualificado junto com o nome do assembly.|  
|**Visível**|Um valor igual a **false** indica que a extensão de processamento de dados não deve ser visível nas interfaces do usuário. Se o atributo não for incluído, o valor padrão será **true**.|  
  
 Para obter mais informações sobre os arquivos RSReportServer.config ou RSReportDesigner.config, consulte [Arquivos de configuração do Reporting Services](../../../reporting-services/report-server/reporting-services-configuration-files.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Como implantar uma extensão de processamento de dados para um Servidor de Relatório](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension-to-a-report-server.md)|Descreve como implantar sua extensão de processamento de dados em um servidor de relatório.|  
|[Como implantar uma extensão de processamento de dados para o Designer de Relatórios](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension-to-report-designer.md)|Descreve como implantar sua extensão de processamento de dados em um Designer de Relatórios.|  
  
## <a name="see-also"></a>Consulte Também  
 [Extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementando uma extensão de processamento de dados](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
