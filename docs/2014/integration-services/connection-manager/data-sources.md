---
title: Fontes de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- data sources [Integration Services], about data sources
ms.assetid: 7ac81612-9822-470f-8d0f-a1dc96142fe3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5fa4a428c1d1f290ceadee19d21f3b8f0b8bd942
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62833834"
---
# <a name="data-sources"></a>Fontes de dados
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] inclui um objeto de tempo de design que você pode usar em pacotes [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]: a fonte de dados.  
  
 Um objeto de fonte de dados é uma referência para uma conexão e, no mínimo, inclui uma cadeia de caracteres de conexão e um identificador de fonte de dados. Ele também pode incluir metadados adicionais como uma descrição, um nome, um nome de usuário e uma senha.  
  
> [!NOTE]  
>  Você pode adicionar fontes de dados somente a projetos que são configurados para usar o modelo de implantação de pacote. Se um projeto estiver configurado para usar o modelo de implantação de projeto, você usará gerenciadores de conexões criados no nível do projeto para compartilhar conexões, em vez de usar fontes de dados.  
>   
>  Para obter mais informações sobre os modelos de implantação, consulte [Deployment of Projects and Packages](../packages/deploy-integration-services-ssis-projects-and-packages.md). Para obter mais informações sobre conversão de um projeto para o modelo de implantação de projetos, consulte [Deploy Projects to Integration Services Server](../deploy-projects-to-integration-services-server.md).  
  
 As vantagens de usar fontes de dados em pacotes [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluem o seguinte:  
  
-   Uma fonte de dados tem um escopo de projeto, o que significa que uma fonte de dados criada em um projeto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] está disponível para todos os pacotes do projeto. Uma fonte de dados pode ser definida uma vez e, depois, referenciada por gerenciadores de conexões em vários pacotes.  
  
-   Uma fonte de dados oferece sincronização entre o objeto da fonte de dados e suas referências de pacote. Se a fonte de dados e os pacotes que a referenciam residem no mesmo projeto, a propriedade da cadeia de caracteres das referências de conexão da fonte de dados é automaticamente atualizada quando a fonte de dados é alterada.  
  
## <a name="reference-data-sources"></a>Referenciar fontes de dados  
 Para adicionar um objeto de fonte de dados a um projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , clique com o botão direito do mouse na pasta **Fontes de Dados** no **Gerenciador de Soluções** e clique em **Nova Fonte de Dados**. O item é adicionado à pasta **Fontes de Dados** . Caso deseje usar objetos de fonte de dados criados em outros projetos, você terá que adicioná-los primeiro ao projeto.  
  
 Você usa o objeto da fonte de dados em um pacote adicionando um gerenciador de conexões que referencie o objeto da fonte de dados para o pacote. Você pode adicioná-lo ao pacote antes de construir o fluxo de controle do pacote e os fluxos de dados, ou como uma etapa na construção do fluxo de controle ou fluxo de dados.  
  
 Um objeto de fonte de dados representa uma conexão simples para uma fonte de dados e fornece acesso aos objetos no repositório de dados que ela referencia. Por exemplo, um objeto de fonte de dados que se conecta ao Banco de dados de exemplo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]AdventureWorks inclui 60 tabelas do banco de dados.  
  
 Não há nenhuma dependência entre uma fonte de dados e os gerenciadores de conexões que fazem referência a ela. Se uma fonte de dados não faz mais parte do projeto, o pacote continua a ser válido, pois informações sobre a fonte de dados, tais como o tipo da conexão e a cadeia de caracteres da conexão, são inclusas na definição do pacote.  
  
  
