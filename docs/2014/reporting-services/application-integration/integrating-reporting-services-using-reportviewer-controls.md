---
title: Integrando o Reporting Services usando os controles ReportViewer | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- ReportViewer controls
- integrating reports [Reporting Services]
ms.assetid: 3ba47fb4-73a9-4059-89fd-329adebe94a8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cbaa41c75297d62e84cfc808463214d19c4ff8fa
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63126250"
---
# <a name="integrating-reporting-services-using-the-reportviewer-controls"></a>Integrando o Reporting Services usando os controles ReportViewer
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)] fornece dois controles ReportViewer para integrar a funcionalidade de exibição de relatório em seus aplicativos. Existe uma versão para aplicativos baseados em Windows Forms e um para aplicativos Web Forms. Cada controle oferece funcionalidade semelhante mas cada é foi criado para ter como destino seus ambientes individuais. Ambos os controles podem processar relatórios que foram implantados em um servidor de relatório (modo de processamento remoto) ou que foram copiados para um computador em que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o não foi instalado (modo de processamento local).  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Integrando Reporting Services em aplicativos](../application-integration/integrating-reporting-services-into-applications.md)   
 [Criar relatórios do SSRS usando o Visual Studio (blog)](https://jwcooney.com/2015/01/07/ssrs-basics-set-up-visual-studio-to-write-a-new-ssrs-report/)  
  
  
