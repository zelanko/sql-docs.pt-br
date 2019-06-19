---
title: Implantando uma extensão de processamento de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- data processing extensions [Reporting Services], deploying
- Extension element
- deploying [Reporting Services], extensions
ms.assetid: e5c0b5a9-1386-47cb-aade-96653ecfaa54
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d4741c822dab24026d823a0e08571ac6aacea9ce
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63165174"
---
# <a name="deploying-a-data-processing-extension"></a>Implantando uma extensão de processamento de dados
  Depois de gravar e compilar a extensão de processamento de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] em uma biblioteca do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], você precisa torná-la detectável pelo servidor de relatório e pelo Designer de Relatórios. Isso é tão fácil quanto copiar a extensão para os diretórios adequados e adicionar entradas aos arquivos de configuração do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] adequados.  
  
## <a name="configuration-file-extension-element"></a>Elemento de extensão do arquivo de configuração  
 As extensões de processamento de dados implantadas no servidor de relatório ou no Designer de Relatórios devem ser inseridas como elementos **Extension** nos arquivos de configuração. Esses arquivos são o RSReportServer.config para o servidor de relatório e o RSReportDesigner.config para Designer de Relatórios.  
  
 A tabela a seguir descreve os atributos do elemento **Extension** das extensões de processamento de dados.  
  
|attribute|Descrição|  
|---------------|-----------------|  
|`Name`|Um nome exclusivo para a extensão, por exemplo, o "SQL" para a extensão de processamento de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou "OLEDB" para a extensão de processamento de dados OLE DB. O comprimento máximo do atributo `Name` é de 255 caracteres. O nome deve ser exclusivo entre todas as entradas dento do elemento **Extension** de um arquivo de configuração.|  
|`Type`|Uma lista separada por vírgulas que inclui o namespace totalmente qualificado junto com o nome do assembly.|  
|`Visible`|Um valor `false` indica que a extensão de processamento de dados não deve ser visível nas interfaces do usuário. Se o atributo não for incluído, o valor padrão será `true`.|  
  
 Para obter mais informações sobre os arquivos RSReportServer.config ou RSReportDesigner.config, consulte [Arquivos de configuração do Reporting Services](../../report-server/reporting-services-configuration-files.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Como: Implantar uma extensão de processamento de dados para um servidor de relatório](deploying-a-data-processing-extension-to-a-report-server.md)|Descreve como implantar sua extensão de processamento de dados em um servidor de relatório.|  
|[Como: Implantar uma extensão de processamento de dados no Designer de relatórios](deploying-a-data-processing-extension-to-report-designer.md)|Descreve como implantar sua extensão de processamento de dados em um Designer de Relatórios.|  
  
## <a name="see-also"></a>Consulte também  
 [Extensões do Reporting Services](../reporting-services-extensions.md)   
 [Implementando uma extensão de processamento de dados](implementing-a-data-processing-extension.md)   
 [Biblioteca de extensões do Reporting Services](../reporting-services-extension-library.md)  
  
  
