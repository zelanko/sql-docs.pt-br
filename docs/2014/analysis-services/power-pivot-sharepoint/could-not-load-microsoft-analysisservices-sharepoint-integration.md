---
title: Não foi possível carregar o arquivo ou assembly &#39;Microsoft. Data. Services, versão = 3.5.0.0, Culture = neutral, PublicKeyToken = b77a5c561934e089&#39; ou uma de suas dependências. O sistema não pode encontrar o arquivo especificado. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 81ed0f44-8782-462d-af8f-0ba5b975df27
author: minewiskan
ms.author: owend
ms.openlocfilehash: 9bcfdde8b3536bbbf8b2429d51a9ee9aecf0d437
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547498"
---
# <a name="could-not-load-file-or-assembly-39microsoftdataservices-version3500-cultureneutral-publickeytokenb77a5c561934e08939-or-one-of-its-dependencies-the-system-cannot-find-the-file-specified"></a>Não foi possível carregar o arquivo ou assembly &#39;Microsoft. Data. Services, versão = 3.5.0.0, Culture = neutral, PublicKeyToken = b77a5c561934e089&#39; ou uma de suas dependências. O sistema não pode encontrar o arquivo especificado.
  Em ambientes do SharePoint 2010 com o PowerPivot para SharePoint, este erro ocorrerá se você tentar fazer uma exportação de feed de dados e o sistema não contiver a versão necessária do Microsoft ADO.NET Data Services.  
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Aplica-se a|PowerPivot para SharePoint|  
|Versão do produto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|O ADO.NET Data Services 3.5 SP1 não foi localizado.|  
|Texto da mensagem|Não foi possível carregar o arquivo ou assembly 'Microsoft.Data.Services, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089' ou uma de suas dependências. O sistema não pôde localizar o arquivo especificado|  
  
## <a name="explanation"></a>Explicação  
 O SharePoint 2010 inclui um botão Exportar como Feed de Dados que pode ser usado para exportar uma lista do SharePoint como um feed de dados XML. Além disso, o Reporting Services no modo do SharePoint e o PowerPivot para SharePoint oferecem suporte aos recursos de feed de dados que exigem o ADO.NET Data Services.  
  
 Se o ADO.NET Data Services não estiver instalado, esse erro ocorrerá quando você solicitar um feed de dados.  
  
## <a name="user-action"></a>Ação do usuário  
  
1.  Acesse a documentação de requisitos de hardware e software para o SharePoint 2010, para [determinar os requisitos de hardware e software (SharePoint 2010)](https://go.microsoft.com/fwlink/?LinkId=169734) ( https://go.microsoft.com/fwlink/?LinkId=169734) .  
  
2.  Em **Instalando pré-requisitos de software**, localize o link para o ADO.NET Data Services 3.5 que corresponde ao sistema operacional você está usando.  
  
3.  Clique no link e execute o programa de instalação que instala o serviço.  
  
## <a name="see-also"></a>Consulte Também  
 [Implantar soluções PowerPivot para SharePoint](deploy-power-pivot-solutions-to-sharepoint.md)  
  
  
