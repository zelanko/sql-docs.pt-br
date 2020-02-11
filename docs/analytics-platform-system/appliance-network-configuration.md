---
title: Configuração de rede do dispositivo
description: O dispositivo de sistema de plataforma de análise (APS) é criado e configurado com um conjunto de correção de endereços IP em todos os servidores e dispositivos aplicáveis do chão de fábrica do IHV. Após a entrega do dispositivo, o IP externo (Ethernet) endereçado deve ser reconfigurado para corresponder aos requisitos de data center do cliente específico.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: af892cbb43b42953732bda59d371e3e22855413b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401416"
---
# <a name="appliance-network-configuration-for-analytics-platform-system"></a>Configuração de rede de dispositivo para o Analytics Platform System
O dispositivo de sistema de plataforma de análise (APS) é criado e configurado com um conjunto de correção de endereços IP em todos os servidores e dispositivos aplicáveis do chão de fábrica do IHV. Após a entrega do dispositivo, o IP externo (Ethernet) endereçado deve ser reconfigurado para corresponder aos requisitos de data center do cliente específico.  
  
> [!NOTE]  
> O PDW v1 exigiu 8 endereços IP externos (*voltados*para o cliente) para fornecer conectividade externa a cada um dos nós de rack de controle. PDW 2012 (v2) comunicação de rede aprimorada expondo todos os componentes do dispositivo externamente por meio de endereços IP. Essa abordagem fornece um design mais robusto que reduz os custos e aumenta a flexibilidade, além de aprimorar a movimentação de dados, o carregamento de dados e a integração do Hadoop. O número de endereços IP necessários depende do número de nós no dispositivo. Para acomodar esse bloco maior de endereços IP, o cliente deve configurar uma sub-rede separada para o PDW. Nessa sub-rede, haverá espaço de endereço IP suficiente (até 250 endereços) para acomodar os componentes de até 5 racks do PDW.  
  
A página **configuração de rede** permite que você exiba as configurações de rede externas para os nós em seu dispositivo de sistema de plataforma de análise. Esta página é somente leitura.  
  
![Rede do dispositivo DWConfig](./media/appliance-network-configuration/SQL_Server_PDW_DWConfig_ApplTopNetwork.png "SQL_Server_PDW_DWConfig_ApplTopNetwork")  
  
## <a name="to-update-the-network-configuration-on-your-appliance"></a>Para atualizar a configuração de rede em seu dispositivo  
Altere os endereços IP do domínio de malha e o domínio de carga de trabalho editando o arquivo **AplianceInfo. xml** e, em seguida, executando a instalação. Esta é uma operação offline. As regiões do PDW serão automaticamente interrompidas durante a alteração do endereço IP.  
  
> [!NOTE]  
> Os nomes de domínio são fornecidos durante a instalação e são especificados como até 6 caracteres alfanuméricos, começando com uma letra. Um sistema de nomenclatura frequente cria um domínio de malha começando com F, um domínio de carga de trabalho do PDW começando com P. Esse formato é presumido em todos os tópicos do arquivo de ajuda, mas não é necessário. <!-- MISSING LINKS For more information about the domain structure, see [PDW Domain Security &#40;SQL Server PDW&#41;](../sqlpdw/pdw-domain-security-sql-server-pdw.md) and [Understanding the Security Model of the HDInsight Region &#40;Analytics Platform System&#41;](../hdinsight/understanding-the-security-model-of-the-hdinsight-region.md)  -->  
  
#### <a name="to-change-the-ip-addresses-of-the-analytics-platform-system"></a>Para alterar os endereços IP do sistema da plataforma de análise  
  
1.  Usando o aplicativo **área de trabalho remota** , conecte-se ao **HST01** usando a conta de administrador de domínio de carga de trabalho.  
  
2.  No nó HST01, abra o arquivo de informações do dispositivo em **c:\pdwinst\media\AplianceInfo.xml**.  
  
    > [!NOTE]  
    > Se o arquivo não estiver presente, talvez seja necessário criar um novo arquivo.  
  
3.  Atualize os valores de IP de Ethernet conforme necessário e salve o arquivo.  
  
4.  Em uma janela de prompt de comando, execute o seguinte comando de instalação para atualizar os endereços IP para a região PDW, usando os nomes de domínio P/F/H e as senhas de administrador.  
  
    ```  
    c:\pdwinst\media\setup.exe /action="ConfigureEthernet" /DomainAdminPassword="<password>" /ApplianceInfoFile="C:\PDWINST\media\ApplianceInfo.xml"  
    ```  
  
## <a name="manufacturer-references"></a>Referências do fabricante  
Para obter informações adicionais sobre dispositivos Dell, consulte:  
  
-   Instruções do switch PowerConnect [Guia de referência da CLI do sistema do Dell powerconnect 6200 Series](https://downloads.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_powerconnect/powerconnect-6224f_Reference%20Guide_en-us.pdf)  
  
-   [Guia do usuário do iDRAC/BMC Integrated Dell Remote Access Controller 7 (iDRAC7) versão 1.30.30](https://downloads.dell.com/Manuals/all-products/esuprt_electronics/esuprt_software/esuprt_remote_ent_sys_mgmt/integrated-dell-remote-access-cntrllr-7-v1.30.30_User%27s%20Guide_en-us.pdf?c=us&l=en&cs=555&s=biz)  
  
-   PDU do **rack medido da Dell** da PDU`ftp://ftp.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_rack_infrastructure/dell-metered-pdu-led_User's%20Guide_en-us.pdf`  
  
## <a name="see-also"></a>Consulte Também  
[Inicie o Configuration Manager &#40;o sistema de plataforma de análise&#41;](launch-the-configuration-manager.md)  
  
