---
title: "Exibições (catálogo do Integration Services) | Microsoft Docs"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- views [Integration Services]
ms.assetid: d0294d43-4852-46dc-9afa-d0c19ea9aa03
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b7293a70046df19eef816d3e7830518959ecbc98
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="views-integration-services-catalog"></a>Exibições (catálogo do Integration Services)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Esta seção descreve as exibições [!INCLUDE[tsql](../../includes/tsql-md.md)] disponíveis para administrar projetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] implantados em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Consulta o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] exibições para inspecionar objetos, configurações e dados operacionais que são armazenados na **SSISDB** catálogo.  
  
 O nome padrão do catálogo é SSISDB. Os objetos armazenados no catálogo incluem projetos, pacotes, parâmetros, ambientes e histórico operacional.  
  
 Você também pode usar as exibições de banco de dados e chamar os procedimentos armazenados diretamente, ou escrever código personalizado que chame a API gerenciada. O [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e a API gerenciada consultam as exibições e chamam os procedimentos armazenados descritos nesta seção para executar muitas de suas tarefas.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Catalog. catalog_properties &#40; Banco de dados SSISDB &#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)  
 Exibe as propriedades do catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [Catalog. effective_object_permissions &#40; Banco de dados SSISDB &#41;](../../integration-services/system-views/catalog-effective-object-permissions-ssisdb-database.md)  
 Exibe as permissões efetivas da entidade de segurança atual para todos os objetos no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.environment_variables &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-environment-variables-ssisdb-database.md)  
 Exibe os detalhes de variável de ambiente para todos os ambientes no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.environments &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-environments-ssisdb-database.md)  
 Exibe os detalhes de ambiente para todos os ambientes no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Os ambientes contêm variáveis que podem ser referenciadas por projetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.execution_parameter_values &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md)  
 Exibe os valores de parâmetros reais que são usados por pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] durante uma instância de execução.  
  
 [catalog.executions &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md)  
 Exibe as instâncias de execução de pacote no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Pacotes que são executados com a tarefa Executar Pacote na mesma instância de execução que o pacote pai.  
  
 [Catalog. explicit_object_permissions &#40; Banco de dados SSISDB &#41;](../../integration-services/system-views/catalog-explicit-object-permissions-ssisdb-database.md)  
 Exibe apenas as permissões que foram explicitamente atribuídas ao usuário.  
  
 [catalog.extended_operation_info &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-extended-operation-info-ssisdb-database.md)  
 Exibe informações estendidas de todas as operações no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [Catalog. Folders &#40; Banco de dados SSISDB &#41;](../../integration-services/system-views/catalog-folders-ssisdb-database.md)  
 Exibe as pastas no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.object_parameters &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-object-parameters-ssisdb-database.md)  
 Exibe os parâmetros para todos os pacotes e projetos no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.object_versions &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-object-versions-ssisdb-database.md)  
 Exibe as versões dos objetos do catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Nesta versão, apenas versões de projetos têm suporte nesta exibição.  
  
 [catalog.operation_messages &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md)  
 Exibe mensagens que são registradas em log durante operações no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.operations &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md)  
 Exibe os detalhes de todas as operações no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.packages &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-packages-ssisdb-database.md)  
 Exibe os detalhes de todos os pacotes exibidos no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.environment_references &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-environment-references-ssisdb-database.md)  
 Exibe as referências de ambiente para todos os projetos no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.projects &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-projects-ssisdb-database.md)  
 Exibe os detalhes de todos os projetos exibidos no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [Catalog. validations &#40; Banco de dados SSISDB &#41;](../../integration-services/system-views/catalog-validations-ssisdb-database.md)  
 Exibe os detalhes de todas as validações de projeto e pacote no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
[Catalog.master_properties &#40; Banco de dados SSISDB &#41;](../../integration-services/system-views/catalog-master-properties-ssisdb-database.md)  
Exibe as propriedades do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] mestre fora de escala.

[Catalog.worker_agents &#40; Banco de dados SSISDB &#41;](../../integration-services/system-views/catalog-worker-agents-ssisdb-database.md)  
Exibe as informações do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] escala fora do trabalho.  

