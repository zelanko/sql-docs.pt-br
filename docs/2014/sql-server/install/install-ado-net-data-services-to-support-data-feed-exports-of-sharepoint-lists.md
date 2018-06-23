---
title: Instalar o ADO.NET Data Services para dar suporte a dados exportações do feed das listas do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f32527ae-f623-4e08-adfb-6d3262f5c2ac
caps.latest.revision: 6
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: d4241d56aa3257bd0ec2cddf4b439a4939f8ab9f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010322"
---
# <a name="install-adonet-data-services-to-support-data-feed-exports-of-sharepoint-lists"></a>Instalar o ADO.NET Data Services para dar suporte a exportações do feed de dados das listas do SharePoint
  O ADO.NET Data Services é obrigatório para uma exportação do feed de dados das listas do SharePoint. Como o SharePoint 2010 não inclui esse componente no programa SharePoint Prerequisite Installer, você deve instalá-lo manualmente.  
  
 Sem esse pré-requisito, você obterá o erro a seguir ao tentar usar uma lista do SharePoint exportada como um feed de dados: "por razões de segurança, o DTD é proibido neste documento XML. Para habilitar o processamento do DTD, defina a propriedade ProhibitDtd em XmlReaderSettings como falsa e passe as configurações para o método XmlReader.Create."  
  
 Use as instruções a seguir para instalar o ADO.NET Data Services em cada SharePoint Server para o qual você deseja permitir a exportação de listas como feeds de dados.  
  
### <a name="download-and-install-adonet-data-services"></a>Baixar e instalar o ADO.NET Data Services  
  
1.  Vá para a documentação de requisitos de hardware e software para o SharePoint 2010, [requisitos de Hardware e Software (SharePoint 2010)](http://go.microsoft.com/fwlink/?LinkId=169734)  
  
2.  Em **acesso ao software aplicável**, localize o link para o ADO.NET Data Services 3.5 correspondente ao sistema operacional que você está usando (Windows Server 2008 SP2 ou Windows Server 2008 R2).  
  
3.  Clique no link e execute o programa de instalação que instala o serviço.  
  
## <a name="see-also"></a>Consulte também  
 [Instalação do PowerPivot para SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  