---
title: Aplicativo sqlservr | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- command prompt utilities [SQL Server], sqlservr
- command prompt [SQL Server], pausing/resuming instance of SQL Server
- starting instance of SQL Server
- command prompt [SQL Server], continuing instance of SQL Server
- sqlservr utility
- pausing instance of SQL Server
- stopping instance of SQL Server
- resuming SQL Server
- command prompt [SQL Server], stopping instance of SQL Server
- command prompt [SQL Server], starting instance of SQL Server
- continuing instance of SQL Server
ms.assetid: 60e8ef0a-0851-41cf-a6d8-cca1e04cbcdb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 23f45c0a2e47381b60fe8f6852f24fd8f5f200fc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68211010"
---
# <a name="sqlservr-application"></a>Aplicativo sqlservr
  O aplicativo **sqlservr** inicia, encerra, pausa e continua uma instância do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] por meio de um prompt de comando.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
      sqlservr [-sinstance_name] [-c] [-dmaster_path] [-f]   
     [-eerror_log_path] [-lmaster_log_path] [-m]  
     [-n] [-Ttrace#] [-v] [-x] [-gnumber]  
```  
  
## <a name="arguments"></a>Argumentos  
 **-s** _instance_name_  
 Especifica uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a qual se conectar. Se não for especificada uma instância nomeada, **sqlservr** iniciará a instância padrão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Ao iniciar uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], é necessário usar o aplicativo **sqlservr** no diretório apropriado para essa instância. Para a instância padrão, execute **sqlservr** no diretório \MSSQL\Binn. Para a instância padrão, execute **sqlservr** no diretório \MSSQL$*instance_name*\Binn.  
  
 **-c**  
 Indica que uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é iniciada independentemente do Gerenciador de Controle de Serviços do Windows. Esta opção é utilizada ao iniciar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de um prompt de comando, para reduzir o tempo de inicialização do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Ao usar esta opção, você não poderá interromper o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Service Manager ou o comando **net stop** , e se fizer o logoff do computador, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] será interrompido.)  
  
 **-d** _master_path_  
 Indica o caminho totalmente qualificado para o arquivo de banco de dados **master** . Não há espaços entre **-d** e *master_path*. Se você não fornecer essa opção, os parâmetros de registro existentes serão usados.  
  
 **-f**  
 Inicia uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com configuração mínima. Isso será útil se a definição de um valor de configuração (por exemplo, sobrecarga de confirmação de memória) impediu o servidor de ser iniciado.  
  
 **-e** _error_log_path_  
 Indica o caminho completamente qualificado para o arquivo de log de erros. Se não for especificado, o local padrão será * \<Drive>*: \Program Files\Microsoft SQL Server\MSSQL\Log\Errorlog para a instância padrão e * \<a unidade>*: \Program Files\Microsoft SQL Server\MSSQL $*instance_name*\Log\Errorlog para uma instância nomeada. Não há espaços entre **-e** e *error_log_path*.  
  
 **-l** _master_log_path_  
 Indica o caminho totalmente qualificado para o arquivo de log de transações do banco de dados **master** . Não há espaços entre **-l** e *master_log_path*.  
  
 **-m**  
 Indica para iniciar uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em modo de usuário único. Somente um único usuário pode conectar quando o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é iniciado em modo de usuário único. O mecanismo de CHECKPOINT, que garante que transações concluídas sejam gravadas regularmente do cache de disco para o dispositivo de banco de dados, não foi iniciado. (Normalmente, esta opção será usada se você experimentar problemas com bancos de dados do sistema que devem ser corrigidos.) Habilita a opção **sp_configure allow updates** . Por padrão, **permitir atualizações** está desabilitado.  
  
 **-n**  
 Permite iniciar uma instância nomeada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Sem o parâmetro **-s** definido, a instância padrão tenta a inicialização. Você deve passar para o diretório BINN apropriado da instância em um prompt de comando antes de iniciar o **sqlservr.exe**. Por exemplo, se Instance1 tiver de usar \mssql$Instance1 para seus binários, o usuário deverá estar no diretório \mssql$Instance1\binn para iniciar **sqlservr.exe -s instance1**. Caso você inicie uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com a opção **-n** , recomendamos usar também a opção **-e** ou os eventos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não serão registrados.  
  
 **-T** _trace #_  
 Indica que uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] deve ser iniciada com um sinalizador de rastreamento especificado (*trace#* ) em vigor. São usados sinalizadores de rastreamento para iniciar o servidor com comportamento fora do padrão. Para obter mais informações, veja, [Sinalizadores de rastreamento &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql).  
  
> [!IMPORTANT]  
>  Ao especificar um sinalizador de rastreamento, use **-T** para passar o número do sinalizador de rastreamento. Um t minúsculo (**-t**) é aceito por [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]; entretanto, **-t** define outros sinalizadores de rastreamento internos que são exigidos pelos engenheiros de suporte do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 **-v**  
 Exibe o número de versão do servidor.  
  
 **-x**  
 Desabilita a manutenção de tempo de CPU e estatísticas de taxa de acertos do cache. Permite desempenho máximo.  
  
 **-g** _memory_to_reserve_  
 Especifica um número inteiro de megabytes (MB) de memória que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] deixara disponível para alocações de memória do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , mas fora do pool de memória do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . A memória fora do pool de memória é a área usada pelo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para carregar itens como arquivos `.dll` de procedimento estendido, os provedores OLE DB referidos por meio de consultas distribuídas e objetos de automação referidos em instruções [!INCLUDE[tsql](../includes/tsql-md.md)] . O padrão é 256 MB.  
  
 O uso dessa opção pode ajudar a ajustar a alocação de memória, mas só quando a memória física excede o limite configurado definido pelo sistema operacional na memória virtual disponível para aplicativos. O uso dessa opção pode ser apropriado em configurações de memória grandes nas quais os requisitos de uso de memória do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] são atípicos e o espaço de endereço virtual do processo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está totalmente em uso. O uso incorreto dessa opção pode conduzir a condições nas quais uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode não ser iniciada ou encontrar erros em tempo de execução.  
  
 Use o padrão para o parâmetro **-g** , a menos que você veja algum dos seguintes avisos no log de erros do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] :  
  
-   “Falha nos bytes virtuais alocados: FAIL_VIRTUAL_RESERVE \<size>”  
  
-   “Falha nos bytes virtuais alocados: FAIL_VIRTUAL_COMMIT \<size>”  
  
 Essas mensagens podem indicar que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está tentando liberar partes do pool de memória do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para encontrar espaço para itens como arquivos .dll de procedimento armazenado estendido ou objetos de automação. Nesse caso, considere aumentar a quantidade de memória reservada pela opção **-g**.  
  
 Usando um valor menor que o padrão aumentará a quantidade de memória disponível para o pool do buffer e pilhas de thread; isso pode, por sua vez, fornecer algum benefício de desempenho a cargas de trabalho de memória intensiva em sistemas que não usam muitos procedimentos armazenados estendidos, consultas distribuídas ou objetos de automação.  
  
## <a name="remarks"></a>Comentários  
 Na maioria dos casos, o programa sqlservr.exe é usado somente para solução de problemas ou manutenção importante. Quando o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é iniciado do prompt de comando sqlservr.exe, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não inicia como um serviço e, desse modo, você pode interromper o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando comandos **net** . Os usuários podem conectar-se ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], mas as ferramentas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mostram o status do serviço, para que o Gerenciador de Configuração do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] indique corretamente que o serviço está interrompido. 
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] pode se conectar ao servidor, mas ele também indica que o serviço está interrompido.  
  
## <a name="compatibility-support"></a>Suporte de compatibilidade  
 Não há suporte para o parâmetro **-h**  no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Este parâmetro foi usado em versões anteriores de instâncias de 32 bits do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para reservar espaço de endereço de memória virtual para metadados de inclusão de memória a quente quando AWE é habilitado. Para obter mais informações, consulte [Recursos do SQL Server descontinuados no SQL Server 2014](../../2014/getting-started/discontinued-sql-server-features-in-sql-server-2014.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Opções de inicialização do serviço Mecanismo de Banco de Dados](../database-engine/configure-windows/database-engine-service-startup-options.md)  
  
  
