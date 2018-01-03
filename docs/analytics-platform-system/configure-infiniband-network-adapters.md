---
title: Configurar adaptadores de rede InfiniBand Analytics Platform System (APS)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "Descreve como configurar os adaptadores de rede InfiniBand em um servidor não seja de aplicação de cliente para conectar-se ao nó de controle no SQL Server Parallel Data Warehouse (PDW)."
ms.date: 01/05/2017
ms.topic: article
ms.assetid: 61f3c51a-4411-4fe8-8b03-c8e1ba279646
caps.latest.revision: "15"
ms.openlocfilehash: 052dfcb32de7fb84acc0ce97c55775944a1d0dc1
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="configure-infiniband-network-adapters-for-analytics-platform-system"></a>Configurar adaptadores de rede InfiniBand para Analytics Platform System
Descreve como configurar os adaptadores de rede InfiniBand em um servidor não seja de aplicação de cliente para conectar-se ao nó de controle no SQL Server Parallel Data Warehouse (PDW). Use estas instruções para a conectividade básica e de alta disponibilidade, para que o carregamento, backup e outros processos vai se conectar automaticamente à rede InfiniBand ativa.  
  
## <a name="Basics"></a>Descrição  
Estas instruções mostram como localizar e, em seguida, definir o IP correto do InfiniBand endereços e máscaras de sub-rede no servidor conectado InfiniBand. Eles também explicam como configurar seu servidor para usar o utilitário de APS DNS para que a conexão será resolvido para a rede InfiniBand ativa.  
  
Para alta disponibilidade, APS tem duas redes InfiniBand, um ativo e passivo de uma. Cada rede InfiniBand tem um endereço IP diferente para o nó de controle. Se a rede InfiniBand ativa falhar, a rede InfiniBand passiva torna-se a rede ativa. Quando isso acontece um script ou processo conecta-se automaticamente à rede InfiniBand active sem alterar parâmetros do script.  
  
Especificamente, este tópico você irá:  
  
1.  Localizar os endereços IP InfiniBand do DNS APS servidores (appliance_domain AD01 e appliance_domain *-AD02). Para fazer isso, você faça logon em servidores AD01 e AD02 e obter os endereços IP para cada rede InfiniBand. Os endereços IP InfiniBand no nó AD são os endereços IP do DNS.  
  
2.  Configure cada adaptador de rede para usar um endereço IP disponível nas redes InfiniBand APS.  
  
    1.  Se você tiver dois adaptadores de rede InfiniBand, você configurará um adaptador com um endereço IP disponível na rede InfiniBand primeiro que é chamado de TeamIB1 e outro com um endereço IP disponível na rede InfiniBand segunda chamada TeamIB2. Usar o TeamIB1 appliance_domain AD01 endereço IP como o servidor DNS preferencial e AD02 appliance_domain TeamIB1 endereço IP como o servidor DNS alternativo para o adaptador de rede TeamIB1. Usar o TeamIB2 appliance_domain AD01 endereço IP como o servidor DNS preferencial e AD02 appliance_domain TeamIB2 endereço IP como o servidor DNS alternativo para o adaptador de rede TeamIB2.  
  
    2.  Se você tiver apenas um adaptador de rede InfiniBand, você irá configurar o adaptador com um endereço IP disponível de uma das redes InfiniBand. Em seguida, você configurará o preferencial e alternativos servidores DNS neste adaptador usando TeamIB1 appliance_domain AD01 e AD02 appliance_domain TeamIB1 ou TeamIB2 appliance_domain AD01 e AD02 appliance_domain TeamIB2 o que for do mesma rede como adaptador configurado como o preferenciais e os servidores DNS alternativos respectivamente.  
  
3.  Configure o adaptador de rede InfiniBand para usar servidores DNS de APS para resolver sua conexão à rede InfiniBand ativa.  
  
    1.  Para configurar isso, você usará as configurações de TCP/IP avançadas para adicionar o sufixo DNS do domínio de aplicativo para o início da lista de sufixos DNS no seu servidor do cliente. Isso só precisa ser configurado em um dos adaptadores de rede; a configuração será aplicada aos dois adaptadores.  
  
Depois de configurar os adaptadores de rede InfiniBand, processos de cliente podem se conectar ao nó de controle na rede InfiniBand usando `PDW_region-SQLCTL01` para o endereço do servidor. O servidor acrescentará o sufixo DNS de sistema de plataforma de análise, ou você pode inserir o endereço completo que é `PDW_region-SQLCTL01.appliance_domain.pdw.local`.  
  
Por exemplo, se o nome da região PDW é MyPDW e o nome do dispositivo é MyAPS, a especificação de dwloader de carregamento de dados será um dos seguintes:  
  
-   `dwloader –S MYPDW-SQLCTL01.MyAPS.pdw.local`  
  
-   `dwloader –S MYPDW-SQLCTL01`  
  
## <a name="BeforeBegin"></a>Antes de começar  
  
### <a name="requirements"></a>Requisitos  
Você precisa de uma conta de domínio do dispositivo de APS para fazer logon no nó AD01. Por exemplo, F12345 * \administrator.  
  
Você precisa ter uma conta do Windows no servidor de cliente que tenha permissão para configurar os adaptadores de rede.  
  
### <a name="prerequisites"></a>Prerequisites  
Essas instruções presumem que o servidor de cliente já está em rack e conectado à rede InfiniBand appliance. Para montagem em rack e cabeamento instruções, consulte [adquirir e configurar um servidor ao carregar](acquire-and-configure-loading-server.md).  
  
### <a name="general-remarks"></a>Comentários gerais  
Usando SQLCTL01, o sistema de plataforma de análise de DNS se conectará seu servidor de cliente para o nó de controle usando a rede InfiniBand active. Isso se aplica apenas a conexão; Se a rede InfiniBand falhar durante o carregamento ou backup, você precisará reiniciar o processo.  
  
Para atender a seus requisitos de negócios, você também pode ingressar o servidor do cliente para seu próprio dispositivo sem grupo de trabalho ou domínio do Windows.  
  
## <a name="Sec1"></a>Etapa 1: Obter o dispositivo de configurações de rede InfiniBand  
*Para obter o dispositivo de configurações de rede InfiniBand*  
  
1.  Logon para o nó de dispositivo AD01 usando a conta appliance_domain\Administrator.  
  
2.  No nó AD01 dispositivo, abra o painel de controle, selecione a rede e Internet, selecione rede e compartilhamento Center * e, em seguida, selecione Alterar configurações do adaptador.  
  
3.  Na janela Conexões de rede, clique duas vezes em equipe IB1 e selecione Propriedades.  
  
    ![Conexões do InfiniBand no nó de gerenciamento](media/network-teamib.png "conexões do InfiniBand no nó de gerenciamento")  
  
4.  Na janela de propriedades de protocolo de Internet versão 4 (TCP/IPv4), anote os valores para o **endereço IP** e **máscara de sub-rede**.  O endereço IP do  ***appliance_domain*-AD01** nó é o endereço IP do servidor DNS de sistema de plataforma de análise.  
  
5.  Repita as etapas 1 a 5 acima para o adaptador TeamIB1 em  ***appliance_domain*-AD02** server.  
  
    ![Propriedades de nó InfiniBand 1 do gerenciamento de PDW](media/network-ip1-properties.png "propriedades de nó InfiniBand 1 do gerenciamento do PDW")  
  
6.  Clique em Cancelar para fechar a janela.  
  
7.  Localizar um endereço IP não usado na rede TeamIB1 e anotá-lo.  
  
    Para localizar um endereço IP não usado, abra uma janela de comando e tente executar o ping de endereços IP dentro do intervalo de endereços para o seu dispositivo. Neste exemplo, o endereço IP da rede TeamIB1 é 172.16.14.30. Localize um endereço IP que começa com 172.16.14 que não é usado. Por exemplo, na linha de comando Inserir "ping 172.16.14.254". Se a solicitação de ping tiver êxito, o endereço IP está disponível.  
  
8.  Fazer a mesma coisa de TeamIB2. No * janela Conexões de rede, clique duas vezes em equipe IB2 e selecione Propriedades.  
  
9. Na janela de propriedades de protocolo de Internet versão 4 (TCP/IPv4), anote os valores para o endereço IP e máscara de sub-rede de TeamIB2.  
  
10. Repita as etapas 8 e 9 acima para o adaptador de TeamIB2 no servidor appliance_domain AD02.  
  
    ![Propriedades de TeamIB2](media/network-ip2-properties.png "propriedades de TeamIB2")  
  
11. Localizar um endereço IP não usado no **TeamIB2** de rede e anotá-lo.  
  
    Para localizar um endereço IP não usado, abra uma janela de comando e tente executar o ping de endereços IP dentro do intervalo de endereços para o seu dispositivo. Neste exemplo, o endereço IP da rede TeamIB2 é 172.16.18.30. Localize um endereço IP que começa com 172.16.18 que não é usado. Por exemplo, na linha de comando Inserir "ping 172.16.18.254". Se a solicitação de ping tiver êxito, o endereço IP está disponível.  
  
## <a name="Sec2"></a>Etapa 2: Configurar as configurações do adaptador de rede InfiniBand no servidor de cliente  

### <a name="notes"></a>Observações  
  
-   Estas etapas mostram como registrar o servidor com os servidores DNS de APS.  
  
-   Para atender às suas necessidades de rede, você também pode ingressar o servidor do cliente para seu próprio dispositivo sem grupo de trabalho ou domínio do Windows.  
  
-   A etapa de instruções por meio de configuração de dois adaptadores de rede em cada servidor.  Se você tiver apenas um adaptador de rede, selecione uma das redes para configurar o adaptador de rede e, em seguida, adicione o segundo endereço IP do DNS como um servidor DNS alternativo.  
  
### <a name="to-configure-the-infiniband-network-adapter-settings-on-your-client-server"></a>Para configurar as configurações do adaptador de rede InfiniBand no servidor de cliente  
  
1.  Faça logon como um administrador do Windows para o carregamento, backup ou outro servidor de cliente na rede InfiniBand appliance.  
  
2.  Abra o painel de controle *, selecione Central de rede e compartilhamento e clique em Alterar configurações do adaptador.  
  
### <a name="to-configure-the-first-network-adapter"></a>Para configurar o primeiro adaptador de rede  
  
1.  Na janela Conexões de rede, clique duas vezes em um dos slots de rede não identificado para o adaptador Mellanox e selecione Propriedades.  
  
    ![Selecione as redes InfiniBand](media/network-connections.png "selecionar as redes InfiniBand")  
  
2.  Na janela Propriedades  
  
    1.  Na guia geral, defina o endereço IP para o endereço IP que você verificou como livre no teste de ping para TeamIB1. Para os valores de exemplo usados neste tópico, você digitaria 172.16.14.254.  
  
    2.  Defina a máscara de sub-rede para a máscara de sub-rede que você anotou para TeamIB1.  
  
    3.  Configure o servidor DNS preferencial para o endereço IP do TeamIB1 que você anotou anteriormente do appliance_domain *-AD01 nó.  
  
    4.  Configure o servidor DNS alternativo para o endereço IP do TeamIB1 que você anotou anteriormente do appliance_domain *-AD02 nó.  
  
        ![Propriedades do adaptador de rede 1 InfiniBand](media/network-ib1-properties.png "SQL_Server_PDW_Network_IB1_properties")  
  
    5.  Clique em Okey para aplicar as alterações.  
  
### <a name="to-configure-the-second-network-adapter"></a>Para configurar o segundo adaptador de rede  
  
1.  Ignore esta seção se você tiver apenas um adaptador de rede.  
  
2.  Na janela Conexões de rede, clique no segundo slot de rede não identificado para o adaptador Mellanox e selecione Propriedades.  
  
    ![Selecione as redes InfiniBand](media/network-connections.png "selecionar as redes InfiniBand")  
  
3.  Na janela Propriedades  
  
    1.  Na guia geral, defina o endereço IP para o endereço IP que você verificou como livre no teste de ping de TeamIB2. Para os valores de exemplo usados neste tópico, você digitaria 172.16.18.254.  
  
    2.  Defina a máscara de sub-rede para a máscara de sub-rede que você anotou de TeamIB2.  
  
    3.  Configure o servidor DNS preferencial para o endereço IP de TeamIB2 que você anotou anteriormente do appliance_domain *-AD01 nó.  
  
    4.  Configure o servidor DNS alternativo para o endereço IP de TeamIB2 que você anotou anteriormente do appliance_domain *-AD02 nó.  
  
        > [!NOTE]  
        > Se você tiver apenas um adaptador de rede, configurar o preferenciais e os servidores DNS alternativos usando o dispositivo TeamIB1 AD01 e o dispositivo AD02 TeamIB1 respectivamente como o preferencial e alternativos servidores DNS ou usar o dispositivo TeamIB2 AD01 e dispositivo TeamIB2 AD02 conforme o desejado e os servidores DNS alternativos dependendo se a máquina virtual do AD falhou em.  
  
        ![Propriedades do adaptador de rede 1 InfiniBand](media/network-ib1-properties.png "InfiniBand propriedades do adaptador de rede 1")  
  
    5.  Clique em Okey para aplicar as alterações.  
  
### <a name="to-configure-the-dns-suffix"></a>Para configurar o sufixo DNS  
  
1.  Na janela Conexões de rede, clique duas vezes em um dos slots de rede para o adaptador Mellanox e selecione Propriedades.  
  
2.  Clique em avançadas... .  
  
3.  Na janela de configurações avançadas de TCP/IP, se a acrescentar essas opções de sufixos DNS (em ordem) não está desativada, o chamado da caixa de seleção Acrescentar estes sufixos DNS (em ordem):, selecione o sufixo de domínio do dispositivo e clique em Adicionar... O sufixo de domínio do dispositivo será`appliance_domain.local`  
  
4.  Se a Acrescentar estes sufixos DNS (em ordem): opção está desativada, você pode adicionar o domínio de pontos de acesso a este servidor, modificando a chave do registro HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\DNSClient.  
  
    ![Configurações TCP/IP](media/network-tcpip.png "configurações TCP/IP")  
  
5.  Para acelerar a resolução de endereço, é recomendável mover o sufixo do dispositivo para a parte superior da lista.  
  
6.  Clique em OK.  
  
7.  Agora, você pode se conectar à rede Infiniband appliance usando `PDW_region-SQLCTL01.appliance_domain.local`, ou simplesmente `appliance_domain-SQLCTL01`. A conexão poderá ser estabelecida com mais rapidez se você se conectar com o nome completo e o sufixo DNS.  
  
    Exemplos de um dispositivo denominado chamados MyAPS com uma região PDW MyPDW:  
  
    -   MyPDW SQLCTL01.MyAPS.local  
  
    -   MyPDW SQLCTL01  
  
## <a name="see-also"></a>Consulte Também  
[Adquirir e configurar um servidor de carregamento](acquire-and-configure-loading-server.md)  
  
