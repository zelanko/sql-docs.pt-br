---
title: "Implantando uma extensão de processamento de dados | Microsoft Docs"
ms.custom: 
ms.date: 03/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- data processing extensions [Reporting Services], deploying
- Extension element
- deploying [Reporting Services], extensions
ms.assetid: e5c0b5a9-1386-47cb-aade-96653ecfaa54
caps.latest.revision: 34
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: dbf0fd628630b51b3e8847539888d46c0c8a590e
ms.contentlocale: pt-br
ms.lasthandoff: 08/12/2017

---
# <a name="deploying-a-data-processing-extension"></a>Implantando uma extensão de processamento de dados
  Depois de ter escrito e compilado sua [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] extensão de processamento de dados em um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] biblioteca, você precisa torná-lo detectável pelo servidor de relatório e pelo Designer de relatórios. Isso é tão fácil quanto copiar a extensão para os diretórios adequados e adicionar entradas aos arquivos de configuração do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] adequados.  
  
## <a name="configuration-file-extension-element"></a>Elemento de extensão do arquivo de configuração  
 Extensões de processamento de dados que você implanta no servidor de relatório ou o Designer de relatórios precisam ser inseridas como **extensão** elementos nos arquivos de configuração. Esses arquivos são o RSReportServer.config para o servidor de relatório e o RSReportDesigner.config para Designer de Relatórios.  
  
 A tabela a seguir descreve os atributos para o **extensão** elemento para extensões de processamento de dados.  
  
|Atributo|Description|  
|---------------|-----------------|  
|**Nome**|Um nome exclusivo para a extensão, por exemplo, o "SQL" para a extensão de processamento de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou "OLEDB" para a extensão de processamento de dados OLE DB. O comprimento máximo do atributo **Name** é de 255 caracteres. O nome deve ser exclusivo entre todas as entradas dento do elemento **Extension** de um arquivo de configuração.|  
|**Tipo**|Uma lista separada por vírgulas que inclui o namespace totalmente qualificado junto com o nome do assembly.|  
|**Visível**|Um valor de **false** indica que a extensão de processamento de dados não deve ser visível nas interfaces do usuário. Se o atributo não for incluído, o valor padrão será **true**.|  
  
 Para obter mais informações sobre os arquivos rsreportserver. config ou RSReportDesigner. config, consulte [arquivos de configuração do Reporting Services](../../../reporting-services/report-server/reporting-services-configuration-files.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Como: implantar uma extensão de processamento de dados para um servidor de relatório](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension-to-a-report-server.md)|Descreve como implantar sua extensão de processamento de dados em um servidor de relatório.|  
|[Como: implantar uma extensão de processamento de dados no Designer de relatórios](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension-to-report-designer.md)|Descreve como implantar sua extensão de processamento de dados em um Designer de Relatórios.|  
  
## <a name="see-also"></a>Consulte também  
 [Extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementando uma extensão de processamento de dados](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
