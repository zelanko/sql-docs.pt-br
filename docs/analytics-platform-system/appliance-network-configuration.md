---
title: "Configuração de dispositivo de rede (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8e2b9abe-963d-479b-a4a7-1739fcb3e249
caps.latest.revision: "27"
ms.openlocfilehash: e24ed8e992591d08628ffeb14c30a47d7fa5b54a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="appliance-network-configuration"></a>Configuração de rede do dispositivo
O utilitário do SQL Server PDW é criado e configurado com um conjunto de correção de endereços IP em todos os servidores e dispositivos aplicáveis de Chão de fábrica do IHVS. Na entrega do aparelho, o IP externo (Ethernet) endereçado deve ser reconfigurado para atender aos requisitos de centro de dados do cliente específico.  
  
> [!NOTE]  
> PDW V1 necessários 8 externo IP (*voltada para o cliente*) endereços para fornecer conectividade externa para cada controle rack nós. 2012 PDW (V2) aprimorado comunicações de rede com a exposição de cada componente do aparelho externamente através de endereços IP. Essa abordagem fornece um design mais robusto que reduz os custos e aumenta a flexibilidade e aprimora a movimentação de dados, o carregamento de dados e a integração do Hadoop. O número de endereços IP necessários depende do número de nós no dispositivo e a presença de recursos, como HDInsight. Para acomodar esse bloco maior de endereços IP, o cliente deve configurar uma sub-rede separada para PDW. Essa sub-rede, haverá espaço de endereços IP suficientes (até 250 endereços) para acomodar os componentes de até 5 racks PDW.  
  
O **configuração de rede** página permite que você exiba as configurações de rede externamente para os nós em sua aplicação Analytics Platform System. Esta página é somente leitura.  
  
![Rede do dispositivo DWConfig](./media/appliance-network-configuration/SQL_Server_PDW_DWConfig_ApplTopNetwork.png "SQL_Server_PDW_DWConfig_ApplTopNetwork")  
  
## <a name="to-update-the-network-configuration-on-your-appliance"></a>Para atualizar a configuração de rede no seu dispositivo  
Alterar os endereços IP do domínio de malha, domínio de carga de trabalho e domínios de HDInsight, editando o **AplianceInfo.xml** de arquivo e, em seguida, executar a instalação. Esta é uma operação offline. O HDInsight (se houver) e PDW regiões serão automaticamente interrompidas durante a alteração do endereço IP.  
  
> [!NOTE]  
> Nomes de domínio são fornecidos durante a instalação e são especificados como até 6 caracteres alfanuméricos, iniciando com uma letra. Um sistema de nomeação frequente cria um domínio de malha começando com F, um domínio de carga de trabalho do PDW começando com P e um domínio de HDInsight começando com H. Esse formato é provável que durante os tópicos do arquivo de Ajuda, mas não é necessário. <!-- MISSING LINKS For more information about the domain structure, see [PDW Domain Security &#40;SQL Server PDW&#41;](../sqlpdw/pdw-domain-security-sql-server-pdw.md) and [Understanding the Security Model of the HDInsight Region &#40;Analytics Platform System&#41;](../hdinsight/understanding-the-security-model-of-the-hdinsight-region.md)  -->  
  
#### <a name="to-change-the-ip-addresses-of-the-analytics-platform-system"></a>Para alterar os endereços IP do sistema de plataforma de análise  
  
1.  Usando o **área de trabalho remota** aplicativo, conecte-se ao **HST01** usando a conta de administrador de domínio de carga de trabalho.  
  
2.  No nó HST01, abra o arquivo de informações do dispositivo em **c:\pdwinst\media\AplianceInfo.xml**.  
  
    > [!NOTE]  
    > Se o arquivo não estiver presente, talvez seja necessário um novo arquivo a ser criado.  
  
3.  Atualize os valores de IP de Ethernet, conforme necessário e salve o arquivo.  
  
4.  Em uma janela de prompt de comando, execute o seguinte comando de instalação para atualizar os endereços IP para a região PDW, usando os nomes de domínio de P/F/H e as senhas de administrador.  
  
    ```  
    c:\pdwinst\media\setup.exe /action="ConfigureEthernet" /DomainAdminPassword="<password>" /ApplianceInfoFile="C:\PDWINST\media\ApplianceInfo.xml"  
    ```  
  
## <a name="manufacturer-references"></a>Referências do fabricante  
Para obter informações adicionais sobre dispositivos Dell, consulte:  
  
-   Instruções Switch PowerConnect [guia de referência do sistema da série Dell PowerConnect 6200 CLI](http://downloads.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_powerconnect/powerconnect-6224f_Reference%20Guide_en-us.pdf)  
  
-   iDRAC/BMC [guia do usuário de versão 1.30.30 integrada Dell remoto acesso controlador 7 (iDRAC7)](http://downloads.dell.com/Manuals/all-products/esuprt_electronics/esuprt_software/esuprt_remote_ent_sys_mgmt/integrated-dell-remote-access-cntrllr-7-v1.30.30_User%27s%20Guide_en-us.pdf?c=us&l=en&cs=555&s=biz)  
  
-   PDUS **Dell limitados Rack PDU**`ftp://ftp.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_rack_infrastructure/dell-metered-pdu-led_User's%20Guide_en-us.pdf`  
  
## <a name="see-also"></a>Consulte também  
[Inicie o Gerenciador de configuração &#40; Analytics Platform System &#41;](launch-the-configuration-manager.md)  
  
