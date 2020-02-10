---
title: Implantando modelos (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deployment packages [Master Data Services], about deployment packages
- deployment packages [Master Data Services]
ms.assetid: 30085c08-034f-4efe-80fe-408f9091ff5c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 6b631686e9daf716bb124ce5fadaf7575420a114
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65483138"
---
# <a name="deploying-models-master-data-services"></a>Implantando modelos (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], um pacote é um arquivo XML que contém uma estrutura de modelo implantável, e opcionalmente, dados do modelo. Use pacotes modelo para mover cópias de modelos de um ambiente MDS para outro, ou crie novos modelos em seu ambiente MDS existente.  
  
> [!IMPORTANT]  
>  Os pacotes podem ser implantados somente na edição do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] na qual eles foram criados. Isso significa que os pacotes criados no [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] não podem ser implantados no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] ou superior.  
  
## <a name="tools-for-deploying-models"></a>Ferramentas para implantar modelos  
 Para trabalhar com pacotes de modelo, você pode usar uma das três ferramentas, dependendo de suas necessidades.  
  
-   **Ferramenta MDSModelDeploy**: para criar e implantar objetos de modelo e dados, use a ferramenta MDSModelDeploy. exe. Se você tiver selecionado o caminho padrão ao instalar o MDS, essa ferramenta estará localizada em *unidade*: \Program Files\Microsoft SQL Server\120\Master data Services\Configuration.  
  
-   **Assistente de implantação de modelo**: para criar e implantar pacotes somente da estrutura do modelo, use o assistente [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] no aplicativo Web. Você não pode usar esse assistente para implantar dados.  
  
-   **Editor de pacote de modelo**: para editar um pacote de modelo, use o ModelPackageEditor. exe que inicia o assistente de editor de pacote de modelo. Use esse assistente para editar um pacote criado pela ferramenta MDSModelDeploy ou pelo assistente de Implantação de Modelo. Se você tiver selecionado o caminho padrão ao instalar o MDS, essa ferramenta estará localizada em *unidade*: \Program Files\Microsoft SQL Server\120\Master data Services\Configuration.  
  
> [!IMPORTANT]  
>  Você pode usar o MDSDeployModel para criar um novo modelo, criar um clone de um modelo ou atualizar um modelo existente e seus dados. Se você usar a ferramenta MDSModelDeploy para atualizar um modelo existente e seus dados, e o pacote não contiver uma entidade, um atributo ou um membro que exista no modelo de destino, MDSModelDeploy não excluirá a entidade, o atributo ou o membro do modelo.  
  
## <a name="what-packages-contain"></a>O que os pacotes contêm  
 Um pacote de modelo é um arquivo XML salvo com a extensão .pkg. Ao criar um pacote de implantação, é possível optar por incluir dados ou não. Se decidir incluir dados, você deverá selecionar uma versão dos dados a ser incluída.  
  
 Todos os objetos de modelo são incluídos em um pacote. Esses objetos são:  
  
-   Entidades  
  
-   Atributos  
  
-   Grupos de atributos  
  
-   Hierarquias  
  
-   Coleções  
  
-   Regras de negócio  
  
-   Sinalizadores de versão  
  
-   Exibições de assinatura  
  
 Metadados definidos pelo usuário, atributos de arquivo e permissões de grupo não estão incluídos. Depois de implantar um modelo, você deve atualizar esses objetos manualmente.  
  
## <a name="sample-packages"></a>Pacotes de exemplo  
 Arquivos de pacotes de exemplo são incluídos quando você instala o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Estes arquivos de pacotes estão no diretório Master Data Services\Samples\Packages onde o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]foi instalado. Quando você implanta esses pacotes de exemplo usando a ferramenta MDSModelDeploy, modelos de exemplo são criados e populados com dados.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Crie um novo pacote de implantação de objetos de modelo e/ou dados usando a ferramenta MDSModelDeploy.|[Criar um pacote de implantação de modelo usando o MDSModelDeploy](../../2014/master-data-services/create-a-model-deployment-package-by-using-mdsmodeldeploy.md)|  
|Crie um novo pacote de implantação somente de objetos de modelo usando o assistente.|[Criar um pacote de implantação de modelo usando o Assistente](../../2014/master-data-services/create-a-model-deployment-package-by-using-the-wizard.md)|  
|Implante um pacote de objetos de modelo e dados usando a ferramenta MDSModelDeploy.|[Implantar um pacote de implantação de modelo usando MDSModelDeploy](../../2014/master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)|  
|Implante um pacote somente de objetos de modelo usando o assistente.|[Implantar um pacote de implantação de modelo usando o Assistente](../../2014/master-data-services/deploy-a-model-deployment-package-by-using-the-wizard.md)|  
|Edite um pacote de implantação de modelo para implantar partes selecionadas de um modelo, em vez do modelo inteiro.|[Editar um pacote de implantação de modelo](../../2014/master-data-services/edit-a-model-deployment-package.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Opções de implantação de modelo &#40;Master Data Services&#41;](model-deployment-options-master-data-services.md)  
  
  
