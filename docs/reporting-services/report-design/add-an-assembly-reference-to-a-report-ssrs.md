---
title: Adicionar uma referência de assembly a um relatório | Microsoft Docs
description: Saiba como fornecer uma referência de assembly a um relatório para o processador de relatório pode resolver nomes no Construtor de Relatórios.
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
helpviewer_keywords:
- code [Reporting Services]
- custom assemblies [Reporting Services], referencing
- custom code [Reporting Services]
- adding assembly references
- assemblies [Reporting Services], references
ms.assetid: 0a03939e-48ce-4c30-b227-98533f2e0ccb
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 34bc95e7b07e7d248018de5ab187699964987fac
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91934829"
---
# <a name="add-an-assembly-reference-to-a-report-ssrs"></a>Adicionar uma referência de assembly a um relatório (SSRS)
  Quando você insere o código personalizado que contém referências a classes [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] que não estão no <xref:System.Math> ou <xref:System.Convert>, você deve fornecer uma referência de assembly ao relatório para que o processador de relatórios possa resolver os nomes. Para obter mais informações, consulte [Adicionar código a um relatório &#40;SSRS&#41;](../../reporting-services/report-design/add-code-to-a-report-ssrs.md).  
  
### <a name="to-add-an-assembly-reference-to-a-report"></a>Para adicionar uma referência de assembly a um relatório  
  
1.  No modo de exibição de **Design** , clique com o botão direito do mouse na superfície de design fora da borda do relatório e clique em **Propriedades do Relatório**.  
  
2.  Clique em **Referências**.  
  
3.  Em **Adicionar ou remover assemblies**, clique em **Adicionar** e clique no botão de reticências para procurar para o assembly.  
  
4.  Em **Adicionar ou remover classes**, clique em **Adicionar** e digite o nome da classe e forneça um nome de instância a ser usado no relatório.  
  
    > [!NOTE]  
    >  Especifique uma classe e um nome de instância somente para membros com base em instâncias. Não especifique os membros estáticos na lista **Classes** . Para obter mais informações, consulte [Referências a código personalizado e assemblies em expressões no Designer de Relatórios &#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md).  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Usando assemblies personalizados com relatórios](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)   
 [Caixa de diálogo Propriedades do Relatório, Referências](./custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)  
  
