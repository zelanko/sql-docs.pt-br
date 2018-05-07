---
title: Criando arquivos de Script (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Script File Creation, Configuring Oracle Console Settings
- Script File Creation, Non-Configurable option
- Script File Creation, Script File Validation
ms.assetid: 55e5bc68-3040-4f07-bb00-0408a17c9821
caps.latest.revision: 37
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 2b2e2623ad486466c7e9e1482d41cc2031e1d4c3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="creating-script-files-oracletosql"></a>Criando arquivos de Script (OracleToSQL)
A primeira etapa antes de iniciar o aplicativo de console SSMA é criar o arquivo de script e, se necessário criar o arquivo de valor da variável e o arquivo de conexão de servidor.  
  
O arquivo de script pode ser dividido em três seções, viz..,:  
  
1.  **configuração:** permite ao usuário definir os parâmetros de configuração para o aplicativo de console.  
  
2.  **servidores:** permite ao usuário definir definições de servidor de origem/destino. Isso também pode ser em um arquivo de conexão de servidor separado.  
  
3.  **comandos de script:** permite que o usuário executar comandos de fluxo de trabalho do SSMA.  
  
Cada seção é descrita em detalhes a seguir:  
  
## <a name="configuring-oracle-console-settings"></a>Definindo as configurações de Console do Oracle  
As configurações de um script são exibidas no arquivo de script de console.  
  
Se qualquer um dos elementos são especificados no nó de configuração, eles serão definidos como a configuração global ou seja, elas são aplicáveis a todos os comandos de script. Esses elementos de configuração também podem ser definidos dentro de cada comando na seção do comando de script se o usuário deseja substituir a configuração global.  
  
As opções configuráveis pelo usuário incluem:  
  
1.  **Provedor de janela de saída:** se suprimir mensagens atributo for definido como 'true', o comando específico mensagens não são exibidas no console. A descrição de atributos é fornecida abaixo:  
  
    -   destino: Especifica se a saída deve obter impresso em um arquivo ou stdout. Isso é false por padrão.  
  
    -   nome do arquivo: O caminho do arquivo (opcional).  
  
    -   Suprimir mensagens: suprime mensagens no console. Isso é 'false' por padrão.  
  
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
    <…All commands…>  
  
      <output-window  
  
         suppress-messages="<true/false>"   (optional)  
  
         destination="<file/stdout>"        (optional)  
  
         file-name="<file-name>"            (optional)  
  
       />  
  
    </…All commands…>  
    ```  
  
2.  **Provedor de Conexão de migração de dados:** Especifica que o servidor de origem/destino seja considerado para migração de dados.  Origem-uso-usado por último indica que o último servidor de origem usado é usado para a migração de dados. Da mesma forma destino-uso-usado por último indica que o último servidor de destino usado é usado para a migração de dados. O usuário também pode especificar o servidor (de origem ou de destino) usando o servidor de origem de atributos ou o servidor de destino.  
  
    Apenas um ou outro atributo especificado pode ser usado por exemplo:  
  
    -   origem-uso-usado por último = "true" (padrão) ou o servidor de origem = "source_servername"  
  
    -   destino-uso-usado por último = "true" (padrão) ou o servidor de destino = "target_servername"  
  
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
  
3.  **Pop-up entrada do usuário:** Isso permite a manipulação de erros, quando os objetos são carregados do banco de dados. O usuário fornece os modos de entrada e, no caso de erro, o console continua conforme o usuário especifica.  
  
    Os modos incluem:  
  
    -   **Pergunte-usuário -** solicita ao usuário continue('yes') ou erro ('não').  
  
    -   **Erro -** o console exibe um erro e interromperá a execução.  
  
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
  
4.  **Provedor de reconexão:** Isso permite ao usuário definir a reconexão configurações caso de falhas de conexão. Isso pode ser definido para servidores de origem e destino.  
  
    Os modos de reconexão são:  
  
    -   reconectar-se a última-usado-servidor: se a conexão não está ativo, ele tentará reconectar-se para o último servidor usado no máximo 5 vezes.  
  
    -   Gerar um erro: se a conexão não está ativa, um erro será gerado.  
  
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
  
5.  **Provedor de substituição de conversor:** Isso permite que o usuário lidar com objetos que já estão presentes no destino de metabase. As ações possíveis incluem:  
  
    -   Erro: O console exibe um erro e interromperá a execução.  
  
    -   Substituir: substitui valores existentes do objeto. Essa ação é executada por padrão.  
  
    -   Ignorar: O console irá ignorar os objetos que já existem no banco de dados  
  
    -   Peça ao usuário: solicita a entrada do usuário ('Sim' / 'não')  
  
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
  
6.  **Provedor de pré-requisitos com falha:** Isso permite que o usuário lidar com todos os pré-requisitos necessários para um comando de processamento. Por padrão, o modo estrito é 'false'. Se ele for definido como 'true', uma exceção será gerado para falha de atender aos pré-requisitos.  
  
    **Exemplo:**  
  
    ```xml  
    <output-providers>  
  
      <prerequisites strict-mode="<true/false>"/>  
  
    </output-providers>  
    ```  
  
7.  **Operação de interrupção:** durante a operação intermediária, se o usuário deseja parar a operação, em seguida, **'Ctrl + C'** tecla de acesso pode ser usada. SSMA para o Console do Oracle aguardará a conclusão da operação e termina a execução do console.  
  
    Se o usuário deseja interromper a execução imediatamente, em seguida, **'Ctrl + C'** tecla de acesso pode ser pressionada novamente para término abrupto de aplicativo do Console SSMA.  
  
8.  **Provedor de progresso:** informa o progresso de cada comando de console. Isso é desabilitado por padrão. Os relatórios de progresso atributos incluem:  
  
    -   off  
  
    -   cada 1%  
  
    -   a cada 2%  
  
    -   a cada 5%  
  
    -   a cada 10%  
  
    -   cada 20%  
  
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
    <…All commands…>  
  
      <progress-reporting  
  
        enable="<true/false>"            (optional)  
  
        report-messages="<true/false>"   (optional)  
  
        report-progress="every-1%/every-2%/every-5%/every-10%/every-20%/off"     (optional)/>  
  
    </…All commands…>  
    ```  
  
9. **Detalhes do agente de log:** conjuntos de nível de detalhes de log. Isso corresponde com a opção de todas as categorias na interface de usuário. Por padrão, o nível de detalhes de log é "error".  
  
    As opções de nível de agente de log incluem:  
  
    -   Erro fatal: somente-erro fatal são registradas.  
  
    -   Erro: somente mensagens de erro e o erro fatal são registradas.  
  
    -   Aviso: todos os níveis, exceto as mensagens de depuração e informações são registrados.  
  
    -   INFO: todos os níveis, exceto as mensagens de depuração são registradas.  
  
    -   Depurar: todos os níveis de mensagens registradas.  
  
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
    <…All commands…>  
  
      <log-verbosity level="fatal-error/error/warning/info/debug"/>  
  
    </…All commands…>  
    ```  
  
10. **Senha de criptografado de substituição:** se 'true', a senha de texto não criptografado especificado na seção de definição de servidor de arquivo de conexão do servidor ou no arquivo de script, substituições a senha criptografada armazenada no armazenamento protegido se existe. Se nenhuma senha for especificada em texto não criptografado, o usuário será solicitado a inserir a senha.  
  
    Aqui surgem dois casos:  
  
    1.  Se substituir a opção é **false**, a ordem de pesquisa será protegido armazenamento -&gt;arquivo de Script -&gt;arquivo de Conexão de servidor -&gt; solicitar ao usuário.  
  
    2.  Se substituir a opção é **true**, será a ordem de pesquisa de arquivo de Script -&gt;arquivo de Conexão de servidor -&gt;solicitar ao usuário.  
  
    **Exemplo:**  
  
    ```xml  
    <output-providers>  
  
      <encrypted-password override="<true/false>"/>  
  
    </output-providers>  
    ```  
  
A opção não configurável é:  
  
-   **Número máximo de tentativas de reconexão:** quando uma conexão estabelecida expira ou quebras devido à falha de rede, o servidor é necessário ser reconectado. As tentativas de reconexão são permitidas para um máximo de **5** tentativas após o qual o console executa automaticamente a reconexão. O recurso de reconexão automática reduz o esforço de executar novamente o script.  
  
## <a name="server-connection-parameters"></a>Parâmetros de Conexão de servidor  
Parâmetros de conexão de servidor podem ser definidos no arquivo de script ou no arquivo de conexão do servidor. Consulte o [criar os arquivos de Conexão de servidor &#40;OracleToSQL&#41; ](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md) seção para obter mais detalhes.  
  
## <a name="script-commands"></a>Comandos de script  
O arquivo de script contém uma sequência de comandos de fluxo de trabalho de migração no formato XML. O aplicativo de console SSMA processa a migração na ordem os comandos que aparecem no arquivo de script.  
  
Por exemplo, uma migração de dados típicos de uma tabela específica no banco de dados Oracle segue a hierarquia de: esquema -&gt; tabela.  
  
Quando todos os comandos no arquivo de script são executados com êxito, o aplicativo de console SSMA é encerrado e retorna o controle ao usuário. O conteúdo de um arquivo de script é mais ou menos estático com informações de variáveis contidas em um [criando arquivos de valores de variável &#40;OracleToSQL&#41; ](../../ssma/oracle/creating-variable-value-files-oracletosql.md) ou, em uma seção separada dentro do arquivo de script para valores de variáveis.  
  
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
Modelos que consiste em 3 de arquivos de script (para executar vários cenários), arquivo de valor da variável e um arquivo de conexão de servidor são fornecidos na pasta Scripts do Console de exemplo do diretório do produto:  
  
-   AssessmentReportGenerationSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
-   SqlStatementConversionSample.xml  
  
-   VariableValueFileSample.xml  
  
-   ServersConnectionFileSample.xml  
  
Você pode executar os modelos (arquivos) depois de alterar os parâmetros exibidos para relevância.  
  
Lista completa de comandos de script pode ser encontrada em [executando o Console SSMA &#40;OracleToSQL&#41;](../../ssma/oracle/executing-the-ssma-console-oracletosql.md)  
  
## <a name="script-file-validation"></a>Validação de arquivo de script  
O usuário pode facilmente validar seu arquivo de script no arquivo de definição de esquema **'O2SSConsoleScriptSchema.xsd'** disponíveis na pasta 'Esquemas'.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa no operando o console é [criando arquivos de valor variável &#40;OracleToSQL&#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md).  
  
## <a name="see-also"></a>Consulte também  
[Criando arquivos do valor da variável &#40;OracleToSQL&#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md)  
  
