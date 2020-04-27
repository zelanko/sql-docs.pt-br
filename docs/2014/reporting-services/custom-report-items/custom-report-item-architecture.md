---
title: Arquitetura de item de relatório personalizado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- custom report items, architecture
ms.assetid: 2a88ea46-c9f8-4dd7-aad1-16de11da4f06
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a053eb55547da9030eebe9036667cca2e14606f1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63264960"
---
# <a name="custom-report-item-architecture"></a>Arquitetura de item de relatório personalizado
  Um item de relatório personalizado é uma extensão da linguagem RDL que permite que desenvolvedores adicionem funcionalidade que não tem suporte nativo na RDL ou estendam a funcionalidade de controles existentes. Existem dois componentes principais para um item de relatório personalizado: o componente de tempo de execução e o componente tempo de design. Esses componentes são implementados como assemblies [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e podem ser escritos em qualquer linguagem em conformidade com CLS.  
  
## <a name="the-run-time-component"></a>O componente de tempo de execução  
 O componente de tempo de execução para um item de relatório personalizado é chamado em tempo de execução pelo processador de relatório. O componente de tempo de execução aceita dados passados pelo processador de relatório em tempo de execução, processa seus dados e retorna uma imagem com o item de relatório personalizado renderizado.  
  
 ![Componente em tempo de execução de item de relatório personalizado](../../../2014/reporting-services/media/customreportitemrun-timecomponentarchitecture.gif "Componente em tempo de execução de item de relatório personalizado")  
  
## <a name="the-design-time-component"></a>O componente de tempo de design  
 O componente de tempo de design permite que o item de relatório personalizado seja definido e manipulado na interface do Designer de Relatórios em [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. O componente de tempo de design consiste em vários subcontroles que controlam a aparência e as propriedades do item de relatório personalizado no ambiente de design.  
  
 ![Componente de tempo de design de item de relatório personalizado](../../../2014/reporting-services/media/customreportitemdesign-timecomponentarchitecture.gif "Componente de tempo de design de item de relatório personalizado")  
  
## <a name="see-also"></a>Consulte Também  
 [Criando um componente de tempo de execução de item de relatório personalizado](../custom-report-items/creating-a-custom-report-item-run-time-component.md)   
 [Criando um componente de item de relatório personalizado em tempo de design](../custom-report-items/creating-a-custom-report-item-design-time-component.md)   
 [Como: implantar um Item de relatório personalizado](../custom-report-items/how-to-deploy-a-custom-report-item.md)  
  
  
