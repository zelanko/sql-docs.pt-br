---
title: Solução de problemas de conexão com o Mecanismo de Banco de Dados do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/07/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- troubleshooting, connecting to Database Engine
- connecting to Database Engine, troubleshooting
ms.assetid: 474c365b-c451-4b07-b636-1653439f4b1f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c491a67b55db4a730db2bb7fcd8977162657e516
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52410903"
---
# <a name="troubleshoot-connecting-to-the-sql-server-database-engine"></a>Solucionar problemas na conexão com o Mecanismo de Banco de Dados do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Esta é uma lista extensa de técnicas de solução de problemas a serem usadas quando você não conseguir se conectar ao Mecanismo de Banco de Dados do SQL Server. Essas etapas não estão na ordem dos problemas mais prováveis, que você provavelmente já tentou. Essas etapas estão na ordem dos problemas mais básicos para os mais complexos. Essas etapas presumem que você está se conectando ao SQL Server de outro computador usando o protocolo TCP/IP, que é a situação mais comum. Essas etapas foram escritas para SQL Server 2016 com o SQL Server e os aplicativos clientes em execução no Windows 10, porém as etapas geralmente se aplicam a outras versões do SQL Server e outros sistemas operacionais com apenas ligeiras modificações.

Essas instruções são especialmente úteis ao solucionar o erro "**Conectar ao Servidor**" erro, que pode ser o Erro Número: 11001 (ou 53), Severidade: 20, Estado: 0, bem como mensagens de erro como:

*   “Ocorreu um erro relacionado à rede ou específico da instância ao estabelecer uma conexão com o SQL Server. O servidor não foi localizado ou não estava acessível. Verifique se o nome de instância está correto e se o SQL Server está configurado para permitir conexões remotas. " 

*   "(provedor: Provedor de Pipes Nomeados, erro: 40 – não foi possível abrir uma conexão com o SQL Server) (Microsoft SQL Server, erro: 53)" ou "(provedor: Provedor TCP, erro: 0 - Nenhum host desse tipo é conhecido.) (Microsoft SQL Server, Erro: 11001) " 

Esse erro geralmente significa que o computador do SQL Server não pode ser encontrado ou o número da porta TCP é desconhecido, não é o número de porta correto ou está bloqueado por um firewall.

>  [!TIP]
>  Uma página interativa de solução de problemas está disponível nos Serviços de Atendimento ao Cliente da [!INCLUDE[msCoName_md](../../includes/msconame-md.md)] em [Resolvendo erros de conectividade com o SQL Server](https://support.microsoft.com/help/4009936/solving-connectivity-errors-to-sql-server).

### <a name="not-included"></a>Não incluído

* Este tópico não inclui informações sobre erros do SSPI. Para erros do SSPI, consulte [Como solucionar a mensagem de erro "Não é possível gerar contexto de SSPI"](https://support.microsoft.com/kb/811889).  
* Este tópico não inclui informações sobre erros do Kerberos. Para obter ajuda, consulte [Microsoft Kerberos Configuration Manager para SQL Server](https://www.microsoft.com/download/details.aspx?id=39046).
* Este tópico não inclui informações sobre erros de Conectividade do SQL Azure. Para obter ajuda, consulte [Solução de problemas de conectividade com o Banco de Dados SQL do Microsoft Azure](https://support.microsoft.com/help/10085/troubleshooting-connectivity-issues-with-microsoft-azure-sql-database). 

## <a name="gathering-information-about-the-instance-of-sql-server"></a>Coletar informações sobre a instância do SQL Server

Primeiro você deve coletar informações básicas sobre o mecanismo de banco de dados.

1. Confirme se que a instância do Mecanismo de Banco de Dados do SQL Server está instalado e em execução.
    1.  Faça logon no computador que hospeda a instância do SQL Server.
    2.  Inicie o SQL Server Configuration Manager (O Configuration Manager é instalado automaticamente no computador quando o SQL Server é instalado. Instruções sobre como iniciar o Configuration Manager variam ligeiramente conforme a versão do SQL Server e do Windows. Para obter ajuda sobre como iniciar o Configuration Manager, consulte [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md).)
    3.  Usando o Configuration Manager, no painel esquerdo, selecione **Serviços do SQL Server**. No painel direito, confirme se a instância do Mecanismo de Banco de Dados está presente e em execução. Uma instância chamada **SQL Server (MSSQLSERVER)** é uma instância padrão (sem nome). Pode haver somente um perfil público padrão. Outras instâncias (nomeadas) terão seus nomes listados entre parênteses. O SQL Server Express usa o nome **SQL Server (SQLEXPRESS)** como o nome da instância, a menos que alguém o renomeie durante a instalação. Anote o nome da instância à qual você está tentando se conectar. Além disso, confirme se a instância está em execução buscando a seta verde. Se a instância tiver um quadrado vermelho, clique com o botão direito do mouse nela e clique em **Iniciar**. Ele deverá ficar verde.
     4. Se você está tentando se conectar a uma instância nomeada, verifique se que o serviço do Navegador do SQL Server está em execução.
 

2.  Obtenha o endereço IP do computador.
    1. No menu Iniciar, clique em **Executar**. Na janela **Executar** , digite **cmd**e clique em **OK**.
    2.  Na janela do prompt de comando, digite **ipconfig** e pressione ENTER. Anote os endereços **IPv4** e **IPv6** . (O SQL Server pode se conectar usando o protocolo IP versão 4 mais antigo ou o IP versão 6 mais recente. Sua rede pode permitir um dos dois ou ambos. A maioria das pessoas começam a solucionar os problemas do endereço **IPv4** . Ele é mais curto e mais fácil de digitar.)


3.  Obter o número da porta TCP usada pelo SQL Server. Na maioria dos casos você está se conectando ao Mecanismo de Banco de dados de outro computador usando o protocolo TCP.
    1.  Usando o SQL Server Management Studio no computador que executa o SQL Server, conecte-se à instância do SQL Server. No Pesquisador de Objetos, expanda **Gerenciamento**, **Logs do SQL Server**e clique duas vezes no log atual.
    2.  No Visualizador de Log, clique no botão **Filtro** na barra de ferramentas. Na caixa **Mensagem contém o texto** , digite **o servidor está escutando em**, clique em **Aplicar filtro**e em **OK**.
    3.  Uma mensagem semelhante a **O servidor está escutando em [“any” \<ipv4> 1433]** deve estar listada. Esta mensagem indica que esta instância do SQL Server está escutando em todos os endereços IP deste computador (para IP versão 4) e está escutando a porta TCP 1433. (A porta TCP 1433 geralmente é usada pelo Mecanismo de Banco de Dados. Somente uma instância do SQL Server pode usar uma porta, portanto, se houver mais de uma instância do SQL Server instalado, algumas instâncias devem usar outros números de porta.) Anote o número da porta usado pela instância do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] à qual você está tentando se conectar. 

    >    [!NOTE] 
    >    O endereço IP 127.0.0.1 provavelmente está listado. Ele é chamado de endereço de adaptador de loopback e só pode ser conectado de processos no mesmo computador. Pode ser útil para solucionar problemas, mas você não pode usá-lo para se conectar de outro computador.

## <a name="enable-protocols"></a>Habilitar Protocolos

Em algumas instalações do SQL Server, conectar-se ao Mecanismo de Banco de Dados de outro computador não está habilitada, a menos que o administrador use o Configuration Manager para habilitá-lo. Para habilitar conexões de outro computador:

1.  Abra o SQL Server Configuration Manager como descrito anteriormente. 
2.  Usando o Configuration Manager, no painel esquerdo, expanda **Configuração de Rede do SQL Server**e selecione a instância do SQL Server que você deseja se conectar. O painel direito lista os protocolos de conexão disponíveis. Normalmente, a memória compartilhada está habilitada. Ele só pode ser usado no mesmo computador, por isso a maioria das instalações deixam a memória compartilhada habilitada. Para conectar-se ao SQL Server de outro computador, você normalmente usará TCP/IP. Se o TCP/IP não estiver habilitado, clique com o botão direito do mouse em **TCP/IP**e depois clique em **Habilitar**. 
3.  Se você alterou a configuração habilitada para qualquer protocolo, você deve reiniciar o Mecanismo de Banco de Dados. No painel esquerdo, selecione **Serviços do SQL Server**. No painel direito, clique com o botão direito do mouse na instância do Mecanismo de Banco de Dados e clique em **Reiniciar**. 

## <a name="testing-tcpip-connectivity"></a>Testando a conectividade TCP/IP

Conectar ao SQL Server usando TCP/IP requer que o Windows possa estabelecer a conexão. Use a ferramenta `ping` para testar TCP.
1.  No menu Iniciar, clique em **Executar**. Na janela **Executar** , digite **cmd**e clique em **OK**. 
2.  Na janela do prompt de comando, digite `ping` e o endereço IP do computador que está executando o SQL Server. Por exemplo, `ping 192.168.1.101` usando um endereço IPv4 ou `ping fe80::d51d:5ab5:6f09:8f48%11` usando um endereço IPv6. (Você deve substituir os números depois do ping com os endereços IP no computador reunido anteriormente.) 
3.  Se a rede estiver configurada corretamente, você receberá uma resposta como **Resposta de \<IP address>**, seguido por algumas informações adicionais. Se você receber um erro como **Host de destino inacessível.** ou a **solicitação atingiu o tempo limite.** e TCP/IP não está configurado corretamente. (Verifique se o endereço IP está correto e se foi digitado corretamente.) Neste ponto, os erros podem indicar um problema com o computador cliente, o computador do servidor ou algo na rede, como um roteador. A Internet tem muitos recursos para solução de problemas de TCP/IP. Um ponto inicial razoável é este artigo de 2006, [Como solucionar problemas básicos de TCP/IP](https://support.microsoft.com/kb/169790).
4.  Em seguida, se o teste de ping foi bem-sucedido usando o endereço IP, teste se o nome do computador pode ser resolvido para o endereço TCP/IP. No computador cliente, na janela do prompt de comando, digite `ping` e o nome do computador que está executando o SQL Server. Por exemplo, `ping newofficepc` 
5.  Se você puder executar ping do endereço IP, mas agora receber um erro como **Host de destino inacessível.** ou a **solicitação atingiu o tempo limite.** você pode ter informações de resolução de nome antigo (obsoleto) armazenadas em cache no computador cliente. Digite `ipconfig /flushdns` para limpar o cache de DNS (Resolução de Nome Dinâmico). Em seguida, execute ping no computador por nome novamente. Com o cache DNS vazio, o computador cliente verificará as informações mais recentes sobre o endereço IP do computador servidor. 
6.  Se a rede estiver configurada corretamente, você receberá uma resposta como **Resposta de \<IP address>**, seguido por algumas informações adicionais. Se você puder executar ping no computador do servidor pelo endereço IP com êxito, mas recebe um erro como **Host de destino inacessível.** ou a **solicitação atingiu o tempo limite.** ao executar ping por nome do computador e, em seguida, a resolução de nomes não está configurada corretamente. (Para obter mais informações, consulte o artigo de 2006 mencionado anteriormente, [Como solucionar problemas básicos de TCP/IP](https://support.microsoft.com/kb/169790).) A resolução de nome bem-sucedida não é necessária para se conectar ao SQL Server, mas se o nome do computador não puder ser resolvido para um endereço IP, as conexões devem ser feitas especificando o endereço IP. Isso não é ideal, mas a resolução de nomes pode ser corrigida posteriormente.
  
  
## <a name="testing-a-local-connection"></a>Testando uma conexão local

Antes de solucionar um problema de conexão de outro computador, primeiro teste a capacidade de conectar-se de um aplicativo cliente instalado no computador que executa o SQL Server. (Isso evitará problemas de firewall.) Esse procedimento usa o SQL Server Management Studio. Se você não tiver o Management Studio instalado, consulte [Baixar o SSMS (SQL Server Management Studio)](../../ssms/download-sql-server-management-studio-ssms.md). (Se você não conseguir instalar o Management Studio, poderá testar a conexão usando o utilitário `sqlcmd.exe` que é instalado com o Mecanismo de Banco de Dados. Para saber mais sobre o `sqlcmd.exe`, consulte o [Utilitário sqlcmd](../../tools/sqlcmd-utility.md).)
1.  Faça logon no computador em que o SQL Server está instalado usando um logon com permissão para acessar o SQL Server. (Durante a instalação, o SQL Server requer que pelo menos um logon seja especificado como Administrador do SQL Server. Se você não conhece um administrador, consulte [Conectar-se ao SQL Server quando os Administradores do Sistema estiverem bloqueados](connect-to-sql-server-when-system-administrators-are-locked-out.md).)
2.   Na página inicial, digite **SQL Server Management Studio**ou, em versões mais antigas do Windows, no menu Iniciar, aponte para **Todos os Programas**, **Microsoft SQL Server**e clique em **SQL Server Management Studio**.
3.  Na caixa de diálogo **Conectar ao Servidor** , na caixa de tipo **Servidor** , selecione **Mecanismo de Banco de Dados**. Na caixa **Autenticação** , selecione **Autenticação do Windows**. Na caixa **Nome do servidor** , digite uma das seguintes opções:

|Conectando a:|Tipo:|Exemplo:|
|-----------------|---------------|-----------------|
|Instância padrão|O nome do computador|ACCNT27|
|Instância nomeada|O nome do computador\instância|ACCNT27\PAYROLL|

>  [!NOTE] 
>  Ao se conectar a um SQL Server de um aplicativo cliente no mesmo computador, é usado o protocolo de memória compartilhada. A memória compartilhada é um tipo de pipe, por isso às vezes são encontrados erros relacionados a pipes.

Se você receber um erro neste ponto, deverá resolvê-lo antes de continuar. Há muitas possibilidades que podem representar um problema. Seu logon pode não estar autorizado a se conectar. O banco de dados padrão pode estar ausente.

>    [!NOTE] 
>    Algumas mensagens de erro passadas para o cliente intencionalmente não fornecem informações suficientes para solucionar o problema. Esse é um recurso de segurança para evitar o fornecimento de informações sobre o SQL Server a um invasor. Para exibir as informações completas sobre o erro, examine o log de erros do SQL Server. Os detalhes são fornecidos abaixo. Se você estiver recebendo o erro **18456 Logon falhou para usuário**, o tópico dos Manuais Online [MSSQLSERVER_18456](../../relational-databases/errors-events/mssqlserver-18456-database-engine-error.md) contém informações adicionais sobre códigos de erro. E o blog de Aaron Bertrand tem uma lista abrangente dos códigos de erro em [Solucionando o erro 18456](https://www2.sqlblog.com/blogs/aaron_bertrand/archive/2011/01/14/sql-server-v-next-denali-additional-states-for-error-18456.aspx). Você pode exibir o log de erros com o SSMS (se puder se conectar), na seção Gerenciamento do Pesquisador de Objetos. Caso contrário, você pode exibir o log de erros com o programa do Bloco de Notas do Windows. O local padrão varia de acordo com a versão e pode ser alterado durante a instalação. O local padrão do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] é `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Log\ERRORLOG`.  

4.   Se você puder se conectar usando memória compartilhada, teste a conexão usando TCP. Você pode forçar uma conexão TCP especificando **tcp:** antes do nome. Por exemplo:

|Conectando a:|Tipo:|Exemplo:|
|-----------------|---------------|-----------------|
|Instância padrão|tcp: o nome do computador|tcp:ACCNT27|
|Instância nomeada|tcp: o nome do computador/instância|tcp:ACCNT27\PAYROLL|
  
Se você puder se conectar à memória compartilhada, mas não ao TCP, você deve corrigir o problema do TCP. O problema mais provável é que o TCP não está habilitado. Para habilitar o TCP, consulte as etapas para **Habilitar protocolos** acima.

5.   Se sua meta é se conectar a uma conta que não é uma conta de administrador, depois que você pode se conectar como administrador, tente realizar a conexão novamente usando o logon de Autenticação do Windows ou o logon de Autenticação do SQL Server que o aplicativo cliente usará.

## <a name="opening-a-port-in-the-firewall"></a>Abrindo uma porta no Firewall

Desde vários anos atrás, com o Windows XP Service Pack 2, o Firewall do Windows está ativado e bloqueia conexões de outro computador. Para se conectar usando TCP/IP de outro computador, no computador do SQL Server, que você deve configurar o firewall para permitir conexões para a porta TCP usada pelo Mecanismo de Banco de Dados. Como mencionamos anteriormente, a instância padrão geralmente escuta na porta TCP 1433. Se você tiver instâncias nomeadas ou se alterou o padrão, a porta TCP [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] poderá estar escutando em outra porta. Consulte a seção inicial sobre como coletar informações para determinar a porta.  
Se você estiver se conectando a uma instância nomeada ou uma porta diferente da porta TCP 1433, também deverá abrir a porta 1434 UDP para o serviço de Navegador do SQL Server. Para obter instruções passo a passo para configurar o Firewall do Windows, consulte [Configurar um Firewall do Windows para acesso ao Mecanismo de Banco de Dados](configure-a-windows-firewall-for-database-engine-access.md).

## <a name="testing-the-connection"></a>Testando a conexão

Depois de se conectar usando TCP no mesmo computador, é hora de tentar se conectar do computador cliente. Teoricamente, você pode usar qualquer aplicativo cliente, porém para evitar complexidade adicional, instale as ferramentas de Gerenciamento do SQL Server no cliente e tente usar o SQL Server Management Studio.

1. No computador cliente, usando o SQL Server Management Studio, tente se conectar usando o endereço IP e o número da porta TCP no formato endereço IP, vírgula e número da porta. Por exemplo, **192.168.1.101,1433** . Se não funcionar, você provavelmente tem um dos seguintes problemas:

    * Realizar**ping** no endereço IP não funciona, indicando um problema de configuração geral do TCP. Volte para a seção **Testar conectividade TCP/IP**. 
    *   O SQL Server não está escutando no protocolo TCP. Volte para a seção **Habilitar Protocolos**. 
    *   O SQL Server está escutando em uma porta diferente da porta que você especificou. Volte para a seção **Coletar informações sobre a instância do SQL Server**. 
    *   A porta TCP do SQL Server está sendo bloqueada pelo firewall. Volte para a seção **Abrir uma porta no Firewall**.


2. Depois de se conectar usando o endereço IP e o número da porta, tente se conectar usando o endereço IP sem um número de porta. Para uma instância padrão, basta usar o endereço IP. Para uma instância nomeada, use o endereço IP e o nome da instância no formato IP endereço barra invertida nome da instância, por exemplo **192.168.1.101\PAYROLL** . Se isso não funcionar, você provavelmente tem um dos seguintes problemas:

    *   Se você estiver se conectando à instância padrão, ele pode estar escutando em uma porta diferente da porta 1433 TCP e o cliente não está tentando se conectar ao número da porta correto.
    *   Se você estiver se conectando a uma instância nomeada, o número da porta não está sendo retornado ao cliente.  

Ambos os problemas são relacionados ao serviço de Navegador do SQL Server, que fornece o número da porta para o cliente. As soluções são:

  * Iniciar o serviço de Navegador do SQL Server. Volte para a seção **Coletando informações sobre a instância do SQL Server**, seção 1.d.
  * O serviço de Navegador do SQL Server está sendo bloqueada pelo firewall. Abra a porta UDP 1434 no firewall. Volte para a seção **Abrir uma porta no Firewall**. (Verifique se você está abrindo uma porta UDP, não uma porta TCP. Elas são diferentes.)
  * As informações da porta UDP 1434 estão sendo bloqueadas por um roteador. A comunicação UDP (protocolo UDP) não foi projetada para passar por roteadores. Isso impede que a rede seja preenchida por tráfego de baixa prioridade. É possível configurar o roteador para encaminhar tráfego UDP ou você pode optar por sempre fornecer o número da porta ao conectar.
  * Se o computador cliente estiver usando o Windows 7 ou o Windows Server 2008 (ou um sistema operacional mais recente), o tráfego UDP pode ser descartado pelo sistema operacional do cliente porque a resposta do servidor é retornada de um endereço IP diferente daquele foi consultado. Esse é um bloqueio do recurso de segurança "mapeamento de origem flexível". Para obter mais informações, consulte a seção **Vários endereços IP do servidor** do tópico dos Manuais Online [Solução de problemas: tempo limite excedido](https://msdn.microsoft.com/library/ms190181.aspx). Este é um artigo do SQL Server 2008 R2, mas as entidades ainda se aplicam. É possível configurar o cliente para usar o endereço IP correto ou você pode optar por sempre fornecer o número da porta ao conectar.
     
3. Depois que você se conectar usando o endereço IP (ou o endereço IP e o nome de instância para uma instância nomeada), tente conectar usando o nome do computador (ou o nome do computador e o nome de instância para uma instância nomeada). Coloque `tcp:` na frente do nome do computador para forçar uma conexão TCP/IP. Por exemplo, para a instância padrão em um computador chamada `ACCNT27`, use `tcp:ACCNT27` . Para uma instância nomeada chamada `PAYROLL`no computador em questão, use `tcp:ACCNT27\PAYROLL` . Se você puder se conectar usando o endereço IP, mas não usando o nome do computador, isso significa que ocorreu um problema de resolução de nome. Volte para a seção **Testar conectividade TCP/IP**, a seção 4.

4. Depois que você se conectar usando o nome do computador forçando TCP, tente conectar usando o nome do computador, mas sem forçar TCP. Por exemplo, para uma instância padrão, use apenas o nome de computador, como `CCNT27` . Para uma instância nomeada, use o nome do computador e da instância, como `ACCNT27\PAYROLL` . Se você puder conectar forçando TCP, mas não sem forçar TCP, o cliente provavelmente está usando outro protocolo (como pipes nomeados, por exemplo).

    1. No computador cliente, usando o SQL Server Configuration Manager, no painel esquerdo, expanda **Configuração** *version* **Configuration**, and then select **Client Protocols**.
    2. No painel direito, verifique se TCP/IP está habilitado. Se o TCP/IP estiver desabilitado, clique com o botão direito do mouse em **TCP/IP** e depois clique em **Habilitar**.
    3. Verifique se a ordem de protocolo de TCP/IP é um número menor do que os protocolos de pipes nomeados (ou VIA em versões anteriores). Em geral, você deve deixar a memória compartilhada como a ordem 1 e TCP/IP como a ordem 2. A memória compartilhada só é usada quando o cliente e o SQL Server estão em execução no mesmo computador. Todos os protocolos habilitados são testados em ordem até obter êxito, exceto que a memória compartilhada é ignorada quando a conexão não está no mesmo computador. 

