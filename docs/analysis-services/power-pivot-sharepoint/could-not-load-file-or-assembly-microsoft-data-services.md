---
title: Não foi possível carregar arquivo ou assembly serviços de dados Microsoft | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9472fffb790d8d18ced8d2a528011927717aabc6
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="could-not-load-file-or-assembly-microsoft-data-services"></a>Não foi possível carregar arquivo ou assembly serviços de dados Microsoft
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Em ambientes do SharePoint 2010 com o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, este erro ocorrerá se você tentar fazer uma exportação de feed de dados e o sistema não contiver a versão necessária do Microsoft ADO.NET Data Services.  
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Aplica-se a|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint|  
|Versão do Produto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|O ADO.NET Data Services 3.5 SP1 não foi localizado.|  
|Texto da mensagem|Não foi possível carregar o arquivo ou assembly 'Microsoft.Data.Services, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089' ou uma de suas dependências. O sistema não pôde localizar o arquivo especificado|  
  
## <a name="explanation"></a>Explicação  
 O SharePoint 2010 inclui um botão Exportar como Feed de Dados que pode ser usado para exportar uma lista do SharePoint como um feed de dados XML. Além disso, o Reporting Services no modo do SharePoint e o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint dão suporte aos recursos de feed de dados que exigem o ADO.NET Data Services.  
  
 Se o ADO.NET Data Services não estiver instalado, esse erro ocorrerá quando você solicitar um feed de dados.  
  
## <a name="user-action"></a>Ação do usuário  
  
1.  Vá para a documentação de requisitos de hardware e software para o SharePoint 2010, [determinar requisitos de Hardware e Software (SharePoint 2010)](http://go.microsoft.com/fwlink/?LinkId=169734) (http://go.microsoft.com/fwlink/?LinkId=169734).  
  
2.  Em **Instalando pré-requisitos de software**, localize o link para o ADO.NET Data Services 3.5 que corresponde ao sistema operacional você está usando.  
  
3.  Clique no link e execute o programa de instalação que instala o serviço.  
  
## <a name="see-also"></a>Consulte também  
 [Implantar soluções Power Pivot para SharePoint](../../analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint.md)  
  
  
