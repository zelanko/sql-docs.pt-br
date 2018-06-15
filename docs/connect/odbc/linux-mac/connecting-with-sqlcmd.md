---
title: Conectando com sqlcmd | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- sqlcmd
ms.assetid: 61a2ec0d-1bcb-4231-bea0-cff866c21463
caps.latest.revision: 45
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c330fd329f28fa7d89b62b9af6bb8d4bb67c2bc4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32853081"
---
# <a name="connecting-with-sqlcmd"></a>Conectando com sqlcmd
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

O [sqlcmd](http://go.microsoft.com/fwlink/?LinkID=154481) utilitário está disponível na [!INCLUDE[msCoName](../../../includes/msconame_md.md)] o Driver ODBC para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] em Linux e macOS.
  
Os comandos a seguir mostram como usar a autenticação do Windows (Kerberos) e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] autenticação, respectivamente:
  
```  
sqlcmd –E –Sxxx.xxx.xxx.xxx  
sqlcmd –Sxxx.xxx.xxx.xxx –Uxxx -Pxxx  
```  
  
## <a name="available-options"></a>Opções disponíveis

Na versão atual, as seguintes opções estão disponíveis:  
  
- -? Exibição `sqlcmd` uso.  
  
- -uma solicitação de um tamanho de pacote.  
  
- -b Terminate trabalho em lotes se houver um erro.  
  
- -c *batch_terminator* especificar o terminador de lote.  
  
- -C certificado do servidor confiável.  

- -d *database_name* problema um `USE ` *database_name* instrução ao iniciar `sqlcmd`.  

- -D faz com que o valor passado para o `sqlcmd` opção -S deve ser interpretado como um nome de fonte de dados (DSN). Para obter mais informações, consulte "sn Support in `sqlcmd` e `bcp`" no final deste tópico.  
  
- -e escrever scripts de entrada para o dispositivo de saída padrão (stdout).

- -E usar conexão confiável (autenticação integrada). Para obter mais informações sobre como estabelecer conexões confiáveis que usam autenticação integrada de um cliente Linux ou macOS, consulte [usando a autenticação integrada](../../../connect/odbc/linux-mac/using-integrated-authentication.md).

- -h *number_of_rows* especifique o número de linhas a imprimir entre cabeçalhos de coluna.  
  
- H - especifique um nome de estação de trabalho.  
  
- -i *input_file*[,*input_file*[,...]] Identifica o arquivo que contém um lote de instruções SQL ou procedimentos armazenados.  
  
- -I conjunto o `SET QUOTED_IDENTIFIER` opção de conexão como ON.  
  
- -k remover ou substituir caracteres de controle.  
  
- **-K * application_intent*  
Declara o tipo de carga de trabalho de aplicativo ao conectar-se a um servidor. O único valor com suporte no momento é **ReadOnly**. Se **-K** não for especificado, `sqlcmd` não oferece suporte a conectividade com uma réplica secundária em um grupo de disponibilidade do AlwaysOn. Para obter mais informações, consulte [Driver ODBC no Linux e macOS - alta disponibilidade e recuperação de desastres](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md).  
  
> [!NOTE]  
> Não há suporte para **-K** no CTP para SUSE Linux. No entanto, você pode especificar o **ApplicationIntent = ReadOnly** palavra-chave em um arquivo DSN passado para `sqlcmd`. Para obter mais informações, consulte "sn Support in `sqlcmd` e `bcp`" no final deste tópico.  
  
- -l *timeout* especifique o número de segundos antes que um `sqlcmd` logon expire quando você tentar se conectar a um servidor.

- -m *error_level* controle quais mensagens de erro são enviadas para stdout.  
  
- **-M * multisubnet_failover*  
Sempre especifique **-M** ao se conectar ao ouvinte do grupo de disponibilidade de um grupo de disponibilidade do [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)] ou de uma Instância de Cluster de Failover do [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)]. **-M** fornece detecção mais rápida de failovers e conexão ao servidor ativo (atualmente). Se **-M** não for especificado, **-M** estará desativado. Para obter mais informações sobre [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)], consulte [Driver ODBC no Linux e macOS - alta disponibilidade e recuperação de desastres](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md).  
  
> [!NOTE]  
> Não há suporte para **-M** no CTP para SUSE Linux. No entanto, você pode especificar o **MultiSubnetFailover = Yes** palavra-chave em um arquivo DSN passado para `sqlcmd`. Para obter mais informações, consulte "sn Support in `sqlcmd` e `bcp`" no final deste tópico.  
  
- -N criptografar a conexão.  
  
- -o *output_file* identificar o arquivo que recebe a saída do `sqlcmd`.  
  
- -p imprimir estatísticas de desempenho cada conjunto de resultados.  
  
- -P especifique uma senha de usuário.  
  
- -q *commandline_query* executar uma consulta quando `sqlcmd` é iniciado, mas não sair quando a consulta for concluída.  

- -Q *commandline_query* executar uma consulta quando `sqlcmd` é iniciado. `sqlcmd` será fechado quando a consulta for concluída.  

- mensagens de erro de redirecionamentos - r para stderr.

- -R faz com que o driver usar configurações regionais do cliente para converter dados de data e hora e moeda em dados de caracteres. Atualmente usa apenas formatação em en_US (inglês dos EUA).
  
- -s *column_separator_char* especifique o caractere separador de coluna.  

- -S [*protocolo*:] *servidor*[**, * * * porta*]  
Especifique a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] para se conectar, ou se -D for usado, um DSN. O driver ODBC no Linux e macOS requer - S. Observe que **tcp** é o único protocolo válido.  
  
- -t *query_timeout* especificar o número de segundos antes que um comando (ou instrução SQL) expire.  
  
- Especificar que output_file -u é armazenado em formato Unicode, independentemente do formato de input_file.  
  
- -U *login_id* especificar uma ID de logon do usuário.  
  
- -V *error_severity_level* controlar o nível de severidade que é usado para definir a variável ERRORLEVEL.  
  
- -w *column_width* especificar a largura da tela de saída.  
  
- -W remover espaços à direita de uma coluna.  
  
- -x desabilitar substituição de variável.  
  
- -X desabilitar comandos, script de inicialização e variáveis de ambiente.  
  
- -y *variable_length_type_display_width* definir o `sqlcmd` variável de script `SQLCMDMAXFIXEDTYPEWIDTH`.
  
- -Y *fixed_length_type_display_width* definir o `sqlcmd` variável de script `SQLCMDMAXVARTYPEWIDTH`.


## <a name="available-commands"></a>Comandos disponíveis

Na versão atual, os comandos a seguir estão disponíveis:  
  
-   [:]!!  
  
-   :Connect  
  
-   :Error  
  
-   [:]EXIT  
  
-   GO [*count*]  
  
-   :Help  
  
-   :List  
  
-   :Listvar  
  
-   :On Error  
  
-   :Out  
  
-   :Perftrace  
  
-   [:]QUIT  
  
-   :r  
  
-   :RESET  
  
-   :setvar  
  
## <a name="unavailable-options"></a>Opções indisponíveis
Na versão atual, as opções a seguir não estão disponíveis:  

- -A efetuar login no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] com uma Conexão de administrador dedicada (DAC). Para obter informações sobre como fazer uma conexão de administrador dedicada (DAC), consulte [diretrizes de programação](../../../connect/odbc/linux-mac/programming-guidelines.md).  
  
- -f *code_page* especificar as páginas de código de entrada e saída.  
  
- -L listar os computadores servidor localmente configurados e os nomes dos computadores servidor que estão transmitindo na rede.  
  
- v - criar um `sqlcmd` variável de script que pode ser usado em um `sqlcmd` script.  
  
Você pode usar o seguinte método alternativo: coloque os parâmetros dentro de um arquivo, que, em seguida, você pode acrescentar a outro arquivo. Isso ajudará você a usar um arquivo de parâmetro para substituir os valores. Por exemplo, crie um arquivo chamado `a.sql` (o arquivo de parâmetro) com o seguinte conteúdo:
  
    :setvar ColumnName object_id  
    :setvar TableName sys.objects  
  
Em seguida, crie um arquivo chamado `b.sql`, com os parâmetros de substituição:  
  
    select $(ColumnName) from $(TableName)  

Na linha de comando, combine `a.sql` e `b.sql` em `c.sql` usando os seguintes comandos:  
  
    cat a.sql > c.sql 
  
    cat b.sql >> c.sql  
  
Executar `sqlcmd` e usar `c.sql` como arquivo de entrada:  
  
    slqcmd -S<…> -P<..> –U<..> -I c.sql  

- z - *senha* alterar a senha.  
  
- -Z *senha* alterar senha e sair.  

## <a name="unavailable-commands"></a>Comandos não disponíveis

Na versão atual, os comandos a seguir não estão disponíveis:  
  
-   :ED  
  
-   :ServerList  
  
-   :XML  
  
## <a name="dsn-support-in-sqlcmd-and-bcp"></a>Suporte para DSN no sqlcmd e no bcp

Você pode especificar um nome de fonte de dados (DSN) em vez de um nome de servidor no **sqlcmd** ou **bcp** `-S` opção (ou **sqlcmd** : conectar-se o comando) se você especificar - D. -D faz com que **sqlcmd** ou **bcp** para se conectar ao servidor especificado no DSN, a opção -S.  
  
DSNs de sistema são armazenados na `odbc.ini` arquivo no diretório SysConfigDir do ODBC (`/etc/odbc.ini` nas instalações padrão). DSNs do usuário são armazenados em `.odbc.ini` no diretório base do usuário (`~/.odbc.ini`).
  
As entradas a seguir têm suporte em um DSN no Linux ou macOS:

-   **ApplicationIntent = ReadOnly**  

-   **Banco de dados = * database_name*  
  
-   **Driver = ODBC Driver 11 para SQL Server** ou **Driver = ODBC Driver 13 para SQL Server**
  
-   **MultiSubnetFailover = Yes**  
  
-   **Server = * server_name_or_IP_address*  
  
-   **Trusted_Connection=yes**|**no**  
  
Em um DSN, apenas a entrada DRIVER é necessária, mas para se conectar a um servidor, `sqlcmd` ou `bcp` precisa o valor na entrada do servidor.  

Se a mesma opção for especificada em tanto no DSN e o `sqlcmd` ou `bcp` linha de comando, a opção de linha de comando substitui o valor usado no DSN. Por exemplo, se o DSN tiver uma entrada de banco de dados e o `sqlcmd` inclui de linha de comando **-d**, o valor passado para **-d** é usado. Se **Trusted_Connection = yes** é especificado no DSN, nome de usuário e é usada a autenticação do Kerberos (**– U**) e a senha (**– P**), se fornecido, são ignorados.

Scripts existentes que chamam `isql` pode ser modificado para usar `sqlcmd` definindo o alias a seguir: `alias isql="sqlcmd –D"`.  

## <a name="see-also"></a>Consulte também  
[Conectando com **bcp**](../../../connect/odbc/linux-mac/connecting-with-bcp.md)  
 
