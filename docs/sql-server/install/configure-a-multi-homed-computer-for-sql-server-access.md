---
title: Configurar um computador multihomed para acesso
description: Saiba como configurar o SQL Server e o Firewall do Windows para fornecer conexões de rede a uma instância do SQL Server em um ambiente multihomed.
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- ports [SQL Server], multi-homed computer
- multi-homed computer [SQL Server] configuring ports
- firewall systems [Database Engine], multi-homed computer
ms.assetid: ba369e5b-7d1f-4544-b7f1-9b098a1e75bc
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 74f365ec21285609055d8ecc04690787f5870802
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85894902"
---
# <a name="configure-a-multi-homed-computer-for-sql-server-access"></a>Configurar um computador multihomed para acesso ao SQL Server
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  Quando um servidor deve fornecer uma conexão a duas ou mais redes ou sub-redes de rede, um cenário típico usa um computador multihomed. Frequentemente este computador está localizado em uma rede de perímetro (também conhecida como DMZ, zona desmilitarizada ou sub-rede filtrada). Este artigo descreve como configurar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o Firewall do Windows com Segurança Avançada para fornecer conexões de rede a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um ambiente multihomed.  
  
> [!NOTE]  
>  Um computador multihomed tem vários adaptadores de rede ou foi configurado para usar vários endereços IP para um único adaptador de rede. Um computador dualhomed tem dois adaptadores de rede ou foi configurado para usar dois endereços IP para um único adaptador de rede.  
  
 Antes de continuar com este artigo, você deve se familiarizar com as informações fornecidas no artigo [Configurar o Firewall do Windows para permitir acesso ao SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md). Esse artigo contém informações básicas sobre como os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funcionam com o firewall.  
  
 **Suposições deste exemplo:**  
  
-   Há dois adaptadores de rede instalados no computador. Um ou mais dos adaptadores de rede podem ser sem-fio. Você pode simular ter dois adaptadores de rede usando o endereço IP de um adaptador de rede e usando o endereço IP de loopback (127.0.0.1) como o segundo adaptador de rede.  
  
-   Para simplificar, este exemplo usa endereços IPv4. Os mesmos procedimentos podem ser executados usando endereços IPv6.  
  
    > [!NOTE]  
    >  Endereços IPv4 são uma série de quatro números conhecida como octetos. Cada número é menor que 255 e os números são separados por pontos, como 127.0.0.1. Endereços IPv6 são uma série de oito números hexadecimais separados por dois-pontos, como fe80:4898:23:3:49a6:f5c1:2452:b994.  
  
-   As regras de firewall podem permitir acesso por meio de uma porta específica, como a porta 1433. Ou as regras de firewall podem permitir acesso ao programa [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] (sqlservr.exe). Nenhum método é melhor que o outro. Como um servidor em uma rede de perímetro é mais vulnerável a ataques do que servidores em uma intranet, este artigo assume que você deseja ter um controle mais preciso e selecionar individualmente as portas que você abre. Por esse motivo, este artigo assume que você configurará o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para escutar em uma porta fixa. Para obter mais informações sobre as portas usadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , veja [Configurar o Firewall do Windows para permitir acesso ao SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
-   Este exemplo configura o acesso ao [!INCLUDE[ssDE](../../includes/ssde-md.md)] usando a porta TCP 1433. As outras portas que são os diferentes usos dos componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ser configuradas usando as mesmas etapas gerais.  
  
 **As seguintes são as etapas gerais deste exemplo:**  
  
-   Determinar os endereços IP no computador.  
  
-   Configurar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para escutar em uma porta TCP específica.  
  
-   Configurar o Firewall do Windows com Advanced Security.  
  
## <a name="optional-procedures"></a>Procedimentos opcionais  
 Se você já conhecer os endereços IP disponíveis para seu computador e que são usados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], poderá saltar esses procedimentos.  
  
#### <a name="to-determine-the-ip-addresses-available-on-the-computer"></a>Para determinar os endereços IP no computador.  
  
1.  No computador no qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado, clique em **Iniciar**, em **Executar**, digite **cmd** e [!INCLUDE[clickOK](../../includes/clickok-md.md)].  
  
2.  Na janela do prompt de comando, digite **ipconfig** e pressione ENTER para listar os endereços IP disponíveis neste computador.  
  
    > [!NOTE]  
    >  O comando **ipconfig** , às vezes, lista diversas conexões possíveis, incluindo conexões que são desconectadas. O comando **ipconfig** pode listar endereços IPv4 e IPv6.  
  
3.  Observe os endereços IPv4 e IPv6 que estão sendo usados. As outras informações na lista, como endereços temporários, máscaras de sub-rede e gateways padrão são informações importantes para configurar uma rede TCP/IP. Mas estas informações não são usadas neste exemplo.  
  
#### <a name="to-determine-the-ip-addresses-and-ports-used-by-ssnoversion"></a>Para determinar os endereços IP e as portas usadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1.  Clique em **Iniciar**, escolha **Todos os Programas**, aponte para [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], para **Ferramentas de Configuração**e clique em **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager**.  
  
2.  No **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager**, no painel do console, expanda **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuração de Rede**, expanda **Protocolos para \<instance name>** e clique duas vezes em **TCP/IP**.  
  
3.  Na caixa de diálogo **Propriedades de TCP/IP** , na guia **Endereços IP** , vários endereços IP aparecem no formato **IP1**, **IP2**, até **IPAll**. Um desses é para o endereço IP do adaptador de loopback, 127.0.0.1. Endereços IP adicionais aparecem para cada Endereço IP configurado no computador.  
  
4.  Para qualquer endereço IP, se a caixa de diálogo **Portas TCP Dinâmicas** contiver **0**, isso indicará que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] está ouvindo em portas dinâmicas. Este exemplo usa portas fixas em vez de portas dinâmicas que podem ser alteradas na reinicialização. Portanto, se a caixa de diálogo **Portas TCP Dinâmicas** contiver **0**, exclua o 0.  
  
5.  Observe a porta TCP que listada para cada endereço IP que você deseja configurar. Para este exemplo, assuma que os dois endereços IP estão escutando na porta padrão, 1433.  
  
6.  Se você não desejar que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] use algumas das portas disponíveis, na guia **Protocolo** , altere o valor **Escutar Tudo** para **Não**; e na guia **Endereços IP** , altere o valor **Ativo** para **Não** para os endereços IP que você não deseja usar.  
  
## <a name="configuring-windows-firewall-with-advanced-security"></a>Configurando o Firewall do Windows com Segurança Avançada  
 Depois que você conhece os endereços IP que o computador usa e as portas que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa, você pode criar regras de firewall e configurar essas regras para endereços IP específicos.  
  
#### <a name="to-create-a-firewall-rule"></a>Para criar uma regra de firewall  
  
1.  No computador no qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado, faça logon como um administrador.  
  
2.  Clique em **Iniciar**, em **Executar**, digite **wf.msc**e clique em **OK**.  
  
3.  Na caixa de diálogo **Controle de Conta de Usuário** , clique em **Continuar** para usar as credenciais de Administrador para abrir o snap-in Firewall do Windows com Segurança Avançada.  
  
4.  Na página **Visão geral** , confirme se o Firewall do Windows está habilitado.  
  
5.  No painel esquerdo, clique em **Regras de Entrada**.  
  
6.  Clique com o botão direito do mouse em **Regras de Entrada**e clique em **Nova Regra** para abrir o **Assistente para Nova Regra de Entrada**.  
  
7.  Você pode criar uma regra para o programa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . No entanto, como este exemplo usa uma porta fixa, selecione **Porta**e clique em **Avançar**.  
  
8.  Na página **Protocolos e Portas** , selecione **TCP**.  
  
9. Selecione **Portas locais especificadas**. Digite os números das portas separados por vírgulas e clique em **Avançar**. Neste exemplo, você configurará a porta padrão; portanto, digite **1433**.  
  
10. Na página **Ação** , examine as opções. Neste exemplo, você não está usando o firewall para forçar conexões seguras. Portanto, clique em **Permitir a conexão**e clique em **Avançar**.  
  
    > [!NOTE]  
    >  Seu ambiente pode exigir conexões seguras. Se você selecionar uma das opções de conexões seguras, poderá ser necessário configurar um certificado e a opção **Forçar Criptografia** . Para obter mais informações sobre conexões seguras, veja [Habilitar conexões criptografadas com o Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md) e [Habilitar conexões criptografadas com o Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
11. Na página **Perfil** , selecione um ou mais perfis para a regra. Se você não estiver familiarizado com os perfis de firewall, clique no link **Saber mais sobre perfis** no programa de firewall.  
  
    -   Se o computador for um servidor e estiver disponível apenas quando está conectado a um domínio, seleciona **Domínio**e clique em **Avançar**.  
  
    -   Se o computador for um computador móvel (por exemplo um laptop), ele provavelmente usará vários perfis ao conectar-se a diferentes redes. Em um computador móvel, você pode configurar recursos de acesso diferentes para perfis diferentes. Por exemplo, você pode permitir acesso quando o computador usa o perfil Domínio mas não permitir acesso quando ele usa o perfil Público.  
  
12. Na página **Nome** , forneça um nome e descrição para a regra e clique em **Concluir**.  
  
13. Repita esse procedimento para criar outra regra para cada endereço IP que será usado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Depois de criar uma ou mais regras, execute as etapas a seguir para configurar cada endereço IP no computador para usar uma regra.  
  
#### <a name="to-configure-the-firewall-rule-for-a-specific-ip-addresses"></a>Para configurar a regra de firewall para um endereço IP específico  
  
1.  Na página **Regras de Entrada** do **Firewall do Windows com Segurança Avançada**, clique com o botão direito do mouse na regra que você acabou de criar e clique em **Propriedades**.  
  
2.  Na caixa de diálogo **Propriedades da Regra** , selecione a guia **Escopo** .  
  
3.  Na área **Endereço IP Local** , selecione **Estes endereços IP**e clique em **Adicionar**.  
  
4.  Na caixa de diálogo **Endereço IP** , selecione **Este endereço IP ou sub-rede**e digite um dos endereços IP a ser configurado.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  Na área **Endereço IP Remoto** , selecione **Estes endereços IP**e clique em **Adicionar**.  
  
7.  Use a caixa de diálogo **Endereço IP** para configurar a conectividade para o endereço IP selecionado no computador. É possível habilitar conexões de endereços IP especificados, intervalos de endereços IP, sub-redes inteiras ou de certos computadores. Para configurar essa opção corretamente, você deve ter um bom entendimento da rede. Para obter informações sobre a rede, consulte o administrador da rede.  
  
8.  Para fechar a caixa de diálogo **Endereço IP** , clique em **OK**e em **OK** novamente para fechar a caixa de diálogo **Propriedades da Regra** .  
  
9. Para configurar os outros endereços IP em um computador multihomed, repita esse procedimento usando outro endereço IP e outra regra.  
  
## <a name="see-also"></a>Consulte Também  
 [Serviço SQL Server Browser &#40;Mecanismo de Banco de Dados e SSAS&#41;](../../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md)   
 [Conectar-se ao SQL Server com um servidor proxy &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/connect-to-sql-server-through-a-proxy-server-sql-server-configuration-manager.md)  
  
  
