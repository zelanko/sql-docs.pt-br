---
title: Integrando o Reporting Services usando os controles do Visualizador de Relatórios | Microsoft Docs
ms.date: 09/18/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
helpviewer_keywords:
- Report Viewer controls
- integrating reports [Reporting Services]
ms.assetid: 3ba47fb4-73a9-4059-89fd-329adebe94a8
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8ffaeb12bc961256959571d18808e2869a1d7485
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62741869"
---
# <a name="integrating-reporting-services-using-report-viewer-controls"></a>Integrando o Reporting Services usando os controles do Visualizador de Relatórios
  O [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio 2015 fornece dois controles do Visualizador de Relatórios para integração da funcionalidade de exibição de relatório aos aplicativos. Existe uma versão para aplicativos baseados em Windows Forms e um para aplicativos Web Forms. Cada controle oferece funcionalidade semelhante mas cada é foi criado para ter como destino seus ambientes individuais. Ambos os controles podem processar relatórios que foram implantados em um servidor de relatório (modo de processamento remoto) ou que foram copiados para um computador em que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não foi instalado (modo de processamento local).  
  
 O controle do Visualizador de Relatórios não inclui suporte interno para adaptar-se de forma dinâmica a dispositivos diferentes com diferentes resoluções de tela.  
  
## <a name="remote-processing-mode"></a>Modo de processamento remoto  
 O modo de processamento remoto é o método preferido para exibir relatórios implantados em um servidor de relatório. O modo de processamento remoto oferece as seguintes vantagens:  
  
-   O processamento remoto fornece uma solução otimizada para a execução de relatórios porque o relatório é processado pelo servidor de relatório.  
  
-   Como todo o processamento é manipulado pelo servidor de relatório, uma solicitação de relatório pode ser processada por vários servidores de relatório em uma implantação em expansão ou por um servidor com vários processadores em um cenário de aumento de escala.  
  
 Além disso, o relatório executado em modo remoto pode utilizar a funcionalidade completa do servidor de relatório, incluindo toda a renderização e extensões de dados.  
  
> [!NOTE]  
>  A lista de extensões disponíveis para o controle do Visualizador de Relatórios, quando ele estiver sendo executado no modo de processamento remoto, dependerá da edição do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalada no servidor de relatório.  
  
## <a name="local-processing-mode"></a>Modo de processamento local  
 O modo de processamento local oferece um método alternativo para a exibição e para a renderização de relatórios quando o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não estiver instalado. Ao contrário do processamento remoto, somente um subconjunto da funcionalidade fornecida pelo servidor de relatório estará disponível no controle. No modo de processamento local, o processamento de dados não é realizado pelo controle, mas implementado pelo aplicativo host. Entretanto, o processamento de relatórios é tratado pelo próprio controle. No modo de processamento local, somente as extensões de renderização PDF, Excel, Word e Imagem estarão disponíveis.  
  
## <a name="see-also"></a>Consulte Também  
 [Integrando o Reporting Services em aplicativos](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)   
 [Usando o controle WebForms do Visualizador de Relatórios](../../reporting-services/application-integration/using-the-webforms-reportviewer-control.md)   
 [Usando o controle WinForms do Visualizador de Relatórios](../../reporting-services/application-integration/using-the-winforms-reportviewer-control.md)  

  
  
