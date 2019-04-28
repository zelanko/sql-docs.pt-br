---
title: Comentários de telemetria - Analytics Platform System | Microsoft Docs
description: Envie comentários de telemetria à Microsoft para o Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 442505d470d1c7b7a82a02610d650d9f0b8c8d07
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62678374"
---
# <a name="send-telemetry-feedback-to-microsoft-for-analytics-platform-system"></a>Enviar comentários de telemetria à Microsoft para o Analytics Platform System
O Analytics Platform System tem um recurso de telemetria opcional que envia dados do Console do administrador para a Microsoft. 
  
> [!NOTE]  
> Nesta versão, Microsoft não está monitorando ativamente os dados de telemetria. Os dados está sendo coletados para apenas para fins de análise.  
  
## <a name="privacy"></a>Privacidade  
Para fornecer a proteção de privacidade máximo, APS é fornecido sem habilitar a telemetria. Antes de habilitar esse recurso, primeiro examine os [declaração de privacidade do Microsoft Analytics Platform System](https://go.microsoft.com/fwlink/?LinkId=400902). Para aceitar, execute o script do PowerShell descrito abaixo.  
  
## <a name="enable"></a>Habilitar a Telemetria  
**Encaminhamento de DNS:** Enviando dados de telemetria para a Microsoft exige o Analytics Platform System para se conectar à internet através de um encaminhador DNS. Para habilitar esse recurso, você deve habilitar o DNS de encaminhamento em todos os hosts e VMs da carga de trabalho. Invocar o `Enable-RemoteMonitoring` com o `SetupDnsForwarder` opção para configurar o encaminhamento de DNS e habilitar a telemetria corretamente. Invocar o `Enable-RemoteMonitoring` comando sem o `SetupDnsForwarder` opção quando o encaminhamento de DNS já está configurado e você deseja habilitar o monitoramento de pulsação.  
  
> [!IMPORTANT]  
> Habilitar o encaminhamento de DNS, a conexão de internet para todos os hosts e VMs da carga de trabalho é aberta.  
  
#### <a name="to-enable-feedback"></a>Para habilitar os comentários  
  
1.  Usando uma conta de administrador de domínio do dispositivo, conecte-se ao nó de controle (<strong>*appliance_domain*-CTL01</strong>) e abra um prompt de comando usando suas credenciais de administrador do Windows.  
  
2.  Navegue até o seguinte diretório: `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`.  
  
3.  Importe o módulo `Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > Para importar, você deve usar dois pontos no comando.  
  
    **Exemplo:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  Invocar o `Enable-RemoteMonitoring` comando.  
  
    > [!NOTE]  
    > O script pressupõe que a conexão de internet está funcionando corretamente e não valida a conexão de internet.  
  
    1.  Na primeira vez que você habilitar a telemetria, use o seguinte comando para garantir que todos os encaminhadores de DNS estão configurados corretamente. Neste exemplo, substitua o endereço IP de DNS encaminhados `xx.xx.xx.xx` com o endereço IP do encaminhador de DNS em seu ambiente.  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring -SetupDnsForwarder -DnsForwarderIp xx.xx.xx.xx  
        ```  
  
    2.  Quando os encaminhadores DNS já estiverem configurados, como reabilitar desabilitada anteriormente telemetria, use o seguinte comando para habilitar a telemetria sem configurar o encaminhamento de DNS.  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring  
        ```  
  
5.  Você será solicitado a leiam e confirmem que APS coletará informações sobre o dispositivo. Haverá um link para a declaração de privacidade do APS que você pode copiar e colar em qualquer navegador da internet para revisão.  
  
6.  Insira **Y** para aceitar e optar por comentários ou insira **N** não aceitar.  
  
7.  Se você inseriu **Y** haverá uma série de comandos que serão executados e que permitem a telemetria (e, opcionalmente, o encaminhador de DNS) recursos em seu dispositivo. Se você vir erros ou informações que levam você acreditar que o comando não foi bem-sucedida entre em contato com o CSS para obter assistência.  
  
Se você inseriu **N**, nenhum comando será executado e o recurso não será habilitado e não há nada mais para que você possa fazer.  
  
Não há nenhum prejuízo em execução o `Enable-RemoteMonitoring` comando várias vezes. Se o encaminhador DNS já estiver definido, você receberá uma mensagem de aviso indicando que é o caso.  
  
## <a name="disable"></a>Desabilitar a Telemetria  
Desabilitando a telemetria interromperá todas as operações que se comunicam informações sobre o estado do dispositivo para pontos de acesso, monitoramento de serviço na nuvem.  
  
> [!IMPORTANT]  
> Executar esta operação não desabilitará o encaminhador de DNS ou conexão de internet que pode estar em uso por outros recursos no dispositivo.  
  
#### <a name="to-disable-telemetry"></a>Para desabilitar a Telemetria  
  
1.  Usando uma conta de administrador de domínio do dispositivo, conecte-se ao nó de controle (<strong>*appliance_domain*-CTL01</strong>) e abra uma janela do PowerShell com privilégios de administrador.  
  
2.  Navegue até o seguinte diretório: `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`.  
  
3.  Importe o módulo `Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > Para importar, você deve usar dois pontos no comando.  
  
    **Exemplo:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  Invocar o `Disable-RemoteMonitoring` comando sem parâmetros. Esse comando irá parar de enviar comentários. (Isso não afetará o monitoramento local.) No entanto, o comando será não desabilitar o encaminhador de DNS e/ou desabilite qualquer conectividade com a internet. Isso deve ser feito manualmente depois de desabilitar o feedback com êxito.  
  
    **Exemplo:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Disable-RemoteMonitoring  
    ```  
  
Se você vir erros ou informações que levam você acreditar que o comando não foi bem-sucedida entre em contato com o CSS para obter assistência.  
  
Não há nenhum prejuízo em execução o `Disable-RemoteMonitoring` comando várias vezes.  
  
## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte:
- [Monitorar o dispositivo usando o Console de administração do &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
- [Monitorar o dispositivo por meio de exibições do sistema &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-views.md)  
- [Monitorar o dispositivo usando o System Center Operations Manager &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
- [Usar um encaminhador DNS para resolver nomes DNS não seja de dispositivo &#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
  
