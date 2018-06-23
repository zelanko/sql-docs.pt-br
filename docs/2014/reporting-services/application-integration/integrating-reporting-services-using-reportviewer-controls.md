---
title: Integrando o Reporting Services usando os controles ReportViewer | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ReportViewer controls
- integrating reports [Reporting Services]
ms.assetid: 3ba47fb4-73a9-4059-89fd-329adebe94a8
caps.latest.revision: 23
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 44ed354ea56f58e08e512fa91fd9a0d7064b7b43
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119842"
---
# <a name="integrating-reporting-services-using-the-reportviewer-controls"></a>Integrando o Reporting Services usando os controles ReportViewer
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)] fornece dois controles ReportViewer para integração da funcionalidade em seus aplicativos de exibição de relatório. Existe uma versão para aplicativos baseados em Windows Forms e um para aplicativos Web Forms. Cada controle oferece funcionalidade semelhante mas cada é foi criado para ter como destino seus ambientes individuais. Ambos os controles podem processar relatórios que foram implantados em um servidor de relatório (modo de processamento remoto) ou que foram copiados para um computador em que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não foi instalado (modo de processamento local).  
  
 O controle ReportViewer não inclui suporte interno para adaptar-se de forma dinâmica a dispositivos diferentes com diferentes resoluções de tela.  
  
## <a name="remote-processing-mode"></a>Modo de processamento remoto  
 O modo de processamento remoto é o método preferido para exibir relatórios implantados em um servidor de relatório. O modo de processamento remoto oferece as seguintes vantagens:  
  
-   O processamento remoto fornece uma solução otimizada para a execução de relatórios porque o relatório é processado pelo servidor de relatório.  
  
-   Como todo o processamento é manipulado pelo servidor de relatório, uma solicitação de relatório pode ser processada por vários servidores de relatório em uma implantação em expansão ou por um servidor com vários processadores em um cenário de aumento de escala.  
  
 Além disso, o relatório executado em modo remoto pode utilizar a funcionalidade completa do servidor de relatório, incluindo toda a renderização e extensões de dados.  
  
> [!NOTE]  
>  A lista de extensões disponíveis para o controle ReportViewer quando ele estiver sendo executado no modo de processamento remoto dependerá da edição do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalada no servidor de relatório.  
  
## <a name="local-processing-mode"></a>Modo de processamento local  
 O modo de processamento local oferece um método alternativo para a exibição e para a renderização de relatórios quando o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não estiver instalado. Ao contrário do processamento remoto, somente um subconjunto da funcionalidade fornecida pelo servidor de relatório estará disponível no controle. No modo de processamento local, o processamento de dados não é realizado pelo controle, mas implementado pelo aplicativo host. Entretanto, o processamento de relatórios é tratado pelo próprio controle. No modo de processamento local, somente as extensões de renderização PDF, Excel, Word e Imagem estarão disponíveis.  
  
## <a name="see-also"></a>Consulte também  
 [Integrando o Reporting Services em aplicativos](../application-integration/integrating-reporting-services-into-applications.md)   
 [Criar relatórios do SSRS usando o Visual Studio (resposta da curadoria)](http://go.microsoft.com/fwlink/?LinkId=321991)  
  
  