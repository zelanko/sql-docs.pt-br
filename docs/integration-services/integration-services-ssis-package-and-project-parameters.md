---
title: Parâmetros de projeto e de pacote | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.parameter.f1
- sql13.dts.designer.parameterwindow.f1
ms.assetid: 9ed9ca8e-8b1e-48d9-907d-285516d6562b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: de9ceed1aa019b82bc943a1985f0f251ad82b1fa
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917519"
---
# <a name="integration-services-ssis-package-and-project-parameters"></a>Parâmetros de pacote e projeto do SSIS (Integration Services)

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  Os parâmetros do[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS) permitem atribuir valores às propriedades nos pacotes em tempo de execução do pacote. Você pode criar *parâmetros de projeto* em nível de projeto e *parâmetros de pacote* em nível de pacote. Os parâmetros do projeto são usados para fornecer uma entrada externa que o projeto recebe para um ou mais pacotes no projeto. Os parâmetros do pacote permitem modificar a execução do pacote sem a necessidade de editar e reimplantar o pacote.  
  
 No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] , você cria, modifica ou exclui parâmetros de projeto usando a janela **Project.params** . Você cria, modifica e exclui parâmetros de pacote usando a guia **Parâmetros** no Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] . Você associa um novo parâmetro ou um existente à propriedade de uma tarefa usando a caixa de diálogo **Parametrizar** . Para saber mais sobre como usar a janela **Project.params** e a guia **Parâmetros** , consulte [Create Parameters](https://msdn.microsoft.com/library/cd5d675b-dd5d-49cc-8b1f-dc717a973f99). Para obter mais informações sobre a caixa de diálogo **Parametrizar** , consulte [Parameterize Dialog Box](https://msdn.microsoft.com/library/fac02b6d-d247-447a-8940-e8700c7ac350).  
  
## <a name="parameters-and-package-deployment-model"></a>Parâmetros e modelo de implantação de pacote  
 Em geral, se você estiver implantando um pacote usando o modelo de implantação de pacote, deverá usar configurações em vez de parâmetros.  
  
 Quando você implantar um pacote que contém parâmetros usando o modelo de implantação de pacote e, em seguida, executar o pacote, os parâmetros não serão chamados durante a execução. Se o pacote contiver parâmetros de pacote e as expressões dentro do pacote usarem os parâmetros, os valores resultantes serão aplicados em runtime. Se o pacote contiver parâmetros de projeto, a execução de pacote poderá falhar.  
  
## <a name="parameters-and-project-deployment-model"></a>Parâmetros e modelo de implantação de projeto  
 Quando você implantar um projeto no servidor Integration Services (SSIS), use exibições, procedimentos armazenados e a interface do usuário do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para gerenciar o projeto e os parâmetros de pacote. Para obter mais informações, consulte os tópicos a seguir.  
  
-   [Exibições &#40;catálogo do Integration Services&#41;](../integration-services/system-views/views-integration-services-catalog.md)  
  
-   [Procedimentos armazenados &#40;catálogo do Integration Services&#41;](../integration-services/system-stored-procedures/stored-procedures-integration-services-catalog.md)  
  
-   [Caixa de diálogo Configurar](../integration-services/service/configure-dialog-box.md)  
  
-   [Caixa de diálogo Executar Pacote](../integration-services/packages/run-integration-services-ssis-packages.md#execute_package_dialog)  
  
### <a name="parameter-values"></a>Valores dos parâmetros  
 Você pode atribuir até três tipos diferentes de valores a um parâmetro. Quando uma execução de pacote é iniciada, um único valor é usado para o parâmetro, o qual é resolvido para seu valor literal final.  
  
 A tabela a seguir lista os tipos de valores.  
  
|Nome do valor|DESCRIÇÃO|Tipo de valor|  
|----------------|-----------------|-------------------|  
|Valor de execução|O valor que é atribuído a uma instância específica da execução do pacote. Essa atribuição substitui todos os outros valores, mas se aplica apenas a uma única instância de execução do pacote.|Literal|  
|Valor do servidor|O valor atribuído ao parâmetro dentro do escopo do projeto, depois que o projeto é implantado no servidor do Integration Services. Esse valor substitui o padrão de design.|Literal ou referência de variável de ambiente|  
|Valor do design|O valor atribuído ao parâmetro quando o projeto é criado ou editado no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Esse valor persiste com o projeto.|Literal|  
  
 Você pode usar um único parâmetro para atribuir um valor a várias propriedades de pacote. Uma única propriedade de pacote pode receber apenas um valor de um único parâmetro.  
  
###  <a name="executions-and-parameter-values"></a><a name="executions"></a> Execuções e valores de parâmetros  
 A *execução* é um objeto que representa uma única instância da execução do pacote. Ao criar uma execução, você especifica todos os detalhes necessários para executar um pacote, como os valores dos parâmetros de execução. Você também pode modificar os valores dos parâmetros para execuções existentes.  
  
 Quando você define explicitamente o valor de um parâmetro de execução, o valor é aplicável apenas àquela instância específica de execução. O valor de execução é usado em vez de um valor de servidor ou um valor de design. Se você não definir explicitamente um valor de execução, e um valor de servidor tiver sido especificado, o valor de servidor será usado.  
  
 Quando um parâmetro estiver marcado como obrigatório, um valor do servidor ou um valor da execução deverá ser especificado para esse parâmetro. Caso contrário, o pacote correspondente não será executado. Embora o parâmetro tenha um valor padrão em tempo de criação, ele nunca será usado assim que o projeto for implantado.  
  
#### <a name="environment-variables"></a>Variáveis de ambiente  
 Se um parâmetro fizer referência a uma variável de ambiente, o valor literal dessa variável será resolvido por meio da referência de ambiente especificada e aplicado ao parâmetro. O valor do parâmetro literal final que é usado para a execução do pacote é referenciado como o valor do parâmetro de execução. A referência de ambiente para uma execução é especificada usando a caixa de diálogo **Executar**  
  
 Se um parâmetro de projeto fizer referência a uma variável de ambiente e o valor literal da variável não puder ser resolvido na execução, o valor de design será usado. O valor de servidor não é usado.  
  
 Para exibir as variáveis de ambiente que são atribuídas a valores de parâmetros, consulte a exibição catalog.object_parameters. Para obter mais informações, consulte [catalog.object_parameters &#40;Banco de dados SSISDB&#41;](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md).  
  
#### <a name="determining-execution-parameter-values"></a>Determinando valores de parâmetros de execução  
 As seguintes exibições e procedimento armazenado Transact-SQL podem ser usados para exibir e definir valores de parâmetros.  
  
 [catalog.execution_parameter_values &#40;Banco de dados SSISDB&#41;](../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md) (exibição)  
 Mostra os valores de parâmetros reais que serão usados por uma execução específica  
  
 [catalog.get_parameter_values &#40;Banco de dados SSISDB&#41;](../integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database.md) (procedimento armazenado)  
 Resolve e mostra os valores reais do pacote especificado e da referência de ambiente  
  
 [catalog.object_parameters &#40;Banco de dados SSISDB&#41;](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md) (exibição)  
 Exibe os parâmetros e as propriedades para todos os pacotes e projetos no catálogo do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , inclusive o padrão do design e os valores padrão do servidor.  
  
 [catalog.set_execution_parameter_value &#40;Banco de dados SSISDB&#41;](../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
 Define o valor de um parâmetro para uma instância de execução no catálogo do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 Você também pode usar a caixa de diálogo **Executar Pacote** no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para modificar o valor do parâmetro. Para obter mais informações, consulte [Execute Package Dialog Box](../integration-services/packages/run-integration-services-ssis-packages.md#execute_package_dialog).  
  
 Você também pode usar a opção **/Parameter** do dtexec para modificar um valor de parâmetro. Para saber mais, veja [dtexec Utility](../integration-services/packages/dtexec-utility.md).  
  
### <a name="parameter-validation"></a>Validação de parâmetro  
 Se não for possível resolver os valores dos parâmetros, haverá falha na execução do pacote correspondente. Para ajudar a evitar falhas, você pode validar projetos e pacotes usando a caixa de diálogo **Validar** em [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. A validação permite confirmar se todos os parâmetros têm os valores necessários ou se os valores necessários podem ser resolvidos com referências de ambiente específicas. A validação também verifica outros problemas comuns de pacotes.  
  
 Para obter mais informações, consulte [Validate Dialog Box](../integration-services/service/validate-dialog-box.md).  
  
### <a name="parameter-example"></a>Exemplo de parâmetro  
 Este exemplo descreve um parâmetro denominado **pkgOptions** que é usado para especificar opções para o pacote no qual reside.  
  
 Durante o tempo de design, quando o parâmetro foi criado no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], um valor padrão de 1 foi atribuído ao parâmetro. Esse valor padrão é referenciado como o padrão de design. Se o projeto for implantado no catálogo do SSISDB e nenhum outro valor tiver sido atribuído a esse parâmetro, a propriedade do pacote correspondente ao parâmetro **pkgOptions** receberá o valor de 1 durante a execução do pacote. O padrão de design persiste com o projeto durante seu ciclo de vida.  
  
 Na preparação de uma instância específica de execução do pacote, um valor 5 é atribuído ao parâmetro **pkgOptions** . Esse valor é referenciado como o valor de execução porque ele se aplica ao parâmetro apenas para aquela instância de execução específica. Quando a execução é iniciada, a propriedade do pacote correspondente ao parâmetro **pkgOptions** recebe o valor de 5.  
  
## <a name="create-parameters"></a>Criar parâmetros
Use o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para criar parâmetros de projeto e parâmetros de pacote. Os procedimentos a seguir fornecem instruções passo a passo para criar parâmetros de pacote/projeto.  
  
> **OBSERVAÇÃO:** se você estiver convertendo um projeto criado usando uma versão anterior do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no modelo de implantação de projeto, use o **Assistente de Conversão de Projeto do Integration Services** para criar parâmetros com base em configurações. Para obter mais informações, consulte [Implantar projetos e pacotes do SSIS (Integration Services)](../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md).  
  
### <a name="create-package-parameters"></a>Criar parâmetros de pacote  
  
1.  Abra o pacote no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]e clique na guia **Parâmetros** no SSIS Designer.  
  
     ![Guia Parâmetro de Pacote](../integration-services/media/denali-package-parameters.gif "Guia Parâmetro de Pacote")  
  
2.  Clique no botão **Adicionar Parâmetro** na barra de ferramentas.  
  
     ![Botão de barra de ferramentas Adicionar](../integration-services/media/denali-parameter-add.gif "Botão de barra de ferramentas Adicionar")  
  
3.  Insira valores para as propriedades **Nome**, **Tipo de Dados**, **Valor**, **Diferencia**e **Obrigatório** na própria lista ou na janela **Propriedades** . A tabela a seguir descreve essas propriedades.  
  
    |Propriedade|DESCRIÇÃO|  
    |--------------|-----------------|  
    |Nome|O nome do parâmetro.|  
    |Tipo de dados|O tipo de dados do parâmetro.|  
    |Valor padrão|O valor padrão do parâmetro atribuído em tempo de design. Também conhecido como o padrão de design.|  
    |Sigiloso|Valores de parâmetros confidenciais são criptografados no catálogo e aparecem como um valor NULL quando exibidos com o Transact-SQL ou o SQL Server Management Studio.|  
    |Obrigatório|Exige que um valor diferente do padrão de design seja especificado para que o pacote possa ser executado.|  
    |DESCRIÇÃO|Para fins de manutenção, a descrição do parâmetro. No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], defina a descrição do parâmetro na janela Propriedades do Visual Studio quando o parâmetro for selecionado na janela de parâmetros aplicável.|  
  
    > **OBSERVAÇÃO:** quando você implanta um projeto no catálogo, várias propriedades adicionais são associadas ao projeto. Para ver todas as propriedades de todos os parâmetros no catálogo, use a exibição [catalog.object_parameters &#40;Banco de Dados SSISDB&#41;](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md).  
  
4.  Salve o projeto para salvar as alterações nos parâmetros. Valores de parâmetros são armazenados no arquivo de projeto.  
  
    > **AVISO** Você pode editar no local na lista ou usar a janela **Propriedades** para modificar os valores de propriedades de parâmetro. Você pode excluir um parâmetro usando o botão da barra de ferramentas **Excluir (X)** . Usando o último botão da barra de ferramentas, você pode especificar um valor para um parâmetro que só seja usado quando você executar o pacote no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
    > **OBSERVAÇÃO:** se você reabrir o arquivo de pacote sem abrir o projeto no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], a guia **Parâmetros** estará vazia e desabilitada.  
  
### <a name="create-project-parameters"></a>Criar parâmetros de projeto  
  
1.  Abra o projeto no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
2.  Clique com o botão direito em **Project.params** no Gerenciador de Soluções e clique em **Abrir** (OU) clique duas vezes em **Project.params** para abri-lo.  
  
     ![Janela Parâmetros do Projeto](../integration-services/media/denali-project-parameters.gif "Janela Parâmetros do Projeto")  
  
3.  Clique no botão **Adicionar Parâmetro** na barra de ferramentas.  
  
     ![Botão de barra de ferramentas Adicionar](../integration-services/media/denali-parameter-add.gif "Botão de barra de ferramentas Adicionar")  
  
4.  Insira valores para as propriedades **Nome**, **Tipo de Dados**, **Valor**, **Diferencia**e **Obrigatório** .  
  
    |Propriedade|DESCRIÇÃO|  
    |--------------|-----------------|  
    |Nome|O nome do parâmetro.|  
    |Tipo de dados|O tipo de dados do parâmetro.|  
    |Valor padrão|O valor padrão do parâmetro atribuído em tempo de design. Também conhecido como o padrão de design.|  
    |Sigiloso|Valores de parâmetros confidenciais são criptografados no catálogo e aparecem como um valor NULL quando exibidos com o Transact-SQL ou o SQL Server Management Studio.|  
    |Obrigatório|Exige que um valor diferente do padrão de design seja especificado para que o pacote possa ser executado.|  
    |DESCRIÇÃO|Para fins de manutenção, a descrição do parâmetro. No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], defina a descrição do parâmetro na janela Propriedades do Visual Studio quando o parâmetro for selecionado na janela de parâmetros aplicável.|  
  
5.  Salve o projeto para salvar as alterações nos parâmetros. O valores de parâmetros são armazenados em configurações no arquivo de projeto. Salve o arquivo de projeto para confirmar em disco as alterações nos valores de parâmetros.  
  
    > **AVISO** Você pode editar no local na lista ou usar a janela **Propriedades** para modificar os valores de propriedades de parâmetro. Você pode excluir um parâmetro usando o botão da barra de ferramentas **Excluir (X)** . Usando o último botão da barra de ferramentas para abrir **Gerenciar Valores de Parâmetro** , você pode especificar um valor para um parâmetro que só seja usado quando você executar o pacote no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
    
## <a name="parameterize-dialog-box"></a>Parameterize Dialog Box
A caixa de diálogo **Parametrizar** permite associar um parâmetro novo ou existente à propriedade de uma tarefa. Você abre a caixa de diálogo clicando com o botão direito em uma tarefa ou na guia Fluxo de Controle no Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] e, em seguida, clique em **Parametrizar**. A lista a seguir descreve os elementos da interface de usuário na caixa de diálogo. Para obter mais informações sobre parâmetros, consulte [Parâmetros do SSIS (Integration Services)](https://msdn.microsoft.com/library/hh213214.aspx).
  
### <a name="options"></a>Opções  
 **Propriedade**  
 Selecione a propriedade da tarefa que você deseja associar a um parâmetro. Esta lista é preenchida com todas as propriedades que podem ser parametrizadas.  
  
 **Usar parâmetro existente**  
 Selecione esta opção para associar a propriedade da tarefa a um parâmetro existente e, em seguida, selecione o parâmetro na lista suspensa.  
  
 **Não usar parâmetros**  
 Selecione esta opção para remover uma referência a um parâmetro. O parâmetro não é excluído.  
  
 **Criar novo parâmetro**  
 Selecione esta opção para criar um novo parâmetro que você deseja associar à propriedade da tarefa.  
  
 **Nome**  
 Especifica o nome do parâmetro que você quer criar.  
  
 **Descrição**  
 Especifique a descrição para o parâmetro.  
  
 **Valor**  
 Especifique o valor padrão para o parâmetro. Isto também é conhecido como o padrão de design que pode ser substituído posteriormente no momento da implantação.  
  
 **Escopo**  
 Especifique o escopo do parâmetro selecionando a opção **Projeto** ou **Pacote** . Os parâmetros do projeto são usados para fornecer uma entrada externa que o projeto recebe para um ou mais pacotes no projeto. Os parâmetros do pacote permitem modificar a execução do pacote sem a necessidade de editar e reimplantar o pacote.  
  
 **Confidencial**  
 Especifique se o parâmetro é confidencial marcando ou desmarcando a caixa de seleção. Valores de parâmetros confidenciais são criptografados no catálogo e aparecem como um valor NULL quando exibidos com o Transact-SQL ou o SQL Server Management Studio.  
  
 **Necessário**  
 Especifique se o parâmetro exige que um valor diferente do padrão de design seja especificado para que o pacote possa ser executado.  
 
## <a name="set-parameter-values-after-the-project-is-deployed"></a>Definir os valores de parâmetro após a implantação do projeto
O Assistente de Implantação permite definir valores de parâmetros padrão de servidor ao implantar seu projeto no catálogo. Depois que seu projeto estiver no catálogo, você pode usar o Pesquisador de Objetos do SQL Server Management Studio (SSMS) ou o Transact-SQL para definir valores padrão de servidor.  
  
### <a name="set-server-defaults-with-ssms-object-explorer"></a>Definir os padrões do servidor com o Pesquisador de Objetos do SSMS  
  
1.  Selecione e clique com o botão direito do mouse no projeto sob o nó **Integration Services**.  
  
2.  Clique em **Propriedades** para abrir janela da caixa de diálogo **Propriedades do Projeto**.  
  
3.  Abra a página de parâmetros com um clique em **Parâmetros** sob **Selecionar uma página**.  
  
4.  Selecione o parâmetro desejado na lista **Parâmetros**. Observação: a coluna **Contêiner** ajuda a distinguir os parâmetros de projeto dos parâmetros de pacote.  
  
5.  Na coluna **Valor**, especifique o valor do parâmetro padrão de servidor desejado.  

### <a name="set-server-defaults-with-transact-sql"></a>Definir os padrões do servidor com o Transact-SQL  
 Para definir padrões de servidor com Transact-SQL, use o procedimento armazenado [catalog.set_object_parameter_value &#40;Banco de Dados SSISDB&#41;](../integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database.md). Para exibir os padrões atuais de servidor, consulte a exibição [catalog.object_parameters &#40;Banco de Dados SSISDB&#41;](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md). Para apagar um valor padrão de servidor, use o procedimento armazenado [catalog.clear_object_parameter_value &#40;Banco de Dados SSISDB&#41;](../integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database.md).  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Entrada de blog, o [Dica Rápida do SSIS: parâmetros necessários](https://go.microsoft.com/fwlink/?LinkId=239781), em mattmasson.com.  
  
  
