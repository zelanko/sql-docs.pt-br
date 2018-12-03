---
title: Conectando com sqlcmd | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sqlcmd
ms.assetid: 61a2ec0d-1bcb-4231-bea0-cff866c21463
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 21021402a10494306a3b667c5f7b83977dc7d205
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52512538"
---
# <a name="connecting-with-sqlcmd"></a>Conectando com sqlcmd
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

O utilitário [sqlcmd](https://go.microsoft.com/fwlink/?LinkID=154481) está disponível no [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em Linux e macOS.
  
Os comandos a seguir mostram como usar a autenticação do Windows (Kerberos) e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] autenticação, respectivamente:
  
```  
sqlcmd -E -Sxxx.xxx.xxx.xxx  
sqlcmd -Sxxx.xxx.xxx.xxx -Uxxx -Pxxx  
```  
  
## <a name="available-options"></a>Opções Disponíveis

Na versão atual, as seguintes opções estão disponíveis:  
  
- -? Exibição `sqlcmd` uso.  
  
- -a Solicitar um tamanho de pacote.  
  
- -b Encerrar o trabalho em lotes se houver um erro.  
  
- -c *batch_terminator* especificar o terminador de lote.  
  
- -C Confiar em certificado do servidor.  

- -d *database_name* problema uma `USE ` *database_name* instrução ao iniciar `sqlcmd`.  

- -D Faz com que o valor passado para a opção -S do `sqlcmd` seja interpretada como um nome da fonte de dados (DSN). Para obter mais informações, veja "Suporte para DSN no `sqlcmd` e no `bcp`" no final deste tópico.  
  
- -e Gravar scripts de entrada no dispositivo de saída padrão (stdout).

- Usar conexão confiável e autenticação integrada. Para obter mais informações sobre como estabelecer conexões confiáveis que usam autenticação integrada em um cliente Linux ou macOS, consulte [usando a autenticação integrada](../../../connect/odbc/linux-mac/using-integrated-authentication.md).

- -h *number_of_rows* Especificar o número de linhas a serem impressas entre os títulos das colunas.  
  
- -H Especificar um nome de estação de trabalho.  
  
- -i *input_file*[,*input_file*[,…]] Identificar o arquivo que contém um lote de instruções SQL ou procedimentos armazenados.  
  
- -I conjunto o `SET QUOTED_IDENTIFIER` opção de conexão como ON.  
  
- -k Remover ou substituir caracteres de controle.  
  
- **-K**_aplicativo\_intenção_  
Declara o tipo de carga de trabalho de aplicativo ao conectar-se a um servidor. O único valor com suporte no momento é **ReadOnly**. Se **-K** não for especificado, o `sqlcmd` não oferecerá suporte à conectividade com uma réplica secundária em um grupo de disponibilidade AlwaysOn. Para obter mais informações, consulte [Driver ODBC no Linux e macOS – alta disponibilidade e recuperação de desastres](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md).  
  
> [!NOTE]  
> Não há suporte para **-K** no CTP para SUSE Linux. No entanto, você pode especificar a palavra-chave **ApplicationIntent=ReadOnly** em um arquivo DSN passado para o `sqlcmd`. Para obter mais informações, veja "Suporte para DSN no `sqlcmd` e no `bcp`" no final deste tópico.  
  
- -l *timeout* especifica o número de segundos antes que um logon no `sqlcmd` expire quando você tentar se conectar a um servidor.

- -m *error_level* Controlar quais mensagens de erro são enviadas para stdout.  
  
- **-M**_com várias sub-redes\_failover_  
Sempre especifique **-M** ao se conectar ao ouvinte do grupo de disponibilidade de um grupo de disponibilidade do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] ou de uma Instância de Cluster de Failover do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]. **-M** proporciona maior rapidez na detecção de failovers e conexão ao servidor ativo (no momento). Se **-M** não for especificado, **-M** estará desativado. Para obter mais informações sobre [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)], consulte [Driver ODBC no Linux e macOS – alta disponibilidade e recuperação de desastres](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md).  
  
> [!NOTE]  
> Não há suporte para **-M** no CTP para SUSE Linux. No entanto, você pode especificar a palavra-chave **MultiSubnetFailover=Yes** em um arquivo DSN passado para o `sqlcmd`. Para obter mais informações, veja "Suporte para DSN no `sqlcmd` e no `bcp`" no final deste tópico.  
  
- -N Criptografar a conexão.  
  
- -o *output_file* Identificar o arquivo que recebe a saída do `sqlcmd`.  
  
- -p Imprimir as estatísticas de desempenho de cada conjunto de resultados.  
  
- -P Especificar uma senha de usuário.  
  
- -q *commandline_query* executar uma consulta quando `sqlcmd` é iniciado, mas não é encerrado quando a consulta for concluída.  

- -Q *commandline_query* executar uma consulta quando `sqlcmd` é iniciado. O `sqlcmd` será fechado quando a consulta for concluída.  

- -r Redireciona as mensagens de erro para stderr.

- -R Faz o driver usar as configurações regionais do cliente para converter dados de moeda e data e hora em dados de caractere. Atualmente usa apenas formatação em en_US (inglês dos EUA).
  
- -s *column_separator_char* especifique o caractere separador de coluna.  

- -S [*protocol*:] *server*[**,**_port_]  
Especifique a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para se conectar ao, ou se -D for usado, um DSN. O driver ODBC no Linux e macOS requer - S. Observe que **tcp** é o único protocolo válido.  
  
- -t *query_timeout* Especificar o número de segundos antes de um comando (ou instrução SQL) expirar.  
  
- -u Especificar que output_file será armazenado em formato Unicode, independentemente do formato de input_file.  
  
- -U *login_id* especificar uma ID de logon do usuário.  
  
- -V *error_severity_level* Controlar o nível de gravidade usado para definir a variável ERRORLEVEL.  
  
- -w *column_width* especificar a largura da tela para saída.  
  
- -W Remover espaços à direita de uma coluna.  
  
- -x Desabilitar substituição de variável.  
  
- -X Desabilitar comandos, script de inicialização e variáveis de ambiente.  
  
- -y *variable_length_type_display_width* definir os `sqlcmd` variável de script `SQLCMDMAXFIXEDTYPEWIDTH`.
  
- -Y *fixed_length_type_display_width* definir os `sqlcmd` variável de script `SQLCMDMAXVARTYPEWIDTH`.


## <a name="available-commands"></a>Comandos disponíveis

Na versão atual, os seguintes comandos estão disponíveis:  
  
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
  
## <a name="unavailable-options"></a>Opções Não Disponíveis
Na versão atual, as seguintes opções não estão disponíveis:  

- -A Fazer logon no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com uma DAC (conexão de administrador dedicada). Para obter informações sobre como fazer uma DAC (conexão de administrador dedicada), veja as [Diretrizes de programação](../../../connect/odbc/linux-mac/programming-guidelines.md).  
  
- -f *code_page* Especificar as páginas de código de entrada e saída.  
  
- -L Listar os computadores servidores localmente configurados e os nomes dos computadores servidores que estão transmitindo na rede.  
  
- -v Criar uma variável de script `sqlcmd` que pode ser usada em um script `sqlcmd`.  
  
Você pode usar o seguinte método alternativo: coloque os parâmetros dentro de um arquivo, que, em seguida, você pode acrescentar a outro arquivo. Isso ajudará você a usar um arquivo de parâmetro para substituir os valores. Por exemplo, crie um arquivo chamado `a.sql` (o arquivo de parâmetro) com o seguinte conteúdo:
  
    :setvar ColumnName object_id  
    :setvar TableName sys.objects  
  
Então crie um arquivo chamado `b.sql` com os parâmetros para substituição:  
  
    select $(ColumnName) from $(TableName)  

Na linha de comando, combine `a.sql` e `b.sql` em `c.sql` usando os seguintes comandos:  
  
    cat a.sql > c.sql 
  
    cat b.sql >> c.sql  
  
Execute `sqlcmd` e use `c.sql` como arquivo de entrada:  
  
    slqcmd -S<...> -P<..> -U<..> -I c.sql  

- -z *senha* alterar a senha.  
  
- -Z *senha* alterar senha e sair.  

## <a name="unavailable-commands"></a>Comandos não disponíveis

Na versão atual, os seguintes comandos não estão disponíveis:  
  
-   :ED  
  
-   :ServerList  
  
-   :XML  
  
## <a name="dsn-support-in-sqlcmd-and-bcp"></a>Suporte para DSN no sqlcmd e no bcp

Você poderá especificar um nome da fonte de dados (DSN) em vez de um nome do servidor na opção **sqlcmd** ou **bcp** `-S` (ou o comando **sqlcmd** :Connect) se especificar -D. -D faz com que **sqlcmd** ou **bcp** para se conectar ao servidor especificado no DSN, a opção -S.  
  
DSNs de sistema são armazenados na `odbc.ini` arquivo no diretório SysConfigDir do ODBC (`/etc/odbc.ini` nas instalações padrão). DSNs do usuário são armazenados no `.odbc.ini` no diretório base de um usuário (`~/.odbc.ini`).
  
Há suporte para as seguintes entradas em um DSN em Linux ou macOS:

-   **ApplicationIntent=ReadOnly**  

-   **Banco de dados =**_banco de dados\_nome_  
  
-   **Driver = ODBC Driver 11 para SQL Server** ou **Driver = ODBC Driver 13 para SQL Server**
  
-   **MultiSubnetFailover=Yes**  
  
-   **Server =**_server\_nome\_ou\_IP\_endereço_  
  
-   **Trusted_Connection=yes**|**no**  
  
Em um DSN, apenas a entrada DRIVER é necessária, mas para se conectar a um servidor, o `sqlcmd` ou o `bcp` precisa do valor na entrada SERVER.  

Se a mesma opção for especificada tanto no DSN quanto na linha de comando do `sqlcmd` ou do `bcp`, a opção de linha de comando substituirá o valor usado no DSN. Por exemplo, se o DSN tiver uma entrada DATABASE e a linha de comando do `sqlcmd` incluir **-d**, o valor passado para **-d** será usado. Se **Trusted_Connection=yes** for especificado no DSN, a autenticação Kerberos será usada e o nome de usuário (**–U**) e a senha (**–P**), se fornecidos, serão ignorados.

Os scripts existentes que invocam `isql` podem ser modificados para usar `sqlcmd` com a definição do seguinte alias: `alias isql="sqlcmd -D"`.  

## <a name="see-also"></a>Consulte Também  
[Conectando-se ao **bcp**](../../../connect/odbc/linux-mac/connecting-with-bcp.md)  
 
