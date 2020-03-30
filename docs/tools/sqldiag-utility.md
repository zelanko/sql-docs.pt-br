---
title: SQLdiag Utility
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- command prompt utilities [SQL Server], SQLdiag
- stopping diagnostic collection
- storing diagnostic information
- performance [SQL Server], diagnostic collection
- diagnostic records [SQL Server]
- scripts [SQL Server], diagnostic collection
- logs [SQL Server], diagnostic collection
- starting diagnostic collection
- clustered instance of SQL Server
- monitoring performance [SQL Server], diagnostic collection
- security [SQL Server], diagnostic collection
- SQLDIAG service
- space [SQL Server], diagnostic collection
- SQLdiag utility
- disk space [SQL Server], diagnostic collection
- configuration files [SQL Server]
- automatic diagnostic collection
- clusters [SQL Server], diagnostic collection
ms.assetid: 45ba1307-33d1-431e-872c-a6e4556f5ff2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a94daa3fc9756c690a5cd6188e59a9bfd97ca27d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75306668"
---
# <a name="sqldiag-utility"></a>SQLdiag Utility
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O utilitário **SQLdiag** é um utilitário de coleta de diagnósticos para fins gerais que pode ser executado como um aplicativo do console ou um serviço. É possível usar o **SQLdiag** para coletar logs e arquivos de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e de outros tipos de servidores, e usá-lo para monitorar os servidores ao longo do tempo ou para solucionar problemas específicos com seus servidores. O**SQLdiag** foi criado para agilizar e simplificar a coleta de informações de diagnóstico para os Serviços de Atendimento ao Cliente da [!INCLUDE[msCoName](../includes/msconame-md.md)] .  
  
> [!NOTE]  
>  Esse utilitário pode ser alterado e os aplicativos ou scripts que dependem dos seus argumentos de linha de comando ou comportamento podem não funcionar corretamente em versões futuras.  
  
 O**SQLdiag** pode coletar os seguintes tipos de informações de diagnóstico:  
  
-   Logs de desempenho do Windows  
  
-   Logs de eventos do Windows  
  
-   [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] rastreamentos  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] bloqueio de informações  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] informações de configuração  
  
 É possível especificar quais tipos de informações você deseja que o **SQLdiag** colete editando o arquivo de configuração SQLDiag.xml, descrito em uma seção a seguir.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqldiag   
     { [/?] }  
     |  
     { [/I configuration_file]  
       [/O output_folder_path]  
       [/P support_folder_path]  
       [/N output_folder_management_option]  
       [/M machine1 [ machine2 machineN]| @machinelistfile]  
       [/C file_compression_type]  
       [/B [+]start_time]  
       [/E [+]stop_time]  
       [/A SQLdiag_application_name]  
       [/T { tcp [ ,port ] | np | lpc } ]  
       [/Q] [/G] [/R] [/U] [/L] [/X] }  
     |  
     { [START | STOP | STOP_ABORT] }  
     |  
     { [START | STOP | STOP_ABORT] /A SQLdiag_application_name }  
```  
  
## <a name="arguments"></a>Argumentos  
 **/?**  
 Exibe informações de uso.  
  
 **/I** _configuration_file_  
 Define o arquivo de configuração para o **SQLdiag** usar. Por padrão, **/I** é definido como SQLDiag.Xml.  
  
 **/O** _output_folder_path_  
 Redireciona a saída do **SQLdiag** para a pasta especificada. Se a opção **/O** não for especificada, a saída do **SQLdiag** será gravada em uma subpasta chamada SQLDIAG na pasta de inicialização do **SQLdiag** . Se a pasta SQLDIAG não existir, o **SQLdiag** tentará criá-la.  
  
> [!NOTE]  
>  O local da pasta de saída é relativo ao local da pasta de suporte que pode ser especificado com **/P**. Para definir um local completamente diferente para a pasta de saída, especifique o caminho completo do diretório para **/O**.  
  
 **/P** _support_folder_path_  
 Define o caminho da pasta de suporte. Por padrão, **/P** é definido como a pasta na qual o executável **SQLdiag** reside. A pasta de suporte contém os arquivos de suporte do **SQLdiag** , como o arquivo de configuração XML, scripts Transact-SQL e outros arquivos que o utilitário usa durante a coleta de diagnósticos. Se você usar essa opção para especificar um caminho alternativo dos arquivos de suporte, o **SQLdiag** copiará automaticamente os arquivos de suporte necessários na pasta especificada, se ainda não existirem.  
  
> [!NOTE]  
>  Para definir sua pasta atual como o caminho de suporte, especifique o **%cd%** na linha de comando como segue:  
>   
>  **SQLDIAG /P %cd%**  
  
 **/N** _output_folder_management_option_  
 Define se o **SQLdiag** substitui ou renomeia a pasta de saída na inicialização. Opções disponíveis:  
  
 1 = Substitui a pasta de saída (padrão)  
  
 2 = Quando o **SQLdiag** é iniciado, ele renomeia a pasta de saída a como SQLDIAG_00001, SQLDIAG_00002 e assim por diante. Depois de renomear a pasta de saída atual, o **SQLdiag** grava a saída na pasta de saída padrão SQLDIAG.  
  
> [!NOTE]  
>  O**SQLdiag** não anexa a saída à pasta de saída atual quando é iniciado. Ele pode apenas substituir a pasta de saída padrão (opção 1) ou renomear a pasta (opção 2) e, em seguida, gravar a saída na nova pasta de saída padrão SQLDIAG.  
  
 **/M** _machine1_ [ *machine2* *machineN*] | *\@machinelistfile*  
 Substitui as máquinas especificadas no arquivo de configuração. Por padrão, o arquivo de configuração é SQLDiag.Xml ou é definido com o parâmetro **/I** . Ao especificar mais de uma máquina, separe cada nome de máquina com um espaço.  
  
 Usar o *\@arquivodelistadecomputadores* especifica um nome de arquivo de lista de máquina a ser armazenado no arquivo de configuração.  
  
 **/C** _file_compression_type_  
 Define o tipo de compactação de arquivo usado nos arquivos da pasta de saída do **SQLdiag** . Opções disponíveis:  
  
 0 = nenhum (padrão)  
  
 1 = usa compactação NTFS  
  
 **/B** [ **+** ]*start_time*  
 Especifica a data e a hora para começar a coletar dados de diagnóstico no seguinte formato:  
  
 AAAAMMDD_HH:MM:SS  
  
 A hora é especificada usando a notação de 24 horas. Por exemplo, 2:00 P.M. deveria ser especificado como **14:00:00**.  
  
 Use **+** sem a data (apenas HH:MM:SS) para especificar uma hora relativa à data e à hora atuais. Por exemplo, se você especificar **/B +02:00:00: 00:00**, o **SQLdiag** aguardará duas horas antes de começar a coletar informações.  
  
 Não insira espaço entre **+** e o *start_time*especificado.  
  
 Se você especificar uma hora de início no passado, o **SQLdiag** forçará a alteração da data de modo que a data e a hora de início estejam no futuro. Por exemplo, se você especificar **/B 01:00:00** e a hora atual for 08:00:00, o **SQLdiag** forçará a alteração da data de início de modo que a data de início seja no dia seguinte.  
  
 Observe que o **SQLdiag** usa a hora local no computador no qual o utilitário está sendo executado.  
  
 **/E** [ **+** ]*stop_time*  
 Especifica a data e a hora para interromper a coleta de dados de diagnóstico no seguinte formato:  
  
 AAAAMMDD_HH:MM:SS  
  
 A hora é especificada usando a notação de 24 horas. Por exemplo, 2:00 P.M. deveria ser especificado como **14:00:00**.  
  
 Use **+** sem a data (apenas HH:MM:SS) para especificar uma hora relativa à data e à hora atuais. Por exemplo, se você especificar uma hora de início e uma hora de término usando **/B +02:00:00 /E +03:00:00**, o **SQLdiag** aguardará duas horas antes de começar a coletar informações, e coletará informações durante três horas antes de parar e fechar. Se **/B** não for especificado, o **SQLdiag** começará a coletar o diagnóstico imediatamente e terminará na data e hora especificadas por **/E**.  
  
 Não insira espaço entre **+** e o *start_time* ou *end_time*especificado.  
  
 Observe que o **SQLdiag** usa a hora local no computador no qual o utilitário está sendo executado.  
  
 **/A** _SQLdiag_application_name_  
 Habilita a execução de várias instâncias do utilitário **SQLdiag** na mesma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 Cada *SQLdiag_application_name* identifica uma instância diferente do **SQLdiag**. Não existe relação entre uma instância do *SQLdiag_application_name* e um nome de instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 *SQLdiag_application_name* pode ser usado para iniciar ou interromper uma instância específica de serviço do **SQLdiag** .  
  
 Por exemplo:  
  
 **SQLDIAG START /A** _SQLdiag_application_name_  
  
 Também pode ser usado com a opção **/R** para registrar uma instância específica do **SQLdiag** como um serviço. Por exemplo:  
  
 **SQLDIAG /R /A** _SQLdiag_application_name_  
  
> [!NOTE]  
>  O**SQLdiag** adiciona automaticamente o prefixo DIAG$ ao nome de instância especificado para *SQLdiag_application_name*. Isso fornecerá um nome de serviço sensato se você registrar o **SQLdiag** como um serviço.  
  
 /T { tcp [ ,*porta* ] | np | lpc }  
 Conecta a uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando o protocolo especificado.  
  
 tcp [,*porta*]  
 Protocolo TCP/IP. Opcionalmente, é possível especificar um número de porta para a conexão.  
  
 np  
 Pipes nomeados. Por padrão, a instância padrão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] escuta nos pipes nomeados `\\.\pipe\sql\query` e `\\.\pipe\MSSQL$<instancename>\sql\query` em busca de uma instância nomeada. Não é possível conectar a uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando um nome de pipe alternado.  
  
 lpc  
 Chamada de procedimento local. Esse protocolo de memória compartilhada também estará disponível se o cliente estiver se conectando a uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no mesmo computador.  
  
 **/Q**  
 Executa o **SQLdiag** no modo silencioso. **/Q** suprime todos os prompts, como prompts de senha.  
  
 **/G**  
 Executa o **SQLdiag** no modo genérico. Quando **/G** é especificado, ao ser inicializado, o **SQLdiag** não impõe a verificação de conectividade do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou verifica se o usuário é membro da função de servidor fixa **sysadmin** . Em vez disso, o **SQLdiag** transfere ao Windows a responsabilidade por determinar se um usuário tem os direitos apropriados para coletar cada diagnóstico solicitado.  
  
 Se **/G** não for especificado, o **SQLdiag** verificará se o usuário é membro do grupo **Administradores** do Windows e não coletará diagnósticos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se o usuário não for membro do grupo **Administradores** .  
  
 **/R**  
 Registra o **SQLdiag** como um serviço. Quaisquer argumentos de linha de comando especificados ao registrar o **SQLdiag** como um serviço são preservados para execuções futuras do serviço.  
  
 Quando o **SQLdiag** é registrado como um serviço, o nome de serviço padrão fica SQLDIAG. Você pode alterar o nome de serviço usando o argumento **/A** .  
  
 Use o argumento de linha de comando **START** para iniciar o serviço:  
  
 **SQLDIAG START**  
  
 Você também pode usar o comando **net start** para iniciar o serviço:  
  
 **net  start SQLDIAG**  
  
 **/U**  
 Cancela o registro do **SQLdiag** como um serviço.  
  
 Use o argumento **/A** se também for cancelar o registro de uma instância nomeada do **SQLdiag** .  
  
 **/L**  
 Executa o **SQLdiag** no modo contínuo quando uma hora de início ou de término também é especificada com os argumentos **/B** ou **/E** , respectivamente. O**SQLdiag** reinicia automaticamente depois que a coleta de diagnósticos é interrompida devido a um desligamento agendado. Por exemplo, usando o argumento **/E** ou **/X** .  
  
> [!NOTE]  
>  O**SQLdiag** ignorar o argumento **/L** se uma hora de início ou de término não for especificada useo os argumentos de linha de comeo **/B** e **/E** comme line arguments.  
  
 Usar **/L** não implica o modo de serviço. Para usar **/L** ao executar o **SQLdiag** como um serviço, especifique-o na linha de comando quando você registrar o serviço.  
  
 **/X**  
 Executa o **SQLdiag** no modo de instantâneo. O**SQLdiag** tira um instantâneo de todo o diagnóstico configurado e desliga automaticamente.  
  
 **START** | **STOP** | **STOP_ABORT**  
 Inicia ou interrompe o serviço do **SQLdiag** . **STOP_ABORT** força o serviço a desligar o mais rápido possível sem terminar a coleção de diagnóstico atual.  
  
 Quando esses argumentos de controle de serviço forem usados, eles deverão ser o primeiro argumento usado na linha de comando. Por exemplo:  
  
 **SQLDIAG START**  
  
 Somente o argumento **/A** , que especifica uma instância nomeada do **SQLdiag**, pode ser usado com **START**, **STOP**ou **STOP_ABORT** para controlar uma instância específica do serviço **SQLdiag** . Por exemplo:  
  
 **SQLDIAG START /A** _SQLdiag_application_name_  
  
## <a name="security-requirements"></a>Requisitos de segurança  
 A não ser que o **SQLdiag** seja executado no modo genérico (especificando o argumento de linha de comando **/G** ), o usuário que está executando o **SQLdiag** deverá ser membro do grupo **Administradores** do Windows e membro da função de servidor fixa [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] **sysadmin**. Por padrão, o **SQLdiag** conecta-se ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando a Autenticação do Windows, mas também tem suporte para a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
## <a name="performance-considerations"></a>Considerações sobre desempenho  
 Os efeitos no desempenho da execução do **SQLdiag** dependem do tipo de dados de diagnóstico que você configurou para coletar. Por exemplo, se você configurou o **SQLdiag** para coletar informações de rastreamento do [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] , quanto maior o número de classes de evento que você escolher para rastreamento, mais o desempenho do servidor será afetado.  
  
 O impacto no desempenho ao executar o **SQLdiag** é aproximadamente equivalente à soma dos custos de coleta do diagnóstico configurado separadamente. Por exemplo, coletar um rastreamento com o **SQLdiag** gera o mesmo custo de desempenho que coletá-lo com o [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]. O impacto no desempenho ao usar o **SQLdiag** é desprezível.  
  
## <a name="required-disk-space"></a>Espaço em disco exigido  
 Como o **SQLdiag** pode coletar diferentes tipos de informações de diagnóstico, o espaço em disco livre exigido para executar o **SQLdiag** varia. A quantidade de informações de diagnóstico coletada depende da natureza e do volume da carga de trabalho que o servidor está processando e pode variar de alguns megabytes a vários gigabytes.  
  
## <a name="configuration-files"></a>Arquivos de configuração  
 Ao inicializar, o **SQLdiag** lê o arquivo de configuração e os argumentos de linha de comando que foram especificados. Você especifica os tipos de informações de diagnóstico que o **SQLdiag** coleta no arquivo de configuração. Por padrão, o **SQLdiag** utiliza o arquivo de configuração SQLDiag.Xml, extraído sempre que a ferramenta é executada e localizado na pasta de inicialização do utilitário **SQLdiag** . O arquivo de configuração utiliza o esquema XML, SQLDiag_schema.xsd, que também é extraído no diretório de inicialização do utilitário por meio do arquivo executável sempre que o **SQLdiag** é executado.  
  
### <a name="editing-the-configuration-files"></a>Editando os arquivos de configuração  
 Você pode copiar e editar o SQLDiag.Xml para alterar os tipos de dados de diagnóstico que o **SQLdiag** coleta. Ao editar o arquivo de configuração, sempre use um editor de XML que pode validar o arquivo de configuração em seu esquema XML como o [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]. Você não deve editar SQLDiag.Xml diretamente. Em vez disso, faça uma cópia do SQLDiag.Xml e renomeie-a com um novo nome de arquivo na mesma pasta. Em seguida, edite o novo arquivo e use o argumento **/I** para passá-lo para o **SQLdiag**.  
  
#### <a name="editing-the-configuration-file-when-sqldiag-runs-as-a-service"></a>Editando o arquivo de configuração quando o SQLdiag é executado como um serviço  
 Se você já executou o **SQLdiag** como um serviço e precisa editar o arquivo de configuração, cancele o registro do serviço SQLDIAG especificando o argumento de linha de comando **/U** e registre o serviço novamente usando o argumento de linha de comando **/R** . Cancelar o registro e registrar novamente o serviço remove informações de configuração antigas que foram armazenadas no registro do Windows.  
  
## <a name="output-folder"></a>Pasta de saída  
 Se você não especificar uma pasta de saída com o argumento **/O** , o **SQLdiag** criará uma subpasta chamada SQLDIAG na pasta de inicialização do **SQLdiag** . Para coleção de informações de diagnóstico que envolva rastreamentos de grande volume, como o [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] , verifique se a pasta de saída está em uma unidade local com espaço suficiente para armazenar a saída de diagnóstico solicitada.  
  
 Quando o **SQLdiag** é reiniciado, ele substitui o conteúdo da pasta de saída. Para evitar isso, especifique a linha de comando **/N 2** .  
  
## <a name="data-collection-process"></a>Processo de coleção de dados  
 Quando o **SQLdiag** é inicializado, ele desempenha as verificações de inicialização necessárias para coletar os dados de diagnóstico que foram especificados no SQLDiag.Xml. Esse processo pode demorar vários segundos. Depois que o **SQLdiag** começar a coletar os dados de diagnóstico ao ser executado como um aplicativo do console, uma mensagem é exibida informando que a coleta do **SQLdiag** começou e que você pode pressionar CTRL+C para interrompê-la. Quando o **SQLdiag** é executado como um serviço, uma mensagem semelhante é gravada no log de eventos do Windows.  
  
 Se você estiver usando o **SQLdiag** para diagnosticar um problema que você pode reproduzir, espere até receber essa mensagem antes de reproduzir o problema em seu servidor.  
  
 O**SQLdiag** coleta a maioria dos dados de diagnóstico em paralelo. Todas as informações de diagnóstico são coletadas por meio da conexão com as ferramentas, como o utilitário [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] **sqlcmd** ou o processador de comandos do Windows, exceto quando as informações são coletadas dos logs de desempenho e logs de evento do Windows. O**SQLdiag** utiliza um thread de trabalho por computador para monitorar a coleção de dados de diagnóstico dessas outras ferramentas, frequentemente aguardando a conclusão de várias ferramentas simultaneamente. Durante o processo de coleta, o **SQLdiag** roteia a saída de cada diagnóstico para a pasta de saída.  
  
## <a name="stopping-data-collection"></a>Interrompendo a coleção de dados  
 Depois que o **SQLdiag** começar a coletar dados de diagnóstico, ele continuará a fazê-lo, a não ser que você o interrompa ou ele esteja configurado para ser interrompido em um determinado horário. Você pode configurar o **SQLdiag** para ser interrompido em uma hora especificada usando o argumento **/E** , que permite que você especifique uma hora de parada ou usando o argumento **/X** , que executa o **SQLdiag** no modo de instantâneo.  
  
 Quando o **SQLdiag** é interrompido, ele interrompe todos os diagnósticos iniciados. Por exemplo, ele interrompe os rastreamentos que o [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] estava coletando, a execução de scripts [!INCLUDE[tsql](../includes/tsql-md.md)] e qualquer subprocesso gerado durante a coleção de dados. Após a conclusão da coleção de dados de diagnóstico, o **SQLdiag** é encerrado.  
  
> [!NOTE]  
>  Não há suporte para pausar o serviço **SQLdiag** . Se você tentar pausar o serviço **SQLdiag** , ele será interrompido depois de concluir a coleta de diagnósticos que estava executando quando você o pausou. Se você reiniciar o **SQLdiag** depois de interrompê-lo, o aplicativo reiniciará e substituirá a pasta de saída. Para evitar a substituição da pasta de saída, especifique **/N 2** na linha de comando.  
  
 **Para interromper o SQLdiag quando estiver sendo executado como um aplicativo do console**  
  
 Se você estiver executando o **SQLdiag** como um aplicativo do console, pressione CTRL+C na janela do console em que o **SQLdiag** está sendo executado para interrompê-lo. Depois de pressionar CTRL+C, uma mensagem é exibida na janela do console informando que a coleção de dados do **SQLdiag** está terminando e que você deve esperar a conclusão do processo, o que pode demorar vários minutos.  
  
 Pressione Ctrl+C duas vezes para finalizar todos os processos de diagnóstico filho e encerrar imediatamente o aplicativo.  
  
 **Para interromper o SQLdiag quando estiver sendo executado como um serviço**  
  
 Se você estiver executando o **SQLdiag** como um serviço, execute **SQLDiag STOP** na pasta de inicialização do **SQLdiag** para interrompê-lo.  
  
 Se você estiver executando várias instâncias do **SQLdiag** no mesmo computador, será possível transferir o nome de instância do **SQLdiag** para a linha de comando quando você interromper o serviço. Por exemplo, para interromper uma instância do **SQLdiag** chamada Instância 1, use a seguinte sintaxe:  
  
```  
SQLDIAG STOP /A Instance1  
```  
  
> [!NOTE]  
>  **/A** é o único argumento de linha de comando que pode ser usado **START**, **STOP**ou **STOP_ABORT**. Se você precisar especificar uma instância nomeada do **SQLdiag** com um dos verbos de controle de serviço, especifique **/A** após o verbo de controle na linha de comando como mostrado no exemplo de sintaxe anterior. Quando verbos de controle são usados, eles devem ser o primeiro argumento na linha de comando.  
  
 Para interromper o serviço o mais rapidamente possível, execute **SQLDIAG STOP_ABORT** na pasta de inicialização do utilitário. Esse comando aborta qualquer coleta de diagnóstico que está sendo executada atualmente sem esperar a sua conclusão.  
  
> [!NOTE]  
>  Use **SQLDiag STOP** ou **SQLDIAG STOP_ABORT** para interromper o serviço **SQLdiag** . Não use o Console de Serviços do Windows para interromper o **SQLdiag** ou outros serviços do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
## <a name="automatically-starting-and-stopping-sqldiag"></a>Iniciando e interrompendo automaticamente o SQLdiag  
 Para iniciar e interromper automaticamente a coleção de dados em uma hora especificada, use os argumentos **/B**_start\_time_ e **/E**_stop\_time_ na notação de 24 horas. Por exemplo, se você estiver solucionando um problema que aparece consistentemente em aproximadamente 02:00:00, poderá configurar o **SQLdiag** para iniciar automaticamente a coleta de dados de diagnóstico à 01:00 e interrompê-la automaticamente às 03:00:00. Use os argumentos **/B** e **/E** para especificar o horário de início e de parada. Use a notação de 24 horas para especificar as data de início e de parada exatas com o formato AAAAMMDD_HH:MM:SS. Para especificar uma hora de início ou de parada relativa, anteponha às horas de início e de parada o **+** e omita a parte da data (AAAAMMDD_) conforme é mostrado no exemplo a seguir, que faz o **SQLdiag** esperar 1 hora antes de começar a coletar informações e, em seguida, coleta informações por 3 horas antes de ser interrompido e fechar:  
  
```  
sqldiag /B +01:00:00 /E +03:00:00  
```  
  
 Quando uma *start_time* relativa é especificada, o **SQLdiag** inicia em uma hora relativa à data e à hora atuais. Quando uma *end_time* relativa é especificada, o **SQLdiag** encerra em uma hora relativa à *start_time*especificada. Se a data e a hora de início e de parada especificadas estiverem no passado, o **SQLdiag** forçará a alteração da data de início de modo que a data e a hora de início estejam no futuro.  
  
 Isto tem implicações importantes nas datas de início e de término que você escolhe. Considere o exemplo a seguir:  
  
```  
sqldiag /B +01:00:00 /E 08:30:00  
```  
  
 Se a hora atual for 08:00, a hora de término passará antes da coleta de diagnóstico começar de fato. Como o **SQLdiag** ajusta automaticamente as datas de início e de término para o próximo dia quando ocorrem no passado, nesse exemplo, a coleta de diagnóstico começará às 09:00 de hoje (uma hora de início relativa foi especificada com **+** ) e continuará até às 08:30 da manhã seguinte.  
  
### <a name="stopping-and-restarting-sqldiag-to-collect-daily-diagnostics"></a>Interrompendo e reiniciando o SQLdiag para coletar diagnósticos diários  
 Para coletar um conjunto de diagnósticos especificado diariamente sem ter que iniciar e interromper manualmente o **SQLdiag**, use o argumento **/L** . O argumento **/L** faz com que o **SQLdiag** seja executado continuamente reiniciando-se automaticamente após um desligamento agendado. Quando **/L** é especificado e o **SQLdiag** é interrompido porque atingiu a hora de término com o argumento **/E** ou porque está sendo executado no modo de instantâneo usando o argumento **/X** , o **SQLdiag** reiniciará em vez de fechar.  
  
 O exemplo a seguir especifica que o **SQLdiag** seja executado no modo contínuo para reiniciar automaticamente depois que a coleta de dados de diagnóstico ocorrer entre 03:00:00 e 05:00:00.  
  
```  
sqldiag /B 03:00:00 /E 05:00:00 /L  
```  
  
 O exemplo a seguir especifica que o **SQLdiag** seja executado no modo contínuo para reiniciar automaticamente depois de tirar um instantâneo dos dados de diagnóstico às 03:00:00.  
  
```  
sqldiag /B 03:00:00 /X /L  
```  
  
## <a name="running-sqldiag-as-a-service"></a>Executando o SQLdiag como um serviço  
 Quando você quiser usar o **SQLdiag** para coletar dados de diagnóstico por longos períodos de tempo durante os quais você precisará fazer logoff do computador no qual o **SQLdiag** está sendo executado, será possível executá-lo como um serviço.  
  
 **Para registrar o SQLdiag para ser executado como um serviço**  
  
 Você pode registrar o **SQLdiag** para ser executado como um serviço especificando o argumento **/R** na linha de comando. Isso registra o **SQLdiag** para ser executado como um serviço O nome do serviço **SQLdiag** é SQLDIAG. Quaisquer outros argumentos especificados na linha de comando ao registrar o **SQLdiag** como um serviço são preservados e reutilizados quando o serviço é iniciado.  
  
 Para alterar o nome de serviço padrão SQLDIAG, use o argumento de linha de comando **/A** para especificar outro nome. O**SQLdiag** automaticamente adiciona o prefixo DIAG$ a qualquer nome de instância do **SQLdiag** especificada com **/A** para criar nomes de serviço sensatos.  
  
 **Para cancelar o registro do serviço SQLDIAG**  
  
 Para cancelar o registro do serviço, especifique o argumento **/U** . Cancelar o registro do **SQLdiag** como um serviço também exclui as chaves do Registro do Windows do serviço.  
  
 **Para iniciar ou reiniciar o serviço SQLDIAG**  
  
 Para iniciar ou reiniciar o serviço SQLDIAG, execute **SQLDiag START** da linha de comando.  
  
 Se você estiver executando várias instâncias do **SQLdiag** usando o argumento **/A** , será possível passar o nome de instância do **SQLdiag** na linha de comando quando você iniciar o serviço. Por exemplo, para iniciar uma instância do **SQLdiag** chamada Instância 1, use a seguinte sintaxe:  
  
```  
SQLDIAG START /A Instance1  
```  
  
 Você também pode usar o comando **net start** para iniciar o serviço SQLDIAG.  
  
 Ao reiniciar o **SQLdiag**, ele substitui o conteúdo na pasta de saída atual. Para evitar isso, especifique **/N 2** na linha de comando para renomear a pasta de saída quando o utilitário iniciar.  
  
 Não há suporte para pausar o serviço **SQLdiag** .  
  
## <a name="running-multiple-instances-of-sqldiag"></a>Executando várias instâncias do SQLdiag  
 Execute várias instâncias do **SQLdiag** no mesmo computador especificando **/A**_SQLdiag\_application\_name_ na linha de comando. Isso é útil para coletar conjuntos diferentes de diagnósticos simultaneamente da mesma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Por exemplo, você pode configurar uma instância nomeada do **SQLdiag** para executar continuamente coletas de dados leves. Então, se algum problema ocorrer no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], você poderá executar a instância padrão do **SQLdiag** para coletar o diagnóstico desse problema ou para reunir um conjunto de diagnósticos que os Serviços de Atendimento ao Cliente da [!INCLUDE[msCoName](../includes/msconame-md.md)] solicitaram a você a fim de diagnosticar um problema.  
  
## <a name="collecting-diagnostic-data-from-clustered-sql-server-instances"></a>Coletando dados de diagnóstico de instâncias do SQL Server clusterizado  
 O**SQLdiag** oferece suporte à coleta de dados de diagnóstico de instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] clusterizadas. Para reunir diagnósticos de instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] clusterizadas, verifique se **"."** está especificado no atributo **name** do elemento **\<Machine>** no arquivo de configuração SQLDiag.Xml e não especifique o argumento **/G** na linha de comando. Por padrão, **"."** é especificado para o atributo **name** no arquivo de configuração e o argumento **/G** é desativado. Normalmente, você não precisa editar o arquivo de configuração ou alterar a linha de comando ao coletar a partir de uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] clusterizada.  
  
 Quando **"."** está especificado como o nome da máquina, o **SQLdiag** detecta que está sendo executado em um cluster e recupera simultaneamente informações de diagnóstico de todas as instâncias virtuais do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instaladas no cluster. Se você quiser coletar informações de diagnóstico de apenas uma instância virtual do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que está sendo executada em um computador, especifique essa [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] virtual para o atributo **name** do elemento **\<Machine>** no SQLDiag.Xml.  
  
> [!NOTE]  
>  Para coletar informações de rastreamento do [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] de instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] clusterizadas, os compartilhamentos administrativos (ADMIN$) devem estar habilitados no cluster.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de utilitários de prompt de comando &#40;Mecanismo de Banco de Dados&#41;](../tools/command-prompt-utility-reference-database-engine.md)  
  
  
