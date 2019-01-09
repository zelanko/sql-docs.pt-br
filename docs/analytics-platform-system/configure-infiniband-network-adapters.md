---
title: Configurar InfiniBand - Analytics Platform System | Microsoft Docs
description: Descreve como configurar os adaptadores de rede InfiniBand em um servidor não seja de dispositivo cliente para se conectar ao nó de controle no Parallel Data Warehouse (PDW). Use estas instruções para a conectividade básica e de alta disponibilidade, para que o carregamento, backup e outros processos se conectam automaticamente à rede InfiniBand Active Directory.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 0421361cf1718d6ee280269f9da125c148aa3afd
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52518268"
---
# <a name="configure-infiniband-network-adapters-for-analytics-platform-system"></a>Configurar adaptadores de rede InfiniBand para o Analytics Platform System
Descreve como configurar os adaptadores de rede InfiniBand em um servidor não seja de dispositivo cliente para se conectar ao nó de controle no Parallel Data Warehouse (PDW). Use estas instruções para a conectividade básica e de alta disponibilidade, para que o carregamento, backup e outros processos se conectam automaticamente à rede InfiniBand Active Directory.  
  
## <a name="Basics"></a>Descrição  
Estas instruções mostram como localizar e, em seguida, definir os correto InfiniBand IP endereços e máscaras de sub-rede no seu servidor conectada ao InfiniBand. Eles também explicam como configurar seu servidor para usar o dispositivo de APS DNS para que sua conexão é resolvido para a rede InfiniBand Active Directory.  
  
Para alta disponibilidade, APS tem duas redes InfiniBand, um ativo e passivo de um. Cada rede InfiniBand tem um endereço IP diferente para o nó de controle. Se a rede InfiniBand Active Directory ficar inativo, a rede InfiniBand passiva torna-se a rede do Active Directory. Quando isso acontece um script ou processo automaticamente se conecta à rede InfiniBand Active Directory sem alterar os parâmetros do script.  
  
Especificamente, neste artigo você:  
  
1.  Localizar os endereços de IP do InfiniBand do DNS APS servidores (appliance_domain AD01 e appliance_domain *-AD02). Para fazer isso, você faça logon em servidores de AD01 e AD02 e obter os endereços IP para cada rede InfiniBand. Os endereços de IP do InfiniBand no nó do AD são os endereços IP de DNS.  
  
2.  Configure cada adaptador de rede para usar um endereço IP disponível nas redes InfiniBand APS.  
  
    1.  Se você tiver dois adaptadores de rede InfiniBand, você configura um adaptador com um endereço IP disponível na rede InfiniBand primeiro que é chamado TeamIB1 e o outro com um endereço IP disponível na rede InfiniBand segundo que é chamada de TeamIB2. Use o TeamIB1 appliance_domain AD01 o endereço IP como o servidor DNS preferencial e AD02 appliance_domain TeamIB1 endereço IP como o servidor DNS alternativo para o adaptador de rede TeamIB1. Use o TeamIB2 appliance_domain AD01 o endereço IP como o servidor DNS preferencial e AD02 appliance_domain TeamIB2 endereço IP como o servidor DNS alternativo para o adaptador de rede TeamIB2.  
  
    2.  Se você tiver apenas um adaptador de rede InfiniBand, você configura o adaptador com um endereço IP disponível de uma das redes InfiniBand. Configurar a preferência e os servidores DNS alternativos neste adaptador usando TeamIB1 appliance_domain AD01 e AD02 appliance_domain TeamIB1 ou TeamIB2 appliance_domain AD01 e AD02 appliance_domain TeamIB2 o que está no mesmo rede como o adaptador configurado como o preferencial e os servidores DNS alternativos, respectivamente.  
  
3.  Configure o adaptador de rede InfiniBand para usar servidores DNS de APS para resolver sua conexão à rede InfiniBand Active Directory.  
  
    1.  Para configurar isso você pode usar as configurações de TCP/IP avançadas para adicionar o sufixo DNS de domínio do dispositivo para o início da lista de sufixos DNS em seu servidor do cliente. Isso só precisa ser configurado em um dos adaptadores de rede; a configuração se aplica aos dois adaptadores.  
  
Depois de configurar os adaptadores de rede InfiniBand, processos de cliente podem se conectar ao nó de controle na rede InfiniBand usando `PDW_region-SQLCTL01` para o endereço do servidor. Seu servidor acrescenta o sufixo DNS do Analytics Platform System, ou você pode inserir o endereço completo que é `PDW_region-SQLCTL01.appliance_domain.pdw.local`.  
  
Por exemplo, se o nome da região PDW é MyPDW e o nome do dispositivo é MyAPS, a especificação do servidor de dwloader de carregamento de dados é um dos seguintes:  
  
-   `dwloader -S MYPDW-SQLCTL01.MyAPS.pdw.local`  
  
-   `dwloader -S MYPDW-SQLCTL01`  
  
## <a name="BeforeBegin"></a>Antes de começar  
  
### <a name="requirements"></a>Requisitos  
Você precisa de uma conta de domínio de dispositivo de APS para fazer logon no nó AD01. Por exemplo, F12345 * \administrator.  
  
Você precisa de uma conta de Windows no servidor de cliente que tenha permissão para configurar os adaptadores de rede.  
  
### <a name="prerequisites"></a>Prerequisites  
Essas instruções pressupõem que o servidor de cliente já está em rack e cabeado para a rede InfiniBand de solução de virtualização. Para o acompanhamento de cabeamento e instruções, consulte [adquirir e configurar um servidor carregando](acquire-and-configure-loading-server.md).  
  
### <a name="general-remarks"></a>Comentários gerais  
Usando SQLCTL01, o sistema de plataforma de análise de DNS se conecta seu servidor de cliente para o nó de controle usando a rede InfiniBand Active Directory. Isso se aplica apenas a conexão; Se a rede InfiniBand fica inativo durante o carregamento ou backup, você precisa reiniciar o processo.  
  
Para atender aos seus requisitos de negócios, você também pode ingressar o servidor de cliente para seu próprio grupo de trabalho não seja de dispositivo ou um domínio do Windows.  
  
## <a name="Sec1"></a>Etapa 1: Obter o dispositivo de configurações de rede InfiniBand  
*Para obter as configurações de rede InfiniBand de dispositivo*  
  
1.  Faça logon no dispositivo de nó AD01 usando a conta appliance_domain\Administrator.  
  
2.  No nó de AD01 do dispositivo, abra o painel de controle, selecione a rede e Internet, selecione rede e compartilhamento Center * e, em seguida, selecione Alterar configurações do adaptador.  
  
3.  Na janela Conexões de rede, clique duas vezes em IB1 de equipe e selecione Propriedades.  
  
    ![Conexões do InfiniBand no nó de gerenciamento](media/network-teamib.png "conexões do InfiniBand no nó de gerenciamento")  
  
4.  Na janela Propriedades do protocolo de Internet versão 4 (TCP/IPv4), anote os valores para o **endereço IP** e **máscara de sub-rede**.  O endereço IP do  **_appliance\_domínio_-AD01** nó é o endereço IP do servidor DNS de sistema de plataforma de análise.  
  
5.  Repita as etapas 1 a 5 acima para o adaptador TeamIB1 na  **_appliance\_domínio_-AD02** server.  
  
    ![Propriedades do InfiniBand 1 do nó de gerenciamento do PDW](media/network-ip1-properties.png "propriedades do InfiniBand 1 do nó de gerenciamento do PDW")  
  
6.  Clique em Cancelar para fechar a janela.  
  
7.  Localizar um endereço IP não usado na rede TeamIB1 e anotá-lo.  
  
    Para localizar um endereço IP não usado, abra uma janela de comando e tente executar o ping de endereços IP dentro do intervalo de endereços para o seu dispositivo. Neste exemplo, o endereço IP da rede TeamIB1 é 172.16.14.30. Localize um endereço IP que começa com 172.16.14 que não seja usado. Por exemplo, na linha de comando digite "ping 172.16.14.254". Se a solicitação de ping falhar, o endereço IP está disponível.  
  
8.  Fazer a mesma coisa de TeamIB2. No * janela Conexões de rede, clique duas vezes em IB2 de equipe e selecione Propriedades.  
  
9. Na janela Propriedades do protocolo de Internet versão 4 (TCP/IPv4), anote os valores para o endereço IP e máscara de sub-rede de TeamIB2.  
  
10. Repita as etapas 8 e 9 acima para o adaptador de TeamIB2 no servidor appliance_domain AD02.  
  
    ![Propriedades de TeamIB2](media/network-ip2-properties.png "propriedades de TeamIB2")  
  
11. Localizar um endereço IP não usado na **TeamIB2** de rede e anotá-lo.  
  
    Para localizar um endereço IP não usado, abra uma janela de comando e tente executar o ping de endereços IP dentro do intervalo de endereços para o seu dispositivo. Neste exemplo, o endereço IP da rede TeamIB2 é 172.16.18.30. Localize um endereço IP que começa com 172.16.18 que não seja usado. Por exemplo, na linha de comando digite "ping 172.16.18.254". Se a solicitação de ping falhar, o endereço IP está disponível.  
  
## <a name="Sec2"></a>Etapa 2: Configurar as configurações do adaptador de rede InfiniBand no seu servidor de cliente  

### <a name="notes"></a>Observações  
  
-   Estas etapas mostram como registrar seu servidor com os servidores DNS de APS.  
  
-   Para atender às suas necessidades de rede, você também pode ingressar o servidor de cliente para seu próprio grupo de trabalho não seja de dispositivo ou um domínio do Windows.  
  
-   A etapa de instruções por meio de configuração de dois adaptadores de rede em cada servidor.  Se você tiver apenas um adaptador de rede, escolha uma das redes configurar no adaptador de rede e, em seguida, adicione o segundo endereço IP de DNS como um servidor DNS alternativo.  
  
### <a name="to-configure-the-infiniband-network-adapter-settings-on-your-client-server"></a>Para configurar as configurações do adaptador de rede InfiniBand no seu servidor de cliente  
  
1.  Fazer logon como um administrador do Windows para o carregamento, backup ou outro servidor de cliente no dispositivo de rede InfiniBand.  
  
2.  Abra o painel de controle *, selecione Central de rede e compartilhamento e, em seguida, selecione Alterar configurações do adaptador.  
  
### <a name="to-configure-the-first-network-adapter"></a>Para configurar o primeiro adaptador de rede  
  
1.  Na janela Conexões de rede, clique duas vezes em um dos slots de rede não identificada para o adaptador Mellanox e selecione Propriedades.  
  
    ![Selecione as redes InfiniBand](media/network-connections.png "selecionar as redes InfiniBand")  
  
2.  Na janela Propriedades  
  
    1.  Na guia geral, defina o endereço IP para o endereço IP que você verificado como livre no teste de ping para TeamIB1. Para os valores de exemplo usados neste artigo, você digitaria 172.16.14.254.  
  
    2.  Defina a máscara de sub-rede para a máscara de sub-rede que você anotou para TeamIB1.  
  
    3.  Defina o servidor DNS preferencial para o endereço IP do TeamIB1 que você anotou anteriormente do appliance_domain *-AD01 nó.  
  
    4.  Configurar o servidor DNS alternativo para o endereço IP do TeamIB1 que você anotou anteriormente do appliance_domain *-AD02 nó.  
  
        ![Propriedades do adaptador de rede 1 InfiniBand](media/network-ib1-properties.png "SQL_Server_PDW_Network_IB1_properties")  
  
    5.  Clique em Okey para aplicar as alterações.  
  
### <a name="to-configure-the-second-network-adapter"></a>Para configurar o segundo adaptador de rede  
  
1.  Ignore esta seção se você tiver apenas um adaptador de rede.  
  
2.  Na janela Conexões de rede, clique com botão direito no slot de rede não identificada segundo para o adaptador Mellanox e selecione Propriedades.  
  
    ![Selecione as redes InfiniBand](media/network-connections.png "selecionar as redes InfiniBand")  
  
3.  Na janela Propriedades  
  
    1.  Na guia geral, defina o endereço IP para o endereço IP que você verificou como livre no teste de ping de TeamIB2. Para os valores de exemplo usados neste artigo, você digitaria 172.16.18.254.  
  
    2.  Defina a máscara de sub-rede para a máscara de sub-rede que você anotou de TeamIB2.  
  
    3.  Defina o servidor DNS preferencial para o endereço IP de TeamIB2 que você anotou anteriormente do appliance_domain *-AD01 nó.  
  
    4.  Configurar o servidor DNS alternativo para o endereço IP de TeamIB2 que você anotou anteriormente do appliance_domain *-AD02 nó.  
  
        > [!NOTE]  
        > Se você tiver apenas um adaptador de rede, configurar a preferência e os servidores DNS alternativos usando o dispositivo TeamIB1 AD01 e appliance AD02 TeamIB1 como o preferencial e os servidores DNS alternativos respectivamente ou usar o dispositivo TeamIB2 AD01 e dispositivo AD02 TeamIB2 como o preferencial e os servidores DNS alternativos, dependendo se a máquina virtual AD realizou o failover.  
  
        ![Propriedades do adaptador de rede 1 InfiniBand](media/network-ib1-properties.png "propriedades do adaptador de rede de 1 de InfiniBand")  
  
    5.  Clique em Okey para aplicar as alterações.  
  
### <a name="to-configure-the-dns-suffix"></a>Para configurar o sufixo DNS  
  
1.  Na janela Conexões de rede, clique duas vezes em um dos slots de rede para o adaptador Mellanox e selecione Propriedades.  
  
2.  Clique em Advanced botão.  
  
3.  Na janela Configurações avançadas de TCP/IP, se o acréscimo opção esses sufixos DNS (em ordem) não está desativada, o chamado da caixa de seleção Acrescentar estes sufixos DNS (em ordem):, selecione o sufixo de domínio do dispositivo e clique em Adicionar... É o sufixo de domínio do dispositivo `appliance_domain.local`  
  
4.  Se a Acrescentar estes sufixos DNS (em ordem): opção está desativada, você pode adicionar o domínio de pontos de acesso a este servidor modificando a chave do registro HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\DNSClient.  
  
    ![Configurações de TCP/IP](media/network-tcpip.png "configurações TCP/IP")  
  
5.  Para acelerar a resolução de endereço, é recomendável mover o sufixo do dispositivo para o topo da lista.  
  
6.  Clique em OK.  
  
7.  Agora, você pode se conectar à rede Infiniband appliance usando `PDW_region-SQLCTL01.appliance_domain.local`, ou simplesmente `appliance_domain-SQLCTL01`. A conexão poderá ser estabelecida com mais rapidez se você se conectar com o nome completo e o sufixo DNS.  
  
    Exemplos para um dispositivo denominado MyAPS com uma região PDW MyPDW:  
  
    -   MyPDW-SQLCTL01.MyAPS.local  
  
    -   MyPDW-SQLCTL01  
  
## <a name="see-also"></a>Consulte também  
[Adquirir e configurar um servidor de carregamento ](acquire-and-configure-loading-server.md)  
  
