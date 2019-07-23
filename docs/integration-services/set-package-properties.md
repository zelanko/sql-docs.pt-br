---
title: Definir as propriedades do pacote | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, properties
- properties [Integration Services]
- checkpoints [Integration Services]
- execution properties [Integration Services]
- packages [Integration Services], properties
- identification properties [Integration Services]
- passwords [Integration Services]
- SSIS packages, properties
- transaction properties [Integration Services]
- updating package properties
- forced execution value properties [Integration Services]
- security properties [Integration Services]
- version properties [Integration Services]
- SQL Server Integration Services packages, properties
ms.assetid: 13f81c3e-2b18-4f83-b445-a2f4a2c560aa
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 9227289bd6ad587744d9025a70d625f6aedb21e0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912516"
---
# <a name="set-package-properties"></a>Definir as propriedades do pacote

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Ao criar um pacote no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] usando a interface gráfica fornecida pelo [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , você define as propriedades do objeto do pacote na janela Propriedades.  
  
 A janela **Propriedades** fornece uma lista de propriedades categorizada e alfabética. Para classificar a janela **Propriedades** por categoria, clique no ícone Categorizado.  
  
 Quando organizada por categoria, a janela **Propriedades** agrupa propriedades nas seguintes categorias:  
  
-   [Pontos de Verificação](#Checkpoints)  
  
-   [Execução](#Execution)  
  
-   [Valor de Execução Forçada](#ForcedExecutionValue)  
  
-   [Identificação](#Identification)  
  
-   [Diversos](#Misc)  
  
-   [Segurança](#Security)  
  
-   [Transactions](#Transactions)  
  
-   [Versão](#Version)  
  
 Para obter informações sobre as propriedades de pacote adicionais que você não pode definir na janela **Propriedades** , consulte <xref:Microsoft.SqlServer.Dts.Runtime.Package>.  
  
### <a name="to-set-package-properties-in-the-properties-window"></a>Para definir as propriedades de pacote na janela Propriedades  
  
-   [Definir as propriedades de um pacote](https://msdn.microsoft.com/library/0d20346e-475c-412f-b3ff-7bce25242b7a)  
  
## <a name="properties-by-category"></a>Propriedades por Categoria  
 As tabelas a seguir listam as propriedades de pacote por categoria.  
  
###  <a name="Checkpoints"></a> Pontos de Verificação  
 Você pode usar as propriedades nessa categoria para reiniciar o pacote a partir de um ponto de falha no fluxo de controle do pacote, em vez de executar novamente o pacote desde o começo de seu fluxo de controle. Para saber mais, confira [Restart Packages by Using Checkpoints](../integration-services/packages/restart-packages-by-using-checkpoints.md).  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**CheckpointFileName**|O nome do arquivo que captura as informações do ponto de verificação que permite a reinicialização de um pacote. Quando o pacote é concluído com sucesso, este arquivo é excluído.|  
|**CheckpointUsage**|Especifica quando um pacote pode ser reinicializado. Os valores são **Never**, **IfExists**e **Always**. O valor padrão dessa propriedade é **Never**, que indica que o pacote não pode ser reinicializado. Para saber mais, confira <xref:Microsoft.SqlServer.Dts.Runtime.DTSCheckpointUsage>.|  
|**SaveCheckpoints**|Especifica se os pontos de verificação são gravados no arquivo de ponto de verificação quando o pacote é executado. O valor padrão dessa propriedade é **False**.|  
  
> [!NOTE]  
>  A opção **/CheckPointing on** de dtexec equivale a definir a propriedade **SaveCheckpoints** do pacote como True, e a propriedade **CheckpointUsage** como Always. Para saber mais, veja [dtexec Utility](../integration-services/packages/dtexec-utility.md).  
  
###  <a name="Execution"></a> Execução  
 As propriedades nesta categoria configuram o comportamento de tempo de execução do objeto de pacote.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**DelayValidation**|Indica se a validação do pacote está adiada até que o pacote seja executado. O valor padrão para essa propriedade é **False**.|  
|**Disable**|Indica se o pacote está desabilitado ou não. O valor padrão dessa propriedade é **False**.|  
|**DisableEventHandlers**|Especifica se os manipuladores de eventos de pacote são executados. O valor padrão dessa propriedade é **False**.|  
|**FailPackageOnFailure**|Especifica se o pacote falha caso ocorra um erro em um componente de pacote. O único valor válido dessa propriedade é **False**.|  
|**FailParentOnError**|Especifica se o contêiner pai falha caso ocorra um erro em um contêiner filho. O valor padrão dessa propriedade é **False**.|  
|**MaxConcurrentExecutables**|O número de arquivos executáveis que o pacote pode executar simultaneamente. O valor padrão dessa propriedade é **-1**, que indica que não há nenhum limite.|  
|**MaximumErrorCount**|O número máximo de erros que podem acontecer antes de um pacote parar de ser executado. O valor padrão desta propriedade é **1**.|  
|**PackagePriorityClass**|A classe de prioridade de thread Win32 do thread de pacote. Os valores são **Default**, **AboveNormal**, **Normal**, **BelowNormal**, **Idle**. O valor padrão dessa propriedade é **Default**. Para saber mais, confira <xref:Microsoft.SqlServer.Dts.Runtime.DTSPriorityClass>.|  
  
###  <a name="ForcedExecutionValue"></a> Valor de Execução Forçada  
 As propriedades dessa categoria configuram um valor de execução opcional para o pacote.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**ForcedExecutionValue**|Caso ForceExecutionValue esteja definido como **True**, um valor que especifica o valor de execução opcional que o pacote retorna. O valor padrão dessa propriedade é **0**.|  
|**ForcedExecutionValueType**|O tipo de dados de ForcedExecutionValue. O valor padrão dessa propriedade é **Int32**.|  
|**ForceExecutionValue**|Um valor Booliano que especifica se o valor de execução opcional do contêiner deve ser forçado a conter um valor específico. O valor padrão dessa propriedade é **False**.|  
  
###  <a name="Identification"></a> Identificação  
 As propriedades dessa categoria fornecem informações como o identificador exclusivo e o nome do pacote.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**CreationDate**|A data em que o pacote foi criado.|  
|**CreatorComputerName**|O nome do computador no qual o pacote foi criado.|  
|**CreatorName**|O nome da pessoa que criou o pacote.|  
|**Descrição**|Uma descrição da funcionalidade do pacote.|  
|**ID**|O GUID do pacote, que é atribuído quando o pacote é criado. Esta propriedade é somente leitura. Para gerar um novo valor aleatório para a propriedade **ID**, selecione **\<Gerar Nova ID\>** na lista suspensa.|  
|**Nome**|O nome do pacote.|  
|**PackageType**|O tipo do pacote. Os valores são **Default**, **DTSDesigner**, **DTSDesigner100**, **DTSWizard**, **SQLDBMaint**e **SQLReplication**. O valor padrão dessa propriedade é **Default**. Para saber mais, confira <xref:Microsoft.SqlServer.Dts.Runtime.DTSPackageType>.|  
  
###  <a name="Misc"></a> Diversos  
 As propriedades desta categoria são usadas para acessar as configurações e expressões que um pacote usa e para fornecer informações sobre a localidade e o modo de log do pacote. Para obter mais informações, consulte [Usar expressões de propriedade em pacotes](../integration-services/expressions/use-property-expressions-in-packages.md).  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**Configurações**|A coleção de configurações que o pacote usa. Clique no botão Procurar **(…)** para exibir e configurar as configurações do pacote.|  
|**Expressões**|Clique no botão Procurar **(…)** para criar expressões para as propriedades do pacote.<br /><br /> Observe que você pode criar expressões de propriedade para todas as propriedades do pacote incluídas pelo modelo de objeto, não apenas as propriedades exibidas na janela Propriedades.<br /><br /> Para obter mais informações, consulte [Usar expressões de propriedade em pacotes](../integration-services/expressions/use-property-expressions-in-packages.md).<br /><br /> Para exibir expressões de propriedade existentes, expanda **Expressions**. Clique no botão Procurar **(…)** em uma caixa de texto de expressão para modificar e avaliar uma expressão.|  
|**ForceExecutionResult**|O resultado de execução do pacote. Os valores são **None**, **Success**, **Failure**e **Completion**. O valor padrão dessa propriedade é **None**. Para obter mais informações, consulte T:Microsoft.SqlServer.Dts.Runtime.DTSForcedExecResult.|  
|**LocaleId**|É uma localidade do Microsoft Win32. O valor padrão dessa propriedade é a localidade do sistema operacional no computador local.|  
|**LoggingMode**|Um valor que especifica o comportamento de log do pacote. Os valores são **Disabled**, **Enabled**e **UseParentSetting**. O valor padrão dessa propriedade é **UseParentSetting**. Para saber mais, confira <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode>.|  
|**OfflineMode**|Indica se o pacote está no modo offline. Esta propriedade é somente leitura. A propriedade é definida no nível de projeto. Geralmente, o Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] tenta se conectar a cada fonte de dados usada por seu próprio pacote para validar os metadados associados às fontes e aos destinos. Você pode habilitar **Trabalhar Offline** no menu **SSIS** , até mesmo antes de abrir um pacote, para evitar essas tentativas de conexão, e os erros de validação resultantes quando as fontes de dados não estão disponíveis. Você também pode habilitar a opção **Trabalhar Offline** para acelerar as operações no designer e a desabilitar apenas quando você desejar validar seu pacote.|  
|**SuppressConfigurationWarnings**|Indica se os avisos gerados por configurações são suprimidos. O valor padrão dessa propriedade é **False**.|  
|**UpdateObjects**|Indica se o pacote está atualizado para usar versões mais novas dos objetos que contém, se essas versões estiverem disponíveis. Por exemplo, se essa propriedade estiver definida como **True**, um pacote que inclui uma tarefa Inserção em Massa será atualizado para usar a versão mais nova da tarefa Inserção em Massa fornecida pelo [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . O valor padrão dessa propriedade é **False**.|  
  
###  <a name="Security"></a> Segurança  
 As propriedades nesta categoria são usadas para definir o nível de proteção do pacote. Para obter mais informações, consulte [Access Control for Sensitive Data in Packages](../integration-services/security/access-control-for-sensitive-data-in-packages.md).  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**PackagePassword**|A senha para níveis de proteção do pacote (**EncryptSensitiveWithPassword** e **EncryptAllWithPassword**) que exige senhas.|  
|**ProtectionLevel**|O nível de proteção do pacote. Os valores são **DontSaveSensitive**, **EncryptSensitiveWithUserKey**, **EncryptSensitiveWithPassword**, **EncryptAllWithPassword**e **ServerStorage**. O valor padrão dessa propriedade é **EncryptSensitiveWithUserKey**. Para saber mais, confira <xref:Microsoft.SqlServer.Dts.Runtime.DTSProtectionLevel>.|  
  
###  <a name="Transactions"></a> Transactions  
 As propriedades nesta categoria configuram o nível de isolamento e a opção de transação do pacote. Para obter mais informações, consulte [Transações do Integration Services](../integration-services/integration-services-transactions.md).  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**IsolationLevel**|O nível de isolamento da transação do pacote. Os valores são **Unspecified**, **Chaos**, **ReadUncommitted**, **ReadCommitted**, **RepeatableRead**, **Serializable**e **Snapshot**. O valor padrão dessa propriedade é **Serializable**.<br /><br /> Observação: o valor **Snapshot** da propriedade **IsolationLevel** é incompatível com transações de pacote. Portanto, você não pode usar a propriedade **IsolationLevel** para definir o nível de isolamento das transações de pacote como **Shapshot**. Em vez disso, use uma consulta SQL para definir as transações de pacote como **Snapshot**. Para obter mais informações, veja [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../t-sql/statements/set-transaction-isolation-level-transact-sql.md).<br /><br /> O sistema aplica a propriedade **IsolationLevel** às transações de pacote somente quando o valor da propriedade **TransactionOption** está definido como **Required**.<br /><br /> O valor da propriedade **IsolationLevel** solicitado por um contêiner filho é ignorado quando as seguintes condições forem verdadeiras:<br />O valor da propriedade **TransactionOption** do contêiner filho é **Supported**.<br />O contêiner filho une-se à transação de um contêiner pai.<br /><br /> O valor da propriedade **IsolationLevel** solicitada pelo contêiner é respeitado apenas quando o contêiner inicia uma nova transação. Um contêiner iniciará uma nova transação quando as seguintes condições forem verdadeiras:<br />O valor da propriedade **TransactionOption** do contêiner for **Required**.<br />O pai ainda não iniciou uma transação.<br /><br /> <br /><br /> Para saber mais, confira <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.IsolationLevel%2A>.|  
|**TransactionOption**|A participação transacional do pacote. Os valores são **NotSupported**, **Supported**e **Required**. O valor padrão dessa propriedade é **Supported**. Para saber mais, confira <xref:Microsoft.SqlServer.Dts.Runtime.DTSTransactionOption>.|  
  
###  <a name="Version"></a> Versão  
 As propriedades nesta categoria fornecem informações sobre a versão do objeto de pacote.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**VersionBuild**|O número de versão da criação do pacote.|  
|**VersionComments**|Comentários sobre a versão do pacote.|  
|**VersionGUID**|O GUID da versão do pacote. Esta propriedade é somente leitura.|  
|**VersionMajor**|A versão principal mais recente do pacote.|  
|**VersionMinor**|A versão secundária mais recente do pacote.|  

## <a name="set-package-properties-in-the-properties-window"></a>Definir as propriedades do pacote na janela Propriedades 
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote que você deseja configurar.  
  
2.  No **Gerenciador de Soluções**, clique duas vezes no pacote para abri-lo no Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] ou clique com o botão direito do mouse e selecione **Designer de Exibição**.  
  
3.  Clique na guia **Fluxo de Controle** e escolha uma das seguintes opções:  
  
    -   Clique com o botão direito do mouse em qualquer lugar da tela de fundo da superfície de design do fluxo de controle e clique em **Propriedades**.  
  
    -   No menu **Exibir** , clique em **Janela Propriedades**.  
  
4.  Edite as propriedades do pacote na janela **Propriedades** .  
  
5.  No menu **Arquivo** , clique em **Salvar Itens Selecionados** para salvar o pacote atualizado.  
  
