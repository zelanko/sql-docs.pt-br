---
title: Conceder permissões nos procedimentos armazenados (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 01793166-a3e5-4856-8302-21b82d494e69
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: c82a2df266f9e6dce2767ecceb3e2af9bd12fc1d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122759"
---
# <a name="grant-permissions-on-stored-procedures-analysis-services"></a>Conceder permissões nos procedimentos armazenados (Analysis Services)
  Procedimentos armazenados ou assemblies, em [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] são rotinas externas, escritas uma [!INCLUDE[msCoName](../includes/msconame-md.md)] linguagem de programação .NET, que estende os recursos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Os assemblies permitem que o desenvolvedor aproveite a integração em qualquer idioma, a manipulação de exceções, o suporte ao controle de versões, o suporte à implantação e o suporte à depuração.  
  
 Você deve ser um Administrador do Servidor para registrar um assembly. Consulte [conceder permissões de administrador de servidor &#40;do Analysis Services&#41;](instances/grant-server-admin-rights-to-an-analysis-services-instance.md).  
  
## <a name="security-context-for-stored-procedure-execution"></a>Contexto de segurança para a execução do procedimento armazenado  
 Qualquer usuário pode chamar um procedimento armazenado. Dependendo da configuração do procedimento armazenado, ele pode ser executado no contexto do usuário chamando o procedimento ou no contexto de um usuário anônimo. Como um usuário anônimo não tem contexto de segurança, use esse recurso junto com a configuração da instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para permitir o acesso anônimo.  
  
 Depois que o usuário chama um procedimento armazenado, mas antes de o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] executar o procedimento armazenado, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] avalia as ações no procedimento armazenado. O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] avalia as ações em um procedimento armazenado com base na interseção das permissões concedidas ao usuário e o conjunto de permissões usado para executar o procedimento. Se o procedimento armazenado contiver qualquer ação que não possa ser executada pela função de banco de dados para o usuário, essa ação não será executada.  
  
 A seguir são apresentados os conjuntos de permissões usados para executar procedimentos armazenados:  
  
-   **Segurança** conjunto de permissões com a segurança, um procedimento armazenado não é possível acessar os recursos protegidos no [!INCLUDE[msCoName](../includes/msconame-md.md)] do .NET Framework. Esse conjunto de permissões somente é usado para cálculos. Esse é o conjunto de permissões mais seguro; as informações não vazam para for a do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], as permissões não podem ser elevadas e o risco de ataques de violação de dados é minimizado.  
  
-   **Acesso externo** conjunto de permissões com o acesso externo, um procedimento armazenado pode acessar recursos externos usando código gerenciado. A definição de um procedimento armazenado para esse conjunto de permissões não causará erros de programação que poderiam levar à instabilidade do servidor. No entanto, esse conjunto de permissões pode provocar o vazamento de informações para fora do servidor, e a possibilidade de uma elevação na permissão e de ataques de violação de dados.  
  
-   **Irrestrito** conjunto de permissões com o irrestrito, um procedimento armazenado pode acessar recursos externos usando qualquer código. Com esse conjunto de permissões, não há garantias de segurança ou confiabilidade para procedimentos armazenados.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciamento de Assemblies de modelo multidimensional](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  