---
title: Funções e permissões (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5e6b463fedda33d8b10fbe2d1e415f1ef248ae92
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34025783"
---
# <a name="roles-and-permissions-analysis-services"></a>Funções e permissões (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]Fornece um modelo de autorização baseada em função que concede acesso a dados, objetos e operações. Todos os usuários que acessam uma instância ou banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] devem fazer isso dentro do contexto de uma função.  
  
 Como um administrador de sistema do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , você é responsável pela concessão de associações à **função de administrador do servidor** que transmite acesso irrestrito às operações no servidor. Essa função tem permissões fixas e não pode ser personalizada. Por padrão, os membros do grupo Administradores local são automaticamente administradores do sistema do Analysis Services.  
  
 Aos usuários não administrativos que consultam ou processam dados são concedidos acesso por meio das **funções de banco de dados**. Tanto os administradores de sistema quanto os administrador de banco de dados podem criar as funções que descrevem níveis de acesso diferentes em um determinado banco de dados e, depois, atribuir a associação a cada usuário que solicitar acesso. Cada função tem um conjunto personalizado de permissões para acessar objetos e operações em um determinado banco de dados. Você pode atribuir permissões nestes níveis: banco de dados, objetos interiores como cubos e dimensões (mas não perspectivas) e linhas.  
  
 É prática comum criar funções e atribuir associação como operações separadas. Frequentemente, o designer de modelos adiciona funções durante a fase de design. Desse modo, todas as definições de função são refletidas nos arquivos de projeto que definem o modelo. A associação de função geralmente é distribuída depois, à medida que o banco de dados vai para produção, em geral pelos administradores de banco de dados que criam scripts que podem ser desenvolvidos, testados e executados como uma operação independente.  
  
 Toda a autorização é predicada em uma identidade de usuário do Windows válida. O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa a autenticação do Windows exclusivamente para autenticar identidades de usuário. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]não fornece nenhum método de autenticação proprietária. Consulte [metodologias de autenticação com suporte no Analysis Services](../../analysis-services/instances/authentication-methodologies-supported-by-analysis-services.md).  
  
> [!IMPORTANT]  
>  As permissões são aditivas para cada usuário ou grupo do Windows, em todas as funções no banco de dados. Se uma função nega a um usuário ou grupo permissão para executar certas tarefas ou exibir certos dados, mas outra função concede essa permissão a esse usuário ou grupo, o usuário ou o grupo terá permissão para executar a tarefa ou exibir os dados.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Autorizar acesso a objetos e operações & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)  
  
-   [Conceder permissões de banco de dados & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md)  
  
-   [Conceder permissões de modelo ou de cubo & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)  
  
-   [Conceder permissões de processo & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md)  
  
-   [Conceder permissões Ler definição em metadados de objeto & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-read-definition-permissions-on-object-metadata-analysis-services.md)  
  
-   [Conceder permissões em um objeto de fonte de dados & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-permissions-on-a-data-source-object-analysis-services.md)  
  
-   [Conceder permissões em estruturas de mineração de dados e modelos de & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)  
  
-   [Conceder permissões em uma dimensão & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-permissions-on-a-dimension-analysis-services.md)  
  
-   [Conceder acesso personalizado a dimensão de dados & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md)  
  
-   [Conceder acesso personalizado a célula de dados & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)  
  
## <a name="see-also"></a>Consulte também  
 [Criar e gerenciar funções](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md)  
  
  
