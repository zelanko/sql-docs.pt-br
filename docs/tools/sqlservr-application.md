---
title: Aplicativo sqlservr
ms.custom: seo-lt-2019
ms.date: 08/01/2019
ms.prod: sql
ms.prod_service: sql-tools
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a4a35081f52ddc6f6e75c4bfa8ff56e1020cb0c6
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75305781"
---
# <a name="sqlservr-application"></a>Aplicativo sqlservr

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O aplicativo **sqlservr** inicia, interrompe, pausa e continua uma instância do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando um prompt de comando.

## <a name="syntax"></a>Sintaxe

```cmd
sqlservr [-s instance_name] [-c] [-d master_path] [-f] 
     [-e error_log_path] [-l master_log_path] [-m]
     [-n] [-T trace#] [-v] [-x]
```

## <a name="arguments"></a>Argumentos

**-s** *instance_name* Especifica uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] à qual se conectar. Se não for especificada uma instância nomeada, **sqlservr** iniciará a instância padrão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

> [!IMPORTANT]
>Ao iniciar uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], é necessário usar o aplicativo **sqlservr** no diretório apropriado para essa instância. Para a instância padrão, execute **sqlservr** no diretório \MSSQL\Binn. Para a instância padrão, execute **sqlservr** no diretório \MSSQL$*instance_name*\Binn.

 **-c** Indica que uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é iniciada independentemente do Gerenciador de Controle de Serviço do Windows. Esta opção é utilizada ao iniciar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de um prompt de comando, para reduzir o tempo de inicialização do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .

> [!NOTE]
>Ao usar esta opção, você não poderá interromper o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Service Manager ou o comando **net stop** , e se fizer o logoff do computador, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] será interrompido.)

**-d** *master_path* Indica o caminho totalmente qualificado para o arquivo de banco de dados **mestre**. Não há espaços entre **-d** e *master_path*. Se você não fornecer essa opção, os parâmetros de registro existentes serão usados.

**-f** Inicia uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com configuração mínima. Isso será útil se a definição de um valor de configuração (por exemplo, sobrecarga de confirmação de memória) impediu o servidor de ser iniciado.

**-e** *error_log_path* Indica o caminho totalmente qualificado para o arquivo de log de erros. Se não for especificado, a localização padrão será `*\<Drive>*:\Program Files\Microsoft SQL Server\MSSQL\Log\Errorlog` para a instância padrão e `*\<Drive>*:\Program Files\Microsoft SQL Server\MSSQL$*instance_name*\Log\Errorlog` para uma instância nomeada. Não há espaços entre **-e** e *error_log_path*.

**-l** *master_log_path* Indica o caminho totalmente qualificado para o arquivo de log de transações do banco de dados **mestre**. Não há espaços entre **-l** e *master_log_path*.

**-m** Indica para iniciar uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em modo de usuário único. Somente um único usuário pode conectar quando o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é iniciado em modo de usuário único. O mecanismo de CHECKPOINT, que garante que transações concluídas sejam gravadas regularmente do cache de disco para o dispositivo de banco de dados, não foi iniciado. (Normalmente, esta opção será usada se você experimentar problemas com bancos de dados do sistema que devem ser corrigidos.) Habilita a opção **sp_configure allow updates** . Por padrão, a opção **allow updates** está desabilitada.

**-n** Permite iniciar uma instância nomeada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Sem o parâmetro **-s** definido, a instância padrão tenta a inicialização. Você deve passar para o diretório BINN apropriado da instância em um prompt de comando antes de iniciar o **sqlservr.exe**. Por exemplo, se Instance1 tiver de usar \mssql$Instance1 para seus binários, o usuário deverá estar no diretório \mssql$Instance1\binn para iniciar **sqlservr.exe -s instance1**. Caso você inicie uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com a opção **-n** , recomendamos usar também a opção **-e** ou os eventos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não serão registrados.

**-T** *trace#* Indica que uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] deve ser iniciada com um sinalizador de rastreamento especificado (*trace#* ) em vigor. São usados sinalizadores de rastreamento para iniciar o servidor com comportamento fora do padrão. Para obter mais informações, veja, [Sinalizadores de rastreamento &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).

>[!IMPORTANT]
>Ao especificar um sinalizador de rastreamento, use **-T** para passar o número do sinalizador de rastreamento. Um t minúsculo ( **-t**) é aceito por [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]; entretanto, **-t** define outros sinalizadores de rastreamento internos que são exigidos pelos engenheiros de suporte do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .

**-v** Exibe o número de versão do servidor.

**-x** Desabilita a manutenção de tempo de CPU e estatísticas de taxa de acertos do cache. Permite desempenho máximo.

## <a name="remarks"></a>Comentários
Na maioria dos casos, o programa sqlservr.exe é usado somente para solução de problemas ou manutenção importante. Quando o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é iniciado do prompt de comando sqlservr.exe, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não inicia como um serviço e, desse modo, você pode interromper o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando comandos **net** . Os usuários podem conectar-se ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], mas as ferramentas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mostram o status do serviço, para que o Gerenciador de Configuração do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] indique corretamente que o serviço está interrompido. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] pode se conectar ao servidor, mas ele também indica que o serviço está interrompido.

## <a name="compatibility-support"></a>Suporte de compatibilidade
Os parâmetros a seguir são obsoletos e não são compatíveis com o [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].

|Parâmetro | Mais informações|
|:-----|:-----|
|**-h** | Em versões anteriores de instâncias de 32 bits do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para reservar espaço de endereço de memória virtual para metadados de inclusão de memória a quente quando AWE é habilitado. Compatível por meio de [!INCLUDE[sssql14](../includes/sssql14-md.md)]. Para obter mais informações, veja [Recursos descontinuados do SQL Server no SQL Server 2016](../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md).|
|**-g** | *memory_to_reserve*<br/><br>Aplica-se a versões anteriores de instâncias de 32 bits de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Compatível por meio de [!INCLUDE[sssql14](../includes/sssql14-md.md)]. Especifica um número inteiro de megabytes (MB) de memória que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] deixara disponível para alocações de memória do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , mas fora do pool de memória do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Para obter mais informações, confira [a documentação do SQL Server 2014 sobre as Opções de Configuração de Memória do Servidor](https://docs.microsoft.com/sql/database-engine/configure-windows/server-memory-server-configuration-options?view=sql-server-2014).|
| &nbsp; | &nbsp; |

## <a name="see-also"></a>Consulte Também
 [Opções de inicialização do serviço Mecanismo de Banco de Dados](../database-engine/configure-windows/database-engine-service-startup-options.md)
