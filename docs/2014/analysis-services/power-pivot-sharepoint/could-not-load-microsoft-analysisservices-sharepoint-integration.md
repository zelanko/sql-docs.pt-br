---
title: Não foi possível carregar arquivo ou assembly &#39;Microsoft.Data.Services, Version = 3.5.0.0, Culture = neutral, PublicKeyToken = b77a5c561934e089&#39; ou uma de suas dependências. O sistema não pôde localizar o arquivo especificado. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 81ed0f44-8782-462d-af8f-0ba5b975df27
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 49e2ce59b8662a8deaf47099c967355150dca201
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62749584"
---
# <a name="could-not-load-file-or-assembly-39microsoftdataservices-version3500-cultureneutral-publickeytokenb77a5c561934e08939-or-one-of-its-dependencies-the-system-cannot-find-the-file-specified"></a>Não foi possível carregar arquivo ou assembly &#39;Microsoft.Data.Services, Version = 3.5.0.0, Culture = neutral, PublicKeyToken = b77a5c561934e089&#39; ou uma de suas dependências. O sistema não pôde localizar o arquivo especificado.
  Em ambientes do SharePoint 2010 com o PowerPivot para SharePoint, este erro ocorrerá se você tentar fazer uma exportação de feed de dados e o sistema não contiver a versão necessária do Microsoft ADO.NET Data Services.  
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Aplica-se a|PowerPivot para SharePoint|  
|Versão do Produto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|O ADO.NET Data Services 3.5 SP1 não foi localizado.|  
|Texto da mensagem|Não foi possível carregar o arquivo ou assembly 'Microsoft.Data.Services, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089' ou uma de suas dependências. O sistema não pôde localizar o arquivo especificado|  
  
## <a name="explanation"></a>Explicação  
 O SharePoint 2010 inclui um botão Exportar como Feed de Dados que pode ser usado para exportar uma lista do SharePoint como um feed de dados XML. Além disso, o Reporting Services no modo do SharePoint e o PowerPivot para SharePoint oferecem suporte aos recursos de feed de dados que exigem o ADO.NET Data Services.  
  
 Se o ADO.NET Data Services não estiver instalado, esse erro ocorrerá quando você solicitar um feed de dados.  
  
## <a name="user-action"></a>Ação do usuário  
  
1.  Vá para a documentação de requisitos de hardware e software para o SharePoint 2010 [determinar requisitos de Hardware e Software (SharePoint 2010)](https://go.microsoft.com/fwlink/?LinkId=169734) (https://go.microsoft.com/fwlink/?LinkId=169734).  
  
2.  Em **Instalando pré-requisitos de software**, localize o link para o ADO.NET Data Services 3.5 que corresponde ao sistema operacional você está usando.  
  
3.  Clique no link e execute o programa de instalação que instala o serviço.  
  
## <a name="see-also"></a>Consulte também  
 [Implantar soluções do PowerPivot para SharePoint](deploy-power-pivot-solutions-to-sharepoint.md)  
  
  
