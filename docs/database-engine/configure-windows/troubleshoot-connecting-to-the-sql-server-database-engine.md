---
title: Solucionar problemas de conexão com o Mecanismo de Banco de Dados do SQL Server | Microsoft Docs
description: Descubra como solucionar problemas de conexão. Veja as etapas a serem seguidas quando não for possível usar TCP/IP para se conectar a um Mecanismo de Banco de Dados do SQL Server em um servidor único.
ms.custom: sqlfreshmay19
ms.date: 11/25/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: troubleshooting
helpviewer_keywords:
- troubleshooting, connecting to Database Engine
- connecting to Database Engine, troubleshooting
ms.assetid: 474c365b-c451-4b07-b636-1653439f4b1f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: afe2679e29f92d4b222067b6ab3b5220078744e1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85763961"
---
# <a name="troubleshoot-connecting-to-the-sql-server-database-engine"></a>Solucionar problemas na conexão com o Mecanismo de Banco de Dados do SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Este artigo lista as técnicas de solução de problemas a ser usadas quando você não pode se conectar a uma instância do Mecanismo de Banco de Dados do SQL Server em um único servidor.

>[!NOTE]
>Para outros cenários, confira:
>- [Ouvinte de grupo de disponibilidade](../availability-groups/windows/listeners-client-connectivity-application-failover.md)
>- [Instâncias de cluster de failover](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)

Essas etapas não estão na ordem dos problemas mais prováveis, que você provavelmente já tentou. Essas etapas estão na ordem dos problemas mais básicos para os mais complexos. Essas etapas presumem que você está se conectando à instância do SQL Server de outro computador, usando o protocolo TCP/IP, que é a situação mais comum.

Estas instruções são úteis ao realizar a solução de problemas do erro "**Conectar-se ao Servidor**", que pode ser `Error Number: 11001 (or 53), Severity: 20, State: 0`. Este é um exemplo de uma mensagem de erro:

> `A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections.`
>
> `(provider: Named Pipes Provider, error: 40 - Could not open a connection to SQL Server) (Microsoft SQL Server, Error: 53)`
>
> `(provider: TCP Provider, error: 0 - No such host is known.) (Microsoft SQL Server, Error: 11001)`

Esse erro normalmente significa que o cliente não consegue localizar a instância do SQL Server. Isso normalmente ocorre quando há pelo menos um dos seguintes problemas:

- O nome do computador que hospeda o SQL Server
- A instância não resolve o IP correto
- O número da porta TCP não foi especificado corretamente

> [!TIP]
> Uma página interativa de solução de problemas está disponível nos Serviços de Atendimento ao Cliente da [!INCLUDE[msCoName_md](../../includes/msconame-md.md)] em [Resolvendo erros de conectividade com o SQL Server](https://support.microsoft.com/help/4009936/solving-connectivity-errors-to-sql-server).

### <a name="not-included"></a>Não incluído

- Este tópico não inclui informações sobre erros do SSPI. Para erros do SSPI, consulte [Como solucionar a mensagem de erro "Não é possível gerar contexto de SSPI"](https://support.microsoft.com/kb/811889).
- Este tópico não inclui informações sobre erros do Kerberos. Para obter ajuda, consulte [Microsoft Kerberos Configuration Manager para SQL Server](https://www.microsoft.com/download/details.aspx?id=39046).
- Este tópico não inclui informações sobre erros de Conectividade do SQL Azure. Para obter ajuda, consulte [Solução de problemas de conectividade com o Banco de Dados SQL do Microsoft Azure](/azure/sql-database/troubleshoot-connectivity-issues-microsoft-azure-sql-database).

## <a name="get-instance-name-from-configuration-manger"></a>Obter o nome da instância do Configuration Manager

No servidor que hospeda a instância de SQL Server, verifique o nome da instância. Use o [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md).

O Configuration Manager é instalado automaticamente no computador quando o SQL Server é instalado. Instruções sobre como iniciar o Configuration Manager variam ligeiramente conforme a versão do SQL Server e do Windows. Confira detalhes específicos da versão em [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md).)

1. Entre no computador que hospeda a instância do SQL Server.
1. Inicie o SQL Server Configuration Manager
1. No painel esquerdo, selecione **Serviços do SQL Server**.
1. No painel direito, verifique o nome da instância do mecanismo de banco de dados.

   - `SQL SERVER (MSSQLSERVER)` indica uma instância padrão do SQL Server. O nome da instância padrão é `<computer name>`.
   - `SQL SERVER (<instance name>)` indica uma instância nomeada do SQL Server. O nome da instância nomeada é `<computer name>\<instance name>`

## <a name="verify---the-instance-is-running"></a>Verificar – a instância está em execução

Para verificar se a instância está em execução, no Configuration Manager, procure o símbolo da instância do SQL Server.

- Uma seta verde indica que uma instância está em execução.
- Um quadrado vermelho indica que uma instância está parada.

Se a instância estiver parada, clique com o botão direito do mouse nela e clique em **Iniciar**. A instância do servidor é iniciada e o indicador muda para uma seta verde.

## <a name="verify---sql-server-browser-service-is-running"></a><a name = "startbrowser"></a> Verifique se o serviço SQL Server Browser está em execução

Para se conectar a uma instância nomeada, o serviço do SQL Server Browser deve estar em execução. No Configuration Manager, localize o serviço **SQL Server Browser** e verifique se ele está em execução. Inicie-o, caso não esteja em execução. O serviço do SQL Server Browser não é necessário para instâncias padrão.

Uma instância padrão do SQL Server não requer o serviço SQL Server Browser.

## <a name="testing-a-local-connection"></a>Como testar uma conexão local

Antes de solucionar um problema de conexão de outro computador, primeiro teste a capacidade de conectar-se de um aplicativo cliente instalado localmente no computador que executa o SQL Server. A conexão local evita problemas com firewalls e redes. 

Esse procedimento usa o SQL Server Management Studio. Se você não tiver o Management Studio instalado, consulte [Baixar o SSMS (SQL Server Management Studio)](../../ssms/download-sql-server-management-studio-ssms.md). Se não conseguir instalar o Management Studio, você pode testar a conexão, usando o utilitário `sqlcmd.exe`. `sqlcmd.exe` é instalado com o Mecanismo de Banco de Dados. Para saber mais sobre o `sqlcmd.exe`, consulte o [Utilitário sqlcmd](../../tools/sqlcmd-utility.md).)

1. Entre no computador em que o SQL Server está instalado, usando um logon com permissão para acessar o SQL Server. (Durante a instalação, o SQL Server requer que pelo menos um logon seja especificado como Administrador do SQL Server. Se você não conhece um administrador, consulte [Conectar-se ao SQL Server quando os Administradores do Sistema estiverem bloqueados](connect-to-sql-server-when-system-administrators-are-locked-out.md).)
1. Na página inicial, digite **SQL Server Management Studio**ou, em versões mais antigas do Windows, no menu Iniciar, aponte para **Todos os Programas**, **Microsoft SQL Server**e clique em **SQL Server Management Studio**.
1. Na caixa de diálogo **Conectar ao Servidor** , na caixa de tipo **Servidor** , selecione **Mecanismo de Banco de Dados**. Na caixa **Autenticação** , selecione **Autenticação do Windows**. Na caixa **Nome do servidor**, digite um dos seguintes tipos de conexão:

   |Conectando a|Type|Exemplo|
   |:-----------------|:---------------|:-----------------|
   |Instância padrão|`<computer name>`|`ACCNT27`|
   |Instância nomeada|`<computer name\instance name>`|`ACCNT27\PAYROLL`|

   > [!NOTE]
   > Ao se conectar a um SQL Server de um aplicativo cliente no mesmo computador, é usado o protocolo de memória compartilhada. A memória compartilhada é um tipo de pipe, por isso às vezes são encontrados erros relacionados a pipes.

   Se você receber um erro neste ponto, deverá resolvê-lo antes de continuar. Há muitas possibilidades que podem representar um problema. Seu logon pode não estar autorizado a se conectar. O banco de dados padrão pode estar ausente.

   > [!NOTE]
   > Algumas mensagens de erro passadas para o cliente intencionalmente não fornecem informações suficientes para solucionar o problema. Esse é um recurso de segurança para evitar o fornecimento de informações sobre o SQL Server a um invasor. Para exibir as informações completas sobre o erro, examine o log de erros do SQL Server. Os detalhes são fornecidos abaixo. 

1. Se você receber o erro `18456 Login failed for user`, o tópico dos Manuais Online [MSSQLSERVER_18456](../../relational-databases/errors-events/mssqlserver-18456-database-engine-error.md) contém informações adicionais sobre os códigos de erro. E o blog de Aaron Bertrand tem uma lista abrangente dos códigos de erro em [Solucionando o erro 18456](https://sqlblog.org/2011/01/14/troubleshooting-error-18456). Você pode exibir o log de erros com o SSMS (se puder se conectar), na seção Gerenciamento do Pesquisador de Objetos. Caso contrário, você pode exibir o log de erros com o programa do Bloco de Notas do Windows. O local padrão varia de acordo com a versão e pode ser alterado durante a instalação. O local padrão do [!INCLUDE[ssSQL15_md](../../includes/sssqlv15-md.md)] é `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Log\ERRORLOG`. 

1. Se você puder se conectar usando memória compartilhada, teste a conexão usando TCP. Você pode forçar uma conexão TCP especificando `tcp:` antes do nome. Por exemplo:

   |Conectando a:|Tipo:|Exemplo:|
   |-----------------|---------------|-----------------|
   |Instância padrão|`tcp:<computer name>`|`tcp:ACCNT27`|
   |Instância nomeada|`tcp:<computer name/instance name>`|`tcp:ACCNT27\PAYROLL`|

1. Se você puder se conectar à memória compartilhada, mas não ao TCP, você deve corrigir o problema do TCP. O problema mais provável é que o TCP não está habilitado. Para habilitar o TCP, consulte as etapas para [Habilitar protocolos](#enableprotocols) acima.

1. Se sua meta é se conectar a uma conta que não é uma conta de administrador, depois que você pode se conectar como administrador, tente realizar a conexão novamente usando o logon de Autenticação do Windows ou o logon de Autenticação do SQL Server que o aplicativo cliente usará.

## <a name="get-the-ip-address-of-the-server"></a>Obter o endereço IP do servidor

Obtenha o endereço IP do computador que hospeda a instância do SQL Server.

1. No menu Iniciar, clique em **Executar**. Na janela **Executar**, digite **cmd** e clique em **OK**.
1. No prompt de comando, digite `ipconfig` e pressione Enter. Anote os endereços **IPv4** e **IPv6** .

  >O SQL Server pode se conectar, usando o protocolo IP versão 4 ou o IP versão 6. Sua rede pode permitir um dos dois ou ambos. A maioria das pessoas começam a solucionar os problemas do endereço **IPv4** . Ele é mais curto e mais fácil de digitar.

## <a name="get-the-sql-server-instance-tcp-port"></a><a name = "getTCP"></a>Obter a porta TCP da instância do SQL Server

Na maioria dos casos, você está se conectando ao Mecanismo de Banco de Dados de outro computador, usando o protocolo TCP.

1. Usando o SQL Server Management Studio no computador que executa o SQL Server, conecte-se à instância do SQL Server. No Pesquisador de Objetos, expanda **Gerenciamento**, **Logs do SQL Server**e clique duas vezes no log atual.
2. No Visualizador de Log, clique no botão **Filtro** na barra de ferramentas. Na caixa **Mensagem contém o texto**, digite `server is listening on`, clique em **Aplicar filtro** e em **OK**.
3. Uma mensagem semelhante a `Server is listening on [ 'any' <ipv4> 1433]` deve estar listada. 

Esta mensagem indica que esta instância do SQL Server está escutando em todos os endereços IP deste computador (para IP versão 4) e está escutando a porta TCP 1433. (A porta TCP 1433 geralmente é a porta usada pelo Mecanismo de Banco de Dados ou uma instância padrão do SQL Server. Somente uma instância do SQL Server pode usar uma porta, portanto, se houver mais de uma instância do SQL Server instalado, algumas instâncias devem usar outros números de porta.) Anote o número da porta usada pela instância [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] à qual você está tentando se conectar.

  > [!NOTE]
  > `IP address 127.0.0.1` provavelmente está listado. Isso é chamado de endereço do adaptador de loopback. Somente os processos no mesmo computador podem usá-lo para se conectar. Pode ser útil para solucionar problemas, mas você não pode usá-lo para se conectar de outro computador.

## <a name="enable-protocols"></a><a name = "enableprotocols"></a>Habilitar Protocolos

Em algumas instalações do SQL Server, conectar-se ao Mecanismo de Banco de Dados de outro computador não está habilitada, a menos que o administrador use o Configuration Manager para habilitá-lo. Para habilitar conexões de outro computador:

1. Abra o SQL Server Configuration Manager como descrito anteriormente.
1. Usando o Configuration Manager, no painel esquerdo, expanda **Configuração de Rede do SQL Server**e selecione a instância do SQL Server que você deseja se conectar. O painel direito lista os protocolos de conexão disponíveis. Normalmente, a memória compartilhada está habilitada. Ele só pode ser usado no mesmo computador, por isso a maioria das instalações deixam a memória compartilhada habilitada. Para conectar-se ao SQL Server de outro computador, você normalmente usa o TCP/IP. Se o TCP/IP não estiver habilitado, clique com o botão direito do mouse em **TCP/IP**e depois clique em **Habilitar**.
1. Se você alterou a configuração habilitada para qualquer protocolo, reinicie o Mecanismo de Banco de Dados. No painel esquerdo, selecione **Serviços do SQL Server**. No painel direito, clique com o botão direito do mouse na instância do Mecanismo de Banco de Dados e clique em **Reiniciar**.

## <a name="testing-tcpip-connectivity"></a><a name="testTCPIP"></a>Como testar a conectividade TCP/IP

Conectar ao SQL Server usando TCP/IP requer que o Windows possa estabelecer a conexão. Use a ferramenta `ping` para testar TCP.

1. No menu Iniciar, clique em **Executar**. Na janela **Executar** , digite **cmd**e clique em **OK**. 
1. Na janela do prompt de comando, digite `ping <ip address>` e o endereço IP do computador que está executando o SQL Server. Por exemplo:

    - IPv4: `ping 192.168.1.101`
    - IPv6: `ping fe80::d51d:5ab5:6f09:8f48%11`

1. Se a sua rede estiver configurada corretamente, `ping` retornará `Reply from <IP address>` seguido por algumas informações adicionais. Se `ping` retornar `Destination host unreachable` ou `Request timed out`, então o TCP/IP não está configurado corretamente. Neste ponto, os erros podem indicar um problema com o computador cliente, o computador do servidor ou algo na rede, como um roteador. Para solucionar problemas de rede, confira[Solução de problemas avançados para TCP/IP](/windows/client-management/troubleshoot-tcpip).
1. Em seguida, se o teste de ping foi bem-sucedido usando o endereço IP, teste se o nome do computador pode ser resolvido para o endereço TCP/IP. No computador cliente, na janela do prompt de comando, digite `ping` e o nome do computador que está executando o SQL Server. Por exemplo, `ping newofficepc` 
1. Se o `ping` para o endereço IP for bem-sucedido, mas o `ping` para o computador retornar `Destination host unreachable` ou `Request timed out`, você pode ter informações de resolução de nome (obsoleto) antigo armazenado em cache no computador cliente. Digite `ipconfig /flushdns` para limpar o cache de DNS (Resolução de Nome Dinâmico). Em seguida, execute ping no computador por nome novamente. Com o cache DNS vazio, o computador cliente verificará as informações mais recentes sobre o endereço IP do computador servidor. 
1. Se a sua rede estiver configurada corretamente, `ping` retornará `Reply from <IP address>` seguido por algumas informações adicionais. Se você conseguir executar o ping do computador servidor pelo endereço IP, mas receber um erro, como `Destination host unreachable.` ou `Request timed out.` ao executar o ping pelo nome do computador, então a resolução do nome não está configurada corretamente. (Para obter mais informações, consulte o artigo de 2006 mencionado anteriormente, [Como solucionar problemas básicos de TCP/IP](https://support.microsoft.com/kb/169790).) A resolução de nome bem-sucedida não é necessária para se conectar ao SQL Server, mas se o nome do computador não puder ser resolvido para um endereço IP, as conexões devem ser feitas especificando o endereço IP. A resolução de nome pode ser corrigida posteriormente.

## <a name="open-a-port-in-the-firewall"></a>Abrir uma porta no firewall

Por padrão, o firewall do Windows está ativado e bloqueia conexões de outro computador. Para se conectar usando TCP/IP de outro computador, no computador do SQL Server, que você deve configurar o firewall para permitir conexões para a porta TCP usada pelo Mecanismo de Banco de Dados. A instância padrão está escutando na porta TCP 1433, por padrão. Se você tiver instâncias nomeadas ou se alterou a porta da instância padrão, a porta TCP [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] poderá estar escutando em outra porta. Confira [Obter a porta TCP da instância do SQL Server](#getTCP).

Se você estiver se conectando a uma instância nomeada ou uma porta diferente da porta TCP 1433, também deverá abrir a porta 1434 UDP para o serviço de Navegador do SQL Server. Para obter instruções passo a passo para configurar o Firewall do Windows, consulte [Configurar um Firewall do Windows para acesso ao Mecanismo de Banco de Dados](configure-a-windows-firewall-for-database-engine-access.md).

## <a name="test-the-connection"></a>Testar a conexão

Depois de se conectar usando TCP no mesmo computador, é hora de tentar se conectar do computador cliente. Teoricamente, você pode usar qualquer aplicativo cliente, porém para evitar complexidade adicional, instale as ferramentas de Gerenciamento do SQL Server no cliente e tente usar o SQL Server Management Studio.

1. No computador cliente, usando o SQL Server Management Studio, tente se conectar usando o endereço IP e o número da porta TCP no formato endereço IP, vírgula e número da porta. Por exemplo, `192.168.1.101,1433`. Se essa conexão falhar, então você provavelmente tem um dos seguintes problemas:

   - `ping` no endereço IP não funciona, indicando um problema de configuração geral do TCP. Volte para a seção [Testar conectividade TCP/IP](#testTCPIP).
   - O SQL Server não está escutando no protocolo TCP. Volte para a seção [Habilitar protocolos](#enableprotocols).
   - O SQL Server está escutando em uma porta diferente da porta que você especificou. Volte para a seção [Obter o número da porta TCP](#getTCP).
   - A porta TCP do SQL Server está sendo bloqueada pelo firewall. Volte para a seção [Abrir uma porta no firewall](#open-a-port-in-the-firewall).

2. Depois de se conectar usando o endereço IP e o número da porta, tente se conectar usando o endereço IP sem um número de porta. Para uma instância padrão, basta usar o endereço IP. Para uma instância nomeada, use o endereço IP e o nome da instância no formato endereço IP barra invertida nome da instância, por exemplo, `192.168.1.101\<instance name>`. Se isso não funcionar, você provavelmente tem um dos seguintes problemas:

   - Se você estiver se conectando à instância padrão, ele pode estar escutando em uma porta diferente da porta 1433 TCP e o cliente não está tentando se conectar ao número da porta correto.
   - Se você estiver se conectando a uma instância nomeada, o número da porta não está sendo retornado ao cliente.

   Ambos os problemas são relacionados ao serviço de Navegador do SQL Server, que fornece o número da porta para o cliente. As soluções são:

   - Iniciar o serviço de Navegador do SQL Server. Confira as instruções para [Iniciar o navegador no SQL Server Configuration Manager](#startbrowser).
   - O serviço de Navegador do SQL Server está sendo bloqueada pelo firewall. Abra a porta UDP 1434 no firewall. Volte para a seção [Abrir uma porta no firewall](#open-a-port-in-the-firewall). Verifique se você está abrindo uma porta UDP, não uma porta TCP.
   - As informações da porta UDP 1434 estão sendo bloqueadas por um roteador. A comunicação UDP (protocolo UDP) não foi projetada para passar por roteadores. Isso impede que a rede seja preenchida por tráfego de baixa prioridade. É possível configurar o roteador para encaminhar tráfego UDP ou você pode optar por sempre fornecer o número da porta ao conectar.
   - Se o computador cliente estiver usando o Windows 7 ou o Windows Server 2008 (ou um sistema operacional mais recente), o tráfego UDP pode ser descartado pelo sistema operacional do cliente porque a resposta do servidor é retornada de um endereço IP diferente daquele foi consultado. Esse é um bloqueio do recurso de segurança "mapeamento de origem flexível". Para obter mais informações, confira a seção **Vários endereços IP do servidor** do tópico dos Manuais Online [Solução de problemas: tempo limite esgotado](https://msdn.microsoft.com/library/ms190181.aspx). Este é um artigo do SQL Server 2008 R2, mas as entidades ainda se aplicam. É possível configurar o cliente para usar o endereço IP correto ou você pode optar por sempre fornecer o número da porta ao conectar.

3. Depois que você se conectar, usando o endereço IP (ou o endereço IP e o nome de instância para uma instância nomeada), tente se conectar, usando o nome do computador (ou o nome do computador e o nome de instância para uma instância nomeada). Coloque `tcp:` na frente do nome do computador para forçar uma conexão TCP/IP. Por exemplo, para a instância padrão em um computador chamada `ACCNT27`, use `tcp:ACCNT27` . Para uma instância nomeada chamada `PAYROLL`no computador em questão, use `tcp:ACCNT27\PAYROLL` . Se você puder se conectar usando o endereço IP, mas não usando o nome do computador, isso significa que ocorreu um problema de resolução de nome. Volte para a seção **Testar conectividade TCP/IP**, a seção 4.

4. Depois que você se conectar usando o nome do computador forçando TCP, tente conectar usando o nome do computador, mas sem forçar TCP. Por exemplo, para uma instância padrão, use apenas o nome de computador, como `CCNT27` . Para uma instância nomeada, use o nome do computador e da instância, como `ACCNT27\PAYROLL` . Se você puder conectar forçando TCP, mas não sem forçar TCP, o cliente provavelmente está usando outro protocolo (como pipes nomeados, por exemplo).

    1. No computador cliente, usando o SQL Server Configuration Manager, no painel esquerdo, expanda **Configuração** *versão* **Configuração** e selecione **Protocolos do Cliente**.
    2. No painel direito, verifique se TCP/IP está habilitado. Se o TCP/IP estiver desabilitado, clique com o botão direito do mouse em **TCP/IP** e depois clique em **Habilitar**.
    3. Verifique se a ordem de protocolo de TCP/IP é um número menor do que os protocolos de pipes nomeados (ou VIA em versões anteriores). Em geral, você deve deixar a memória compartilhada como a ordem 1 e TCP/IP como a ordem 2. A memória compartilhada só é usada quando o cliente e o SQL Server estão em execução no mesmo computador. Todos os protocolos habilitados são testados em ordem até obter êxito, exceto que a memória compartilhada é ignorada quando a conexão não está no mesmo computador.
