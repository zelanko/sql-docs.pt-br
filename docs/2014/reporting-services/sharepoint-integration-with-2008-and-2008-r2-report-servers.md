---
title: Integração do SharePoint com o 2008 e 2008 R2 Report Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: d9f51c37-b071-45d0-baec-f82fa6db366f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d29d41069d5daca25d53477326e864720aa87ca1
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66101201"
---
# <a name="sharepoint-integration-with-2008-and-2008-r2--report-servers"></a>Integração do SharePoint com o 2008 Report Server e o 2008 R2 Report Server
  A versão [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] incorporou uma arquitetura na qual o modo do SharePoint baseia-se no serviço compartilhado SharePoint. Gerenciamento da nova funcionalidade está concluído na Administração Central do SharePoint na **Manage Services** e **os aplicativos de serviço do Gerenciador de** páginas. O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ainda há suporte para a arquitetura anterior para integração do SharePoint com o [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] suplemento para produtos do SharePoint 2010 para que você pode integrar o SharePoint 2010 com versões anteriores de um servidor de relatório.  
  
 As páginas da Administração Central do SharePoint que você usará para administrar a arquitetura mais antiga podem ser encontradas no seguinte local:  
  
1.  Na Administração Central do SharePoint, clique em **configurações gerais do aplicativo**.  
  
2.  O grupo **SQL-Server Reporting Services (2008 e 2008 R2)** contém os links e páginas de gerenciamento para a arquitetura mais antiga  
  
## <a name="server-integration-architecture"></a>Arquitetura de integração de servidor  
 Ao integrar um servidor de relatório junto com uma instância de um produto do SharePoint, itens e propriedades são armazenados nos bancos de dados de conteúdo do SharePoint. Isso fornece um nível de integração maior entre as tecnologias de servidor que afetam o armazenamento, a proteção e o acesso do conteúdo.  
  
 O armazenamento de itens e propriedades de relatório nos bancos de dados de conteúdo do SharePoint permite procurar tipos de conteúdo de servidor de relatório nas bibliotecas do SharePoint, proteger itens usando os mesmos níveis de permissão e o mesmo provedor de autenticação que controla o acesso a outros documentos empresariais hospedados em um site do SharePoint, usar os recursos de colaboração e gerenciamento de documentos para aprovar ou não modificações em relatórios, usar alertas para descobrir se um item foi alterado e inserir ou personalizar a parte da Web do Report Viewer em páginas e sites dentro do aplicativo. Se você tiver permissões suficientes em um site do SharePoint, também poderá gerar modelos de relatório a partir de fontes de dados compartilhadas e usar o Construtor de Relatórios para criar relatórios.  
  
 O servidor de relatório continua fornecendo todo o processamento de dados, a renderização e a entrega. Também dá suporte a todo o processamento de relatório agendado para instantâneos e histórico de relatório. Quando você abre um relatório de um site do SharePoint, o ponto de extremidade do Report Server conecta-se a um servidor de relatório, cria uma sessão, prepara o relatório para processamento, recupera dados, mescla o relatório no layout de relatório e o exibe na parte da Web do Report Viewer. Enquanto o relatório estiver aberto, você poderá exportá-lo para diferentes formatos de aplicativos, bem como interagir com dados analisando a entrada de números subjacentes ou clicando em um relatório relacionado. As operações de exportação e interação de relatórios são executadas no servidor de relatório.  
  
 O servidor de relatório sincroniza operações e dados com o SharePoint e rastreia informações sobre os arquivos processados. Quando você modifica propriedades e configurações de qualquer item de servidor de relatório, a alteração é armazenada em um banco de dados do SharePoint e, em seguida, copiada para um banco de dados do servidor de relatório que fornece armazenamento interno para um servidor de relatório.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Ativar o servidor de relatório e os recursos de integração do Power View no SharePoint](activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)  
 Descreve como ativar o recurso Servidor de Relatório necessário para integração com servidores de relatório de versões anteriores.  
  
  
