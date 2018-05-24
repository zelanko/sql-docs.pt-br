---
title: Use um encaminhador DNS Analytics Platform System | Microsoft Docs"
description: Use um encaminhador DNS para resolver nomes DNS não seja de aplicação Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 2f707d4c681c695105daf23d5fc640279bb83658
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
---
# <a name="use-a-dns-forwarder-to-resolve-non-appliance-dns-names-in-analytics-platform-system"></a>Use um encaminhador DNS para resolver nomes DNS não seja de aplicação no sistema de plataforma de análise
Um encaminhador DNS pode ser configurado em nós do Active Directory Domain Services (***appliance_domain *-AD01** e ***appliance_domain *-AD02**) do seu dispositivo Analytics Platform System para permitir scripts e aplicativos de software para acessar servidores externos.  
  
## <a name="ResolveDNS"></a>Usando um encaminhador do DNS  
O dispositivo Analytics Platform System está configurado para impedir a resolução de nomes DNS de servidores que não estão no dispositivo. Alguns processos, como o Windows Software Update Services (WSUS), serão necessário acessar servidores fora do dispositivo. Para dar suporte a esse cenário de uso do sistema de plataforma de análise de DNS pode ser configurado para dar suporte a um encaminhador de nome externo que permitirá Analytics Platform System hosts e máquinas virtuais (VMs) usar servidores DNS externos para resolver nomes fora do dispositivo. Configuração personalizada de sufixos de DNS não tem suporte, o que significa que você deve usar nomes de domínio totalmente qualificado para resolver um nome de servidor não seja de aplicação.  
  
**Para criar um encaminhador DNS com a GUI do DNS**  
  
1.  Faça logon na ***appliance_domain *-AD01** nó.  
  
2.  Abra o Gerenciador de DNS (**dnsmgmt.msc**).  
  
3.  Clique no nome do servidor e, em seguida, clique em **propriedades**.  
  
4.  No **avançado** guia, desmarque o **desabilitar a recursão (também desabilita encaminhadores)** opção e, em seguida, clique em **aplicar**.)  
  
5.  Clique o **encaminhadores** guia e, em seguida, clique em **editar**.  
  
6.  Insira o endereço IP para o servidor DNS externo que fornecerá a resolução de nome. As VMs e servidores (hosts) em que o dispositivo se conectará a servidores externos usando nomes de domínio totalmente qualificado.  
  
7.  Repita as etapas de 1 a 6 no ***appliance_domain *-AD02** nó  
  
**Para criar um encaminhador do DNS por meio do Windows PowerShell**  
  
1.  Faça logon na ***appliance_domain *-AD01**nó.  
  
2.  Execute o seguinte script do Windows PowerShell do ***appliance_domain *-AD01** nó. Antes de executar o script do Windows PowerShell, substitua os endereços IP com os endereços IP dos servidores DNS não seja de aplicação.  
  
    ```  
    $DNS=Get-WmiObject -class "MicrosoftDNS_Server"  -Namespace "root\microsoftdns"  
    $DNS.Forwarders = ("xxx.xxx.xxx.xxx", "xxx.xxx.xxx.xxx")  
    $DNS.put()  
    ```  
  
3.  Execute o comando mesmo no ***appliance_domain *-AD02** nó.  
  
## <a name="configuring-dns-resolution-for-wsus"></a>Configurando a resolução de DNS para o WSUS  
PDW do SQL Server 2012 fornece funcionalidade de aplicação de patch e manutenção integrado. SQL Server PDW usa o Microsoft Update e outra tecnologias de serviço da Microsoft. Para habilitar atualizações do que dispositivo deve ser capaz de se conectar ou para um repositório WSUS corporativo ou no repositório do WSUS pública do Microsoft.  
  
Para clientes que optar por configurar o dispositivo para procurar atualizações no repositório Microsoft público do WSUS, as instruções a seguir defina os detalhes de configuração apropriada no dispositivo.  
  
> [!NOTE]  
> O administrador de rede do cliente deve fornecer o endereço IP para um servidor DNS corporativo que pode resolver nomes no **Microsoft.com**.  
  
1.  Usando a área de trabalho remota, faça logon no VMM VM (<fabric domain>- VMM) usando a conta de administrador de domínio de malha.  
  
2.  Abra o painel de controle, clique em **rede e Internet**e, em seguida, clique em **Central de rede e compartilhamento**.  
  
3.  Na lista de conexão, clique em **VMSEthernet**e, em seguida, clique em **propriedades**.  
  
4.  Selecione **Internet Protocol versão 4 (TCP/IPv4)** e, em seguida, clique em **propriedades**.  
  
5.  No **servidor DNS alternativo** caixa, adicione o endereço IP fornecido pelo administrador de rede do cliente.  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
