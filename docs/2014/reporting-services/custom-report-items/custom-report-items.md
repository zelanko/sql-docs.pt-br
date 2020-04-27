---
title: Itens de relatório personalizados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- extending Reporting Services
- Reporting Services, extending
- custom report items
ms.assetid: 64dcaf2c-1af5-4937-8ff7-98f1ec3b367e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 39860a2b147a2db392219552ebfd18cbbf7b7992
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63264783"
---
# <a name="custom-report-items"></a>Itens de Relatório Personalizados
  O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece um conjunto de ferramentas avançadas para a criação e publicação de relatórios corporativos, o gerenciamento de segurança e de assinaturas, e a extensão da funcionalidade de relatório por meio de uma API abrangente. Os relatórios são definidos por meio de uma linguagem baseada em XML chamada linguagem RDL. A RDL oferece um conjunto de instruções que descrevem o layout, as informações de consulta e os tipos de itens para um relatório. É possível estender a RDL escrevendo um item de relatório personalizado. O item de relatório personalizado consiste em um componente de tempo de execução, chamado pelo processador de relatório em tempo de execução, e em um componente de tempo de design, que permite que o item de relatório personalizado esteja disponível no Designer de Relatórios.  
  
 Para obter uma amostra de um item de relatório personalizado totalmente implementado, consulte [Amostras de produto do SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="custom-report-item-scenarios"></a>Cenários de item de relatório personalizado  
 Os desenvolvedores que precisam integrar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a seus aplicativos podem precisar de funcionalidade que não seja nativamente suportada em RDL. Isso pode incluir itens como: controles de mapa, listas horizontais, listas colunares e matrizes de tabela dinâmica. Um item de relatório personalizado de tempo de execução pode ser desenvolvido e pode ser distribuído com um aplicativo para atender a essa necessidade.  
  
 Além de fornecer funcionalidade que não tem suporte nativo, alguns desenvolvedores podem desejar estender a funcionalidade existente com versões alternativas de controles já incluídas no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Nesse cenário, um desenvolvedor poderia fornecer três componentes: um componente de tempo de execução, um componente de tempo de design e um componente de conversão de item de relatório de tempo de design que converta um item de relatório existente em um item de relatório personalizado sob demanda.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Arquitetura de item de relatório personalizado](custom-report-item-architecture.md)  
 Descreve os componentes que compõem um item de relatório personalizado.  
  
 [Requisitos de implementação de item de relatório personalizado](custom-report-item-implementation-requirements.md)  
 Descreve os pré-requisitos para a criação de um item de relatório personalizado.  
  
 [Criando um componente de item de relatório personalizado em tempo de execução](creating-a-custom-report-item-run-time-component.md)  
 Descreve como criar um componente de tempo de execução de item de relatório personalizado.  
  
 [Criando um componente de tempo de design de item de relatório personalizado](creating-a-custom-report-item-design-time-component.md)  
 Descreve como criar um componente de tempo de design de item de relatório personalizado.  
  
 [Como: implantar um Item de relatório personalizado](how-to-deploy-a-custom-report-item.md)  
 Descreve como implantar um item de relatório personalizado.  
  
 [Bibliotecas de classes de itens de relatório personalizados](custom-report-item-class-libraries.md)  
 Descreve as classes de infraestrutura de item de relatório personalizado e as classes wrapper gerenciadas do namespace `Microsoft.ReportDesigner`.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência técnica &#40;SSRS&#41;](../technical-reference-ssrs.md)  
  
  
