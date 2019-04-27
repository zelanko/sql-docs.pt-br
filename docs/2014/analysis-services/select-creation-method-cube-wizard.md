---
title: Selecionar método de criação (Assistente para cubos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubewizard.cubedefinition.f1
ms.assetid: 985d3b5b-7891-465b-862d-f7e75431b342
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 48a6ef3849e91f606cb94ae7fa1f7c67817bfff7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62747878"
---
# <a name="select-creation-method-cube-wizard"></a>Selecionar Método de Criação (Assistente para Cubos)
  Use a página **Selecionar Método de Criação** para especificar como criar o cubo.  
  
## <a name="options"></a>Opções  
 **Usar tabelas existentes**  
 Selecione para criar um cubo usando tabelas existentes em uma fonte de dados. O assistente guiará você pelo processo de seleção e definição de grupos de medidas e dimensões com base nas tabelas existentes para criar seu novo cubo.  
  
 **Criar um cubo vazio**  
 Selecione para criar um cubo vazio. Essa opção será útil quando você desejar criar tudo manualmente ou quando todos os grupos de medidas no cubo forem grupos de medidas vinculados.  
  
> [!NOTE]  
>  Essa opção só estará disponível quando você estiver trabalhando com um projeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e não quando você estiver conectado diretamente com um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]   
  
 **Gerar tabelas na fonte de dados**  
 Selecione para criar um cubo primeiro e, em seguida, gerar novas tabelas na fonte de dados com base na definição do cubo.  
  
> [!NOTE]  
>  Para usar esta opção, você deve ter permissão para criar objetos na fonte de dados subjacente.  
  
 Selecionar essa opção tornará a opção **Modelo** disponível.  
  
 **Modelo**  
 Selecione o modelo que deseja usar para criar o cubo. Os modelos oferecem um conjunto de definições orientado para um propósito de negócio específico.  
  
> [!NOTE]  
>  Essa opção só estará disponível quando a opção **Gerar tabelas na fonte de dados** for selecionada.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos de cubo &#40;Analysis Services - dados multidimensionais&#41;](multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md)   
 [Cubos em modelos multidimensionais](multidimensional-models/cubes-in-multidimensional-models.md)   
 [Dimensões em modelos multidimensionais](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
