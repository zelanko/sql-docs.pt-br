---
title: Usar um encaminhador DNS no Analytics Platform System | Microsoft Docs"
description: Use um encaminhador DNS para resolver nomes DNS não seja de dispositivo no Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 841d2da521bada840c1298d3fb9cea28c2835b4a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959823"
---
# <a name="use-a-dns-forwarder-to-resolve-non-appliance-dns-names-in-analytics-platform-system"></a>Usar um encaminhador DNS para resolver nomes DNS não seja de dispositivo no Analytics Platform System
Um encaminhador DNS pode ser configurado em nós do Active Directory Domain Services ( **_appliance\_domínio_-AD01** e  **_appliance\_ domínio_-AD02**) de seu dispositivo do Analytics Platform System para permitir que scripts e aplicativos de software para acessar servidores externos.  
  
## <a name="ResolveDNS"></a>Usando um encaminhador do DNS  
O dispositivo do Analytics Platform System está configurado para evitar a resolução de nomes DNS dos servidores que não estão no dispositivo. Alguns processos, como o Software Update Services (WSUS) de Windows, serão necessário acessar servidores fora do dispositivo. Para dar suporte a esse cenário de uso, o sistema de plataforma de análise de DNS pode ser configurado para dar suporte a um encaminhador de nome externo que permitirá que os hosts do Analytics Platform System e máquinas virtuais (VMs) para usar servidores DNS externos para resolver nomes fora do dispositivo. Configuração personalizada de sufixos DNS não for compatível, o que significa que você deve usar nomes de domínio totalmente qualificado para resolver um nome de servidor não seja de dispositivo.  
  
**Para criar um encaminhador DNS com a GUI do DNS**  
  
1.  Faça logon na  **_appliance\_domínio_-AD01** nó.  
  
2.  Abra o Gerenciador de DNS (**Dnsmgmt. msc**).  
  
3.  Clique no nome do servidor e, em seguida, clique em **propriedades**.  
  
4.  Na **Advanced** guia, desmarque as **desabilitar a recursão (também desabilita encaminhadores)** opção e, em seguida, clique em **aplicar**.)  
  
5.  Clique o **encaminhadores** guia e, em seguida, clique em **editar**.  
  
6.  Insira o endereço IP para o servidor DNS externo que fornecerá a resolução de nome. As VMs e servidores (hosts) no dispositivo se conectará a servidores externos por meio de nomes de domínio totalmente qualificado.  
  
7.  Repita as etapas de 1 a 6 na  **_appliance\_domínio_-AD02** nó  
  
**Para criar um encaminhador DNS usando o Windows PowerShell**  
  
1.  Faça logon na  **_appliance\_domínio_-AD01**nó.  
  
2.  Execute o seguinte script do Windows PowerShell do  **_appliance\_domínio_-AD01** nó. Antes de executar o script do Windows PowerShell, substitua os endereços IP com os endereços IP dos servidores DNS não seja de dispositivo.  
  
    ```  
    $DNS=Get-WmiObject -class "MicrosoftDNS_Server"  -Namespace "root\microsoftdns"  
    $DNS.Forwarders = ("xxx.xxx.xxx.xxx", "xxx.xxx.xxx.xxx")  
    $DNS.put()  
    ```  
  
3.  Executar o mesmo comando sobre o  **_appliance\_domínio_-AD02** nó.  
  
## <a name="configuring-dns-resolution-for-wsus"></a>Configurar a resolução de DNS para o WSUS  
PDW do SQL Server 2012 fornece a funcionalidade de aplicação de patch e manutenção integrado. SQL Server PDW usa o Microsoft Update e outra tecnologias de manutenção da Microsoft. Para habilitar atualizações para que o dispositivo deve ser capaz de se conectar a um repositório corporativo do WSUS ou para o repositório WSUS público do Microsoft.  
  
Para clientes que optar por configurar o dispositivo para procurar por atualizações sobre o repositório WSUS pública da Microsoft, as instruções a seguir definem os detalhes de configuração adequada no dispositivo.  
  
> [!NOTE]  
> O administrador de rede do cliente deve fornecer o endereço IP para um servidor DNS corporativo que pode resolver nomes em **Microsoft.com**.  
  
1.  Usando a área de trabalho remota, faça logon em VM do VMM (<fabric domain>- VMM) usando a conta de administrador de domínio de malha.  
  
2.  Abra o painel de controle, clique em **rede e Internet**e, em seguida, clique em **Central de rede e compartilhamento**.  
  
3.  Na lista de conexão, clique em **VMSEthernet**e, em seguida, clique em **propriedades**.  
  
4.  Selecione **Internet Protocol versão 4 (TCP/IPv4)** e, em seguida, clique em **propriedades**.  
  
5.  No **servidor DNS alternativo** caixa, adicione o endereço IP fornecido pelo administrador de rede do cliente.  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
