---
title: Conceder permissões nos procedimentos armazenados (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 01793166-a3e5-4856-8302-21b82d494e69
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5f24a5ca8ea44f3e05bc11d0148ab30d6f83e993
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48148546"
---
# <a name="grant-permissions-on-stored-procedures-analysis-services"></a>Conceder permissões nos procedimentos armazenados (Analysis Services)
  Procedimentos armazenados ou assemblies, na [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] são rotinas externas, escritas em uma [!INCLUDE[msCoName](../includes/msconame-md.md)] linguagem de programação .NET, que estendem os recursos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Os assemblies permitem que o desenvolvedor aproveite a integração em qualquer idioma, a manipulação de exceções, o suporte ao controle de versões, o suporte à implantação e o suporte à depuração.  
  
 Você deve ser um Administrador do Servidor para registrar um assembly. Ver [conceder permissões de administrador do servidor &#40;Analysis Services&#41;](instances/grant-server-admin-rights-to-an-analysis-services-instance.md).  
  
## <a name="security-context-for-stored-procedure-execution"></a>Contexto de segurança para a execução do procedimento armazenado  
 Qualquer usuário pode chamar um procedimento armazenado. Dependendo da configuração do procedimento armazenado, ele pode ser executado no contexto do usuário chamando o procedimento ou no contexto de um usuário anônimo. Como um usuário anônimo não tem contexto de segurança, use esse recurso junto com a configuração da instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para permitir o acesso anônimo.  
  
 Depois que o usuário chama um procedimento armazenado, mas antes de o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] executar o procedimento armazenado, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] avalia as ações no procedimento armazenado. O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] avalia as ações em um procedimento armazenado com base na interseção das permissões concedidas ao usuário e o conjunto de permissões usado para executar o procedimento. Se o procedimento armazenado contiver qualquer ação que não possa ser executada pela função de banco de dados para o usuário, essa ação não será executada.  
  
 A seguir são apresentados os conjuntos de permissões usados para executar procedimentos armazenados:  
  
-   **Seguro** conjunto de permissões com a segurança, um procedimento armazenado não é possível acessar os recursos protegidos no [!INCLUDE[msCoName](../includes/msconame-md.md)] do .NET Framework. Esse conjunto de permissões somente é usado para cálculos. Esse é o conjunto de permissões mais seguro; as informações não vazam para for a do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], as permissões não podem ser elevadas e o risco de ataques de violação de dados é minimizado.  
  
-   **Acesso externo** conjunto de permissões com o acesso externo, um procedimento armazenado pode acessar recursos externos usando código gerenciado. A definição de um procedimento armazenado para esse conjunto de permissões não causará erros de programação que poderiam levar à instabilidade do servidor. No entanto, esse conjunto de permissões pode provocar o vazamento de informações para fora do servidor, e a possibilidade de uma elevação na permissão e de ataques de violação de dados.  
  
-   **Unrestricted** conjunto de permissões com o irrestrito, um procedimento armazenado pode acessar recursos externos por meio de qualquer código. Com esse conjunto de permissões, não há garantias de segurança ou confiabilidade para procedimentos armazenados.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciamento de Assemblies de modelo multidimensional](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
