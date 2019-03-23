---
title: Integration Services (SSIS) parâmetros | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9ed9ca8e-8b1e-48d9-907d-285516d6562b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cfd6a65e1561f252574ff919c8b63b0bbd57876f
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58377970"
---
# <a name="integration-services-ssis-parameters"></a>Parâmetros do Integration Services (SSIS)
  Os parâmetros do[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS) permitem atribuir valores às propriedades nos pacotes em tempo de execução do pacote. Você pode criar *parâmetros de projeto* em nível de projeto e *parâmetros de pacote* em nível de pacote. Os parâmetros do projeto são usados para fornecer uma entrada externa que o projeto recebe para um ou mais pacotes no projeto. Os parâmetros do pacote permitem modificar a execução do pacote sem a necessidade de editar e reimplantar o pacote.  
  
 No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] , você cria, modifica ou exclui parâmetros de projeto usando a janela **Project.params** . Você cria, modifica e exclui parâmetros de pacote usando a guia **Parâmetros** no Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] . Você associa um novo parâmetro ou um existente à propriedade de uma tarefa usando a caixa de diálogo **Parametrizar** . Para saber mais sobre como usar a janela **Project.params** e a guia **Parâmetros** , consulte [Create Parameters](create-parameters.md). Para obter mais informações sobre a caixa de diálogo **Parametrizar** , consulte [Parameterize Dialog Box](parameterize-dialog-box.md).  
  
## <a name="parameters-and-package-deployment-model"></a>Parâmetros e modelo de implantação de pacote  
 Em geral, se você estiver implantando um pacote usando o modelo de implantação de pacote, deverá usar configurações em vez de parâmetros.  
  
 Quando você implantar um pacote que contém parâmetros usando o modelo de implantação de pacote e, em seguida, executar o pacote, os parâmetros não serão chamados durante a execução. Se o pacote contiver parâmetros de pacote e as expressões dentro do pacote usarem os parâmetros, os valores resultantes serão aplicados em tempo de execução. Se o pacote contiver parâmetros de projeto, a execução de pacote poderá falhar.  
  
## <a name="parameters-and-project-deployment-model"></a>Parâmetros e modelo de implantação de projeto  
 Quando você implantar um projeto no servidor [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , use exibições, procedimentos armazenados e a interface de usuário do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para gerenciar o projeto e os parâmetros de pacote. Para obter mais informações, consulte os tópicos a seguir.  
  
-   [Exibições &#40;catálogo do Integration Services&#41;](/sql/integration-services/system-views/views-integration-services-catalog)  
  
-   [Procedimentos armazenados &#40;catálogo do Integration Services&#41;](/sql/integration-services/system-stored-procedures/stored-procedures-integration-services-catalog)  
  
-   [Caixa de diálogo Configurar](catalog/configure-dialog-box.md)  
  
-   [Caixa de diálogo Executar Pacote](../../2014/integration-services/execute-package-dialog-box.md)  
  
### <a name="parameter-values"></a>Valores dos parâmetros  
 Você pode atribuir até três tipos diferentes de valores a um parâmetro. Quando uma execução de pacote é iniciada, um único valor é usado para o parâmetro, o qual é resolvido para seu valor literal final.  
  
 A tabela a seguir lista os tipos de valores.  
  
|Nome do valor|Descrição|Tipo de valor|  
|----------------|-----------------|-------------------|  
|Valor de execução|O valor que é atribuído a uma instância específica da execução do pacote. Essa atribuição substitui todos os outros valores, mas se aplica apenas a uma única instância de execução do pacote.|Literal|  
|Valor do servidor|O valor atribuído ao parâmetro dentro do escopo do projeto, depois que o projeto é implantado no servidor do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Esse valor substitui o padrão de design.|Literal ou referência de variável de ambiente|  
|Valor do design|O valor atribuído ao parâmetro quando o projeto é criado ou editado no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Esse valor persiste com o projeto.|Literal|  
  
 Você pode usar um único parâmetro para atribuir um valor a várias propriedades de pacote. Uma única propriedade de pacote pode receber apenas um valor de um único parâmetro.  
  
###  <a name="executions"></a> Execuções e valores de parâmetros  
 A *execução* é um objeto que representa uma única instância da execução do pacote. Ao criar uma execução, você especifica todos os detalhes necessários para executar um pacote, como os valores dos parâmetros de execução. Você também pode modificar os valores dos parâmetros para execuções existentes.  
  
 Quando você define explicitamente o valor de um parâmetro de execução, o valor é aplicável apenas àquela instância específica de execução. O valor de execução é usado em vez de um valor de servidor ou um valor de design. Se você não definir explicitamente um valor de execução, e um valor de servidor tiver sido especificado, o valor de servidor será usado.  
  
 Quando um parâmetro estiver marcado como obrigatório, um valor do servidor ou um valor da execução deverá ser especificado para esse parâmetro. Caso contrário, o pacote correspondente não será executado. Embora o parâmetro tenha um valor padrão em tempo de criação, ele nunca será usado assim que o projeto for implantado.  
  
#### <a name="environment-variables"></a>Variáveis de ambiente  
 Se um parâmetro fizer referência a uma variável de ambiente, o valor literal dessa variável será resolvido por meio da referência de ambiente especificada e aplicado ao parâmetro. O valor do parâmetro literal final que é usado para a execução do pacote é referenciado como o valor do parâmetro de execução. A referência de ambiente para uma execução é especificada usando a caixa de diálogo **Executar**  
  
 Se um parâmetro de projeto fizer referência a uma variável de ambiente e o valor literal da variável não puder ser resolvido na execução, o valor de design será usado. O valor de servidor não é usado.  
  
 Para exibir as variáveis de ambiente que são atribuídas a valores de parâmetros, consulte a exibição catalog.object_parameters. Para obter mais informações, consulte [catalog.object_parameters &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-views/catalog-object-parameters-ssisdb-database).  
  
#### <a name="determining-execution-parameter-values"></a>Determinando valores de parâmetros de execução  
 As seguintes exibições e procedimento armazenado Transact-SQL podem ser usados para exibir e definir valores de parâmetros.  
  
 [catalog.execution_parameter_values &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-views/catalog-execution-parameter-values-ssisdb-database) (exibição)  
 Mostra os valores de parâmetros reais que serão usados por uma execução específica  
  
 [catalog.get_parameter_values &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database) (procedimento armazenado)  
 Resolve e mostra os valores reais do pacote especificado e da referência de ambiente  
  
 [catalog.object_parameters &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-views/catalog-object-parameters-ssisdb-database) (exibição)  
 Exibe os parâmetros e as propriedades para todos os pacotes e projetos no catálogo do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , inclusive o padrão do design e os valores padrão do servidor.  
  
 [catalog.set_execution_parameter_value &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database)  
 Define o valor de um parâmetro para uma instância de execução no catálogo do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 Você também pode usar a caixa de diálogo **Executar Pacote** no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para modificar o valor do parâmetro. Para obter mais informações, consulte [Execute Package Dialog Box](../../2014/integration-services/execute-package-dialog-box.md).  
  
 Você também pode usar a opção `/Parameter` do dtexec para modificar um valor de parâmetro. Para saber mais, veja [dtexec Utility](packages/dtexec-utility.md).  
  
### <a name="parameter-validation"></a>Validação de parâmetro  
 Se não for possível resolver os valores dos parâmetros, haverá falha na execução do pacote correspondente. Para ajudar a evitar falhas, você pode validar projetos e pacotes usando a caixa de diálogo **Validar** em [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. A validação permite confirmar se todos os parâmetros têm os valores necessários ou se os valores necessários podem ser resolvidos com referências de ambiente específicas. A validação também verifica outros problemas comuns de pacotes.  
  
 Para obter mais informações, consulte [Validate Dialog Box](catalog/validate-dialog-box.md).  
  
### <a name="parameter-example"></a>Exemplo de parâmetro  
 Este exemplo descreve um parâmetro denominado **pkgOptions** que é usado para especificar opções para o pacote no qual reside.  
  
 Durante o tempo de design, quando o parâmetro foi criado no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], um valor padrão de 1 foi atribuído ao parâmetro. Esse valor padrão é referenciado como o padrão de design. Se o projeto for implantado no catálogo do SSISDB e nenhum outro valor tiver sido atribuído a esse parâmetro, a propriedade do pacote correspondente ao parâmetro **pkgOptions** receberá o valor de 1 durante a execução do pacote. O padrão de design persiste com o projeto durante seu ciclo de vida.  
  
 Na preparação de uma instância específica de execução do pacote, um valor 5 é atribuído ao parâmetro **pkgOptions** . Esse valor é referenciado como o valor de execução porque ele se aplica ao parâmetro apenas para aquela instância de execução específica. Quando a execução é iniciada, a propriedade do pacote correspondente ao parâmetro **pkgOptions** recebe o valor de 5.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Criar Parâmetros](create-parameters.md)  
  
 [Definir os valores de parâmetro após a implantação do projeto](../../2014/integration-services/set-parameter-values-after-the-project-is-deployed.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Entrada de blog, [dica rápida do SSIS: Os parâmetros necessários](https://go.microsoft.com/fwlink/?LinkId=239781), em mattmasson.com.  
  
  
