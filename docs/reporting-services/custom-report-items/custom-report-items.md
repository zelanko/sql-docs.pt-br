---
title: "Itens de relatório personalizados | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: custom-report-items
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- extending Reporting Services
- Reporting Services, extending
- custom report items
ms.assetid: 64dcaf2c-1af5-4937-8ff7-98f1ec3b367e
caps.latest.revision: "22"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 224b29e8df95d5ec83f385e62edf872a9a0a4341
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="custom-report-items"></a>Itens de Relatório Personalizados
  O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece um conjunto de ferramentas avançadas para a criação e publicação de relatórios corporativos, o gerenciamento de segurança e de assinaturas, e a extensão da funcionalidade de relatório por meio de uma API abrangente. Os relatórios são definidos por meio de uma linguagem baseada em XML chamada linguagem RDL. A RDL oferece um conjunto de instruções que descrevem o layout, as informações de consulta e os tipos de itens para um relatório. É possível estender a RDL escrevendo um item de relatório personalizado. O item de relatório personalizado consiste em um componente de tempo de execução, chamado pelo processador de relatório em tempo de execução, e em um componente de tempo de design, que permite que o item de relatório personalizado esteja disponível no Designer de Relatórios.  
  
 Para obter uma amostra de um item de relatório personalizado totalmente implementado, consulte [Amostras de produto do SQL Server Reporting Services](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="custom-report-item-scenarios"></a>Cenários de item de relatório personalizado  
 Os desenvolvedores que precisam integrar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a seus aplicativos podem precisar de funcionalidade que não seja nativamente suportada em RDL. Isso pode incluir itens como: controles de mapa, listas horizontais, listas colunares e matrizes de tabela dinâmica. Um item de relatório personalizado de tempo de execução pode ser desenvolvido e pode ser distribuído com um aplicativo para atender a essa necessidade.  
  
 Além de fornecer funcionalidade que não seja suportada de forma nativa, alguns desenvolvedores podem desejar estender a funcionalidade existente com versões alternativas de controles já incluídos no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Nesse cenário, um desenvolvedor poderia fornecer três componentes: um componente de tempo de execução, um componente de tempo de design e um componente de conversão de item de relatório de tempo de design que converta um item de relatório existente em um item de relatório personalizado sob demanda.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Arquitetura de item de relatório personalizado](../../reporting-services/custom-report-items/custom-report-item-architecture.md)  
 Descreve os componentes que compõem um item de relatório personalizado.  
  
 [Requisitos de implementação de item de relatório personalizado](../../reporting-services/custom-report-items/custom-report-item-implementation-requirements.md)  
 Descreve os pré-requisitos para a criação de um item de relatório personalizado.  
  
 [Criar um componente de item de relatório personalizado em tempo de execução](../../reporting-services/custom-report-items/creating-a-custom-report-item-run-time-component.md)  
 Descreve como criar um componente de tempo de execução de item de relatório personalizado.  
  
 [Criar um componente de tempo de design de item de relatório personalizado](../../reporting-services/custom-report-items/creating-a-custom-report-item-design-time-component.md)  
 Descreve como criar um componente de tempo de design de item de relatório personalizado.  
  
 [Como implantar um item de relatório personalizado](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)  
 Descreve como implantar um item de relatório personalizado.  
  
 [Bibliotecas de classes de itens de relatório personalizados](../../reporting-services/custom-report-items/custom-report-item-class-libraries.md)  
 Descreve as classes de infraestrutura de item de relatório personalizado e as classes wrapper gerenciadas do namespace **Microsoft.ReportDesigner**.  
  
## <a name="see-also"></a>Consulte também  
 [Referência técnica &#40;SSRS&#41;](../../reporting-services/technical-reference-ssrs.md)  
  
  
