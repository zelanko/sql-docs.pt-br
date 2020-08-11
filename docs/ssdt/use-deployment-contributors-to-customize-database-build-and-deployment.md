---
title: Personalizar implantações de banco de dados usando colaboradores de implantação
description: Saiba como modificar o comportamento de projetos de banco de dados. Veja recursos em colaboradores de build e de implantação e confira exemplos de cenários em que eles são usados.
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: fe2064bb-e01e-4a12-9f12-a99aa9a5203f
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 0f5235969a2289220e7a70b035296e1ba0092714
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85883368"
---
# <a name="customize-database-build-and-deployment-by-using-build-and-deployment-contributors"></a>Personalize a compilação e a implantação do banco de dados usando os colaboradores de compilação e implantação

O Visual Studio fornece os pontos de extensibilidade que você pode usar para modificar o comportamento das ações de compilação e implantação de projetos de banco de dados.  
  
## <a name="available-extensibility-points"></a>Pontos de extensibilidade disponíveis  
Você pode criar uma extensão para os pontos de extensibilidade, conforme mostrado na seguinte tabela:  
  
|**Ação**|**Tipo de colaborador**|**Observações**|  
|--------------|------------------------|-------------|  
|Build|BuildContributor|Esse tipo de extensão é executado quando o projeto SQL é compilado depois que o modelo de projeto tiver sido completamente validado. O colaborador de compilação pode acessar o modelo concluído, além de todas as propriedades da tarefa de compilação e todos os argumentos personalizados.|  
|Implantar|DeploymentPlanModifier|Esse tipo de extensão foi executado quando o projeto SQL foi implantado, como parte do pipeline de implantação, depois que o plano de implantação foi gerado, mas antes de o plano de implantação ser executado. Você pode usar um DeploymentPlanModifier para modificar o plano de implantação adicionando ou removendo etapas. Os colaboradores de implantação podem acessar o plano de implantação, os resultados da comparação e os modelos de origem e destino.|  
|Implantar|DeploymentPlanExecutor|Esse tipo de extensão é executado quando o plano de implantação é executado e fornece acesso somente leitura para o plano de implantação. O DeploymentPlanExectutor executa ações com base no plano de implantação.|  
  
### <a name="supported-extensibility-scenarios"></a>Cenários de extensibilidade com suporte  
Você pode implementar os colaborador de compilação ou implantação para habilitar os seguintes cenários de exemplo:  
  
-   **Gerar a documentação do esquema durante a compilação do projeto** - para dar suporte a esse cenário, você implementa um [BuildContributor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.buildcontributor.aspx) e substitui o método OnExecute para gerar a documentação do esquema. Você pode criar um arquivo de destino que define os argumentos padrão que controlam se a extensão é executada e para especificar o nome do arquivo de saída.  
  
-   **Gerar um relatório de diferença quando um projeto SQL é implantado** - para dar suporte a esse cenário, você implementa um [DeploymentPlanExecutor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanexecutor.aspx) que gera o arquivo XML quando o projeto SQL é implantado.  
  
-   **Modificar o plano de implantação para alterar quando a movimentação dos dados ocorrer** - para dar suporte a esse cenário, você implementa uma [DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx) e o itera no plano de implantação. Para cada SqlTableMigrationStep nesse plano, você examinará o resultado da comparação para determinar se essa etapa deve ser executada ou ignorada.  
  
-   **Copiar os arquivos para o dacpac gerado quando um projeto SQL foi implantado** - para dar suporte a esse cenário, você implementa um colaborador de implantação e substitui o método OnEstablishDeploymentConfiguration para especificar quais arquivos são marcados como DeploymentExtensionConfiguration pelo sistema de projeto. Esses arquivos devem ser copiados para a pasta de saída e adicionado ao dacpac gerado. Você também pode modificar o colaborador para mesclar vários arquivos em um novo arquivo que será copiado para a pasta de saída e adicionado ao manifesto de implantação. Durante a implantação, você pode implementar o método OnApplyDeploymentConfiguration para extrair os arquivos do dacpac e para prepará-los para serem usados no método OnExecute.  
  
Além disso, você pode expor pares personalizados de argumentos de nome/valor de seu colaborador que são gravados no arquivo de projeto de banco de dados. Você pode usar esses argumentos para habilitar o colaborador para extrair informações do MSBuild ou permitir que o usuário final do seu colaborador personalize o comportamento. Por exemplo, você pode permitir que os usuários especifiquem o nome de um arquivo de entrada ou saída.  
  
## <a name="common-tasks"></a>Tarefas comuns  
  
|**Tarefas comuns**|**Conteúdo de suporte**|  
|--------------------|--------------------------|  
|**Saiba mais sobre os pontos de extensibilidade:** você pode ler sobre as classes base que usa para implementar os colaboradores de build e implantação.|[BuildContributor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.buildcontributor.aspx)<br /><br />[DeploymentContributor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentcontributor.aspx)|  
|**Criar colaboradores de exemplo:** conheça as etapas necessárias para criar um colaborador de compilação ou implantação. Se você seguir esse passo a passo, você poderá:<br /><br />-   Criar um colaborador de compilação que gera um relatório que lista todos os elementos no modelo.<br />-   Criar um colaborador de implantação que altera o plano de implantação antes de ser executado.<br />-   Criar um colaborador de implantação que gera um relatório de implantação quando você implanta um projeto SQL.<br /><br />Você pode criar todos os seus colaboradores em um único assembly ou entre vários assemblies, dependendo de como você deseja que os colaboradores sejam distribuídos em sua equipe.|[Passo a passo: Estender o build do projeto de banco de dados para gerar as estatísticas do modelo](../ssdt/walkthrough-extend-database-project-build-to-generate-model-statistics.md)<br /><br />[Passo a passo: estenda a implantação do projeto de banco de dados para modificar o plano de implantação](../ssdt/walkthrough-extend-database-project-deployment-to-modify-the-deployment-plan.md)<br /><br />[Passo a passo: Estender a implantação do projeto de banco de dados para analisar o plano de implantação](../ssdt/walkthrough-extend-database-project-deployment-to-analyze-the-deployment-plan.md)|  
  
## <a name="see-also"></a>Consulte Também  
[Definir condições personalizadas para testes de unidade do SQL](https://msdn.microsoft.com/library/jj860449(v=vs.103).aspx)  
  
