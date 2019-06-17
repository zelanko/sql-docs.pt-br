---
title: Instalar o ADO.NET Data Services para dar suporte a dados do feed exportações das listas do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: f32527ae-f623-4e08-adfb-6d3262f5c2ac
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 622d729e0b86a210bbdaaedf29818a49e81ed2ce
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66094659"
---
# <a name="install-adonet-data-services-to-support-data-feed-exports-of-sharepoint-lists"></a>Instalar o ADO.NET Data Services para dar suporte a exportações do feed de dados das listas do SharePoint
  O ADO.NET Data Services é obrigatório para uma exportação do feed de dados das listas do SharePoint. Como o SharePoint 2010 não inclui esse componente no programa SharePoint Prerequisite Installer, você deve instalá-lo manualmente.  
  
 Sem esse pré-requisito, você obterá o seguinte erro ao tentar usar uma lista do SharePoint que foi exportada como um feed de dados: "Por motivos de segurança DTD é proibido neste documento XML. Para habilitar o processamento do DTD, defina a propriedade ProhibitDtd em XmlReaderSettings como falsa e passe as configurações para o método XmlReader.Create."  
  
 Use as instruções a seguir para instalar o ADO.NET Data Services em cada SharePoint Server para o qual você deseja permitir a exportação de listas como feeds de dados.  
  
### <a name="download-and-install-adonet-data-services"></a>Baixar e instalar o ADO.NET Data Services  
  
1.  Vá para a documentação de requisitos de hardware e software para o SharePoint 2010 [requisitos de Hardware e Software (SharePoint 2010)](https://go.microsoft.com/fwlink/?LinkId=169734)  
  
2.  Na **acesso ao software aplicável**, localize o link para o ADO.NET Data Services 3.5 que corresponde ao sistema operacional que você está usando (Windows Server 2008 SP2 ou Windows Server 2008 R2).  
  
3.  Clique no link e execute o programa de instalação que instala o serviço.  
  
## <a name="see-also"></a>Consulte também  
 [Instalação do PowerPivot para SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
