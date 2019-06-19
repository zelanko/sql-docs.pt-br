---
title: Tarefa do Azure Data Lake Analytics | Microsoft Docs
description: Com a tarefa do Azure Data Lake Analytics, é possível enviar trabalhos U-SQL para o serviço Azure Data Lake Analytics.
ms.custom: ''
ms.date: 05/18/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: maghan
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSTASK.F1
- SQL14.DTS.DESIGNER.AFPADLSTASK.F1
author: yanancai
ms.author: yanacai
manager: craigg
ms.openlocfilehash: f68a57063f0619458d6961308bbaeeee9c22c323
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014921"
---
# <a name="azure-data-lake-analytics-task"></a>Tarefa do Azure Data Lake Analytics

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Com a tarefa do Azure Data Lake Analytics, é possível enviar trabalhos U-SQL para o serviço Azure Data Lake Analytics. Essa tarefa é um componente do [feature pack para Azure do SSIS (SQL Server Integration Services)](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

Para obter informações gerais, consulte [Azure Data Lake Analytics](https://azure.microsoft.com/services/data-lake-analytics/).

## <a name="configure-the-task"></a>Configurar a tarefa

Para adicionar uma tarefa do Azure Data Lake Analytics a um pacote, arraste-a da Caixa de Ferramentas do SSIS para a tela do designer. Clique duas vezes na tarefa, ou clique com o botão direito na tarefa, e selecione **Editar**. A caixa de diálogo **Editor de tarefas do Azure Data Lake Analytics** é aberta. Você pode definir as propriedades por meio do Designer SSIS ou programaticamente.

## <a name="general-page-configuration"></a>Configuração de página geral

Use a página **Geral** para configurar a tarefa e fornecer o script U-SQL que a tarefa envia. Para saber mais sobre a linguagem U-SQL, confira [Referência da linguagem U-SQL](https://msdn.microsoft.com/azure/data-lake-analytics/u-sql/u-sql-language-reference).

### <a name="basic-configuration"></a>Configuração básica

É possível especificar o nome e a descrição da tarefa.

### <a name="u-sql-configuration"></a>Configuração do U-SQL

A configuração do U-SQL tem duas configurações: **SourceType** e opções dinâmicas com base no valor de **SourceType**. 

**SourceType** especifica a origem do script U-SQL. O script será enviado a uma conta do Azure Data Lake Analytics durante a execução do pacote do SSIS. As opções para essa propriedade são:

|Valor|Descrição|  
|-----------|-----------------|  
|**DirectInput**|Especifica o script U-SQL por meio do editor embutido. A seleção desse valor exibe a opção dinâmica **USQLStatement**.|  
|**FileConnection**|Especifica um arquivo. usql local que contém o script U-SQL. A seleção dessa opção exibe a opção dinâmica **FileConnection**.|  
|**Variável**|Especifica uma variável SSIS que contém o script U-SQL. Selecionando esse valor, a opção dinâmica **SourceVariable**é exibida.|

**Opções Dinâmicas de SourceType** especifica o conteúdo de script para a consulta U-SQL. 

|SourceType|Opções dinâmicas|  
|-----------|-----------------|  
|**SourceType = DirectInput**|Digite a consulta U-SQL a ser enviada diretamente na caixa de opção ou selecione o botão Procurar (...) para digitar a consulta U-SQL na caixa de diálogo **Digitar a consulta U-SQL**.|  
|**SourceType = FileConnection**|Selecione um gerenciador de conexões de arquivo existente ou selecione <**Nova conexão...** > para criar uma nova conexão de arquivo. Para obter informações relacionadas, confira [Gerenciador de Conexões de Arquivos](../../integration-services/connection-manager/file-connection-manager.md) e [Editor do Gerenciador de Conexões de Arquivos](../../integration-services/connection-manager/file-connection-manager-editor.md).|  
|**SourceType = Variable**|Selecione uma variável existente ou selecione \<**Nova variável...**> para criar uma nova variável. Para saber mais, confira [Variáveis do &#40;SSIS&#41; Integration Services](../../integration-services/integration-services-ssis-variables.md) e [Adicionar Variável](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).|


### <a name="job-configuration"></a>Configuração do trabalho
A configuração de trabalho especifica as propriedades de envio do trabalho de U-SQL.

- **AzureDataLakeAnalyticsConnection:** Especifica a conta do Data Lake Analytics na qual o script U-SQL é enviado. Escolha a conexão a partir de uma lista definida de gerenciadores de conexões. Para criar uma nova conexão, selecione <**Nova conexão**>. Para obter informações relacionadas, confira [Gerenciador de Conexões do Azure Data Lake Analytics](../../integration-services/connection-manager/azure-data-lake-analytics-connection-manager.md).

- **JobName:** Especifica o nome do trabalho do U-SQL. 
- **AnalyticsUnits:** Especifica a contagem de unidades de análise do trabalho do U-SQL.
- **Priority:** Especifica a prioridade do trabalho do U-SQL. Defina com um valor de 0 a 1000. Quanto menor o número, maior a prioridade.
- **RuntimeVersion:** Especifica a versão de tempo de execução do Data Lake Analytics do trabalho do U-SQL. Ele é definido como "padrão" por padrão. Normalmente, você não precisa alterar essa propriedade.
- **Synchronous:** Um valor booliano especifica se a tarefa deve aguardar a conclusão do trabalho ou não. Se o valor for definido como true, a tarefa será marcada como **sucesso** após a conclusão do trabalho. Se o valor for definido como false, a tarefa será marcada como **sucesso** após o trabalho passar pela fase de preparação.

  |Valor|Descrição|
  |-----------|-----------------|
  |True|O resultado da tarefa baseia-se no resultado de execução do trabalho U-SQL. Trabalho bem-sucedido > tarefa bem-sucedida. Falha do trabalho > falha na tarefa. Falha ou sucesso da tarefa > a tarefa é concluída.|
  |Falso|O resultado da tarefa baseia-se no resultado de envio e preparação do trabalho U-SQL. Envio do trabalho bem-sucedido e fase de preparação realizada > tarefa bem-sucedida. Falha no envio do trabalho ou reprovação do trabalho na fase de preparação > falha na tarefa. Falha ou sucesso da tarefa > a tarefa é concluída.|

- **TimeOut:** Especifica um tempo limite, em segundos, para a execução do trabalho. Se o trabalho atingir o tempo limite, será cancelado e marcado como com falha. A propriedade não estará disponível se **Synchronous** for definido como falso.

## <a name="parameter-mapping-page-configuration"></a>Configuração de página de mapeamento de parâmetro

Use a página **Mapeamento de Parâmetros** da caixa de diálogo **Editor de Tarefa do Azure Data Lake Analytics** para mapear variáveis para parâmetros (variáveis de U-SQL) no script U-SQL.

- **Nome da Variável:** Depois de adicionar um mapeamento de parâmetros selecionando **Adicionar**, selecione um sistema ou uma variável definida pelo usuário na lista. Como alternativa, você pode selecionar <**Nova variável...** > para adicionar uma nova variável usando a caixa de diálogo **Adicionar Variável**. Para obter informações relacionadas, confira [Variáveis do &#40;SSIS&#41; Integration Services](../../integration-services/integration-services-ssis-variables.md).  

- **Nome do Parâmetro:** Forneça um nome de parâmetro/variável no script U-SQL. Verifique se o nome do parâmetro começa com o sinal \@, como \@Param1. 

Aqui está um exemplo de como passar parâmetros para o script U-SQL.

**Exemplo de script U-SQL**
```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int,
            Urls            string,
            ClickedUrls     string
    FROM @in
    USING Extractors.Tsv(nullEscape:"#NULL#");

@rs1 =
    SELECT Start, Region, Duration
    FROM @searchlog
WHERE Region == "en-gb";

@rs1 =
    SELECT Start, Region, Duration
    FROM @rs1
    WHERE Start <= DateTime.Parse("2012/02/19");

OUTPUT @rs1   
    TO @out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

No exemplo de script acima, os caminhos de entrada e saída são definidos em parâmetros **\@in** e **\@out**. Os valores para os parâmetros **\@in** e **\@out** no script U-SQL são passados dinamicamente pela configuração de mapeamento de parâmetros.

|Nome da variável|Nome do parâmetro|
|-------------|--------------|
|Usuário: Variable1|\@in|
|Usuário: Variable2|\@out| 

## <a name="expression-page-configuration"></a>Configuração de página de expressão

É possível atribuir todas as propriedades na configuração de página Geral como uma expressão de propriedade para habilitar a atualização dinâmica da propriedade em tempo de execução. Para obter informações relacionadas, confira [Usar expressões de propriedade em pacotes](../../integration-services/expressions/use-property-expressions-in-packages.md).

## <a name="see-also"></a>Confira também
- [Gerenciador de Conexão do Azure Data Lake Analytics](../../integration-services/connection-manager/azure-data-lake-analytics-connection-manager.md)
- [Tarefa do sistema de arquivos do Azure Data Lake Store](../../integration-services/control-flow/azure-data-lake-store-file-system-task.md)
- [Gerenciador de conexões do Azure Data Lake Store](../../integration-services/connection-manager/azure-data-lake-store-connection-manager.md)

