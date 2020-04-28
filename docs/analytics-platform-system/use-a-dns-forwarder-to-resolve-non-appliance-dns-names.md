---
title: Usar um encaminhador DNS
description: Use um encaminhador DNS para resolver nomes DNS que não são de dispositivo no Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 3d1d0d9428138da615fad7ff5745c758d9fcd3b8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74399430"
---
# <a name="use-a-dns-forwarder-to-resolve-non-appliance-dns-names-in-analytics-platform-system"></a>Usar um encaminhador DNS para resolver nomes DNS que não são de dispositivo no Analytics Platform System
Um encaminhador de DNS pode ser configurado nos nós de Active Directory Domain Services (**_domínio de dispositivo\__– AD01** e domínio de ** _dispositivo\__-AD02**) do seu dispositivo de sistema de plataforma de análise para permitir que scripts e aplicativos de software acessem servidores externos.  
  
## <a name="using-a-dns-forwarder"></a><a name="ResolveDNS"></a>Usando um encaminhador DNS  
O dispositivo Analytics Platform System está configurado para impedir a resolução de nomes DNS de servidores que não estão no dispositivo. Alguns processos, como o WSUS (Windows Software Update Services), precisarão acessar os servidores fora do dispositivo. Para dar suporte a esse cenário de uso, o DNS do sistema da plataforma de análise pode ser configurado para dar suporte a um encaminhador de nome externo que permitirá que os hosts do sistema da plataforma de análise e VMs (máquinas virtuais) usem servidores DNS externos para resolver nomes fora do dispositivo. Não há suporte para a configuração personalizada de sufixos DNS, o que significa que você deve usar nomes de domínio totalmente qualificados para resolver um nome de servidor que não seja de dispositivo.  
  
**Para criar um encaminhador DNS com a GUI do DNS**  
  
1.  Faça logon no nó ** _domínio\_do dispositivo_– AD01** .  
  
2.  Abra o Gerenciador DNS (**DNSMGMT. msc**).  
  
3.  Clique com o botão direito do mouse no nome do servidor e clique em **Propriedades**.  
  
4.  Na guia **avançado** , desmarque a opção **desabilitar recursão (também desabilita encaminhadores)** e clique em **aplicar**.)  
  
5.  Clique na guia **encaminhadores** e clique em **Editar**.  
  
6.  Insira o endereço IP para o servidor DNS externo que fornecerá a resolução de nomes. As VMs e os servidores (hosts) no dispositivo serão conectados a servidores externos usando nomes de domínio totalmente qualificados.  
  
7.  Repita as etapas de 1-6 no ** _domínio do dispositivo\__– nó AD02**  
  
**Para criar um encaminhador DNS usando o Windows PowerShell**  
  
1.  Faça logon no nó ** _domínio\_do dispositivo_– AD01**.  
  
2.  Execute o seguinte script do Windows PowerShell no nó ** _domínio do dispositivo\__– AD01** . Antes de executar o script do Windows PowerShell, substitua os endereços IP pelos endereços IP dos servidores DNS que não são do dispositivo.  
  
    ```  
    $DNS=Get-WmiObject -class "MicrosoftDNS_Server"  -Namespace "root\microsoftdns"  
    $DNS.Forwarders = ("xxx.xxx.xxx.xxx", "xxx.xxx.xxx.xxx")  
    $DNS.put()  
    ```  
  
3.  Execute o mesmo comando no nó do ** _dispositivo\_domínio_-AD02** .  
  
## <a name="configuring-dns-resolution-for-wsus"></a>Configurando a resolução de DNS para o WSUS  
O SQL Server PDW 2012 fornece manutenção integrada e funcionalidade de aplicação de patches. O SQL Server PDW usa Microsoft Update e outras tecnologias de serviço da Microsoft. Para habilitar atualizações, o dispositivo deve ser capaz de se conectar a um repositório WSUS corporativo ou ao repositório do WSUS público da Microsoft.  
  
Para clientes que optam por configurar o dispositivo para procurar atualizações no repositório do WSUS público da Microsoft, as instruções a seguir definem os detalhes de configuração apropriados no dispositivo.  
  
> [!NOTE]  
> O administrador de rede do cliente deve fornecer o endereço IP para um servidor DNS corporativo que pode resolver nomes em **Microsoft.com**.  
  
1.  Usando a área de trabalho remota, faça logon na<fabric domain>VM do VMM (-VMM) usando a conta de administrador de domínio da malha.  
  
2.  Abra o painel de controle, clique em **rede e Internet**e, em seguida, clique em **central de rede e compartilhamento**.  
  
3.  Na lista conexão, clique em **VMSEthernet**e em **Propriedades**.  
  
4.  Selecione **Internet Protocol Version 4 (TCP/IPv4)** e, em seguida, clique em **Propriedades**.  
  
5.  Na caixa **servidor DNS alternativo** , adicione o endereço IP fornecido pelo administrador de rede do cliente.  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
