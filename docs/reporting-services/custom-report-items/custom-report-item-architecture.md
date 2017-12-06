---
title: "Arquitetura de item de relatório personalizado | Microsoft Docs"
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
helpviewer_keywords: custom report items, architecture
ms.assetid: 2a88ea46-c9f8-4dd7-aad1-16de11da4f06
caps.latest.revision: "16"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 8f4a2929d4ae9083f9d14419433247d0f3b20c32
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="custom-report-item-architecture"></a>Arquitetura de item de relatório personalizado
  Um item de relatório personalizado é uma extensão da linguagem RDL que permite que desenvolvedores adicionem funcionalidade que não é suportada de forma nativa na RDL ou estendam a funcionalidade de controles existentes. Existem dois componentes principais para um item de relatório personalizado: o componente de tempo de execução e o componente tempo de design. Esses componentes são implementados como assemblies [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e podem ser escritos em qualquer linguagem em conformidade com CLS.  
  
## <a name="the-run-time-component"></a>O componente de tempo de execução  
 O componente de tempo de execução para um item de relatório personalizado é chamado em tempo de execução pelo processador de relatório. O componente de tempo de execução aceita dados passados pelo processador de relatório em tempo de execução, processa seus dados e retorna uma imagem com o item de relatório personalizado renderizado.  
  
 ![Componente de item de relatório personalizado em tempo de execução](../../reporting-services/custom-report-items/media/customreportitemrun-timecomponentarchitecture.gif "Componente de item de relatório personalizado em tempo de execução")  
  
## <a name="the-design-time-component"></a>O componente de tempo de design  
 O componente de tempo de design permite que o item de relatório personalizado seja definido e manipulado na interface do Designer de Relatórios em [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. O componente de tempo de design consiste em vários subcontroles que controlam a aparência e as propriedades do item de relatório personalizado no ambiente de design.  
  
 ![Componente de item de relatório personalizado em tempo de design](../../reporting-services/custom-report-items/media/customreportitemdesign-timecomponentarchitecture.gif "Componente de item de relatório personalizado em tempo de design")  
  
## <a name="see-also"></a>Consulte também  
 [Criando um componente de item de relatório personalizado em tempo de execução](../../reporting-services/custom-report-items/creating-a-custom-report-item-run-time-component.md)   
 [Criando um componente de item de relatório personalizado em tempo de design](../../reporting-services/custom-report-items/creating-a-custom-report-item-design-time-component.md)   
 [Como implantar um item de relatório personalizado](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)  
  
  
