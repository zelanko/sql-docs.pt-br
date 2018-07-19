---
title: Tarefa do Azure Data Lake Analytics | Microsoft Docs
ms.custom: ''
ms.date: 05/18/2018
ms.prod: sql
ms.prod_service: integration-services
ms.component: control-flow
ms.reviewer: douglasl
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSTASK.F1
- SQL14.DTS.DESIGNER.AFPADLSTASK.F1
author: yanancai
ms.author: yanacai
manager: craigg
ms.openlocfilehash: 395d790069294aed541f9756fa7caefbb62f9a7b
ms.sourcegitcommit: 44e9bf62f2c75449c17753ed66bf85c43928dbd5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37854402"
---
# <a name="azure-data-lake-analytics-task"></a>Tarefa do Azure Data Lake Analytics

A Tarefa do Azure Data Lake Analytics permite aos usuários enviar trabalhos U-SQL para o serviço Azure Data Lake Analytics. [Azure Data Lake Analytics (ADLA)](https://azure.microsoft.com/services/data-lake-analytics/)

A Tarefa do Azure Data Lake Analytics é um componente do [SSIS (SQL Server Integration Services) Feature Pack para o Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

## <a name="configure-the-azure-data-lake-analytics-task"></a>Configurar a tarefa do Azure Data Lake Analytics

Para adicionar uma Tarefa do Azure Data Lake Analytics para um pacote, arraste-o da Caixa de Ferramentas do SSIS para a tela do designer. Em seguida, clique duas vezes na tarefa ou clique com o botão direito do mouse na tarefa e selecione **Editar** para abrir a caixa de diálogo **Editor de Tarefa do Azure Data Lake Analytics**. Você pode definir as propriedades por meio do Designer SSIS ou programaticamente.

## <a name="general-page-configuration"></a>Configuração de Página Geral

Use a página **Geral** para configurar a tarefa do Azure Data Lake Analytics e fornecer o script U-SQL que a tarefa envia. Para saber mais sobre a linguagem U-SQL, confira [Referência da linguagem U-SQL](https://msdn.microsoft.com/azure/data-lake-analytics/u-sql/u-sql-language-reference).

### <a name="basic-configuration"></a>Configuração básica

- **Nome:** especifica o nome da tarefa do Azure Data Lake Analytics.
- **Descrição:** Especifica a descrição da tarefa do Azure Data Lake Analytics.

### <a name="u-sql-configuration"></a>Configuração do U-SQL

A configuração de U-SQL tem duas configurações: **SourceType** e as opções dinâmicas com base no valor **SourceType**. 

- **SourceType:** especifica a origem do script U-SQL. O script será enviado a uma conta do Azure Data Lake Analytics durante a execução de pacote SSIS. Essa propriedade tem três opções listadas na tabela a seguir.

|Valor|Descrição|  
|-----------|-----------------|  
|**DirectInput**|Especifica o script U-SQL por meio do editor embutido. A seleção desse valor exibe a opção dinâmica **USQLStatement**.|  
|**FileConnection**|Especifica um arquivo. usql local que contém o script U-SQL. A seleção dessa opção exibe a opção dinâmica **FileConnection**.|  
|**Variável**|Especifica uma variável SSIS que contém o script U-SQL. Selecionando esse valor, a opção dinâmica **SourceVariable**é exibida.|

- **Opções Dinâmicas de SourceType:** especifica o conteúdo de script para a consulta U-SQL. 

|SourceType|Opções dinâmicas|  
|-----------|-----------------|  
|**SourceType = DirectInput**|Digite a consulta U-SQL a ser enviada diretamente na caixa de opção ou clique no botão Procurar (...) para digitar a consulta U-SQL na caixa de diálogo **Digitar a consulta U-SQL**.|  
|**SourceType = FileConnection**|Selecione um gerenciador de conexões de arquivo existente ou clique em <**Nova conexão...** > para criar uma nova conexão de arquivo. **Artigo relacionado:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)|  
|**SourceType = Variable**|Selecione uma variável existente ou clique em \<**Nova variável...**> para criar uma nova variável. **Artigo relacionado:** [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)|


### <a name="job-configuration"></a>Configuração do Trabalho
A configuração de trabalho especifica as propriedades de envio do trabalho de U-SQL.

- **AzureDataLakeAnalyticsConnection:** Especifica a conta do Azure Data Lake Analytics em que o script U-SQL será enviado. Escolha a conexão a partir de uma lista definida de gerenciadores de conexões. Para criar uma nova conexão, selecione <**Nova conexão**>. Artigo relacionado: [Gerenciador de Conexão do Azure Data Lake Analytics](../../integration-services/connection-manager/azure-data-lake-analytics-connection-manager.md).

- **JobName:** especifica o nome do trabalho U-SQL. 
- **AnalyticsUnits:** Especifica a contagem de Unidades de Análise do trabalho U-SQL.
- **Priority:** especifica a prioridade do trabalho U-SQL. A prioridade pode ser definida de 0 a 1000; quanto menor o número, maior a prioridade.
- **RuntimeVersion:** especifica a versão de tempo de execução do Azure Data Lake Analytics do trabalho U-SQL. Ele é definido como "padrão" por padrão. Normalmente, você não precisa alterar essa propriedade.
- **Synchronous:** um valor booliano que especifica se a tarefa aguarda até a execução do trabalho ser concluído ou não. Definido como Ture; a tarefa será ser marcada como tendo êxito depois que o trabalho for concluído. Definido como Falso; a tarefa será marcada como tendo êxito depois que o trabalho passar pela fase de Preparação.

|Valor|Descrição|
|-----------|-----------------|
|True|O resultado da tarefa baseia-se no resultado de execução do trabalho U-SQL. O Trabalho é bem-sucedido--> a Tarefa é bem-sucedida; o Trabalho falha --> a Tarefa falha; a Tarefa é bem-sucedida ou falha--> a Tarefa é concluída.|
|Falso|O resultado da tarefa baseia-se no resultado de envio e preparação do trabalho U-SQL. O envio de trabalho é bem-sucedido e passa pela fase de Preparação--> a Tarefa é bem-sucedida; o Envio do trabalho falha ou o trabalho falha na fase de Preparação--> a Tarefa falha; a Tarefa é bem-sucedida ou falha--> a Tarefa é concluída.|

- **TimeOut:** especifica um tempo limite em segundos para a execução do trabalho. O trabalho será cancelado, e a tarefa será marcada como com falha depois que o trabalho atingir o tempo limite. A propriedade TimeOut não estará disponível se Synchronous for definido como Falso. A propriedade TimeOut não estará disponível se **Synchronous** for definido como **Falso**.

## <a name="parameter-mapping-page-configuration"></a>Configuração de Página de Mapeamento de Parâmetro

Use a página **Mapeamento de Parâmetros** da caixa de diálogo **Editor de Tarefa do Azure Data Lake Analytics** para mapear variáveis para parâmetros (variáveis de U-SQL) no script U-SQL.

- **Nome da Variável:** depois de adicionar um mapeamento de parâmetros clicando em **Adicionar**, selecione uma variável de sistema ou definida pelo usuário na lista ou clique em \<**Nova variável...**> para adicionar uma nova variável usando a caixa de diálogo **Adicionar Variável**. **Tópicos relacionados:** [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md)  

- **Nome do Parâmetro:** forneça um nome de parâmetro/variável no script U-SQL. Verifique se o nome do parâmetro começa com o sinal @, como @Param1. 

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

No exemplo de script acima, os caminhos de entrada e saída são definidos em parâmetros **@in** e **@out**. Os valores para os parâmetros **@in** e **@out** no script U-SQL são passados dinamicamente pela configuração de Mapeamento de Parâmetros.

|Nome da Variável|Nome do parâmetro|
|-------------|--------------|
|Usuário: Variável1|@in|
|Usuário: Variável2|@out| 

## <a name="expression-page-configuration"></a>Configuração de Página de Expressão

Todas as propriedades na configuração de página Geral podem ser atribuídas como uma expressão de propriedade para habilitar a atualização dinâmica da propriedade em tempo de execução. **Tópicos relacionados:** [Usar expressões de propriedade em pacotes](../../integration-services/expressions/use-property-expressions-in-packages.md)

## <a name="see-also"></a>Consulte Também
- [Gerenciador de Conexão do Azure Data Lake Analytics](../../integration-services/connection-manager/azure-data-lake-analytics-connection-manager.md)
- [Tarefa do sistema de arquivos do Azure Data Lake Store](../../integration-services/control-flow/azure-data-lake-store-file-system-task.md)
- [Gerenciador de conexões do Azure Data Lake Store](../../integration-services/connection-manager/azure-data-lake-store-connection-manager.md)

