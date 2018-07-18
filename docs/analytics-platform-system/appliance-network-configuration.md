---
title: Configuração de rede do dispositivo - Analytics Platform System | Microsoft Docs
description: O dispositivo do Analytics Platform System (APS) é criado e configurado com um conjunto de correção de endereços IP em toda a todos os servidores e dispositivos aplicáveis de Chão de fábrica do IHV. Após a entrega do dispositivo, o endereço IP externo (Ethernet) deve ser reconfigurado para atender aos requisitos de centro de dados do cliente específico.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d11184c1fd12ae40188ef4e4442e7f9b7fb6b04a
ms.sourcegitcommit: 731c5aed039607a8df34c63e780d23a8fac937e1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/07/2018
ms.locfileid: "37909806"
---
# <a name="appliance-network-configuration-for-analytics-platform-system"></a>Configuração de rede do dispositivo para o Analytics Platform System
O dispositivo do Analytics Platform System (APS) é criado e configurado com um conjunto de correção de endereços IP em toda a todos os servidores e dispositivos aplicáveis de Chão de fábrica do IHV. Após a entrega do dispositivo, o endereço IP externo (Ethernet) deve ser reconfigurado para atender aos requisitos de centro de dados do cliente específico.  
  
> [!NOTE]  
> PDW V1 necessário 8 externo IP (*voltado ao cliente*) nós de rack de endereços para fornecer conectividade externa para cada controle. 2012 PDW (V2) aprimorados comunicações de rede, expondo todos os componentes do dispositivo externamente por meio de endereços IP. Essa abordagem fornece um design mais robusto que reduz os custos, aumenta a flexibilidade e aprimora a movimentação de dados, carregamento de dados e integração de Hadoop. O número de endereços IP necessários depende do número de nós no dispositivo. Para acomodar esse bloco maior de endereços IP, o cliente deverá configurar uma sub-rede separada para PDW. Dentro dessa sub-rede, haverá espaço de endereço IP suficiente (até 250 endereços) para acomodar os componentes de até 5 racks PDW.  
  
O **configuração de rede** página permite que você exiba as configurações de rede voltado para o exterior para os nós em seu dispositivo do Analytics Platform System. Esta página é somente leitura.  
  
![DWConfig Appliance Network](./media/appliance-network-configuration/SQL_Server_PDW_DWConfig_ApplTopNetwork.png "SQL_Server_PDW_DWConfig_ApplTopNetwork")  
  
## <a name="to-update-the-network-configuration-on-your-appliance"></a>Para atualizar a configuração de rede em seu dispositivo  
Alterar os endereços IP do domínio de malha e do domínio de carga de trabalho, editando a **AplianceInfo.xml** arquivo e, em seguida, executar a instalação. Esta é uma operação offline. As regiões do PDW serão interrompidas automaticamente durante a alteração de endereço IP.  
  
> [!NOTE]  
> Nomes de domínio são fornecidos durante a instalação e são especificados como até 6 caracteres alfanuméricos, começando com uma letra. Um sistema de nomenclatura frequente cria um domínio de malha começando com o F, um domínio de carga de trabalho do PDW começam com P. Esse formato é provável que ao longo de tópicos do arquivo de Ajuda, mas não é necessário. <!-- MISSING LINKS For more information about the domain structure, see [PDW Domain Security &#40;SQL Server PDW&#41;](../sqlpdw/pdw-domain-security-sql-server-pdw.md) and [Understanding the Security Model of the HDInsight Region &#40;Analytics Platform System&#41;](../hdinsight/understanding-the-security-model-of-the-hdinsight-region.md)  -->  
  
#### <a name="to-change-the-ip-addresses-of-the-analytics-platform-system"></a>Para alterar os endereços IP do Analytics Platform System  
  
1.  Usando o **área de trabalho remota** aplicativo, se conectar ao **HST01** usando a conta de administrador de domínio de carga de trabalho.  
  
2.  No nó HST01, abra o arquivo de informações do dispositivo no **c:\pdwinst\media\AplianceInfo.xml**.  
  
    > [!NOTE]  
    > Se o arquivo não estiver presente, talvez seja necessário um novo arquivo a ser criado.  
  
3.  Atualize os valores de IP de Ethernet, conforme necessário e salve o arquivo.  
  
4.  Em uma janela de prompt de comando, execute o seguinte comando de instalação para atualizar os endereços IP para a região do PDW, usando os nomes de domínio do P/F/H e as senhas de administrador.  
  
    ```  
    c:\pdwinst\media\setup.exe /action="ConfigureEthernet" /DomainAdminPassword="<password>" /ApplianceInfoFile="C:\PDWINST\media\ApplianceInfo.xml"  
    ```  
  
## <a name="manufacturer-references"></a>Referências do fabricante  
Para obter informações adicionais sobre dispositivos de Dell, consulte:  
  
-   Instruções Switch PowerConnect [guia de referência do sistema da série Dell PowerConnect 6200 CLI](http://downloads.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_powerconnect/powerconnect-6224f_Reference%20Guide_en-us.pdf)  
  
-   iDRAC/BMC [guia do usuário da versão 1.30.30 integrada Dell Remote Access Controller 7 (iDRAC7)](http://downloads.dell.com/Manuals/all-products/esuprt_electronics/esuprt_software/esuprt_remote_ent_sys_mgmt/integrated-dell-remote-access-cntrllr-7-v1.30.30_User%27s%20Guide_en-us.pdf?c=us&l=en&cs=555&s=biz)  
  
-   Da PDU **Dell monitorados Rack PDU**`ftp://ftp.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_rack_infrastructure/dell-metered-pdu-led_User's%20Guide_en-us.pdf`  
  
## <a name="see-also"></a>Consulte também  
[Inicie o Gerenciador de configuração &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)  
  
