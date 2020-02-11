---
title: Comentários de telemetria
description: Envie comentários de telemetria para a Microsoft para o Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 639eb4e9e5c531e154b9eb7f91165af365bc519f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74400358"
---
# <a name="send-telemetry-feedback-to-microsoft-for-analytics-platform-system"></a>Enviar comentários de telemetria para a Microsoft para o Analytics Platform System
O Analytics Platform System tem um recurso de telemetria opcional que envia dados do console de administração para a Microsoft. 
  
> [!NOTE]  
> Nesta versão, a Microsoft não está monitorando ativamente os dados de telemetria. Os dados estão sendo coletados apenas para fins de análise.  
  
## <a name="privacy"></a>Privacidade  
Para fornecer a proteção máxima de privacidade, o APS é fornecido sem habilitar a telemetria. Antes de habilitar esse recurso, primeiro examine a [declaração de privacidade de Microsoft Analytics Platform System](https://go.microsoft.com/fwlink/?LinkId=400902). Para aceitar, execute o script do PowerShell descrito abaixo.  
  
## <a name="enable"></a>Habilitar telemetria  
**Encaminhamento de DNS:** O envio de dados de telemetria para a Microsoft exige que o sistema de plataforma de análise se conecte à Internet por meio de um encaminhador DNS. Para habilitar esse recurso, você deve habilitar o encaminhamento de DNS em todos os hosts e VMs de carga de trabalho. Invoque o `Enable-RemoteMonitoring` comando com a `SetupDnsForwarder` opção de configurar corretamente o encaminhamento de DNS e habilitar a telemetria. Invoque o `Enable-RemoteMonitoring` comando sem a `SetupDnsForwarder` opção quando o encaminhamento de DNS já estiver configurado e você quiser habilitar o monitoramento de pulsação.  
  
> [!IMPORTANT]  
> Habilitar o encaminhamento de DNS abre a conexão com a Internet para todos os hosts e VMs de carga de trabalho.  
  
#### <a name="to-enable-feedback"></a>Para habilitar os comentários  
  
1.  Usando uma conta de administrador de domínio de dispositivo, conecte-se ao nó de controle (<strong>*appliance_domain*-CTL01</strong>) e abra um prompt de comando usando suas credenciais de administrador do Windows.  
  
2.  Navegue até o seguinte diretório: `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`.  
  
3.  Importar o módulo`Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > Para importar, você deve usar dois pontos no comando.  
  
    **Exemplo:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  Invoque o `Enable-RemoteMonitoring` comando.  
  
    > [!NOTE]  
    > O script supõe que a conexão com a Internet está funcionando corretamente e não valida a conexão com a Internet.  
  
    1.  Na primeira vez que você habilitar a telemetria, use o comando a seguir para garantir que todos os encaminhadores DNS estejam configurados corretamente. Neste exemplo, substitua o endereço `xx.xx.xx.xx` IP encaminhado DNS pelo endereço IP do encaminhador de DNS em seu ambiente.  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring -SetupDnsForwarder -DnsForwarderIp xx.xx.xx.xx  
        ```  
  
    2.  Quando os encaminhadores DNS já estão configurados, como reabilitar a telemetria desabilitada anteriormente, use o comando a seguir para habilitar a telemetria sem configurar o encaminhamento de DNS.  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring  
        ```  
  
5.  Você será solicitado a ler e reconhecer que o APS coletará informações sobre o dispositivo. Haverá um link para a política de privacidade do APS que você pode copiar e colar em qualquer navegador da Internet para revisão.  
  
6.  Digite **Y** para aceitar e optar por comentários ou digite **N** para não aceitar.  
  
7.  Se você tiver inserido **Y** , haverá uma série de comandos que serão executados, o que habilitará o recurso telemetria (e, opcionalmente, o encaminhador de DNS) em seu dispositivo. Se você vir quaisquer erros ou informações que o levam a acreditar que o comando não foi bem-sucedido, contate o CSS para obter assistência.  
  
Se você inseriu **N**, nenhum comando será executado e o recurso não será habilitado e não haverá nada mais para você fazer.  
  
Não há nenhum dano na execução do `Enable-RemoteMonitoring` comando várias vezes. Se o encaminhador DNS já estiver definido, você receberá uma mensagem de aviso indicando que é o caso.  
  
## <a name="disable"></a>Desabilitar telemetria  
Desabilitar a telemetria interromperá todas as operações que comunicam informações sobre o estado do dispositivo para o serviço de monitoramento do APS na nuvem.  
  
> [!IMPORTANT]  
> A execução dessa operação não desabilitará o encaminhador DNS ou a conexão com a Internet que pode estar em uso por outros recursos no dispositivo.  
  
#### <a name="to-disable-telemetry"></a>Para desabilitar a telemetria  
  
1.  Usando uma conta de administrador de domínio de dispositivo, conecte-se ao nó de controle (<strong>*appliance_domain*-CTL01</strong>) e abra uma janela do PowerShell com privilégios de administrador.  
  
2.  Navegue até o seguinte diretório: `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`.  
  
3.  Importar o módulo`Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > Para importar, você deve usar dois pontos no comando.  
  
    **Exemplo:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  Invoque o `Disable-RemoteMonitoring` comando sem parâmetros. Este comando deixará de enviar comentários. (Isso não afetará o monitoramento local.) No entanto, o comando não desabilitará o encaminhador de DNS e/ou desabilitará qualquer conectividade com a Internet. Isso deve ser feito manualmente após a desabilitação bem-sucedida dos comentários.  
  
    **Exemplo:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Disable-RemoteMonitoring  
    ```  
  
Se você vir quaisquer erros ou informações que o levam a acreditar que o comando não foi bem-sucedido, contate o CSS para obter assistência.  
  
Não há nenhum dano na execução do `Disable-RemoteMonitoring` comando várias vezes.  
  
## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte:
- [Monitore o dispositivo usando o console de administração &#40;o sistema de plataforma de análise&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
- [Monitore o dispositivo usando as exibições do sistema &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-views.md)  
- [Monitore o dispositivo usando System Center Operations Manager &#40;o sistema de plataforma de análise&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
- [Use um encaminhador DNS para resolver nomes DNS que não são de dispositivo &#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
  
