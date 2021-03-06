---
title: Conectando com sqlcmd
description: Saiba como usar o utilitário sqlcmd com o Microsoft ODBC Driver for SQL Server no Linux e no macOS.
ms.custom: ''
ms.date: 06/22/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sqlcmd
ms.assetid: 61a2ec0d-1bcb-4231-bea0-cff866c21463
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5d69f1a19e0494b7426eebbac7d8732794f90be8
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987902"
---
# <a name="connecting-with-sqlcmd"></a>Conectando com sqlcmd
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

O utilitário [sqlcmd](../../../tools/sqlcmd-utility.md) está disponível com o [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Linux e macOS.
  
Os seguintes comandos mostram como usar a Autenticação do Windows (Kerberos) e a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], respectivamente:
  
```console
sqlcmd -E -Sxxx.xxx.xxx.xxx  
sqlcmd -Sxxx.xxx.xxx.xxx -Uxxx -Pxxx  
```  
  
## <a name="available-options"></a>Opções Disponíveis

Na versão atual, as seguintes opções estão disponíveis:  
  
- -? Exibir o uso do `sqlcmd`.  
  
- -a Solicitar um tamanho de pacote.  
  
- -b Encerrar o trabalho em lotes se houver um erro.  
  
- -c *batch_terminator* Especificar o terminador de lote.  
  
- -C Confiar em certificado do servidor.  

- -d *database_name* Emitir uma instrução *database_name* do `USE` quando você iniciar o `sqlcmd`.  

- -D Faz com que o valor passado para a opção -S do `sqlcmd` seja interpretada como um nome da fonte de dados (DSN). Para obter mais informações, veja "Suporte para DSN no `sqlcmd` e no `bcp`" no final deste tópico.  
  
- -e Gravar scripts de entrada no dispositivo de saída padrão (stdout).

- =E Usar uma conexão confiável (autenticação integrada). Para obter mais informações sobre como estabelecer conexões confiáveis que usam autenticação integrada de um cliente Linux ou macOS, confira [Como usar a autenticação integrada](using-integrated-authentication.md).

- -f codepage | i:codepage[,o:codepage] | o:codepage[,i:codepage] especifica as páginas de código de entrada e saída. O número da página de código é um valor numérico que especifica uma página de código do Linux instalada.
(disponível desde 17.5.1.1)

- -h *number_of_rows* Especificar o número de linhas a serem impressas entre os títulos das colunas.  
  
- -H Especificar um nome de estação de trabalho.  
  
- -i *input_file*[,*input_file*[,…]] Identificar o arquivo que contém um lote de instruções SQL ou procedimentos armazenados.  
  
- -I Definir a opção de conexão `SET QUOTED_IDENTIFIER` como ON.  
  
- -k Remover ou substituir caracteres de controle.  
  
- **-K**_application\_intent_  
Declara o tipo de carga de trabalho de aplicativo ao conectar-se a um servidor. O único valor com suporte no momento é **ReadOnly**. Se **-K** não for especificado, o `sqlcmd` não oferecerá suporte à conectividade com uma réplica secundária em um grupo de disponibilidade AlwaysOn. Para saber mais, confira [ODBC Driver no Linux e macOS - alta disponibilidade e recuperação de desastres](odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md).  
  
> [!NOTE]  
> Não há suporte para **-K** no CTP para SUSE Linux. No entanto, você pode especificar a palavra-chave **ApplicationIntent=ReadOnly** em um arquivo DSN passado para o `sqlcmd`. Para obter mais informações, veja "Suporte para DSN no `sqlcmd` e no `bcp`" no final deste tópico.  
  
- -l *timeout* especifica o número de segundos antes que um logon no `sqlcmd` expire quando você tentar se conectar a um servidor.

- -m *error_level* Controlar quais mensagens de erro são enviadas para stdout.  
  
- **-M**_multisubnet\_failover_  
Sempre especifique **-M** ao se conectar ao ouvinte do grupo de disponibilidade de um grupo de disponibilidade do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] ou de uma Instância de Cluster de Failover do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]. **-M** proporciona maior rapidez na detecção de failovers e conexão ao servidor ativo (no momento). Se **-M** não estiver especificado, **-M** está desativado. Para saber mais sobre [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)], confira [ODBC Driver no Linux e macOS – alta disponibilidade e recuperação de desastres](odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md).  
  
> [!NOTE]  
> Não há suporte para **-M** no CTP para SUSE Linux. No entanto, você pode especificar a palavra-chave **MultiSubnetFailover=Yes** em um arquivo DSN passado para o `sqlcmd`. Para obter mais informações, veja "Suporte para DSN no `sqlcmd` e no `bcp`" no final deste tópico.  
  
- -N Criptografar a conexão.  
  
- -o *output_file* Identificar o arquivo que recebe a saída do `sqlcmd`.  
  
- -p Imprimir as estatísticas de desempenho de cada conjunto de resultados.  
  
- -P Especificar uma senha de usuário.  
  
- -q *commandline_query* Executar uma consulta quando `sqlcmd` for iniciado, mas não encerrar quando a consulta for concluída.  

- -Q *commandline_query* Executar uma consulta quando `sqlcmd` for iniciado. O `sqlcmd` será fechado quando a consulta for concluída.  

- -r Redireciona as mensagens de erro para stderr.

- -R Faz o driver usar as configurações regionais do cliente para converter dados de moeda e data e hora em dados de caractere. Atualmente usa apenas formatação em en_US (inglês dos EUA).
  
- -s *column_separator_char* Especificar o caractere separador de coluna.  

- -S [*protocol*:] *server*[ **,** _port_]  
Especificar o nome da instância de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] à qual se conectar ou, se -D for usado, um DSN. O driver ODBC no Linux e no macOS requer -S. Observe que **tcp** é o único protocolo válido.  
  
- -t *query_timeout* Especificar o número de segundos antes de um comando (ou instrução SQL) expirar.  
  
- -u Especificar que output_file será armazenado em formato Unicode, independentemente do formato de input_file.  
  
- -U *login_id* Especificar uma ID de logon do usuário.  
  
- -V *error_severity_level* Controlar o nível de gravidade usado para definir a variável ERRORLEVEL.  
  
- -w *column_width* Especificar a largura da tela para saída.  
  
- -W Remover espaços à direita de uma coluna.  
  
- -x Desabilitar substituição de variável.  
  
- -X Desabilitar comandos, script de inicialização e variáveis de ambiente.  
  
- -y *variable_length_type_display_width* Definir a variável de script `SQLCMDMAXFIXEDTYPEWIDTH` de `sqlcmd`.
  
- -Y *fixed_length_type_display_width* Definir a variável de script `SQLCMDMAXVARTYPEWIDTH` de `sqlcmd`.


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

- -A Fazer logon no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com uma DAC (conexão de administrador dedicada). Para obter informações sobre como fazer uma DAC (conexão de administrador dedicada), veja as [Diretrizes de programação](programming-guidelines.md).  
  
- -L Listar os computadores servidores localmente configurados e os nomes dos computadores servidores que estão transmitindo na rede.  
  
- -v Criar uma variável de script `sqlcmd` que pode ser usada em um script `sqlcmd`.  
  
Você pode usar o seguinte método alternativo: Coloque os parâmetros dentro de um arquivo, que você poderá depois acrescentar a outro arquivo. Isso ajudará você a usar um arquivo de parâmetro para substituir os valores. Por exemplo, crie um arquivo chamado `a.sql` (o arquivo de parâmetro) com o seguinte conteúdo:
  
```console
    :setvar ColumnName object_id  
    :setvar TableName sys.objects  
```
  
Então crie um arquivo chamado `b.sql` com os parâmetros para substituição:  
  
```sql
    select $(ColumnName) from $(TableName)  
```

Na linha de comando, combine `a.sql` e `b.sql` em `c.sql` usando os seguintes comandos:  
  
```console
    cat a.sql > c.sql 
  
    cat b.sql >> c.sql  
```
  
Execute `sqlcmd` e use `c.sql` como arquivo de entrada:  
  
```console
    sqlcmd -S<...> -P<..> -U<..> -I c.sql  
```

- -z *password* Alterar senha.  
  
- -Z *password* Alterar senha e sair.  

## <a name="unavailable-commands"></a>Comandos não disponíveis

Na versão atual, os seguintes comandos não estão disponíveis:  
  
-   :ED  
  
-   :ServerList  
  
-   :XML  
  
## <a name="dsn-support-in-sqlcmd-and-bcp"></a>Suporte para DSN no sqlcmd e no bcp

Você poderá especificar um DNS (nome da fonte de dados) em vez de um nome do servidor na opção **sqlcmd** ou **bcp** `-S` (ou no comando **sqlcmd** :Connect) se especificar `-D`. `-D` faz com que **sqlcmd** ou o **bcp** conecte-se ao servidor especificado no DSN pela opção `-S`.  
  
Os DSNs de sistema são armazenados no arquivo `odbc.ini` no diretório SysConfigDir do ODBC (`/etc/odbc.ini` nas instalações padrão). Os DSNs de usuário são armazenados no arquivo `.odbc.ini` no diretório base do usuário (`~/.odbc.ini`).

Em sistemas Windows, os DSNs do Sistema e do Usuário são armazenados no Registro e gerenciados por meio de odbcad32.exe. O bcp e o sqlcmd não dão suporte a DSNs de Arquivo.

Confira [Atributos e palavras-chave da cadeia de conexão e DSN](../dsn-connection-string-attribute.md) para ver a lista de entradas às quais o driver dá suporte.

Em um DSN, apenas a entrada DRIVER é necessária, mas para se conectar a um servidor remoto, `sqlcmd` ou `bcp` precisa de um valor no elemento SERVER. Se o elemento SERVER estiver vazio ou não estiver presente no DSN, `sqlcmd` e `bcp` tentarão se conectar à instância padrão no sistema local.

Ao usar o bcp em sistemas Windows, [!INCLUDE [sssql17-md](../../../includes/sssql17-md.md)] e anteriores exigem o driver SQL Native Client 11 (sqlncli11.dll), enquanto [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)] e posteriores exigem o Microsoft ODBC Driver 17 for SQL Server (msodbcsql17.dll).  

Se a mesma opção for especificada tanto no DSN quanto na linha de comando do `sqlcmd` ou do `bcp`, a opção de linha de comando substituirá o valor usado no DSN. Por exemplo, se o DSN tiver uma entrada DATABASE e a linha de comando do `sqlcmd` incluir **-d**, o valor passado para **-d** será usado. Se **Trusted_Connection=yes** for especificado no DSN, a autenticação Kerberos será usada e o nome de usuário ( **-U**) e a senha ( **-P**), se fornecidos, serão ignorados.

Os scripts existentes que invocam `isql` podem ser modificados para usar `sqlcmd` com a definição do seguinte alias: `alias isql="sqlcmd -D"`.  

## <a name="see-also"></a>Consulte Também  
[Conectando-se ao **bcp**](connecting-with-bcp.md)  
[Notas de Versão](release-notes-tools.md)
