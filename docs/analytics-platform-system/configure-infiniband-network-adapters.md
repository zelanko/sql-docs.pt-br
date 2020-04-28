---
title: Configurar InfiniBand
description: Descreve como configurar os adaptadores de rede InfiniBand em um servidor cliente que não seja de dispositivo para se conectar ao nó de controle em Parallel data warehouse (PDW). Use estas instruções para conectividade básica e alta disponibilidade, para que o carregamento, o backup e outros processos se conectem automaticamente à rede InfiniBand ativa.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 583d7617c0620d5d1ec24d60fbf10435a547616d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401289"
---
# <a name="configure-infiniband-network-adapters-for-analytics-platform-system"></a>Configurar adaptadores de rede InfiniBand para o sistema de plataforma de análise
Descreve como configurar os adaptadores de rede InfiniBand em um servidor cliente que não seja de dispositivo para se conectar ao nó de controle em Parallel data warehouse (PDW). Use estas instruções para conectividade básica e alta disponibilidade, para que o carregamento, o backup e outros processos se conectem automaticamente à rede InfiniBand ativa.  
  
## <a name="description"></a><a name="Basics"></a>Descrição  
Estas instruções mostram como localizar e definir os endereços IP e as máscaras de sub-rede corretos do InfiniBand em seu servidor conectado a InfiniBand. Eles também explicam como definir seu servidor para usar o DNS do dispositivo APS para que sua conexão seja resolvida para a rede InfiniBand ativa.  
  
Para alta disponibilidade, o APS tem duas redes InfiniBand, uma ativa e uma passiva. Cada rede InfiniBand tem um endereço IP diferente para o nó de controle. Se a rede InfiniBand ativa falhar, a rede InfiniBand passiva se tornará a rede ativa. Quando isso acontece, um script ou um processo se conecta automaticamente à rede InfiniBand ativa sem alterar os parâmetros do script.  
  
Especificamente, neste artigo, você:  
  
1.  Localize os endereços IP de InfiniBand dos servidores DNS do APS (appliance_domain-AD01 e appliance_domain *-AD02). Para fazer isso, faça logon nos servidores AD01 e AD02 e obtenha os endereços IP para cada rede InfiniBand. Os endereços IP de InfiniBand no nó do AD são os endereços IP do DNS.  
  
2.  Configure cada adaptador de rede para usar um endereço IP disponível nas redes APS InfiniBand.  
  
    1.  Se você tiver dois adaptadores de rede InfiniBand, configure um adaptador com um endereço IP disponível na primeira rede InfiniBand que é chamada de TeamIB1 e o outro adaptador com um endereço IP disponível na segunda rede InfiniBand que é chamada TeamIB2. Use o endereço IP appliance_domain-AD01 TeamIB1 como o servidor DNS preferencial e o endereço IP do TeamIB1 de appliance_domain AD02 como o servidor DNS alternativo para o adaptador de rede TeamIB1. Use o endereço IP appliance_domain-AD01 TeamIB2 como o servidor DNS preferencial e o endereço IP do TeamIB2 de appliance_domain AD02 como o servidor DNS alternativo para o adaptador de rede TeamIB2.  
  
    2.  Se você tiver apenas um adaptador de rede InfiniBand, configure o adaptador com um endereço IP disponível de uma das redes InfiniBand. Em seguida, configure os servidores DNS preferenciais e alternativos nesse adaptador usando appliance_domain-AD01 TeamIB1 e appliance_domain-AD02 TeamIB1 ou usando appliance_domain-AD01 TeamIB2 e appliance_domain-AD02 TeamIB2 o que estiver na mesma rede que o adaptador configurado como os servidores DNS preferenciais e alternativos, respectivamente.  
  
3.  Configure o adaptador de rede InfiniBand para usar servidores DNS APS para resolver sua conexão com a rede InfiniBand ativa.  
  
    1.  Para configurar isso, use as configurações avançadas de TCP/IP para adicionar o sufixo DNS do domínio do dispositivo ao início da lista de sufixos DNS no servidor cliente. Isso só precisa ser configurado em um dos adaptadores de rede; a configuração se aplica a ambos os adaptadores.  
  
Depois de configurar os adaptadores de rede InfiniBand, os processos de cliente podem se conectar ao nó de controle `PDW_region-SQLCTL01` na rede InfiniBand usando o para o endereço do servidor. O servidor acrescenta o sufixo DNS do sistema da plataforma de análise ou você pode inserir o endereço completo que `PDW_region-SQLCTL01.appliance_domain.pdw.local`é.  
  
Por exemplo, se o nome da região do PDW for MyPDW e o nome do dispositivo for MyAPS, a especificação de servidor dwloader para carregar dados será uma das seguintes:  
  
-   `dwloader -S MYPDW-SQLCTL01.MyAPS.pdw.local`  
  
-   `dwloader -S MYPDW-SQLCTL01`  
  
## <a name="before-you-begin"></a><a name="BeforeBegin"></a>Antes de começar  
  
### <a name="requirements"></a>Requisitos  
Você precisa de uma conta de domínio do dispositivo APS para fazer logon no nó do AD01. Por exemplo, F12345 * \Administrator.  
  
Você precisa de uma conta do Windows no servidor cliente que tenha permissão para configurar os adaptadores de rede.  
  
### <a name="prerequisites"></a>Pré-requisitos  
Essas instruções pressupõem que o servidor cliente já está em rack e cabeado à rede InfiniBand do dispositivo. Para obter instruções de conexão e cabeamento, consulte [adquirir e configurar um servidor de carregamento](acquire-and-configure-loading-server.md).  
  
### <a name="general-remarks"></a>Comentários gerais  
Usando o SQLCTL01, o DNS do sistema de plataforma de análise conecta o servidor cliente ao nó de controle usando a rede InfiniBand ativa. Isso se aplica somente à conexão; se a rede InfiniBand falhar durante uma carga ou um backup, você precisará reiniciar o processo.  
  
Para atender aos seus próprios requisitos de negócios, você também pode ingressar o servidor cliente em seu próprio grupo de trabalho ou domínio do Windows que não seja de dispositivo.  
  
## <a name="step-1-obtain-the-appliance-infiniband-network-settings"></a><a name="Sec1"></a>Etapa 1: obter as configurações de rede InfiniBand do dispositivo  
*Para obter as configurações de rede InfiniBand do dispositivo*  
  
1.  Faça logon no nó do dispositivo AD01 usando a conta do appliance_domain \Administrador.  
  
2.  No nó do dispositivo AD01, abra o painel de controle, selecione rede e Internet, selecione Central de rede e compartilhamento * e, em seguida, selecione Alterar configurações do adaptador.  
  
3.  Na janela conexões de rede, clique com o botão direito do mouse em Team IB1 e selecione Propriedades.  
  
    ![Conexões InfiniBand no nó de gerenciamento](media/network-teamib.png "Conexões InfiniBand no nó de gerenciamento")  
  
4.  Na janela Propriedades de protocolo IP versão 4 (TCP/IPv4), anote os valores para o **endereço** e a **máscara de sub-rede**.  O endereço IP do nó ** _domínio\__-AD01 do dispositivo** é o endereço IP do servidor DNS do sistema de plataforma de análise.  
  
5.  Repita as etapas 1-5 acima para o adaptador TeamIB1 no servidor **de _domínio do\_dispositivo_AD02** .  
  
    ![Propriedades InfiniBand 1 do nó de gerenciamento do PDW](media/network-ip1-properties.png "Propriedades InfiniBand 1 do nó de gerenciamento do PDW")  
  
6.  Clique em Cancelar para fechar a janela.  
  
7.  Localize um endereço IP não utilizado na rede TeamIB1 e anote-o.  
  
    Para localizar um endereço IP não utilizado, abra uma janela de comando e tente executar ping nos endereços IP dentro do intervalo de endereços para seu dispositivo. Neste exemplo, o endereço IP da rede TeamIB1 é 172.16.14.30. Localize um endereço IP que começa com 172.16.14 que não é usado. Por exemplo, na linha de comando, digite "ping 172.16.14.254". Se a solicitação de ping não for bem-sucedida, o endereço IP estará disponível.  
  
8.  Faça a mesma coisa para TeamIB2. Na janela * conexões de rede, clique com o botão direito do mouse em Team IB2 e selecione Propriedades.  
  
9. Na janela Propriedades do protocolo IP versão 4 (TCP/IPv4), anote os valores para o endereço e a máscara de sub-rede do TeamIB2.  
  
10. Repita as etapas 8-9 acima para o adaptador TeamIB2 no servidor appliance_domain AD02.  
  
    ![Propriedades de TeamIB2](media/network-ip2-properties.png "Propriedades de TeamIB2")  
  
11. Localize um endereço IP não utilizado na rede **TeamIB2** e anote-o.  
  
    Para localizar um endereço IP não utilizado, abra uma janela de comando e tente executar ping nos endereços IP dentro do intervalo de endereços para seu dispositivo. Neste exemplo, o endereço IP da rede TeamIB2 é 172.16.18.30. Localize um endereço IP que começa com 172.16.18 que não é usado. Por exemplo, na linha de comando, digite "ping 172.16.18.254". Se a solicitação de ping não for bem-sucedida, o endereço IP estará disponível.  
  
## <a name="step-2-configure-the-infiniband-network-adapter-settings-on-your-client-server"></a><a name="Sec2"></a>Etapa 2: definir as configurações do adaptador de rede InfiniBand no seu servidor cliente  

### <a name="notes"></a>Observações  
  
-   Estas etapas mostram como registrar seu servidor com os servidores DNS APS.  
  
-   Para atender às suas necessidades de rede, você também pode ingressar o servidor cliente em seu próprio grupo de trabalho ou domínio do Windows que não seja de dispositivo.  
  
-   As instruções percorrem a configuração de dois adaptadores de rede em cada servidor.  Se você tiver apenas um adaptador de rede, escolha uma das redes a serem configuradas no adaptador de rede e, em seguida, adicione o segundo endereço IP DNS como um servidor DNS alternativo.  
  
### <a name="to-configure-the-infiniband-network-adapter-settings-on-your-client-server"></a>Para definir as configurações do adaptador de rede InfiniBand no seu servidor cliente  
  
1.  Faça logon como administrador do Windows para carregar, fazer backup ou outro servidor cliente na rede InfiniBand do dispositivo.  
  
2.  Abra o painel de controle *, selecione Central de rede e compartilhamento e, em seguida, selecione Alterar configurações do adaptador.  
  
### <a name="to-configure-the-first-network-adapter"></a>Para configurar o primeiro adaptador de rede  
  
1.  Na janela conexões de rede, clique com o botão direito do mouse em um dos slots de rede não identificados para o adaptador Mellanox e selecione Propriedades.  
  
    ![Selecionar as redes InfiniBand](media/network-connections.png "Selecionar as redes InfiniBand")  
  
2.  No janela Propriedades  
  
    1.  Na guia geral, defina o endereço IP para o endereço IP que você verificou como livre no teste de ping para TeamIB1. Para os valores de exemplo usados neste artigo, você digitaria 172.16.14.254.  
  
    2.  Defina a máscara de sub-rede para a máscara de sub-rede que você anotou para TeamIB1.  
  
    3.  Defina o servidor DNS preferencial como o endereço IP do TeamIB1 que você anotou anteriormente no nó appliance_domain *-AD01.  
  
    4.  Defina o servidor DNS alternativo para o endereço IP do TeamIB1 que você anotou anteriormente no nó appliance_domain *-AD02.  
  
        ![Propriedades do adaptador de rede InfiniBand 1](media/network-ib1-properties.png "SQL_Server_PDW_Network_IB1_properties")  
  
    5.  Clique em OK para aplicar as alterações.  
  
### <a name="to-configure-the-second-network-adapter"></a>Para configurar o segundo adaptador de rede  
  
1.  Ignore esta seção se você tiver apenas um adaptador de rede.  
  
2.  Na janela conexões de rede, clique com o botão direito do mouse no segundo slot de rede não identificado para o adaptador Mellanox e selecione Propriedades.  
  
    ![Selecionar as redes InfiniBand](media/network-connections.png "Selecionar as redes InfiniBand")  
  
3.  No janela Propriedades  
  
    1.  Na guia geral, defina o endereço IP para o endereço IP que você verificou como livre no teste de ping para TeamIB2. Para os valores de exemplo usados neste artigo, você digitaria 172.16.18.254.  
  
    2.  Defina a máscara de sub-rede para a máscara de sub-rede que você anotou para TeamIB2.  
  
    3.  Defina o servidor DNS preferencial como o endereço IP do TeamIB2 que você anotou anteriormente no nó appliance_domain *-AD01.  
  
    4.  Defina o servidor DNS alternativo para o endereço IP do TeamIB2 que você anotou anteriormente no nó appliance_domain *-AD02.  
  
        > [!NOTE]  
        > Se você tiver apenas um adaptador de rede, configure os servidores DNS preferenciais e alternativos usando o dispositivo AD01 TeamIB1 e o dispositivo AD02 TeamIB1 como os servidores DNS preferenciais e alternativos, respectivamente, ou use o dispositivo AD01 TeamIB2 e o dispositivo AD02 TeamIB2 como os servidores DNS preferenciais e alternativos, dependendo de se a máquina virtual do AD tiver realizado o failover.  
  
        ![Propriedades do adaptador de rede InfiniBand 1](media/network-ib1-properties.png "Propriedades do adaptador de rede InfiniBand 1")  
  
    5.  Clique em OK para aplicar as alterações.  
  
### <a name="to-configure-the-dns-suffix"></a>Para configurar o sufixo DNS  
  
1.  Na janela conexões de rede, clique com o botão direito do mouse em um dos slots de rede para o adaptador Mellanox e selecione Propriedades.  
  
2.  Clique no botão Avançado... Button.  
  
3.  Na janela Configurações avançadas de TCP/IP, se a opção acrescentar estes sufixos DNS (em ordem) não estiver esmaecida, marque a caixa chamada acrescentar estes sufixos DNS (em ordem):, selecione o sufixo de domínio do dispositivo e clique em Adicionar.... O sufixo de domínio do dispositivo é`appliance_domain.local`  
  
4.  Se a opção acrescentar estes sufixos DNS (em ordem): estiver esmaecida, você poderá adicionar o domínio APS a esse servidor modificando a chave do registro HKEY_LOCAL_MACHINE \SOFTWARE\Policies\Microsoft\Windows NT\DNSClient.  
  
    ![Configurações TCP/IP](media/network-tcpip.png "Configurações TCP/IP")  
  
5.  Para uma resolução de endereço mais rápida, recomendamos mover o sufixo do dispositivo para o topo da lista.  
  
6.  Clique em OK.  
  
7.  Agora, você pode se conectar à rede InfiniBand do dispositivo usando `PDW_region-SQLCTL01.appliance_domain.local`ou simplesmente `appliance_domain-SQLCTL01`. A conexão pode ser estabelecida mais rapidamente se você se conectar com o nome completo e o sufixo DNS.  
  
    Exemplos de um dispositivo chamado MyAPS com uma região MyPDW PDW:  
  
    -   MyPDW-SQLCTL01. MyAPS. local  
  
    -   MyPDW-SQLCTL01  
  
## <a name="see-also"></a>Consulte Também  
[Adquirir e configurar um servidor de carregamento](acquire-and-configure-loading-server.md)  
  
