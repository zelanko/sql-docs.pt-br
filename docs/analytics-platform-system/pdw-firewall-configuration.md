---
title: Configuração do firewall do PDW
description: A página Firewall do SQL Server PDW Configuration Manager permite habilitar ou desabilitar as regras de firewall que permitem ou impedem o acesso a portas específicas no dispositivo de sistema de plataforma de análise.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 4ed739ce12170aa6d0ab79b996de0075cd6723ee
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400881"
---
# <a name="parallel-data-warehouse-firewall-configuration-in-analytics-platform-system"></a>Configuração de firewall paralelo data warehouse no Analytics Platform System

A página **Firewall** do SQL Server PDW Configuration Manager permite habilitar ou desabilitar as regras de firewall que permitem ou impedem o acesso a portas específicas no dispositivo de sistema de plataforma de análise.  
  
## <a name="to-manage-ports-and-firewall-rules-for-appliance-nodes"></a>Para gerenciar portas e regras de firewall para nós de dispositivo  
  
1.  Inicie o Configuration Manager. Para obter mais informações, consulte [iniciar o Configuration Manager &#40;&#41;do sistema de plataforma de análise ](launch-the-configuration-manager.md).  
  
2.  No painel esquerdo da Configuration Manager, expanda **data warehouse topologia paralela**e clique em **Firewall**.  
  
3.  Localize a porta ou a regra de firewall para atualizar na lista de configuração e, em seguida, marque ou desmarque a caixa ao lado desse item. Somente SQL Server PDW opções configuráveis pelo administrador são mostradas nesta lista, incluindo as portas de abertura e fechamento em nós voltados externamente.  
  
4.  Clique em **aplicar** para salvar as alterações.  
  
![Firewall PDW do dispositivo DWConfig](./media/pdw-firewall-configuration/SQL_Server_PDW_DWConfig_ApplPDWFirewall.png "SQL_Server_PDW_DWConfig_ApplPDWFirewall")  
  
## <a name="external-ports"></a>Portas externas  
As portas a seguir são abertas para conexões de cliente provenientes de fora do PDW.  
  
|Finalidade|Porto #|Nós|  
|-----------|-----------|---------|  
|Acesso para cliente do SQL para PDW (TDS)|17001|CERTIFICADOS|  
|Acesso de cliente do carregador (dwloader & SSIS)|8001|CERTIFICADOS|  
|Acesso remoto à área de trabalho|3389|CTL, CMP|  
|BinaryLoaderDataChannel SSIS|16551|CERTIFICADOS|  
|dwloader BinaryLoaderDataChannel|16551|CMP|  
|Conexões SSL criptografadas (para comunicações internas, para acessar o console de administração)|443|Todos os nós|  
|Fluxo de controle de carga SQL Server PDW-credenciais do Windows|8002|CERTIFICADOS|  
|_Kerberos|88|AD01 e AD02,|  
|_ldap|389|AD01 e AD02|  
| &nbsp; | &nbsp; | &nbsp; |
  
## <a name="internal-ports"></a>Portas internas  
As portas a seguir são usadas pelo PDW para comunicação interna, mas não são abertas para conexões provenientes de fora do dispositivo PDW.  
  
|Finalidade|Porto #|Nós|  
|-----------|-----------|---------|  
|Tráfego de canal de controle DMS|16450|CTL, CMP|  
|Tráfego de canal de dados DMS|16550|CTL, CMP|  
|Diagnóstico interno|16650|CTL, CMP|  
|Status de failover (DMS)|15000|CTL, CMP|  
|Status de failover (mecanismo)|15001|CMP|  
|Intervalo de portas dinâmica (efêmera)|20000-65535|CTL, CMP|  
|Intervalos de porta SQL Server (TDS)|1433, 1500-1508|CTL, CMP|  
| &nbsp; | &nbsp; | &nbsp; |
  
> [!NOTE]  
> A criação de tabelas externas ou de fontes de dados externas usa a porta TCP 8020 por padrão. Essas instruções podem ser configuradas para usar outras portas em vez disso. O Hortonworks JOB_TRACKER_LOCATION porta padrão é 50300. A integração com outros sistemas e ferramentas pode exigir portas adicionais.  
  
<!-- MISSING LINKS ## See Also  
[HDInsight Firewall Configuration &#40;Analytics Platform System&#41;](hdinsight-firewall-configuration.md)
-->
  
