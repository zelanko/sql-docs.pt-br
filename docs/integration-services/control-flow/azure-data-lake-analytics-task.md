---
title: Tarefa do Azure Data Lake Analytics | Microsoft Docs
description: Com a tarefa do Azure Data Lake Analytics, é possível enviar trabalhos U-SQL para o serviço Azure Data Lake Analytics.
ms.custom: ''
ms.date: 06/27/2019
ms.prod: sql
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSTASK.F1
- SQL14.DTS.DESIGNER.AFPADLSTASK.F1
author: yanancai
ms.author: yanacai
ms.reviewer: maghan
ms.openlocfilehash: d3fd592913164d92851ca738090de9dd200df66f
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91719190"
---
# <a name="azure-data-lake-analytics-task"></a>Tarefa do Azure Data Lake Analytics

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]



Com a tarefa do Azure Data Lake Analytics, é possível enviar trabalhos U-SQL para o serviço Azure Data Lake Analytics. Essa tarefa é um componente do [feature pack para Azure do SSIS (SQL Server Integration Services)](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

Para obter informações gerais, consulte [Azure Data Lake Analytics](https://azure.microsoft.com/services/data-lake-analytics/).

## <a name="configure-the-task"></a>Configurar a tarefa

Para adicionar uma tarefa do Azure Data Lake Analytics a um pacote, arraste-a da Caixa de Ferramentas do SSIS para a tela do designer. Clique duas vezes na tarefa, ou clique com o botão direito na tarefa, e selecione **Editar**. A caixa de diálogo **Editor de tarefas do Azure Data Lake Analytics** é aberta. Você pode definir as propriedades por meio do Designer SSIS ou programaticamente.

## <a name="general-page-configuration"></a>Configuração de página geral

Use a página **Geral** para configurar a tarefa e fornecer o script U-SQL que a tarefa envia. Para saber mais sobre a linguagem U-SQL, confira [Referência da linguagem U-SQL](/u-sql/).

### <a name="basic-configuration"></a>Configuração básica

É possível especificar o nome e a descrição da tarefa.

### <a name="u-sql-configuration"></a>Configuração do U-SQL

A configuração de U-SQL tem duas configurações: **SourceType** e as opções dinâmicas com base no valor de **SourceType**. 

**SourceType** especifica a origem do script U-SQL. O script será enviado a uma conta do Azure Data Lake Analytics durante a execução do pacote do SSIS. As opções para essa propriedade são:

|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**DirectInput**|Especifica o script U-SQL por meio do editor embutido. A seleção desse valor exibe a opção dinâmica **USQLStatement**.|  
|**FileConnection**|Especifica um arquivo. usql local que contém o script U-SQL. A seleção dessa opção exibe a opção dinâmica **FileConnection**.|  
|**Variável**|Especifica uma variável SSIS que contém o script U-SQL. Selecionando esse valor, a opção dinâmica **SourceVariable**é exibida.|
| &nbsp; | &nbsp; |

**Opções Dinâmicas de SourceType** especifica o conteúdo de script para a consulta U-SQL. 

|SourceType|Opções dinâmicas|  
|-----------|-----------------|  
|**SourceType = DirectInput**|Digite a consulta U-SQL a ser enviada diretamente na caixa de opção ou selecione o botão Procurar (...) para digitar a consulta U-SQL na caixa de diálogo **Digitar a consulta U-SQL**.|  
|**SourceType = FileConnection**|Selecione um gerenciador de conexões de arquivo existente ou selecione <**Nova conexão...** > para criar uma nova conexão de arquivo. Para obter informações relacionadas, confira [Gerenciador de Conexões de Arquivos](../../integration-services/connection-manager/file-connection-manager.md) e [Editor do Gerenciador de Conexões de Arquivos](../connection-manager/file-connection-manager.md).|  
|**SourceType = Variable**|Selecione uma variável existente ou selecione \<**New variable...**> para criar uma variável. Para saber mais, confira [Variáveis do &#40;SSIS&#41; Integration Services](../../integration-services/integration-services-ssis-variables.md) e [Adicionar Variável](../integration-services-ssis-variables.md).|
| &nbsp; | &nbsp; |


### <a name="job-configuration"></a>Configuração do trabalho
A configuração de trabalho especifica as propriedades de envio do trabalho de U-SQL.

- **AzureDataLakeAnalyticsConnection:** Especifica a conta do Data Lake Analytics em que o script U-SQL é enviado. Escolha a conexão a partir de uma lista definida de gerenciadores de conexões. Para criar uma nova conexão, selecione <**Nova conexão**>. Para obter informações relacionadas, confira [Gerenciador de Conexões do Azure Data Lake Analytics](../../integration-services/connection-manager/azure-data-lake-analytics-connection-manager.md).

- **JobName:** especifica o nome do trabalho U-SQL. 
- **AnalyticsUnits:** especifica a contagem de unidades de análise do trabalho U-SQL.
- **Priority:** especifica a prioridade do trabalho U-SQL. Defina com um valor de 0 a 1000. Quanto menor o número, maior a prioridade.
- **RuntimeVersion:** especifica a versão de tempo de execução do Data Lake Analytics do trabalho U-SQL. Ele é definido como "padrão" por padrão. Normalmente, você não precisa alterar essa propriedade.
- **Synchronous:** um valor booliano que especifica se a tarefa deve aguardar a conclusão do trabalho ou não. Se o valor for definido como true, a tarefa será marcada como **sucesso** após a conclusão do trabalho. Se o valor for definido como false, a tarefa será marcada como **sucesso** após o trabalho passar pela fase de preparação.

  |Valor|DESCRIÇÃO|
  |-----------|-----------------|
  |True|O resultado da tarefa baseia-se no resultado de execução do trabalho U-SQL. Trabalho bem-sucedido > tarefa bem-sucedida. Falha do trabalho > falha na tarefa. Falha ou sucesso da tarefa > a tarefa é concluída.|
  |Falso|O resultado da tarefa baseia-se no resultado de envio e preparação do trabalho U-SQL. Envio do trabalho bem-sucedido e fase de preparação realizada > tarefa bem-sucedida. Falha no envio do trabalho ou reprovação do trabalho na fase de preparação > falha na tarefa. Falha ou sucesso da tarefa > a tarefa é concluída.|
  | &nbsp; | &nbsp; |

- **TimeOut:** especifica um tempo limite em segundos para a execução do trabalho. Se o trabalho atingir o tempo limite, será cancelado e marcado como com falha. A propriedade não estará disponível se **Synchronous** for definido como falso.

## <a name="parameter-mapping-page-configuration"></a>Configuração de página de mapeamento de parâmetro

Use a página **Mapeamento de Parâmetros** da caixa de diálogo **Editor de Tarefa do Azure Data Lake Analytics** para mapear variáveis para parâmetros (variáveis de U-SQL) no script U-SQL.

- **Nome da Variável:** Depois de adicionar um mapeamento de parâmetros selecionando **Adicionar**, selecione um sistema ou variável definida pelo usuário na lista. Como alternativa, você pode selecionar <**Nova variável...** > para adicionar uma nova variável usando a caixa de diálogo **Adicionar Variável**. Para obter informações relacionadas, confira [Variáveis do &#40;SSIS&#41; Integration Services](../../integration-services/integration-services-ssis-variables.md).  

- **Nome do Parâmetro:** forneça um nome de parâmetro/variável no script U-SQL. Verifique se o nome do parâmetro começa com o sinal \@, como \@Param1. 

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
|Usuário: Variável1|\@in|
|Usuário: Variável2|\@out| 
| &nbsp; | &nbsp; |

## <a name="expression-page-configuration"></a>Configuração de página de expressão

É possível atribuir todas as propriedades na configuração de página Geral como uma expressão de propriedade para habilitar a atualização dinâmica da propriedade em runtime. Para obter informações relacionadas, confira [Usar expressões de propriedade em pacotes](../../integration-services/expressions/use-property-expressions-in-packages.md).

## <a name="see-also"></a>Confira também
- [Gerenciador de Conexão do Azure Data Lake Analytics](../../integration-services/connection-manager/azure-data-lake-analytics-connection-manager.md)
- [Tarefa do sistema de arquivos do Azure Data Lake Store](../../integration-services/control-flow/azure-data-lake-store-file-system-task.md)
- [Gerenciador de conexões do Azure Data Lake Store](../../integration-services/connection-manager/azure-data-lake-store-connection-manager.md)