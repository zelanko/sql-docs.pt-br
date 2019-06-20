---
title: Criar arquivos de Script (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Script File Creation, Configuring Oracle Console Settings
- Script File Creation, Non-Configurable option
- Script File Creation, Script File Validation
ms.assetid: 55e5bc68-3040-4f07-bb00-0408a17c9821
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: fe8dd1ebcc6604b8cff514cff3628abc23275517
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63287250"
---
# <a name="creating-script-files-oracletosql"></a>Criar arquivos de script (OracleToSQL)
A primeira etapa antes de iniciar o aplicativo de console do SSMA é criar o arquivo de script e se for necessário criar o arquivo de valor da variável e o arquivo de conexão do servidor.  
  
O arquivo de script pode ser dividido em três seções, sobre visualização..,:  
  
1.  **config:** Permite que o usuário definir os parâmetros de configuração para o aplicativo de console.  
  
2.  **servers:** Permite que o usuário defina definições de servidor de origem/destino. Isso também pode ser em um arquivo de conexão de servidor separado.  
  
3.  **script-commands:** Permite que o usuário execute comandos de fluxo de trabalho do SSMA.  
  
Cada seção é descrita em detalhes abaixo:  
  
## <a name="configuring-oracle-console-settings"></a>Definindo as configurações de Console do Oracle  
As configurações de um script são exibidas no arquivo de script de console.  
  
Se qualquer um dos elementos são especificados no nó de configuração, elas serão definidas como a configuração global ou seja, eles são aplicáveis a todos os comandos de script. Esses elementos de configuração também podem ser definidos dentro de cada comando na seção de comando de script se o usuário deseja substituir a configuração global.  
  
As opções configuráveis pelo usuário incluem:  
  
1.  **Provedor de janela de saída:** Se o atributo de suprimir as mensagens é definido como 'true', específicos do comando mensagens não são exibidas no console. A descrição de atributos é fornecida abaixo:  
  
    -   Destino: Especifica se a saída deve obter impresso em um arquivo ou o stdout. Isso é false por padrão.  
  
    -   nome do arquivo: O caminho do arquivo (opcional).  
  
    -   suppress-messages: Suprime as mensagens do console. Isso é 'false', por padrão.  
  
    **Exemplo:**  
  
    ```xml  
    <output-providers>  
  
      <output-window  
  
        suppress-messages="<true/false>"   (optional)  
  
        destination="<file/stdout>"        (optional)  
  
        file-name="<file-name>"            (optional)  
  
       />  
  
    </output-providers>  
    ```  
    *ou*  
  
    ```xml  
    <...All commands...>  
  
      <output-window  
  
         suppress-messages="<true/false>"   (optional)  
  
         destination="<file/stdout>"        (optional)  
  
         file-name="<file-name>"            (optional)  
  
       />  
  
    </...All commands...>  
    ```  
  
2.  **Provedor de Conexão de migração de dados:** Isso especifica que o servidor de origem/destino seja considerado para a migração de dados.  Código-fonte-use-last-used indica que o último servidor de origem usados é usado para a migração de dados. Da mesma forma destino-use-last-used indica que o último servidor de destino usado é usado para a migração de dados. O usuário também pode especificar o servidor (origem ou destino) usando o servidor de origem de atributos ou o servidor de destino.  
  
    Apenas um ou outro atributo especificado pode ser usado ou seja:  
  
    -   source-use-last-used="true" (default) or source-server="source_servername"  
  
    -   target-use-last-used="true" (default) or target-server="target_servername"  
  
    **Exemplo:**  
  
    ```xml  
    <output-providers>  
  
      <data-migration-connection source-use-last-used="true"  
  
                                 target-server="<target-server-unique-name>"/>  
  
    </output-providers>  
    ```  
    *ou*  
  
    ```xml  
    <migrate-data>  
  
      <data-migration-connection   source-server="<source-server-unique-name>"  
  
                                   target-use-last-used="true"/>  
  
    </migrate-data>  
    ```  
  
3.  **Popup de entrada do usuário:** Isso permite o tratamento de erros, quando os objetos são carregados do banco de dados. O usuário fornece os modos de entrada e, em caso de erro, o console continua conforme o usuário especifica.  
  
    Os modos incluem:  
  
    -   **Pergunte-usuário-** solicita que o usuário continue('yes') ou ocorre um erro ('não').  
  
    -   **Erro -** o console exibirá um erro e interrompe a execução.  
  
    -   **continuar-** console prossegue com a execução.  
  
    O modo padrão é **erro**.  
  
    **Exemplo:**  
  
    ```xml  
    <output-providers>  
  
      <user-input-popup mode="<ask-user/continue/error>"/>  
  
    </output-providers>  
    ```  
    *ou*  
  
    ```xml  
    <!-- Connect to target database -->  
  
    <connect-target-database server="<target-server-unique-name>">  
  
      <user-input-popup mode="<ask-user/continue/error>"/>  
  
    </connect-target-database>  
    ```  
  
4.  **Provedor de reconexão:** Isso permite que o usuário defina a reconexão configurações caso de falhas de conexão. Isso pode ser definido para servidores de origem e destino.  
  
    Os modos de reconexão são:  
  
    -   reconnect-to-last-used-server: Se a conexão não está ativo, ele tentará reconectar-se para o último servidor usado no máximo 5 vezes.  
  
    -   Gerar-um-erro: Se a conexão não está ativa, um erro será gerado.  
  
    O modo padrão é **gerar um erro**.  
  
    **Exemplo:**  
  
    ```xml  
    <output-providers>  
  
      <reconnect-manager on-source-reconnect="<reconnect-to-last-used-server/generate-an-error>"  
  
                         on-target-reconnect="<reconnect-to-last-used-server/generate-an-error>"/>  
  
    </output-providers>  
    ```  
    *ou*  
  
    ```xml  
    <!--synchronization-->  
  
    <synchronize-target>  
  
      <reconnect-manager on-target-reconnect="reconnect-to-last-used-server"/>  
  
    </synchronize-target>  
    ```  
    *ou*  
  
    ```xml  
    <!--data migration-->  
  
    <migrate-data server="<target-server-unique-name>">  
  
      <reconnect-manager  
  
        on-source-reconnect="reconnect-to-last-used-server"  
  
        on-target-reconnect="generate-an-error"/>  
  
    </migrate-data>  
    ```  
  
5.  **Conversor de substituir o provedor:** Isso permite que o usuário lidar com objetos que já estão presentes no destino de metabase. As ações possíveis incluem:  
  
    -   Erro: O console exibe um erro e interrompe a execução.  
  
    -   overwrite: Substitui os valores de objeto existentes. Essa ação é executada por padrão.  
  
    -   Ignore: O console irá ignorar os objetos que já existem no banco de dados  
  
    -   Pergunte-usuário: Solicita que a entrada do usuário ('Sim' / 'não')  
  
    **Exemplo:**  
  
    ```xml  
    <output-providers>  
  
      <object-overwrite action="<error/skip/overwrite/ask-user>"/>  
  
    </output-providers>  
    ```  
    *ou*  
  
    ```xml  
    <convert-schema object-name="<object-name>">  
  
      <object-overwrite action="<error/skip/overwrite/ask-user>"/>  
  
    </convert-schema>  
    ```  
  
6.  **Falha na pré-requisitos provedor:** Isso permite que o usuário lidar com todos os pré-requisitos que são necessários para processar um comando. Por padrão, o modo estrito é 'false'. Se ele for definido como 'true', uma exceção será gerado para falha de atender aos pré-requisitos.  
  
    **Exemplo:**  
  
    ```xml  
    <output-providers>  
  
      <prerequisites strict-mode="<true/false>"/>  
  
    </output-providers>  
    ```  
  
7.  **Pare operação:** Durante a operação intermediária, se o usuário deseja parar a operação, então **'Ctrl + C'** tecla de acesso pode ser usada. O SSMA para Oracle Console aguardará a conclusão da operação e finaliza a execução do console.  
  
    Se o usuário deseja parar a execução imediatamente, em seguida, **'Ctrl + C'** tecla de acesso pode ser pressionada novamente para término abrupto do aplicativo de Console do SSMA.  
  
8.  **Provedor de progresso:** Informa o progresso de cada comando de console. Isso está desabilitado por padrão. Os atributos de relatório de progresso compreendem:  
  
    -   off  
  
    -   todos - 1%  
  
    -   todos - 2%  
  
    -   todos - 5%  
  
    -   todos - 10%  
  
    -   todos - 20%  
  
    **Exemplo:**  
  
    ```xml  
    <output-providers>  
  
      <progress-reporting enable="<true/false>"            (optional)  
  
                          report-messages="<true/false>"   (optional)  
  
                          report-progress="every-1%/every-2%/every-5%/every-10%/every-20%/off" (optional)/>  
  
    </output-providers>  
    ```  
    *ou*  
  
    ```xml  
    <...All commands...>  
  
      <progress-reporting  
  
        enable="<true/false>"            (optional)  
  
        report-messages="<true/false>"   (optional)  
  
        report-progress="every-1%/every-2%/every-5%/every-10%/every-20%/off"     (optional)/>  
  
    </...All commands...>  
    ```  
  
9. **Detalhamento do agente de log:** Conjuntos de nível de detalhes de log. Isso corresponde com a opção de todas as categorias na interface do usuário. Por padrão, o nível de detalhamento do log é "error".  
  
    As opções de nível de agente de log incluem:  
  
    -   fatal-error: Somente as mensagens de erro fatal são registradas.  
  
    -   Erro: Apenas as mensagens de erro e fatal erro são registradas.  
  
    -   Aviso: Todos os níveis, exceto as mensagens de depuração e as informações são registradas.  
  
    -   info: Todos os níveis, exceto as mensagens de depuração são registrados.  
  
    -   Depure: Todos os níveis de mensagens registradas.  
  
    > [!NOTE]  
    > Obrigatórias mensagens são registradas em qualquer nível.  
  
    **Exemplo:**  
  
    ```xml  
    <output-providers>  
  
      <log-verbosity level="fatal-error/error/warning/info/debug"/>  
  
    </output-providers>  
    ```  
    *ou*  
  
    ```xml  
    <...All commands...>  
  
      <log-verbosity level="fatal-error/error/warning/info/debug"/>  
  
    </...All commands...>  
    ```  
  
10. **Substitua a senha criptografada:** Se for 'true', a senha de texto não criptografado especificado na seção de definição de servidor do arquivo de conexão do servidor ou no arquivo de script, substitui a senha criptografada armazenada no armazenamento protegido se existe. Se nenhuma senha for especificada em texto não criptografado, o usuário é solicitado a inserir a senha.  
  
    Aqui surgem dois casos:  
  
    1.  Se substituir a opção é **falsos**, a ordem de pesquisa será protegido armazenamento -&gt;arquivo de Script -&gt;arquivo de Conexão do servidor -&gt; solicitar ao usuário.  
  
    2.  Se substituir a opção é **verdadeira**, será a ordem de pesquisa de arquivo de Script -&gt;arquivo de Conexão do servidor -&gt;solicitar ao usuário.  
  
    **Exemplo:**  
  
    ```xml  
    <output-providers>  
  
      <encrypted-password override="<true/false>"/>  
  
    </output-providers>  
    ```  
  
A opção não configurável é:  
  
-   **Máximo a tentativas de reconexão:** Quando uma conexão estabelecida expira ou é interrompida devido a falha de rede, o servidor é necessário ser reconectado. As tentativas de reconexão são permitidas no máximo **5** novas tentativas depois disso, o console executa automaticamente a reconexão. O recurso de reconexão automática reduz o esforço em executar novamente o script.  
  
## <a name="server-connection-parameters"></a>Parâmetros de Conexão do servidor  
Parâmetros de conexão de servidor podem ser definidos no arquivo de script ou no arquivo de conexão do servidor. Consulte a [criar os arquivos de Conexão de servidor &#40;OracleToSQL&#41; ](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md) para obter mais detalhes.  
  
## <a name="script-commands"></a>Comandos de script  
O arquivo de script contém uma sequência de comandos de fluxo de trabalho de migração no formato XML. O aplicativo de console do SSMA processa a migração na ordem os comandos que aparecem no arquivo de script.  
  
Por exemplo, uma migração de dados típicos de uma tabela específica no banco de dados Oracle segue a hierarquia de: Esquema -&gt; tabela.  
  
Quando todos os comandos no arquivo de script são executados com êxito, o aplicativo de console do SSMA é encerrado e retorna o controle para o usuário. O conteúdo de um arquivo de script é mais ou menos estático com informações de variáveis contidas em uma [criando arquivos de valor da variável &#40;OracleToSQL&#41; ](../../ssma/oracle/creating-variable-value-files-oracletosql.md) ou, em uma seção separada dentro do arquivo de script para valores de variáveis.  
  
**Exemplo:**  
  
```xml  
<!--Sample of script file commands -->  
  
<ssma-script-file>  
  
  <script-commands>  
  
    <create-new-project project-folder="<project-folder>"  
  
                        project-name="<project-name>"  
  
                        overwrite-if-exists="<true/false>"/>  
  
    <connect-source-database server="<source-server-unique-name>"/>  
  
    <save-project/>  
  
    <close-project/>  
  
  </script-commands>  
  
</ssma-script-file>  
```  
Modelos consiste em 3 arquivos de script (para executar vários cenários), arquivo de valor da variável e um arquivo de conexão de servidor são fornecidos na pasta Scripts do Console de exemplo do diretório do produto:  
  
-   AssessmentReportGenerationSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
-   SqlStatementConversionSample.xml  
  
-   VariableValueFileSample.xml  
  
-   ServersConnectionFileSample.xml  
  
Você pode executar os modelos (arquivos) depois de alterar os parâmetros exibidos para relevância.  
  
Lista completa dos comandos de script pode ser encontrada no [executar o Console do SSMA &#40;OracleToSQL&#41;](../../ssma/oracle/executing-the-ssma-console-oracletosql.md)  
  
## <a name="script-file-validation"></a>Validação do arquivo de script  
O usuário pode validar com facilidade seu arquivo de script no arquivo de definição de esquema **'O2SSConsoleScriptSchema.xsd'** disponível na pasta "Esquemas".  
  
## <a name="next-step"></a>Próxima etapa  
É a próxima etapa no operando o console [criando arquivos de valor de variável &#40;OracleToSQL&#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md).  
  
## <a name="see-also"></a>Consulte também  
[Criando arquivos de valor da variável &#40;OracleToSQL&#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md)  
  
