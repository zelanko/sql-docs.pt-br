---
title: Escolhendo entre o acesso de URL e SOAP no Reporting Services | Microsoft Docs
ms.custom: 
ms.date: 10/19/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 1d9b4df388cd1d6bb96d88b64bf319f5fd9866e9
ms.contentlocale: pt-br
ms.lasthandoff: 10/20/2017

---
# <a name="choosing-between-url-access-and-soap-in-reporting-services"></a>Escolhendo entre o acesso de URL e SOAP no Reporting Services

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

A integração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a aplicativos personalizados pode ser desafiadora. No entanto, o desafio não é a complexidade do modelo de programação ou das APIs, mas as muitas maneiras possíveis de integrá-los. O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] foi criado a partir do zero como uma plataforma de desenvolvedor e, portanto, é compilado tendo em mente a flexibilidade da programação. Com a flexibilidade vem a necessidade de tomar decisões importantes sobre como integrar a navegação de relatórios e a funcionalidade de gerenciamento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aos seus aplicativos comerciais existentes.

> [!NOTE]
> Começando com o Reporting Services do SQL Server de 2017, acesso à API REST está disponível para o desenvolvimento de soluções. Acesso de SOAP API foi preterido. Para obter mais informações, consulte [desenvolver com as APIs REST para o Reporting Services](../developer/rest-api.md).
  
 Existem dois modos de integrar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a aplicativos personalizados: acesso à URL e a API SOAP do Reporting Services. A opção utilizada dependerá de vários fatores. Em alguns casos, integrando [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em sua empresa personalizada aplicativos requer o uso de acesso à URL e SOAP. Você deve fazer as seguintes perguntas:  
  
-   Que tipo de funcionalidade de relatório empresarial você ou os seus usuários finais exigem? Você precisa de uma maneira simples de abrir relatórios e de navegar neles ou precisa de recursos mais avançados de gerenciamento de servidor de relatório a partir da sua solução comercial personalizada?  
  
-   Em qual tipo de ambiente os seus usuários operam normalmente? O seu aplicativo comercial é um aplicativo Web ou um aplicativo do Windows? Como é fácil seus usuários finais alternar de um ambiente Win32 para um ambiente da Web? De que tipo de controle você precisa sobre o ambiente nos quais os relatórios serão executados e gerenciados?  
  
 Depois de responder as perguntas anteriores, você poderá decidir como integrará o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] à sua infraestrutura de TI. Normalmente, o acesso à URL é o preferido para a exibição e navegação de relatórios individuais. O acesso à URL permite que você navegue de forma livre e rápida sem a sobrecarga do serviço Web. Além disso, o acesso à URL é, atualmente, a única técnica de programação que usa o Visualizador de HTML completo para navegação de relatórios, o que inclui a barra de ferramentas de relatório. O acesso à URL também oferece um desempenho melhor do que o SOAP porque ignora o marshalling de solicitações SOAP para e do servidor. Em cenários de integração que exigem acesso rápido e fácil a relatórios com ferramentas internas para exibição e navegação, o acesso à URL é a melhor opção.  
  
> [!NOTE]  
> O acesso à URL do servidor de relatório dá suporte ao Visualizador de HTML e à funcionalidade estendida da barra de ferramentas de relatório. A API SOAP API não dá suporte a esse tipo de relatório renderizado. Se você renderizar relatórios usando a API SOAP, projetar e desenvolver suas próprias ferramentas de relatório.
  
 Para obter mais informações sobre a barra de ferramentas de relatório, consulte [Visualizador de HTML e a barra de ferramentas relatório](../../reporting-services/html-viewer-and-the-report-toolbar.md).  
  
 Para obter mais informações sobre o acesso de URL, consulte [acesso à URL](../../reporting-services/url-access-ssrs.md).  
  
 O acesso à URL é útil para a visualização de relatórios, mas não oferece a funcionalidade de gerenciamento de relatórios e de namespaces que pode ser essencial para qualquer cenário de relatórios empresarial. Nesse caso, a funcionalidade ampla e sofisticada da API SOAP do Reporting Services é recomendada. Com a API SOAP você pode gerenciar e implantar relatórios, criar agendas, configurar propriedades de servidor, gerenciar o namespace de servidor de relatório, criar assinaturas e mais. A API SOAP exibe o conjunto completo de funcionalidades de gerenciamento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. A API SOAP também pode habilitar a exibição e a navegação de relatórios por meio do método <xref:ReportExecution2005.ReportExecutionService.Render%2A> da API. No entanto, exibir relatórios por meio da API SOAP não habilita a funcionalidade de exibição interna da barra de ferramentas de relatório, nem faz que ele controla automaticamente a interatividade do relatório que fornece acesso à URL.  
  
 Para obter mais informações sobre a API de SOAP do Reporting Services, consulte [Report Server Web Service](../../reporting-services/report-server-web-service/report-server-web-service.md).  
  
 Na maioria dos casos, o acesso à URL e as chamadas SOAP serão necessários para que você atenda às suas necessidades de relatórios. SOAP é usado na conexão inicial ao banco de dados do servidor de relatório e na apresentação da lista de relatórios disponível em uma interface do usuário e o acesso à URL é usado para acessar os relatórios individuais e para navegar por eles.  
  
 Para obter um exemplo da combinação de acesso à URL e o serviço da Web para fornecer relatórios integrados, consulte [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889).

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
