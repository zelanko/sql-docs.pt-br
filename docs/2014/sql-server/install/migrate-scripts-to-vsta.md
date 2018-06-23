---
title: Migrar Scripts para o VSTA | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SSIS Script task, converting scripts
- Script component [Integration Services], converting scripts
- Script task [Integration Services], converting scripts
- SSIS Script component, converting scripts
ms.assetid: d685098b-86a1-46bf-939a-63d56951e009
caps.latest.revision: 44
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 99acbad66d2a614431bc1f08ad88bd12f2a3e6b4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122320"
---
# <a name="migrate-scripts-to-vsta"></a>Migrar scripts para o VSTA
  Quando você atualiza [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] pacotes [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] migra os scripts em qualquer Script de tarefas ou componentes de Script para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA). O VSTA é o ambiente de script usado pelo [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Em [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], o ambiente de script para [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] para Applications (VSA).  
  
 Se os scripts em qualquer uma das tarefas ou componentes de Script fizerem referência a interfaces, talvez você precise modificar essas referências antes de atualizar o pacote. Caso contrário, o pacote não será atualizado ou os scripts não serão validados, dependendo do método de atualização utilizado. Para modificar essas referências, substitua referências a IDTS*xxx*90 interfaces com referências para o correspondente IDTS*xxx*100 interfaces.  
  
 Para obter mais informações sobre como migrar scripts e atualizar pacotes, consulte [atualizar pacotes do Integration Services](../../integration-services/install-windows/upgrade-integration-services-packages.md).  
  
## <a name="understanding-migration-failures"></a>Noções básicas sobre falhas de migração  
 Quando você migra os scripts, a migração pode falhar por um dos seguintes motivos:  
  
-   O ponto de entrada do script VSA foi renomeado.  
  
     O ponto de entrada especifica o método na classe `ScriptMain` do projeto VSTA que o tempo de execução do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] chama como ponto de entrada para o código da tarefa Script. A classe `ScriptMain` é a classe padrão gerada pelos modelos de script.  
  
-   Não há nenhum ponto de entrada ou existem vários pontos de entrada no script VSA.  
  
-   Não foi possível adicionar referências de assembly.  
  
-   A classe `ScriptMain` foi modificada para herdar de outras classes além da classe `ScriptObjectModelSSIS`. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] não oferece suporte a várias heranças.  
  
 Não é possível converter um script VSA que usa [!INCLUDE[vbprvblong](../../includes/vbprvblong-md.md)] para um script VSTA que usa [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csharp_orcas_long](../../includes/csharp-orcas-long-md.md)]. No entanto, você pode criar um novo script VSTA que usa [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csharp_orcas_long](../../includes/csharp-orcas-long-md.md)]. Para obter mais informações, consulte [Codificando e depurando a tarefa Script](../../integration-services/control-flow/script-task.md) e [Codificando e depurando o componente Script](../../integration-services/data-flow/transformations/script-component.md).  
  
## <a name="see-also"></a>Consulte também  
 [Estender pacotes com scripts](../../relational-databases/server-management-objects-smo/tasks/scripting.md)  
  
  