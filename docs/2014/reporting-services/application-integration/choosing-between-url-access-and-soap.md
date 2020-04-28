---
title: Escolhendo entre o acesso à URL e SOAP | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- SOAP [Reporting Services], vs. URL access
- Report Server Web service, application integration
- URL access [Reporting Services], vs. SOAP
- Web service [Reporting Services], application integration
ms.assetid: bccdc243-4366-4ce5-8e63-3dd6c463fa52
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 59e44b53baff0cd55c6a8016408fd2af685bbc26
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78173953"
---
# <a name="choosing-between-url-access-and-soap"></a>Optando entre acesso à URL e SOAP
  A integração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a aplicativos personalizados pode ser desafiadora. No entanto, o desafio não é a complexidade do modelo de programação ou das APIs, mas as muitas maneiras possíveis de integrá-los. O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] foi criado a partir do zero como uma plataforma de desenvolvedor e, portanto, é compilado tendo em mente a flexibilidade da programação. Com a flexibilidade vem a necessidade de tomar decisões importantes sobre como integrar a navegação de relatórios e a funcionalidade de gerenciamento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aos seus aplicativos comerciais existentes.

 ![Cenários de programação de Reporting Services](../../../2014/reporting-services/media/bk-ext-04.gif "Cenários de programação do Reporting Services") A programação de Reporting Services dá suporte a uma ampla gama de cenários.

 Existem dois modos de integrar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a aplicativos personalizados: acesso à URL e a API SOAP do Reporting Services. A opção utilizada dependerá de vários fatores. Em alguns casos, a integração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aos seus aplicativos comerciais personalizados exigirá que você use o acesso à URL e o SOAP. Você deve fazer as seguintes perguntas:

-   Que tipo de funcionalidade de relatório empresarial você ou os seus usuários finais exigem? Você precisa de uma maneira simples de abrir relatórios e de navegar neles ou precisa de recursos mais avançados de gerenciamento de servidor de relatório a partir da sua solução comercial personalizada?

-   Em qual tipo de ambiente os seus usuários operam normalmente? O seu aplicativo comercial é um aplicativo Web ou um aplicativo do Windows? Como que facilidade os seus usuários finais podem alternar entre um ambiente Win32 e um ambiente da Web? De que tipo de controle você precisa sobre o ambiente nos quais os relatórios serão executados e gerenciados?

 Depois de responder as perguntas anteriores, você poderá decidir como integrará o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] à sua infraestrutura de TI. Normalmente, o acesso à URL é o preferido para a exibição e navegação de relatórios individuais. O acesso à URL permite que você navegue de forma livre e rápida sem a sobrecarga do serviço Web. Além disso, o acesso à URL é, atualmente, a única técnica de programação que usa o Visualizador de HTML completo para navegação de relatórios, o que inclui a barra de ferramentas de relatório. O acesso à URL também oferece um desempenho melhor do que o SOAP porque ignora o marshalling de solicitações SOAP para e do servidor. Em cenários de integração que exigem acesso rápido e fácil a relatórios com ferramentas internas para exibição e navegação, o acesso à URL é a melhor opção.

> [!NOTE]
>  O acesso à URL do servidor de relatório dá suporte ao Visualizador de HTML e à funcionalidade estendida da barra de ferramentas de relatório. A API SOAP API não dá suporte a esse tipo de relatório renderizado. Você precisará criar e desenvolver a sua própria barra de ferramentas de relatório, se renderizar relatórios usando SOAP.

 Para obter mais informações sobre a barra de ferramentas de relatório, consulte [Visualizador de HTML e a barra de ferramentas de relatório](../html-viewer-and-the-report-toolbar.md).

 Para obter mais informações sobre o acesso à URL, consulte [acesso à url &#40;&#41;SSRS ](../url-access-ssrs.md).

 O acesso à URL é útil para a visualização de relatórios, mas não oferece a funcionalidade de gerenciamento de relatórios e de namespaces que pode ser essencial para qualquer cenário de relatórios empresarial. Nesse caso, a funcionalidade ampla e sofisticada da API SOAP do Reporting Services é recomendada. Com a API SOAP você pode gerenciar e implantar relatórios, criar agendas, configurar propriedades de servidor, gerenciar o namespace de servidor de relatório, criar assinaturas e mais. A API SOAP exibe o conjunto completo de funcionalidades de gerenciamento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. A API SOAP também pode habilitar a exibição e a navegação de relatórios por meio do método <xref:ReportExecution2005.ReportExecutionService.Render%2A> da API. No entanto, exibir relatórios por meio da API SOAP não habilita a funcionalidade de exibição interna da barra de ferramentas de relatório, nem manipula automaticamente a interatividade do relatório fornecida pelo acesso à URL.

 Para obter mais informações sobre a API SOAP do Reporting Services, consulte [Serviço Web do Servidor de Relatórios](../report-server-web-service/report-server-web-service.md).

 Na maioria dos casos, o acesso à URL e as chamadas SOAP serão necessários para que você atenda às suas necessidades de relatórios. SOAP é usado na conexão inicial ao banco de dados do servidor de relatório e na apresentação da lista de relatórios disponível em uma interface do usuário e o acesso à URL é usado para acessar os relatórios individuais e para navegar por eles.

 Para obter um exemplo de combinação do acesso de URL com o serviço Web para fornecer relatórios integrados, consulte [Amostras de produto do SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).

## <a name="see-also"></a>Consulte Também
 [Integração do Reporting Services a aplicativos](../../../2014/reporting-services/application-integration/integrating-reporting-services-into-applications.md) que [integram Reporting Services usando](../application-integration/integrating-reporting-services-using-soap.md) a integração SOAP Reporting Services usando referência técnica de [acesso à URL](../application-integration/integrating-reporting-services-using-url-access.md) [&#40;SSRS&#41;](../../../2014/reporting-services/technical-reference-ssrs.md)


