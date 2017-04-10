---
title: "Pacote do Integration Services (SSIS) e os par&#226;metros de projeto | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.designer.parameter.f1"
  - "sql13.dts.designer.paramterwindow.f1"
ms.assetid: 9ed9ca8e-8b1e-48d9-907d-285516d6562b
caps.latest.revision: 23
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 22
---
# Pacote do Integration Services (SSIS) e os par&#226;metros de projeto
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Parâmetros (SSIS) permitem atribuir valores às propriedades nos pacotes em tempo de execução do pacote. Você pode criar *parâmetros de projeto* em nível de projeto e *parâmetros de pacote* em nível de pacote. Os parâmetros do projeto são usados para fornecer uma entrada externa que o projeto recebe para um ou mais pacotes no projeto. Os parâmetros do pacote permitem modificar a execução do pacote sem a necessidade de editar e reimplantar o pacote.  
  
 No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] , você cria, modifica ou exclui parâmetros de projeto usando a janela **Project.params** . Você cria, modifica e exclui parâmetros de pacote usando a guia **Parâmetros** no Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] . Você associa um novo parâmetro ou um existente à propriedade de uma tarefa usando a caixa de diálogo **Parametrizar** . Para saber mais sobre como usar a janela **Project.params** e a guia **Parâmetros** , consulte [Create Parameters](../Topic/Create%20Parameters.md). Para obter mais informações sobre a caixa de diálogo **Parametrizar** , consulte [Parameterize Dialog Box](../Topic/Parameterize%20Dialog%20Box.md).  
  
## Parâmetros e modelo de implantação de pacote  
 Em geral, se você estiver implantando um pacote usando o modelo de implantação de pacote, deverá usar configurações em vez de parâmetros.  
  
 Quando você implantar um pacote que contém parâmetros usando o modelo de implantação de pacote e, em seguida, executar o pacote, os parâmetros não serão chamados durante a execução. Se o pacote contiver parâmetros de pacote e as expressões dentro do pacote usarem os parâmetros, os valores resultantes serão aplicados em tempo de execução. Se o pacote contiver parâmetros de projeto, a execução de pacote poderá falhar.  
  
## Parâmetros e modelo de implantação de projeto  
 Quando você implanta um projeto para o servidor do Integration Services (SSIS), use exibições, procedimentos armazenados e o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] interface do usuário para gerenciar parâmetros de projeto e pacote. Para obter mais informações, consulte os tópicos a seguir.  
  
-   [Modos de exibição e 40; catálogo do Integration Services e 41;](../integration-services/system-views/views-integration-services-catalog.md)  
  
-   [Armazenado procedimentos 40; catálogo do Integration Services e 41;](../integration-services/system-stored-procedures/stored-procedures-integration-services-catalog.md)  
  
-   [Caixa de diálogo Configurar](../integration-services/service/configure-dialog-box.md)  
  
-   [Caixa de diálogo Executar Pacote](../integration-services/packages/execute-package-dialog-box.md)  
  
### Valores dos parâmetros  
 Você pode atribuir até três tipos diferentes de valores a um parâmetro. Quando uma execução de pacote é iniciada, um único valor é usado para o parâmetro, o qual é resolvido para seu valor literal final.  
  
 A tabela a seguir lista os tipos de valores.  
  
|Nome do valor|Descrição|Tipo de valor|  
|----------------|-----------------|-------------------|  
|Valor de execução|O valor que é atribuído a uma instância específica da execução do pacote. Essa atribuição substitui todos os outros valores, mas se aplica apenas a uma única instância de execução do pacote.|Literal|  
|Valor do servidor|O valor atribuído ao parâmetro dentro do escopo do projeto, depois que o projeto é implantado no servidor do Integration Services. Esse valor substitui o padrão de design.|Literal ou referência de variável de ambiente|  
|Valor do design|O valor atribuído ao parâmetro quando o projeto é criado ou editado no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Esse valor persiste com o projeto.|Literal|  
  
 Você pode usar um único parâmetro para atribuir um valor a várias propriedades de pacote. Uma única propriedade de pacote pode receber apenas um valor de um único parâmetro.  
  
###  <a name="executions"></a> Execuções e valores de parâmetros  
 A *execução* é um objeto que representa uma única instância da execução do pacote. Ao criar uma execução, você especifica todos os detalhes necessários para executar um pacote, como os valores dos parâmetros de execução. Você também pode modificar os valores dos parâmetros para execuções existentes.  
  
 Quando você define explicitamente o valor de um parâmetro de execução, o valor é aplicável apenas àquela instância específica de execução. O valor de execução é usado em vez de um valor de servidor ou um valor de design. Se você não definir explicitamente um valor de execução, e um valor de servidor tiver sido especificado, o valor de servidor será usado.  
  
 Quando um parâmetro estiver marcado como obrigatório, um valor do servidor ou um valor da execução deverá ser especificado para esse parâmetro. Caso contrário, o pacote correspondente não será executado. Embora o parâmetro tenha um valor padrão em tempo de criação, ele nunca será usado assim que o projeto for implantado.  
  
#### Variáveis de ambiente  
 Se um parâmetro fizer referência a uma variável de ambiente, o valor literal dessa variável será resolvido por meio da referência de ambiente especificada e aplicado ao parâmetro. O valor do parâmetro literal final que é usado para a execução do pacote é referenciado como o valor do parâmetro de execução. A referência de ambiente para uma execução é especificada usando a caixa de diálogo **Executar**  
  
 Se um parâmetro de projeto fizer referência a uma variável de ambiente e o valor literal da variável não puder ser resolvido na execução, o valor de design será usado. O valor de servidor não é usado.  
  
 Para exibir as variáveis de ambiente que são atribuídas a valores de parâmetros, consulte a exibição catalog.object_parameters. Para obter mais informações, consulte [object_parameters & #40. SSISDB 41; & banco de dados](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md).  
  
#### Determinando valores de parâmetros de execução  
 As seguintes exibições e procedimento armazenado Transact-SQL podem ser usados para exibir e definir valores de parâmetros.  
  
 [Catalog. execution_parameter_values & #40. SSISDB 41; & banco de dados](../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md)(visualização)  
 Mostra os valores de parâmetros reais que serão usados por uma execução específica  
  
 [Catalog. get_parameter_values & #40. SSISDB 41; & banco de dados](../integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database.md) (procedimento armazenado)  
 Resolve e mostra os valores reais do pacote especificado e da referência de ambiente  
  
 [object_parameters & #40. SSISDB 41; & banco de dados](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md) (visualização)  
 Exibe os parâmetros e as propriedades para todos os pacotes e projetos no catálogo do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], inclusive o padrão do design e os valores padrão do servidor.  
  
 [Catalog. set_execution_parameter_value & #40. Banco de dados SSISDB & 41;](../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
 Define o valor de um parâmetro para uma instância de execução no catálogo do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
 Você também pode usar a caixa de diálogo **Executar Pacote** no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para modificar o valor do parâmetro. Para obter mais informações, consulte [Execute Package Dialog Box](../integration-services/packages/execute-package-dialog-box.md).  
  
 Você também pode usar o dtexec **/parâmetro** opção para modificar um valor de parâmetro. Para saber mais, veja [dtexec Utility](../integration-services/packages/dtexec-utility.md).  
  
### Validação de parâmetro  
 Se não for possível resolver os valores dos parâmetros, haverá falha na execução do pacote correspondente. Para ajudar a evitar falhas, você pode validar projetos e pacotes usando a caixa de diálogo **Validar** em [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. A validação permite confirmar se todos os parâmetros têm os valores necessários ou se os valores necessários podem ser resolvidos com referências de ambiente específicas. A validação também verifica outros problemas comuns de pacotes.  
  
 Para obter mais informações, consulte [Validate Dialog Box](../integration-services/service/validate-dialog-box.md).  
  
### Exemplo de parâmetro  
 Este exemplo descreve um parâmetro denominado **pkgOptions** que é usado para especificar opções para o pacote no qual reside.  
  
 Durante o tempo de design, quando o parâmetro foi criado no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], um valor padrão de 1 foi atribuído ao parâmetro. Esse valor padrão é referenciado como o padrão de design. Se o projeto for implantado no catálogo do SSISDB e nenhum outro valor tiver sido atribuído a esse parâmetro, a propriedade do pacote correspondente ao parâmetro **pkgOptions** receberá o valor de 1 durante a execução do pacote. O padrão de design persiste com o projeto durante seu ciclo de vida.  
  
 Na preparação de uma instância específica de execução do pacote, um valor 5 é atribuído ao parâmetro **pkgOptions** . Esse valor é referenciado como o valor de execução porque ele se aplica ao parâmetro apenas para aquela instância de execução específica. Quando a execução é iniciada, a propriedade do pacote correspondente ao parâmetro **pkgOptions** recebe o valor de 5.  
  
## Tarefas relacionadas  
 [Criar parâmetros](../Topic/Create%20Parameters.md)  
  
 [Definir valores de parâmetros depois que o projeto foi implantado](../Topic/Set%20Parameter%20Values%20After%20the%20Project%20Is%20Deployed.md)  
  
## Conteúdo relacionado  
 Entrada de blog, [Dica rápida de SSIS: Parâmetros necessários](http://go.microsoft.com/fwlink/?LinkId=239781), em mattmasson.com.  
  
  