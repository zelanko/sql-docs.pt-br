---
title: Ativar a integração de recursos do PowerPivot para coleções de sites na administração central | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 62a27e53-446a-42d7-b5db-c009e02d4904
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c5a8e3f2930d7975f8c75c8f89ab90b78461a650
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66072005"
---
# <a name="activate-powerpivot-feature-integration-for-site-collections-in-central-administration"></a>Ativar a integração de recursos do PowerPivot para coleções de sites na Administração Central
  A ativação da integração de recursos do PowerPivot para coleções de sites específicas será necessária se você tiver usado a opção de instalação Farm Existente para instalar o SQL Server PowerPivot para SharePoint. Se você instalou o PowerPivot para SharePoint usando a opção Novo Servidor, poderá ignorar esta tarefa pois a Instalação do SQL Server já ativou a integração de recurso do PowerPivot para a coleção de sites raiz quando configurou sua implantação.  
  
 A ativação de recursos em nível de coleção de sites é necessária para tornar as páginas e os modelos disponíveis em seus sites, incluindo páginas de configuração para atualização de dados agendada e páginas de aplicativo para Galeria do PowerPivot e bibliotecas de Feed de Dados.  
  
 Você deve ativar a integração do PowerPivot para cada conjunto de sites que dê suporte ao processamento de consultas do PowerPivot.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você deve ser um administrador de conjunto de sites.  
  
## <a name="activate-powerpivot-features"></a>Ativar os recursos do PowerPivot  
  
1.  Em um site do SharePoint, clique em **Ações do Site**.  
  
     Por padrão, os aplicativos Web do SharePoint são acessados pela porta 80. Isso significa que, com frequência, você pode acessar um site do\<SharePoint digitando http://nome do computador> para abrir o conjunto de sites raiz.  
  
2.  Clique em **Configurações de Site**.  
  
3.  Em Administração do Conjunto de Sites, clique em **Recursos do conjunto de sites**.  
  
4.  Role a página até encontrar o **recurso de coleção de sites de integração do PowerPivot**.  
  
5.  Clique em **Ativar**.  
  
6.  Repita a operação em outros conjuntos de sites, abrindo cada site e clicando em **Ações do Site**.  
  
## <a name="see-also"></a>Consulte Também  
 [Administração e configuração do servidor PowerPivot na administração central](power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [PowerPivot para SharePoint de configuração inicial &#40;&#41;](../../sql-server/install/initial-configuration-powerpivot-for-sharepoint.md)   
 [Instalação do PowerPivot para SharePoint 2010](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
