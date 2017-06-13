---
title: "Itens de relatório personalizados | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- extending Reporting Services
- Reporting Services, extending
- custom report items
ms.assetid: 64dcaf2c-1af5-4937-8ff7-98f1ec3b367e
caps.latest.revision: 22
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 2396af94f8c28c41d41c52cd505d12aa8dceee17
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="custom-report-items"></a>Itens de Relatório Personalizados
  O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece um conjunto de ferramentas avançadas para a criação e publicação de relatórios corporativos, o gerenciamento de segurança e de assinaturas, e a extensão da funcionalidade de relatório por meio de uma API abrangente. Os relatórios são definidos por meio de uma linguagem baseada em XML chamada linguagem RDL. A RDL oferece um conjunto de instruções que descrevem o layout, as informações de consulta e os tipos de itens para um relatório. É possível estender a RDL escrevendo um item de relatório personalizado. O item de relatório personalizado consiste em um componente de tempo de execução, chamado pelo processador de relatório em tempo de execução, e em um componente de tempo de design, que permite que o item de relatório personalizado esteja disponível no Designer de Relatórios.  
  
 Para obter um exemplo de um item de relatório personalizado totalmente implementado, consulte [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="custom-report-item-scenarios"></a>Cenários de item de relatório personalizado  
 Os desenvolvedores que precisam integrar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a seus aplicativos podem precisar de funcionalidade que não seja nativamente suportada em RDL. Isso pode incluir itens como: controles de mapa, listas horizontais, listas colunares e matrizes de tabela dinâmica. Um item de relatório personalizado de tempo de execução pode ser desenvolvido e pode ser distribuído com um aplicativo para atender a essa necessidade.  
  
 Além de fornecer funcionalidade que não seja suportada de forma nativa, alguns desenvolvedores podem desejar estender a funcionalidade existente com versões alternativas de controles já incluídos no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Nesse cenário, um desenvolvedor poderia fornecer três componentes: um componente de tempo de execução, um componente de tempo de design e um componente de conversão de item de relatório de tempo de design que converta um item de relatório existente em um item de relatório personalizado sob demanda.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Arquitetura de Item de relatório personalizado](../../reporting-services/custom-report-items/custom-report-item-architecture.md)  
 Descreve os componentes que compõem um item de relatório personalizado.  
  
 [Requisitos de implementação de Item de relatório personalizado](../../reporting-services/custom-report-items/custom-report-item-implementation-requirements.md)  
 Descreve os pré-requisitos para a criação de um item de relatório personalizado.  
  
 [Criando um componente de tempo de execução do Item de relatório personalizado](../../reporting-services/custom-report-items/creating-a-custom-report-item-run-time-component.md)  
 Descreve como criar um componente de tempo de execução de item de relatório personalizado.  
  
 [Criando um componente de tempo de Design de Item de relatório personalizado](../../reporting-services/custom-report-items/creating-a-custom-report-item-design-time-component.md)  
 Descreve como criar um componente de tempo de design de item de relatório personalizado.  
  
 [Como: implantar um Item de relatório personalizado](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)  
 Descreve como implantar um item de relatório personalizado.  
  
 [Bibliotecas de classe de Item de relatório personalizado](../../reporting-services/custom-report-items/custom-report-item-class-libraries.md)  
 Descreve as classes de infraestrutura de item de relatório personalizado e classes wrapper gerenciadas do **reportdesigner** namespace.  
  
## <a name="see-also"></a>Consulte também  
 [Referência técnica &#40;SSRS&#41;](../../reporting-services/technical-reference-ssrs.md)  
  
  
