---
title: Conceitos básicos de pacote do SSIS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- package requirements
ms.assetid: b0c86c35-e3d3-4724-9a96-4087e9d74bf3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3a12fb33db8b1b4da1b33c02850a108b1e30b2d2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62766381"
---
# <a name="ssis-package-essentials"></a>Informações essenciais sobre pacotes SSIS
  Um pacote é o objeto que implementa a funcionalidade do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para extrair, transformar e carregar dados. Crie um pacote usando o Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Você também pode criar um pacote executando o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou o Assistente para Conexões de Projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Para obter mais informações, [criar pacotes no SQL Server Data Tools](create-packages-in-sql-server-data-tools.md) no Designer SSIS e [Assistente de importação de projeto](../../2014/integration-services/import-project-wizard.md).  
  
 Um pacote básico inclui os seguintes elementos:  
  
 **Elementos de fluxo de controle**  
 Esses elementos obrigatórios executam várias funções, fornecem estrutura e controlam a ordem em que os elementos são executados. Os elementos de fluxo de controle principais são as tarefas, os contêineres e as restrições de precedência. Deve haver pelo menos um elemento de fluxo de controle em um pacote.  
  
 Para obter mais informações, consulte [Control Flow](control-flow/control-flow.md).  
  
 **Elementos de fluxo de dados**  
 Esses elementos opcionais extraem, modificam e carregam dados em fontes de dados. Os elementos de fluxo de dados principais são fontes, transformações e destinos. Não é necessário haver elementos de fluxo de dados no pacote.  
  
 Para obter mais informações, consulte [Data Flow](data-flow/data-flow.md).  
  
 Para obter um exemplo de como criar um pacote básico, consulte [lição 1: Criando o projeto e pacote básico](lesson-1-create-a-project-and-basic-package-with-ssis.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Criar pacotes nas Ferramentas de Dados do SQL Server](create-packages-in-sql-server-data-tools.md)  
  
-   [Adicionar ou excluir uma tarefa ou um contêiner em um fluxo de controle](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
-   [Definir as propriedades de uma tarefa ou contêiner](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)  
  
-   [Adicionar ou excluir um componente em um fluxo de dados](data-flow/add-or-delete-a-component-in-a-data-flow.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
1.  Vídeo, [Criando um pacote básico (vídeo do SQL Server)](https://go.microsoft.com/fwlink/?LinkId=131023), no site MSDN.Microsoft.com  
  
## <a name="see-also"></a>Consulte também  
 [Pacotes do Integration Services &#40;SSIS&#41;](../../2014/integration-services/integration-services-ssis-packages.md)   
 [Restrições de precedência](control-flow/precedence-constraints.md)  
  
  
