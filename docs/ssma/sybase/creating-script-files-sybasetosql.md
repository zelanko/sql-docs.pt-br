---
title: Criando arquivos de script (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Configuring Settings
- Sybase Console,Script Commands
- Sybase Console,Script File Validation
- Sybase Console,Server Connection Parameters
ms.assetid: e6baf106-abbd-4200-b3de-33b4b4f1b294
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: e5abea3995ae8b2515c142812ee47498c37497f6
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87931994"
---
# <a name="creating-script-files-sybasetosql"></a>Criar arquivos de script (SybaseToSQL)
A primeira etapa antes de iniciar o aplicativo do console do SSMA é criar o arquivo de script e, se necessário, criar o arquivo de valor da variável e o arquivo de conexão do servidor.  
  
O arquivo de script pode ser dividido em três seções, aula sobre visualização..,:  
  
1.  **configuração:** Permite que o usuário defina os parâmetros de configuração para o aplicativo de console.  
  
2.  **servidores:** Permite que o usuário defina as definições do servidor de origem/destino. Isso também pode estar em um arquivo de conexão de servidor separado.  
  
3.  **comandos de script:** Permite que o usuário execute comandos de fluxo de trabalho do SSMA.  
  
Cada seção é descrita em detalhes abaixo:  
  
## <a name="configuring-sybase-console-settings"></a>Definindo as configurações do console do Sybase  
As configurações de um script são exibidas no arquivo de script do console.  
  
Se qualquer um dos elementos for especificado no nó Configuração, eles serão definidos como a configuração global, ou seja, serão aplicáveis a todos os comandos de script. Esses elementos de configuração também podem ser definidos dentro de cada comando na seção script-Command se o usuário quiser substituir a configuração global.  
  
As opções configuráveis pelo usuário incluem:  
  
1.  **Provedor de janela de saída:** Se o atributo suprimir mensagens for definido como ' true ', as mensagens específicas do comando não serão exibidas no console. A descrição dos atributos é fornecida abaixo:  
  
    -   destino: especifica se a saída precisa ser impressa em um arquivo ou stdout. Isso é falso por padrão.  
  
    -   nome-do-arquivo: o caminho do arquivo (opcional).  
  
    -   suprimir-mensagens: suprime mensagens no console. Isso é ' false ' por padrão.  
  
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
    *or*  
  
    ```xml  
    <...All commands...>  
  
      <output-window  
  
         suppress-messages="<true/false>"   (optional)  
  
         destination="<file/stdout>"        (optional)  
  
         file-name="<file-name>"            (optional)  
  
       />  
  
    </...All commands...>  
    ```  
  
2.  **Provedor de conexão de migração de dados:** Isso especifica qual servidor de origem/destino deve ser considerado para a migração de dados.  Origem-uso-último-usado indica que o último servidor de origem usado é usado para migração de dados. De forma semelhante, use-Last-used indica que o último servidor de destino usado é usado para a migração de dados. O usuário também pode especificar o servidor (origem ou destino) usando os atributos origem-servidor ou destino-servidor.  
  
    Somente um ou outro atributo especificado pode ser usado, ou seja,:  
  
    -   Source-use-Last-used = "true" (padrão) ou Source-Server = "source_servername"  
  
    -   Target-use-Last-used = "true" (padrão) ou target-Server = "target_servername"  
  
    **Exemplo:**  
  
    ```xml  
    <output-providers>  
  
      <data-migration-connection   source-use-last-used="true"  
  
                                   target-server="<target-server-unique-name>"/>  
  
    </output-providers>  
    ```  
    *or*  
  
    ```xml  
    <migrate-data>  
  
      <data-migration-connection   source-server="<source-server-unique-name>"  
  
                                   target-use-last-used="true"/>  
  
    </migrate-data>  
    ```  
  
3.  **Pop-up de entrada do usuário:** Isso permite o tratamento de erros quando os objetos são carregados do banco de dados. O usuário fornece os modos de entrada e, no caso de um erro, o console prossegue conforme o usuário especifica.  
  
    Os modos incluem:  
  
    -   **Ask-usuário-** Solicita que o usuário Continue (' Yes ') ou Error out (' no ').  
  
    -   **erro-** O console exibe um erro e interrompe a execução.  
  
    -   **continuar-** O console prossegue com a execução.  
  
    O modo padrão é **Error**.  
  
    **Exemplo:**  
  
    ```xml  
    <output-providers>  
  
      <user-input-popup mode="<ask-user/continue/error>"/>  
  
    </output-providers>  
    ```  
    *or*  
  
    ```xml  
    <!-- Connect to target database -->  
  
    <connect-target-database server="<target-server-unique-name>">  
  
      <user-input-popup mode="<ask-user/continue/error>"/>  
  
    </connect-target-database>  
    ```  
  
4.  **Reconectar provedor:** Isso permite que o usuário defina as configurações de reconexão caso haja falhas de conexão. Isso pode ser definido para servidores de origem e de destino.  
  
    Os modos de reconexão são:  
  
    -   reconectar-se-para-último-servidor: se a conexão não estiver ativa, ela tentará se reconectar ao último servidor usado no máximo 5 vezes.  
  
    -   gerar-um-erro: se a conexão não estiver ativa, um erro será gerado.  
  
    O modo padrão é **gerar-um-erro**.  
  
    **Exemplo:**  
  
    ```xml  
    <output-providers>  
  
      <reconnect-manager  on-source-reconnect="<reconnect-to-last-used-server/generate-an-error>"  
  
                          on-target-reconnect="<reconnect-to-last-used-server/generate-an-error>"/>  
  
    </output-providers>  
    ```  
    *or*  
  
    ```xml  
    <!--synchronization-->  
  
    <synchronize-target>  
  
      <reconnect-manager on-target-reconnect="reconnect-to-last-used-server"/>  
  
    </synchronize-target>  
    ```  
    *or*  
  
    ```xml  
    <!--data migration-->  
  
    <migrate-data server="<target-server-unique-name>">  
  
      <reconnect-manager  
  
        on-source-reconnect="reconnect-to-last-used-server"  
  
        on-target-reconnect="generate-an-error"/>  
  
    </migrate-data>  
    ```  
  
5.  **Converter provedor de substituição:** Isso permite que o usuário manipule objetos que já estão presentes na metabase de destino. As ações possíveis incluem:  
  
    -   erro: o console do exibe um erro e interrompe a execução.  
  
    -   substituir: substitui os valores de objeto existentes. Essa ação é feita por padrão.  
  
    -   ignorar: o console ignora os objetos que já existem no banco de dados  
  
    -   Ask-User: solicita ao usuário a entrada (' Yes '/' no ')  
  
    **Exemplo:**  
  
    ```xml  
    <output-providers>  
  
      <object-overwrite action="<error/skip/overwrite/ask-user>"/>  
  
    </output-providers>  
    ```  
    *or*  
  
    ```xml  
    <convert-schema object-name="<object-name>">  
  
      <object-overwrite action="<error/skip/overwrite/ask-user>"/>  
  
    </convert-schema>  
    ```  
  
6.  **Falha no provedor de pré-requisitos:** Isso permite que o usuário manipule todos os pré-requisitos necessários para processar um comando. Por padrão, o modo estrito é ' false '. Se estiver definido como ' true ', uma exceção será gerada para falha ao atender aos pré-requisitos.  
  
    **Exemplo:**  
  
    ```xml  
    <output-providers>  
  
      <prerequisites strict-mode="<true/false>"/>  
  
    </output-providers>  
    ```  
  
7.  **Parar operação:** Durante a operação mid, se o usuário quiser interromper a operação, a tecla de atalho **' CTRL + C'** poderá ser usada. O console do SSMA para Sybase aguardará a conclusão da operação e encerrará a execução do console.  
  
    Se o usuário quiser interromper a execução imediatamente, então, a tecla de atalho **' CTRL + C '** poderá ser pressionada novamente para o encerramento abrupta do aplicativo de console do SSMA  
  
8.  **Provedor de progresso:** Informa o progresso de cada comando do console. Isso está desabilitado por padrão. Os atributos de relatório de progresso incluem:  
  
    -   Desligar  
  
    -   a cada-1%  
  
    -   a cada-2%  
  
    -   a cada-5%  
  
    -   a cada-10%  
  
    -   a cada-20%  
  
    **Exemplo:**  
  
    ```xml  
    <output-providers>  
  
      <progress-reporting enable="<true/false>"           (optional)  
  
                          report-messages="<true/false>"  (optional)  
  
                          report-progress="every-1%/every-2%/every-5%/every-10%/every-20%/off" (optional)/>  
  
    </output-providers>  
    ```  
    *or*  
  
    ```xml  
    <...All commands...>  
  
      <progress-reporting  
  
        enable="<true/false>"          (optional)  
  
        report-messages="<true/false>" (optional)  
  
        report-progress="every-1%/every-2%/every-5%/every-10%/every-20%/off (optional)/>  
  
    </...All commands...>  
    ```  
  
9. **Detalhes do agente:** Define o nível de detalhes do log. Isso corresponde à opção todas as categorias na interface do usuário. Por padrão, o nível de detalhes do log é "Error".  
  
    As opções de nível de agente incluem:  
  
    -   fatal-erro: somente mensagens fatais-erro são registradas.  
  
    -   erro: somente mensagens de erro e fatal são registradas.  
  
    -   Aviso: todos os níveis, exceto depuração e mensagens de informações, são registrados.  
  
    -   informações: todos os níveis, exceto as mensagens de depuração, são registrados.  
  
    -   depuração: todos os níveis de mensagens registradas.  
  
    > [!NOTE]  
    > As mensagens obrigatórias são registradas em qualquer nível.  
  
    **Exemplo:**  
  
    ```xml  
    <output-providers>  
  
      <log-verbosity level="fatal-error/error/warning/info/debug"/>  
  
    </output-providers>  
    ```  
    *or*  
  
    ```xml  
    <...All commands...>  
  
      <log-verbosity level="fatal-error/error/warning/info/debug"/>  
  
    </...All commands...>  
    ```  
  
10. **Substituir senha criptografada:** Se for ' true ', a senha de texto não criptografada especificada na seção de definição de servidor do arquivo de conexão do servidor ou no arquivo de script substituirá a senha criptografada armazenada no armazenamento protegido, se existir. Se nenhuma senha for especificada em texto não criptografado, será solicitado que o usuário insira a senha.  
  
    Aqui, surgem dois casos:  
  
    1.  Se a opção Override for **false**, a ordem de pesquisa será Protected Storage- &gt; script File- &gt; Server Connection File- &gt; prompt User.  
  
    2.  Se a opção substituir for **verdadeira**, a ordem de pesquisa será arquivo de script- &gt; arquivo de conexão do servidor- &gt; avisar usuário.  
  
    **Exemplo:**  
  
    ```xml  
    <output-providers>  
  
      <encrypted-password override="<true/false>"/>  
  
    </output-providers>  
    ```  
  
A opção não configurável é:  
  
-   **Máximo de tentativas de reconexão:** Quando uma conexão estabelecida atinge o tempo limite ou é interrompida devido a uma falha de rede, o servidor precisa ser reconectado. As tentativas de reconexão têm permissão para um máximo de **5** repetições após o qual o console do executa automaticamente a reconexão. A facilidade de reconexão automática reduz seu esforço na execução do script.  
  
## <a name="server-connection-parameters"></a>Parâmetros de conexão do servidor  
Os parâmetros de conexão do servidor podem ser definidos no arquivo de script ou no arquivo de conexão do servidor. Veja a seção [criando os arquivos de conexão do servidor &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md) para obter mais detalhes  
  
## <a name="script-commands"></a>Comandos de script  
O arquivo de script contém uma sequência de comandos de fluxo de trabalho de migração no formato XML. O aplicativo de console do SSMA processa a migração na ordem dos comandos que aparecem no arquivo de script.  
  
Por exemplo, uma migração de dados típica de uma tabela específica em um banco de dados Sybase segue a hierarquia de: Database- &gt; Schema- &gt; Table.  
  
Quando todos os comandos no arquivo de script são executados com êxito, o aplicativo do console do SSMA sai e retorna o controle para o usuário. O conteúdo de um arquivo de script é mais ou menos estático com informações de variáveis contidas em um [valor de variável files](creating-variable-value-files-sybasetosql.md) ou em uma seção separada dentro do arquivo de script para valores de variáveis.  
  
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
Modelos que consistem em três arquivos de script (para executar vários cenários), arquivo de valor de variável e um arquivo de conexão de servidor são fornecidos na pasta de scripts de console de exemplo do diretório do produto:  
  
-   AssessmentReportGenerationSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
-   SqlStatementConversionSample.xml  
  
-   VariableValueFileSample.xml  
  
-   ServersConnectionFileSample.xml  
  
Você pode executar os modelos (arquivos) depois de alterar os parâmetros exibidos aqui para fins de relevância.  
  
A lista completa de comandos de script pode ser encontrada na [execução do console do SSMA &#40;SybaseToSQL&#41;](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md)  
  
## <a name="script-file-validation"></a>Validação de arquivo de script  
O usuário pode facilmente validar seu arquivo de script em relação ao **2ssconsolescriptschema. xsd do** arquivo de definição de esquema disponível na pasta ' schemas '  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa na operação do console é [criar arquivos de valor de variável &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md).  
  
## <a name="see-also"></a>Consulte Também  
[Criando arquivos de valor de variável &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)  
  
