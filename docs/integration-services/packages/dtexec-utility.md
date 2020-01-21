---
title: Utilitário dtexec | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7b6867fa-1039-49b3-90fb-85b84678a612
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b27fc68fc3c7685583248b39a7c27d4d33efa38c
ms.sourcegitcommit: e0067f3687003e1b59a83619fdd19b666cf61e10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2019
ms.locfileid: "74249737"
---
# <a name="dtexec-utility"></a>Utilitário dtexec

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  O utilitário de prompt de comando **dtexec** é usado para configurar e executar pacotes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. O utilitário **dtexec** fornece acesso a toda a configuração e recursos de execução de pacotes, como parâmetros, conexões, propriedades, variáveis, logs e indicadores de progresso. O utilitário **dtexec** permite carregar pacotes destas origens: do servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], de um arquivo de projeto .ispac, de um banco de dados do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], do Armazenamento de Pacotes do [!INCLUDE[ssIS](../../includes/ssis-md.md)] e do sistema de arquivos.  
  
> **OBSERVAÇÃO:** Quando você usa a versão atual do utilitário **dtexec** para executar um pacote criado por uma versão anterior do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], o utilitário atualiza o pacote temporariamente para o formato do pacote atual. No entanto, você não pode usar o utilitário **dtexec** para salvar o pacote atualizado. Para saber mais sobre como atualizar permanentemente um pacote para o a versão atual, confira [Upgrade Integration Services Packages](../../integration-services/install-windows/upgrade-integration-services-packages.md).  
  
 Este tópico inclui as seções a seguir:  
  
-   [Serviço do Integration Services e arquivo de projeto](#server)  
  
-   [Considerações sobre a instalação em computadores de 64 bits](#bit)  
  
-   [Considerações em computadores com instalações lado a lado](#side)  
  
-   [Fases de execução](#phases)  
  
-   [Códigos de saída retornados](#exit)  
  
-   [Regras de sintaxe](#syntaxRules)  
  
-   [Usando dtexec a partir do xp_cmdshell](#cmdshell)  

-   [Usanr dtexec no Bash](#bash)
  
-   [Sintaxe](#syntax)  
  
-   [Parâmetros](#parameter)  
  
-   [Comentários](#remark)  
  
-   [Exemplos](#example)  
  
##  <a name="server"></a> Serviço do Integration Services e arquivo de projeto  
 Quando você usa o **dtexec** para executar pacotes no servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], o **dtexec** chama os procedimentos armazenados [catalog.create_execution &#40;banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md), [catalog.set_execution_parameter_value &#40;banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md) e [catalog.start_execution &#40;banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md) para criar uma execução, definir valores de parâmetros e iniciar a execução. Todos os logs de execução podem ser consultados do servidor nas exibições relacionadas ou usando relatórios padrão disponíveis no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para saber mais sobre os relatórios, consulte [Relatórios do servidor do Integration Services](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports).  
  
 Veja a seguir um exemplo de execução de um pacote no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
```  
DTExec /ISSERVER "\SSISDB\folderB\Integration Services Project17\Package.dtsx" /SERVER "." /Envreference 2 /Par "$Project::ProjectParameter(Int32)";1 /Par "Parameter(Int32)";21 /Par "CM.sqlcldb2.SSIS_repro.InitialCatalog";ssisdb /Par "$ServerOption::SYNCHRONIZED(Boolean)";True  
```  
  
 Quando você usar **dtexec** para executar um pacote do arquivo de projeto .ispac, as opções relacionadas serão: /Proj[ect] e /Pack[age], que são usadas para especificar o caminho de projeto e nome de fluxo de pacote. Quando você converte um projeto ao modelo de implantação de projeto executando o **Assistente de Conversão de Projeto do Integration Services** do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o assistente gera um arquivo de projeto .ispac. Para obter mais informações, consulte [Implantar projetos e pacotes do SSIS (Integration Services)](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md).  
  
 Você pode usar o **dtexec** com ferramentas de agendamento de terceiros para agendar pacotes que são implantados no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
##  <a name="bit"></a> Considerações sobre a instalação em computadores de 64 bits  
 Em um computador de 64 bits, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] instala a versão de 64 bits do utilitário **dtexec** (dtexec.exe). Se for necessário executar alguns pacotes no modo de 32 bits, você precisará instalar a versão de 32 bits do utilitário **dtexec** . Para instalar a versão de 32 bits do utilitário **dtexec** , você deve selecionar Ferramentas de Cliente ou [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] durante a instalação.  
  
 Por padrão, um computador de 64 bits que tem as versões de 64 e de 32 bits de um prompt de comando do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] instaladas executará a versão de 32 bits no prompt de comando. A versão de 32 bits é executada porque o caminho do diretório da versão de 32 bits aparece na variável de ambiente PATH antes do caminho do diretório da versão de 64 bits. (Normalmente, o caminho do diretório de 32 bits é *\<drive>* :\Program Files(x86)\Microsoft SQL Server\110\DTS\Binn, enquanto o caminho do diretório de 64 bits é *\<drive>* :\Program Files\Microsoft SQL Server\110\DTS\Binn.)  
  
> **OBSERVAÇÃO:** Se você usar o SQL Server Agent para executar o utilitário, o SQL Server Agent usará automaticamente a versão de 64 bits do utilitário. O SQL Server Agent usa o Registro, não a variável de ambiente PATH, para localizar o executável correto do utilitário.  
  
 Para garantir que a versão de 64 bits do utilitário no prompt de comando seja executada, execute uma das seguintes ações:  
  
-   Abra uma janela do Prompt de Comando, altere para o diretório que contém a versão de 64 bits do utilitário ( *\<drive>* :\Program Files\Microsoft SQL Server\110\DTS\Binn) e execute o utilitário nesse local.  
  
-   No prompt de comando, execute o utilitário inserindo o caminho completo ( *\<drive>* :\Program Files\Microsoft SQL Server\110\DTS\Binn) para a versão de 64 bits do utilitário.  
  
-   Altere permanentemente a ordem dos caminhos na variável de ambiente PATH colocando o caminho de 64 bits ( *\<drive>* :\Program Files\Microsoft SQL Server\110\DTS\Binn) antes do caminho de 32 bits ( *\<drive>* :\ Program Files(x86)\Microsoft SQL Server\110\DTS\Binn) na variável.  
  
##  <a name="side"></a> Considerações em computadores com instalações lado a lado  
 Quando o [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] é instalado em um computadou o com o [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] ou o [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] instalado, várias versões do utilitário **dtexec** são instaladas.  
  
 Para garantir a execução da versão correta do utilitário, no prompt de comando, execute o utilitário inserindo o caminho completo ( *\<drive>* :\Program Files\Microsoft SQL Server\\<version\>\DTS\Binn).  
  
##  <a name="phases"></a> Fases de execução  
 O utilitário passa por quatro fases à medida que é executado. As fases são as seguintes:  
  
1.  Fase de fornecimento de comando: o prompt de comando lê a lista de opções e argumentos que foram especificados. Todas as fases subsequentes serão ignoradas se uma opção **/?** ou **/HELP** for encontrada.  
  
2.  Fase de carga do pacote: o pacote especificado pela opção **/SQL**, **/FILE**ou **/DTS** é carregado.  
  
3.  Fase de configuração: as opções são processadas nesta ordem:  
  
    -   Opções que definem sinalizadores, variáveis e propriedades do pacote.  
  
    -   Opções que verificam a versão e a compilação do pacote.  
  
    -   Opções que configuram o comportamento de tempo de execução do utilitário, como a geração de relatórios.  
  
4.  Fase de validação e execução: O pacote será executado ou validado sem executar se a opção **/VALIDATE** tiver sido especificada.  
  
##  <a name="exit"></a> Códigos de saída retornados  
 **Códigos de saída retornados do utilitário dtexec**  
  
 Quando um pacote é executado, o **dtexec** pode retornar um código de saída. O código de saída é usado para popular a variável ERRORLEVEL, cujo valor pode, então, ser testado em instruções condicionais ou lógica de ramificação dentro de um arquivo em lote. A tabela a seguir lista os valores que o utilitário **dtexec** pode definir ao sair.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|0|O pacote foi executado com êxito.|  
|1|Falha no pacote.|  
|3|O pacote foi cancelado pelo usuário.|  
|4|O utilitário não pôde localizar o pacote solicitado. Não foi possível encontrar pacote.|  
|5|O utilitário não pôde carregar o pacote solicitado. Não foi possível carregar o pacote.|  
|6|O utilitário encontrou um erro interno de sintática ou semântica na linha de comando.|  
  
##  <a name="syntaxRules"></a> Regras de sintaxe  
 **Regras de sintaxe do utilitário**  
  
 Todas as opções devem iniciar com uma barra (/) ou um sinal de menos (-). As opções que são mostradas aqui iniciam com uma barra (/), mas ela pode ser substituída pelo sinal de menos (-).  
  
 Argumentos que contém espaços devem ser colocados entre aspas. Se o argumento não estiver entre aspas, ele não poderá conter espaço em branco.  
  
 Aspas duplas dentro de cadeias de caracteres entre aspas representam aspas simples.  
  
 Opções e argumentos não diferenciam maiúsculas e minúsculas, exceto em senhas.  
  
##  <a name="cmdshell"></a> Usando dtexec a partir do xp_cmdshell  
 **Usando dtexec a partir do xp_cmdshell**  
  
 Você pode executar o dtexec no prompt do **xp_cmdshell** . O exemplo a seguir mostra como executar um pacote chamado UpsertData.dtsx e ignorar o código de retorno:  
  
```  
EXEC xp_cmdshell 'dtexec /f "C:\UpsertData.dtsx"'  
```  
  
 O exemplo a seguir mostra como executar o mesmo pacote e capturar o código de retorno:  
  
```  
DECLARE @returncode int  
EXEC @returncode = xp_cmdshell 'dtexec /f "C:\UpsertData.dtsx"'  
```  
  
> **IMPORTANTE:** No [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a opção **xp_cmdshell** é desabilitada por padrão nas novas instalações. A opção pode ser habilitada com a execução do procedimento armazenado de sistema **sp_configure** . Para obter mais informações, veja [Opção de configuração de servidor xp_cmdshell](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md).  

##  <a name="bash"></a> Usar dtexec no Bash

O shell **Bash** é um shell popular para Linux. Ele também pode ser usado no Windows. Você pode executar o dtexec no prompt do Bash. Observe que um ponto e vírgula (`;`) é um operador de delimitador de comando no Bash. Isso é particularmente importante ao passar valores para o pacote usando as opções `/Conn[ection]`, `/Par[arameter]` ou '`/Set`, pois elas usam o ponto e vírgula para separar o nome e o valor do item fornecido. O exemplo a seguir mostra como escapar corretamente o ponto e vírgula e outros itens ao usar o Bash e passar valores para um pacote:

```bash
dtexec /F MyPackage.dtsx /CONN "MyConnection"\;"\"MyConnectionString\""
```

##  <a name="syntax"></a> Sintaxe  
  
```  
dtexec /option [value] [/option [value]]...  
```  
  
##  <a name="parameter"></a> Parâmetros  
  
-   **/?** [*option_name*]: (Opcional). Exibe as opções de prompt de comando ou a ajuda para o *option_name* especificado e fecha o utilitário.  
  
     Se você especificar um argumento *option_name* , o **dtexec** iniciará os Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e exibirá o tópico do utilitário dtexec.  
  
-   **/Ca[llerInfo]** : (Opcional). Especifica informações adicionais para uma execução de pacote. Quando você executa um pacote usando o SQL Server Agent, o agente define este argumento para indicar que a execução de pacote é chamada pelo SQL Server Agent. Este parâmetro é ignorado quando o utilitário **dtexec** é executado da linha de comando.  
  
-   **/CheckF[ile]** _filespec_: (Opcional). Define a propriedade **CheckpointFileName** no pacote como o caminho e arquivo especificados em *filespec*. Esse arquivo é usado quando o pacote é reiniciado. Se esta opção for especificada e nenhum valor for fornecido para o nome de arquivo, o **CheckpointFileName** do pacote será definido como uma cadeia de caracteres vazia. Se esta opção não for especificada, os valores no pacote serão retidos.  
  
-   **/CheckP[ointing]** _{on\off}_ : (Opcional). Define um valor que determina se o pacote usará pontos de verificação durante sua execução. O valor **on** especifica que pacotes com falha devem ser executados novamente. Quando o pacote com falha é executado novamente, o mecanismo de tempo de execução usa o arquivo de ponto de verificação para reiniciar o pacote a partir do ponto de falha.  
  
     O valor padrão será “on”, se a opção estiver declarada sem um valor. A execução do pacote falhará se o valor for definido como “on” e não for possível encontrar o arquivo de ponto de verificação. Se essa opção não for especificada, o conjunto de valores no pacote será retido. Para saber mais, confira [Restart Packages by Using Checkpoints](../../integration-services/packages/restart-packages-by-using-checkpoints.md).  
  
     A opção **/CheckPointing on** de dtexec equivale a definir a propriedade **SaveCheckpoints** do pacote como True, e a propriedade **CheckpointUsage** como Always.  
  
-   **/Com[mandFile]** _filespec_: (Opcional). Especifica as opções de comando que são executados com **dtexec**. O arquivo especificado em *filespec* está aberto e as opções do arquivo são lidas até o EOF ser localizado no arquivo. *filespec* é um arquivo de texto. O argumento *filespec* especifica o nome de arquivo e caminho do arquivo de comando a ser associado à execução do pacote.  
  
-   **/Conf[igFile]** _filespec_: (Opcional). Especifica um arquivo de configuração do qual extrair valores. Usando esta opção, você pode definir uma configuração de tempo de execução que difere da configuração especificada em tempo de design para o pacote. Você pode armazenar parâmetros de configuração diferentes em um arquivo de configuração XML e carregá-los antes de executar o pacote por meio da opção **/ConfigFile** .  
  
     Você pode usar a opção **/ConfigFile** para carregar configurações adicionais em tempo de execução que você não especificou em tempo de design. Porém, você não pode usar a opção **/ConfigFile** para substituir valores configurados que você também especificou em tempo de design. Para compreender como são aplicadas as configurações de pacote, consulte [Package Configurations](../../integration-services/packages/package-configurations.md).  
  
-   **/Conn[ection]** _id_or_name;connection_string [[;id_or_name;connection_string]...]_ : (Opcional). Especifica que o gerenciador de conexões com o nome ou o GUID especificado está localizado no pacote e especifica uma cadeia de conexão.  
  
     Essa opção requer que ambos os parâmetros sejam especificados: o nome ou o GUID do gerenciador de conexões deve ser fornecido no argumento *id_or_name* , e uma cadeia de conexão válida deve ser especificada no argumento *connection_string* . Para obter mais informações, consulte [Integration Services &#40;SSIS&#41; Conexões](../../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
     Em tempo de execução, você pode usar a opção **/Connection** para carregar configurações de pacote de um local diferente do local especificado em tempo de design. Os valores dessas configurações substituem os valores que foram especificados originalmente. Porém, você pode usar a opção **/Connection** apenas para configurações, como as configurações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , que usam um gerenciador de conexões. Para compreender como as configurações do pacote são aplicadas, consulte [Configurações de pacote](../../integration-services/packages/package-configurations.md) e [Alterações de comportamento dos recursos do Integration Services no SQL Server 2016](https://msdn.microsoft.com/library/611d22fa-5ac7-485e-9a40-7131e852f794).  
  
-   **/Cons[oleLog]** [[*displayoptions*];[*list_options*;*src_name_or_guid*]...]: (Opcional). Exibe as entradas de log especificadas ao console durante a execução do pacote. Se esta opção for omitida, nenhuma entrada de log será mostrada no console. Se a opção for especificada sem parâmetros que limitem a exibição, toda entrada de log será exibida. Para limitar as entradas exibidas no console, você pode especificar as colunas a exibir, usando o parâmetro *displayoptions* , e limitar os tipos de entrada de log, usando o parâmetro *list_options* .  
  
    > **OBSERVAÇÃO:**  Quando você executa um pacote no servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usando o parâmetro **/ISSERVER**, a saída do console fica limitada, e a maioria das opções de **/Cons[oleLog]** não são aplicáveis. Todos os logs de execução podem ser consultados do servidor nas exibições relacionadas ou usando relatórios padrão disponíveis no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para saber mais sobre os relatórios, consulte [Relatórios do servidor do Integration Services](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports).  
  
     Os valores de *displayoptions* são os seguintes:  
  
    -   N (Nome)  
  
    -   C (Computador)  
  
    -   O (Operador)  
  
    -   S (Nome da Origem)  
  
    -   G (GUID da origem)  
  
    -   X (GUID da execução)  
  
    -   M (Mensagem)  
  
    -   T (Hora de Início e de Término)  
  
     Os valores de *list_options* são os seguintes:  
  
    -   *I* – Especifica a lista de inclusão. Só os nomes ou GUIDs de origem que estão especificados são registrados.  
  
    -   *E* – Especifica a lista de exclusões. Os nomes ou GUIDs de origem que estão especificados não são registrados.  
  
    -   O parâmetro *src_name_or_guid* especificado para inclusão ou exclusão é um nome de evento, nome de origem ou GUID de origem.  
  
     Se você usar várias opções **/ConsoleLog** no mesmo prompt de comando, elas vão interagir da seguinte maneira:  
  
    -   Sua ordem de aparição não tem efeito nenhum.  
  
    -   Se nenhuma lista de inclusão estiver presente na linha de comando, as listas de exclusão serão aplicadas contra todos os tipos de entrada de log.  
  
    -   Se alguma lista de inclusão estiver presente na linha de comando, as listas de exclusão serão aplicadas contra a união de todas as listas de inclusão.  
  
     Para examinar vários exemplos da opção **/ConsoleLog** , consulte a seção **Comentários** .  
  
-   **/D[ts]** _package_path_: (Opcional). Carrega um pacote do Armazenamento de Pacotes SSIS. Os pacotes que estão armazenados no Armazenamento de Pacotes SSIS são implantados usando o modelo de implantação de pacote herdado. Para executar pacotes que são implantados no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usando o modelo de implantação de projeto, use a opção **/ISServer** . Para obter mais informações sobre os modelos de implantação de pacote e projeto, consulte [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx).  
  
     O argumento *package_path* especifica o caminho relativo do pacote [!INCLUDE[ssIS](../../includes/ssis-md.md)] , iniciando na raiz do Repositório de Pacotes SSIS, e inclui o nome do pacote [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Se o caminho ou o nome do arquivo especificado no argumento *package_path* contiver um espaço, você deverá colocar o argumento *package_path* entre aspas.  
  
     A opção **/DTS** não pode ser usada junto com a opção **/File** ou a opção **/SQL** . Se várias opções forem especificadas, o **dtexec** falhará.  
  
-   **/De[crypt]**  _password_: (Opcional). Define a senha de decodificação usada ao carregar um pacote com criptografia de senha.  
  
-   (Opcional) Cria os arquivos de despejo de depuração, .mdmp e .tmp, quando um ou mais eventos especificados ocorrem enquanto o pacote está em execução. O argumento *error code* especifica o tipo de código de evento (erro, aviso ou informação) que disparará o sistema para criar os arquivos de despejo de depuração. Para especificar vários códigos de evento, separe cada argumento *error code* por um ponto-e-vírgula (;). Não inclua aspas com o argumento *error code* .  
  
     O exemplo a seguir gera arquivos de despejo de depuração quando o erro DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER ocorre.  
  
    ```  
    /Dump 0xC020801C  
    ```  
  
     **/Dump** _error code_: Por padrão, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] armazena os arquivos de despejo de depuração na pasta *\<unidade>* :\Arquivos de Programas\Microsoft SQL Server\110\Shared\ErrorDumps.  
  
    > **OBSERVAÇÃO:** Os arquivos de despejo de depuração podem conter informações confidenciais. Use uma ACL (lista de controle de acesso) para restringir o acesso aos arquivos ou copie os arquivos em uma pasta que tenha acesso restrito. Por exemplo, antes de enviar os arquivos de depuração para o serviço de suporte da Microsoft, recomendamos que você remova todas as informações confidenciais.  
  
     Para aplicar essa opção a todos os pacotes executados pelo utilitário **dtexec** , adicione um valor REG_SZ **DumpOnCodes** à chave do Registro HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS\Setup\DtsPath. O valor dos dados em **DumpOnCodes** especifica os códigos de erro que dispararão o sistema para criar arquivos de despejo de depuração. Vários códigos de erro devem ser separados por um ponto e vírgula (;).  
  
     Se um valor **DumpOnCodes** for adicionado à chave do Registro, e a opção **/Dump** for usada, o sistema criará arquivos de despejo de depuração com base nessas duas configurações.  
  
     Para obter mais informações sobre os arquivos de despejo de depuração, consulte [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md).  
  
-   **/DumpOnError**: (opcional) cria os arquivos de despejo de depuração, .mdmp e .tmp, quando ocorre um erro enquanto o pacote está em execução.  
  
     Por padrão, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] armazena os arquivos de despejo de depuração na pasta *\<drive>* :\Program Files\Microsoft SQL Server\110\Shared\ErrorDumps.  
  
    > **OBSERVAÇÃO:** Os arquivos de despejo de depuração podem conter informações confidenciais. Use uma ACL (lista de controle de acesso) para restringir o acesso aos arquivos ou copie os arquivos em uma pasta que tenha acesso restrito. Por exemplo, antes de enviar os arquivos de depuração para o serviço de suporte da Microsoft, recomendamos que você remova todas as informações confidenciais.  
  
     Para aplicar essa opção a todos os pacotes executados pelo utilitário **dtexec** , adicione um valor REG_DWORD **DumpOnError** à chave do Registro HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS\Setup\DtsPath. O valor de REG_DWORD **DumpOnError** determina se a opção **/DumpOnError** precisa ser usada com o utilitário **dtexec** :  
  
    -   Um valor de dados diferente de zero indica que o sistema criará arquivos de despejo de depuração quando ocorrer um erro, independentemente de a opção **/DumpOnError** ser usada com o utilitário **dtexec** .  
  
    -   Um valor de dados igual a zero indica que o sistema não criará os arquivos de despejo de depuração a não ser que a opção **/DumpOnError** ser usada com o utilitário **dtexec** .  
  
     Para obter mais informações sobre os arquivos de despejo de depuração, consulte [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md).  
  
-   **/Env[Reference]** _environment reference ID_: (Opcional). Especifica a ID de referência do ambiente que é usada pela execução do pacote, para um pacote que é implantado para o servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Os parâmetros configurados para associar a variáveis usarão os valores das variáveis que estão contidas no ambiente.  
  
     Use a opção **/Env [Reference]** com as opções **/ISServer** e **/Server** .  
  
     Este parâmetro é usado pelo SQL Server Agent.  
  --    **/F[ile]** _filespec_: (Opcional). Carrega um pacote que é salvo no sistema de arquivos. Os pacotes que estão salvos no sistema de arquivos são implantados usando o modelo de implantação de pacote herdado. Para executar pacotes que são implantados no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usando o modelo de implantação de projeto, use a opção **/ISServer** . Para obter mais informações sobre os modelos de implantação de pacote e projeto, consulte [Deployment of Projects and Packages](deploy-integration-services-ssis-projects-and-packages.md)  

  O argumento *filespec* especifica o caminho e nome de arquivo do pacote. Você pode especificar o caminho como local ou de UNC (Convenção Universal de Nomenclatura). Se o caminho ou o nome do arquivo especificado no argumento *filespec* contiver um espaço, você deverá colocar o argumento *filespec* entre aspas.  
  
-   A opção **/File** não pode ser usada junto com a opção **/DTS** ou a opção **/SQL** . Se várias opções forem especificadas, o **dtexec** falhará.
  
-   **/H[elp]** [*option_name*]: (Opcional). Exibe a ajuda das opções ou do *option_name* especificado e, em seguida, fecha o utilitário.  
  
     Se você especificar um argumento *option_name* , o **dtexec** iniciará os Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e exibirá o tópico do utilitário dtexec.  
  
-   **/ISServer** _packagepath_: (Opcional). Executa um pacote que é implantado no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . O argumento *PackagePath* especifica o caminho completo e o nome do arquivo do pacote implantado no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Se o caminho ou o nome do arquivo especificado no argumento *PackagePath* contiver um espaço, você deverá colocar o argumento *PackagePath* entre aspas.  
  
     O formato do pacote é o seguinte:  
  
    ```  
    \<catalog name>\<folder name>\<project name>\package file name  
    ```  
  
     Use a opção **/Server** com a opção **/ISSERVER** . Somente a Autenticação do Windows pode executar um pacote no Servidor do SSIS. O usuário atual do Windows é usado para acessar o pacote. Se a opção /Server for omitida, será assumida a instância local padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     A opção **/ISSERVER** não pode ser usada com as opções **/DTS**, **/SQL** ou **/File** . Se forem especificadas várias opções, o dtexec irá falhar.  
  
     Este parâmetro é usado pelo SQL Server Agent.  
  
-   **/L[ogger]** _classid_orprogid;configstring_: (Opcional). Associa um ou mais provedores de log à execução de um pacote [!INCLUDE[ssIS](../../includes/ssis-md.md)] . O parâmetro *classid_orprogid* especifica o provedor de log e pode ser especificado como um GUID de classe. O *configstring* é a cadeia de caracteres que é usada para configurar o provedor de log.  
  
     A lista a seguir mostra os provedores de log disponíveis:  
  
    -   Arquivo de texto:  
  
        -   ProgID: DTS.LogProviderTextFile.1  
  
        -   ClassID: {59B2C6A5-663F-4C20-8863-C83F9B72E2EB}  
  
    -   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]:  
  
        -   ProgID: DTS.LogProviderSQLProfiler.1  
  
        -   ClassID: {5C0B8D21-E9AA-462E-BA34-30FF5F7A42A1}  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
        -   ProgID: DTS.LogProviderSQLServer.1  
  
        -   ClassID: {6AA833A1-E4B2-4431-831B-DE695049DC61}  
  
    -   Log de eventos do Windows:  
  
        -   ProgID: DTS.LogProviderEventLog.1  
  
        -   ClassID: {97634F75-1DC7-4F1F-8A4C-DAF0E13AAA22}  
  
    -   Arquivo XML:  
  
        -   ProgID: DTS.LogProviderXMLFile.1  
  
        -   ClassID: {AFED6884-619C-484F-9A09-F42D56E1A7EA}  
  
-   **/M[axConcurrent]** _concurrent_executables_: (Opcional). Especifica o número de arquivos executáveis que o pacote pode executar simultaneamente. O valor especificado deve ser um inteiro não negativo ou -1. O valor de -1 significa que o [!INCLUDE[ssIS](../../includes/ssis-md.md)] permitirá um número máximo de executáveis em processamento simultâneo igual ao número total de processadores no computador executando o pacote mais dois.  
  
-   **/Pack[age]** _PackageName_: (Opcional). Especifica o pacote que é executado. Este parâmetro é usado principalmente quando você executa o pacote de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
-   **/P[assword]** _password_: (Opcional). Permite a recuperação de um pacote que está protegido pela Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Essa opção é usada junto com a opção **/User** . Se a opção **/Password** for omitida e a opção **/User** for usada, uma senha em branco será usada. O valor de *password* pode ser colocado entre aspas.  
  
    > **IMPORTANTE:** [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
-   **/Par[ameter]** [$Package:: | $Project:: | $ServerOption::] *nome_do_parâmetro* [(data_type)]; *valor_da_literal*: (Opcional). Especifica os valores de parâmetro. É possível especificar várias opções **/Parameter** . Os tipos de dados são TypeCodes CLR como cadeias de caracteres. Para um parâmetro que não é cadeia de caracteres, o tipo de dados é especificado em parênteses, seguindo o nome do parâmetro.  
  
     A opção **/Parameter** só pode ser especificada com a opção **/ISServer** .  
  
     Você usa os prefixos $Package, $Project, and $ServerOption para indicar um parâmetro de pacote, um parâmetro de projeto e um parâmetro de opção de servidor, respectivamente. O tipo de parâmetro padrão é pacote.  
  
     Veja a seguir um exemplo de execução de pacote e fornecimento do myvalue para o parâmetro de projeto (myparam) e o valor inteiro 12 para o parâmetro de pacote (anotherparam).  
  
     `Dtexec /isserver "SSISDB\MyFolder\MyProject\MyPackage.dtsx" /server "." /parameter $Project::myparam;myvalue /parameter anotherparam(int32);12`  
  
     Você também pode definir as propriedades do gerenciador de conexões usando parâmetros. Use o prefixo CM para denotar um parâmetro do gerenciador de conexões.  
  
     No exemplo a seguir, a propriedade InitialCatalog do gerenciador de conexões do SourceServer é definida como `ssisdb`.  
  
    ```  
    /parameter CM.SourceServer.InitialCatalog;ssisdb  
    ```  
  
     No exemplo a seguir, a propriedade ServerName do gerenciador de conexões do SourceServer é definida como um ponto (.) para indicar o servidor local.  
  
    ```  
    /parameter CM.SourceServer.ServerName;.  
    ```  
  
-   **/Proj[ect]** _ProjectFile_: (Opcional). Especifica o projeto do qual recuperar o pacote que é executado. O argumento *ProjectFile* especifica o nome da arquivo .ispac. Este parâmetro é usado principalmente quando você executa o pacote de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
-   **/Rem** _comment_: (Opcional). Inclui comentários no prompt de comando ou nos arquivos de comando. O argumento é opcional. O valor de *comment* é uma cadeia de caracteres que deve ser colocada entre aspas ou não conter nenhum espaço em branco. Se nenhum argumento for especificado, uma linha em branco será inserida. Os valores de*comment* serão descartados durante a fase de fornecimento.  
  
-   **/Rep[orting]** _level_ [ *;event_guid_or_name*[ *;event_guid_or_name*[...]]: (Opcional). Especifica que tipos de mensagens devem ser relatadas. As opções de relatório disponíveis para *level* são as seguintes:  
  
     **N** Sem geração de relatórios.  
  
     **E** Relata erros.  
  
     **W** Relata avisos.  
  
     **I** Relata mensagens informativas.  
  
     **C** Relata eventos personalizados.  
  
     **D** Relata eventos da tarefa Fluxo de Dados.  
  
     **P** Relata o progresso.  
  
     **V** Geração de relatórios detalhados.  
  
     Os argumentos de V e N são mutuamente excludentes a todos os outros argumentos; eles devem ser especificados sozinhos. Se a opção **/Reporting** não for especificada, o nível padrão será **E** (erros), **W** (avisos) e **P** (progresso).  
  
     Todos os eventos são precedidos de um carimbo de data e hora no formato "AA/MM/DD HH:MM:SS" e um GUID ou nome amigável, se disponível.  
  
     O parâmetro opcional *event_guid_or_name* é uma lista de exceções aos provedores de log. A exceção especifica os eventos que não são registrados e que devem ser registrados de outra forma.  
  
     Você não precisa excluir um evento caso ele não seja registrado ordinariamente por padrão.  
  
-   **/Res[tart]** {*deny | force | ifPossible*}: (Opcional). Especifica um novo valor para a propriedade <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> no pacote. O significado dos parâmetros é o seguinte:  
  
     *Deny* define a propriedade <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> como <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSCheckpointUsage.DTSCU_NEVER>.  
  
     *Force* define a propriedade <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> como <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSCheckpointUsage.DTSCU_ALWAYS>.  
  
     *ifPossible* define a propriedade <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> como <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSCheckpointUsage.DTSCU_IFEXISTS>.  
  
     O valor padrão de **force** será usado se nenhum valor for especificado.  
  
-   **/Set** [$Sensitive::]*propertyPath;value*: (Opcional). Substitui a configuração de um parâmetro, variável, propriedade, contêiner, provedor de log, enumerador Foreach ou conexão dentro de um pacote. Quando essa opção é usada, **/Set** altera o argumento *propertyPath* para o valor especificado. É possível especificar várias opções **/Set** .  
  
     Além de usar a opção **/Set** com a opção **/F[ile]** , você também pode usar o a opção **/Set** com a opção **/ISServer** ou a opção **/Project** . Quando você usa **/Set** com **/Project**, **/Set** define os valores do parâmetro. Quando você usa **/Set** com **/ISServer**, **/Set** define as substituições da propriedade. Além disso, quando você usa **/Set** com **/ISServer**, é possível usar o prefixo $Sensitive opcional para indicar que a propriedade deve ser tratada como confidencial no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Você pode determinar o valor de *propertyPath* executando o Assistente de Configuração de Pacotes. Os caminhos dos itens selecionados por você são exibidos na página final **Concluindo o Assistente** e podem ser copiados e colados. Se usou o assistente apenas com esse fim, você poderá cancelá-lo depois de copiar os caminhos.  
  
     Veja a seguir um exemplo de execução de um pacote que é salvo no sistema de arquivos e fornecimento de um novo valor para uma variável:  
  
     `dtexec /f mypackage.dtsx /set \package.variables[myvariable].Value;myvalue`  
  
     O exemplo a seguir de execução de um pacote do arquivo de projeto .ispac e da configuração de parâmetros de pacote e projeto.  
  
     `/Project c:\project.ispac /Package Package1.dtsx /SET \Package.Variables[$Package::Parameter];1 /SET \Package.Variables[$Project::Parameter];1`  
  
     Você pode usar a opção **/Set** para alterar o local do qual são carregadas configurações de pacote. Porém, você não pode usar a opção **/Set** para substituir um valor que foi especificado em tempo de design por uma configuração. Para compreender como as configurações do pacote são aplicadas, consulte [Configurações de pacote](../../integration-services/packages/package-configurations.md) e [Alterações de comportamento dos recursos do Integration Services no SQL Server 2016](https://msdn.microsoft.com/library/611d22fa-5ac7-485e-9a40-7131e852f794).  
  
-   **/Ser[ver]** _server_: (Opcional). Quando a opção **/SQL** ou **/DTS** é especificada, ela especifica o nome do servidor no qual o pacote deve ser recuperado. Se você omitir a opção **/Server** e a opção **/SQL** ou **/DTS** for especificada, ocorrerá uma nova tentativa da execução do pacote no servidor local. O valor *server_instance* pode estar entre aspas.  
  
     A opção **/Ser[ver]** é necessária quando a opção **/ISServer** é especificada.  
  
-   **/SQ[L]** _package_path_: Carrega um pacote que é armazenado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], no banco de dados **msdb**. Os pacotes que estão armazenados no banco de dados **msdb** são implantados usando o modelo de implantação de pacote. Para executar pacotes que são implantados no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usando o modelo de implantação de projeto, use a opção **/ISServer** . Para obter mais informações sobre os modelos de implantação de pacote e projeto, consulte [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx).   
  
     O argumento *package_path* especifica o caminho e nome de arquivo do pacote a recuperar. Se forem incluídas pastas no caminho, elas terminarão com barras invertidas ("\\"). O valor *package_path* pode estar entre aspas. Se o caminho ou o nome do arquivo especificado no argumento *package_path* contiver um espaço, você deverá colocar o argumento *package_path* entre aspas.  
  
     Você pode usar as opções **/User**, **/Password**e **/Server** com a opção **/SQL** .  
  
     Se você omitir a opção **/User** , a Autenticação do Windows será usada para acessar o pacote. Se você usar a opção **/User** , o nome de logon **/User** especificado será associado à Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     A opção **/Password** é usada apenas junto com a opção **/User** . Se você usar a opção **/Password** , o pacote será acessado com as informações de nome de usuário e senha fornecidas. Se você omitir a opção **/Password** , uma senha em branco será usada.  
  
    > **IMPORTANTE:** [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
     Se a opção **/Server** for omitida, será assumida a instância local padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     A opção **/SQL** não pode ser usada junto com a opção **/DTS** ou a opção **/File** . Se várias opções forem especificadas, o **dtexec** falhará.  
  
-   **/Su[m]** : (Opcional). Mostra um contador incremental que contém o número de linhas que serão recebidas pelo próximo componente.  
  
-   **/U[ser]** _user_name_: (Opcional). Permite a recuperação de um pacote que está protegido pela Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Essa opção é usada apenas quando a opção **/SQL** é especificada. O valor *user_name* pode estar entre aspas.  
  
    > **IMPORTANTE:**  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
-   **/Va[lidate]** : (Opcional). Interrompe a execução do pacote depois da fase de validação, sem executar realmente o pacote. Durante a validação, o uso da opção **/WarnAsError** faz com que o **dtexec** trate um aviso como um erro, portanto, haverá falha no pacote se ocorrer um aviso durante a validação.  
  
-   **/VerifyB[uild]** _major_[ *;minor*[ *;build*]]: (Opcional). Verifica o número da compilação de um pacote contra os números de compilação especificados durante a fase de verificação no *major*, *minor*e nos argumentos *build* . Se uma ocorrer um erro de correspondência, o pacote não será executado.  
  
     Os valores são inteiros longos. O argumento pode ter um dentre três formulários, sendo sempre obrigatório um valor para *major* :  
  
    -   *major*  
  
    -   *major*;*minor*  
  
    -   *major*; *minor*; *build*  
  
-   **/VerifyP[ackageID]** _packageID_: (Opcional). Verifica o GUID do pacote a ser executado, comparando-o ao valor especificado no argumento *package_id* .  
  
-   **/VerifyS[igned]** : (Opcional). Faz com que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verifique a assinatura digital do pacote. Se o pacote não for assinado ou a assinatura não for válida, o pacote falhará. Para obter mais informações, consulte [Identificar a origem de pacotes com assinaturas digitais](../../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md).  
  
    > **IMPORTANTE:** Quando configurado para verificar a assinatura do pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] apenas verifica se a assinatura digital está presente, se é válida e se provém de uma origem confiável. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não verifica se o pacote foi alterado.  
  
    > **OBSERVAÇÃO:** O valor opcional do Registro **BlockedSignatureStates** pode especificar uma configuração mais restritiva do que a opção de assinatura digital definida no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ou na linha de comando do **dtexec** . Nesta situação, a configuração de Registro mais restritiva substitui as outras configurações.  
  
-   **/VerifyV[ersionID]** _versionID_: (Opcional). Verifica o GUID de versão do pacote a ser executado, comparando-o ao valor especificado no argumento *version_id* durante a fase de validação do pacote.  
  
-   **/VLog** _[Filespec]_ : (Opcional). Grava todos os eventos de pacote do Integration Services nos provedores de log que foram habilitados quando o pacote foi projetado. Para que o Integration Services habilite um provedor de log para arquivos de texto e grave eventos de log em um arquivo de texto especificado, inclua um caminho e nome de arquivo como o parâmetro *Filespec* .  
  
     Se você não incluir o parâmetro *Filespec* , o Integration Services não habilitará um provedor de log para arquivos de texto. O Integration Services vai gravar eventos de log somente nos provedores de log que foram habilitados quando o pacote foi projetado.  
  
-   **/W[arnAsError]** : (Opcional). Faz com que o pacote considere avisos como erro; portanto, o pacote falhará se ocorrer um aviso durante a validação. Se não ocorrer qualquer aviso durante a validação e a opção **/Validate** não estiver especificada, o pacote será executado.  
  
-   **/X86**: (Opcional). Faz com que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent execute o pacote no modo de 32 bits em um computador de 64 bits. Esta opção é definida pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent quando as seguintes condições são verdadeiras:  
  
    -   O tipo de etapa de trabalho é **Pacote do SQL Server Integration Services**.  
  
    -   A opção **Usar runtime de 32 bits** na guia **Opções de execução** da caixa de diálogo **Nova Etapa de Trabalho** está selecionada.  
  
     Você também pode definir esta opção para uma etapa de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent usando procedimentos armazenados ou o SQL Server Management Objects (SMO) para criar o trabalho via programação.  
  
     Esta opção só é usada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Essa opção será ignorada se você executar o utilitário **dtexec** no prompt de comando.  
  
##  <a name="remark"></a> Comentários  
 A ordem na qual as opções de comando são especificadas pode influenciar o modo de execução do pacote:  
  
-   As opções são processadas na ordem em que são encontradas na linha de comando. Os arquivos de comando são lidos à medida que são encontrados na linha de comando. Os comandos no arquivo de comandos também são processados na ordem em que são encontrados.  
  
-   Se a mesma opção, parâmetro ou variável aparecer na mesma instrução de linha de comando mais de uma vez, a última instância da opção terá precedência.  
  
-   As opções **/Set** e **/ConfigFile** são processadas na ordem em que são encontradas.  
  
##  <a name="example"></a> Exemplos  
 Os exemplos a seguir demonstram como usar o utilitário de prompt de comando **dtexec** para configurar e executar pacotes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 **Pacotes em Execução**  
  
 Para executar um pacote [!INCLUDE[ssIS](../../includes/ssis-md.md)] salvo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando Autenticação do Windows, use o seguinte código:  
  
```  
dtexec /sq pkgOne /ser productionServer  
```  
  
 Para executar um pacote [!INCLUDE[ssIS](../../includes/ssis-md.md)] salvo na pasta Sistema de Arquivos do Armazenamento de Pacotes SSIS, use o seguinte código:  
  
```  
dtexec /dts "\File System\MyPackage"  
```  
  
 Para validar um pacote que usa Autenticação do Windows e está salvo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sem executar o pacote, use o seguinte código:  
  
```  
dtexec /sq pkgOne /ser productionServer /va  
```  
  
 Para executar um pacote [!INCLUDE[ssIS](../../includes/ssis-md.md)] salvo no sistema de arquivos, use o seguinte código:  
  
```  
dtexec /f "c:\pkgOne.dtsx"   
```  
  
 Para executar um pacote [!INCLUDE[ssIS](../../includes/ssis-md.md)] salvo no sistema de arquivos e especificar opções de log, use o seguinte código:  
  
```  
dtexec /f "c:\pkgOne.dtsx" /l "DTS.LogProviderTextFile;c:\log.txt"  
```  
  
 Para executar um pacote que usa Autenticação do Windows e está salvo na instância local padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e verificar a versão antes de sua execução, use o seguinte código:  
  
```  
dtexec /sq pkgOne /verifyv {c200e360-38c5-11c5-11ce-ae62-08002b2b79ef}  
```  
  
 Para executar um pacote [!INCLUDE[ssIS](../../includes/ssis-md.md)] salvo no sistema de arquivos e configurado externamente, use o seguinte código:  
  
```  
dtexec /f "c:\pkgOne.dtsx" /conf "c:\pkgOneConfig.cfg"  
```  
  
> **OBSERVAÇÃO:** Os argumentos *package_path* ou *filespec* das opções /SQL, /DTS ou /FILE deverão ser colocados entre aspas, se o caminho ou nome de arquivo contiver um espaço. Se o argumento não estiver entre aspas, ele não poderá conter espaço em branco.  
  
 **Opção de Log**  
  
 Se houver três tipos de entrada de log de A, B e C, a opção **ConsoleLog** a seguir sem um parâmetro exibirá todos os três tipos de log com todos os campos:  
  
```  
/CONSOLELOG  
```  
  
 A seguinte opção exibe todos os tipos de log, mas apenas com as colunas Nome e Mensagem:  
  
```  
/CONSOLELOG NM  
```  
  
 A seguinte opção exibe todas as colunas, mas só para o tipo de entrada de log A:  
  
```  
/CONSOLELOG I;LogEntryTypeA  
```  
  
 A seguinte opção exibe apenas o tipo de entrada de log A, com as colunas Nome e Mensagem:  
  
```  
/CONSOLELOG NM;I;LogEntryTypeA  
```  
  
 A seguinte opção exibe as entradas de logo de tipo A e B:  
  
```  
/CONSOLELOG I;LogEntryTypeA;LogEntryTypeB  
```  
  
 Você pode alcançar os mesmos resultados por meio de várias opções **ConsoleLog** :  
  
```  
/CONSOLELOG I;LogEntryTypeA /CONSOLELOG I;LogEntryTypeB  
```  
  
 Se a opção **ConsoleLog** for usada sem parâmetros, todos os campos serão exibidos. A inclusão de um parâmetro *list_options* faz com que o seguinte exiba apenas o tipo de entrada de log A, com todos os campos:  
  
```  
/CONSOLELOG NM;I;LogEntryTypeA /CONSOLELOG  
```  
  
 O seguinte exibe todas as entradas de log, exceto o tipo de entrada de log A (ou seja, exibe entradas de log B e C):  
  
```  
/CONSOLELOG E;LogEntryTypeA  
```  
  
 O exemplo a seguir alcança os mesmos resultados por meio de várias opções **ConsoleLog** e uma única exclusão:  
  
```  
/CONSOLELOG E;LogEntryTypeA /CONSOLELOG  
/CONSOLELOG E;LogEntryTypeA /CONSOLELOG E;LogEntryTypeA  
/CONSOLELOG E;LogEntryTypeA;LogEntryTypeA  
```  
  
 O exemplo a seguir não exibe mensagens de log, porque quando um tipo de arquivo de log é achado em ambas a listas, de inclusão e exclusão, elas são excluídas.  
  
```  
/CONSOLELOG E;LogEntryTypeA /CONSOLELOG I;LogEntryTypeA  
```  
  
 **Opção SET**  
  
 O seguinte mostra como usar a opção **/SET** , que lhe permite alterar o valor de qualquer propriedade de pacote ou variável ao iniciar o pacote a por meio da linha de comando.  
  
```  
/SET \package\DataFlowTask.Variables[User::MyVariable].Value;newValue  
```  
  
 **Opção de projetos**  
  
 O exemplo a seguir mostra como usar as opções **/Project** e **/Package** .  
  
```  
/Project c:\project.ispac /Package Package1.dtsx  
```  
  
 O exemplo a seguir mostra como usar as opções **/Project** e **/Package** , e definir os parâmetros de pacote e projeto.  
  
```  
/Project c:\project.ispac /Package Package1.dtsx /SET \Package.Variables[$Package::Parameter];1 /SET \Package.Variables[$Project::Parameter];1  
  
```  
  
 **Opção ISServer**  
  
 O exemplo a seguir mostra como usar a opção **/ISServer** .  
  
```  
dtexec /isserver "\SSISDB\MyFolder\MyProject\MyPackage.dtsx" /server "."  
```  
  
 O exemplo a seguir mostra como usar a opção **/ISServer** e definir parâmetros do gerenciador de conexões e projetos.  
  
```  
/Server localhost /ISServer "\SSISDB\MyFolder\Integration Services Project1\Package.dtsx" /Par "$Project::ProjectParameter(Int32)";1 /Par "CM.SourceServer.InitialCatalog";SourceDB  
  
```  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Entrada de blog [Códigos de saída, DTEXEC e catálogo do SSIS](https://www.mattmasson.com/2012/02/exit-codes-dtexec-and-ssis-catalog/)no www.mattmasson.com.  
  
  
