---
title: Caixa de diálogo Propriedades do assembly (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.assemblyproperties.f1
ms.assetid: da1174d6-d82b-4337-ac19-7368dbd95a84
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 36ad3870fbbbfbcb457e54929bcd4729b7814d8b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62643559"
---
# <a name="assembly-properties-dialog-box-analysis-services---multidimensional-data"></a>Caixa de diálogo Propriedades do Assembly (Analysis Services - Dados Multidimensionais)
  Use a caixa de diálogo **Propriedades do Assembly** no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para definir as propriedades de uma referência de assembly em um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . É possível exibir a caixa de diálogo **Propriedades do Assembly** clicando com o botão direito do mouse em um assembly no **Explorador de Objetos** e selecionando **Propriedades**.  
  
## <a name="options"></a>Opções  
  
|Termo|Definição|  
|----------|----------------|  
|**Nome**|Digite para alterar o nome da referência de assembly.<br /><br /> Observação: A alteração desse valor não altera o nome do assembly referido pela referência de assembly, mas em vez disso, altera o nome usado o pela [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] instância ou banco de dados ao fazer referência à referência de assembly.|  
|**ID**|Exibe o identificador do assembly referenciado para pela referência de assembly.|  
|**Descrição**|Digite para alterar a descrição da referência de assembly.|  
|**Criar Carimbo de Data/Hora**|Exibe a data e a hora de criação da referência de assembly.|  
|**Última Atualização de Esquema**|Exibe a data e a hora da última atualização dos metadados da referência de assembly.|  
|**Tipo**|Exibe o tipo da referência de assembly. Os seguintes valores são exibidos:<br /><br /> **Assembly .NET**: A referência de assembly faz referência a um assembly [!INCLUDE[msCoName](../includes/msconame-md.md)] .NET Framework.<br /><br /> **DLL COM**: A referência de assembly faz referência a uma biblioteca COM.|  
|**Origem**|Exibe a origem da referência de assembly. Essa propriedade normalmente contém o caminho completo e o nome de arquivo do assembly referido pela referência de assembly.|  
|**Conjunto de permissões**|Selecione o conjunto de permissões usado para determinar acesso à referência de assembly. Para obter mais informações sobre os valores disponíveis para essa propriedade, consulte <xref:Microsoft.AnalysisServices.ClrAssembly.PermissionSet%2A>.|  
|**Informações sobre Representação**|Selecione a informações de representação a serem usadas ao acessar a referência de assembly. Para obter mais informações sobre os valores disponíveis para essa propriedade, consulte [Elemento ImpersonationInfo &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/impersonationinfo-element-assl)|  
  
## <a name="see-also"></a>Consulte também  
 [Designers e caixas de diálogo do Analysis Services &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Gerenciamento de assemblies de modelo multidimensional](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
