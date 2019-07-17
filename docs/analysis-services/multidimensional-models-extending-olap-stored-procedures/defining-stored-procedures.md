---
title: Definindo procedimentos armazenados | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 54b14cd5ee54edab4508c06c55e5815bfeab934f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209384"
---
# <a name="defining-stored-procedures"></a>Definindo procedimentos armazenados
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Você pode usar procedimentos armazenados para chamar rotinas externas a partir [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. É possível gravar rotinas externas chamadas por um procedimento armazenado em uma linguagem CLR (Common Language Runtime), como C, C++, C#, Visual Basic ou Visual Basic .NET. Um procedimento armazenado pode ser criado e então chamado a partir de diversos contextos, como outros procedimentos armazenados, medidas calculadas ou aplicativos cliente. Os procedimentos armazenados simplificam o desenvolvimento e a implementação de bancos de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ao possibilitar que um código comum seja desenvolvido e então armazenado em um único local. Eles podem ser usados para adicionar a seus aplicativos funcionalidades comerciais que não existem como funcionalidade nativa do MDX.  
  
 Esta seção fornece as informações necessárias para você entender, projetar e implementar procedimentos armazenados.  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Projetando procedimentos armazenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/designing-stored-procedures.md)|Descreve como projetar assemblies para uso com o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[Criando procedimentos armazenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/creating-stored-procedures.md)|Descreve como criar assemblies para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[Chamando procedimentos armazenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/calling-stored-procedures.md)|Fornece informações sobre como usar assemblies no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[Acessando o contexto de consulta nos procedimentos armazenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/accessing-query-context-in-stored-procedures.md)|Descreve como acessar informações de escopo e contexto com assemblies.|  
|[Configurando a segurança para procedimentos armazenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/setting-security-for-stored-procedures.md)|Descreve como configurar a segurança de assemblies no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[Depurando procedimentos armazenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/debugging-stored-procedures.md)|Descreve como depurar assemblies no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciamento de assemblies de modelo multidimensional](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
