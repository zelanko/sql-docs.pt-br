---
title: Configuração do firewall do PDW - Analytics Platform System | Microsoft Docs
description: A página de firewall do SQL Server PDW Configuration Manager permite que você habilitar ou desabilitar regras de firewall para permitem ou impedir o acesso a portas específicas no dispositivo do Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d92d92752b4de105857f5611fbe95262476a4e13
ms.sourcegitcommit: 96090bb369ca8aba364c2e7f60b37165e5af28fc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/10/2019
ms.locfileid: "66822436"
---
# <a name="parallel-data-warehouse-firewall-configuration-in-analytics-platform-system"></a>Configuração de firewall Parallel Data Warehouse no Analytics Platform System

O **Firewall** página do SQL Server PDW Configuration Manager permite habilitar ou desabilitar regras de firewall para permitem ou impedir o acesso a portas específicas no dispositivo do Analytics Platform System.  
  
## <a name="to-manage-ports-and-firewall-rules-for-appliance-nodes"></a>Para gerenciar as portas e regras de firewall para nós de dispositivo  
  
1.  Inicie o Gerenciador de configuração. Para obter mais informações, consulte [iniciar o Configuration Manager &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md).  
  
2.  No painel esquerdo do Configuration Manager, expanda **topologia de depósito de dados paralela**e, em seguida, clique em **Firewall**.  
  
3.  Localize a regra de firewall ou de porta para atualizar a lista de configurações e, em seguida, marque ou desmarque a caixa ao lado desse item. Somente opções configuráveis pelo administrador do SQL Server PDW são mostradas nesta lista, incluindo a abertura e fechamento de portas em nós com face externa.  
  
4.  Clique em **aplicar** para salvar suas alterações.  
  
![DWConfig Appliance PDW Firewall](./media/pdw-firewall-configuration/SQL_Server_PDW_DWConfig_ApplPDWFirewall.png "SQL_Server_PDW_DWConfig_ApplPDWFirewall")  
  
## <a name="external-ports"></a>Portas externas  
As seguintes portas estão abertas para conexões de cliente provenientes de fora do PDW.  
  
|Finalidade|Porta n º|Nós|  
|-----------|-----------|---------|  
|Acesso para cliente do SQL para PDW (TDS)|17001|CTL|  
|Acesso para cliente do carregador (dwloader & SSIS)|8001|CTL|  
|Acesso de área de trabalho remoto|3389|CTL, CMP|  
|SSIS BinaryLoaderDataChannel|16551|CTL|  
|dwloader BinaryLoaderDataChannel|16551|CMP|  
|SSL criptografado conexões (para comunicações internas, para acessar o Console de administração)|443|Todos os nós|  
|Fluxo de controle de carregamento do SQL Server PDW - credenciais do Windows|8002|CTL|  
|_Kerberos|88|AD01 e AD02,|  
|_ldap|389|AD01 e AD02|  
| &nbsp; | &nbsp; | &nbsp; |
  
## <a name="internal-ports"></a>Portas internas  
As seguintes portas são usadas pelo PDW para a comunicação interna, mas não estiverem abertas para conexões provenientes de fora o dispositivo de PDW.  
  
|Finalidade|Porta n º|Nós|  
|-----------|-----------|---------|  
|Tráfego de canal de controle DMS|16450|CTL, CMP|  
|Tráfego de canal de dados DMS|16550|CTL, CMP|  
|Diagnósticos internos|16650|CTL, CMP|  
|Status do failover (DMS)|15000|CTL, CMP|  
|Status do failover (mecanismo de)|15001|CMP|  
|Intervalo de portas dinâmicas de (efêmero)|20000-65535|CTL, CMP|  
|Intervalos de porta do SQL Server (TDS)|1433, 1500-1508|CTL, CMP|  
| &nbsp; | &nbsp; | &nbsp; |
  
> [!NOTE]  
> Criando tabelas externas ou fontes de dados externa usa a porta TCP 8020 por padrão. Essas instruções podem ser configuradas para usar outras portas em vez disso. A porta padrão Hortonworks JOB_TRACKER_LOCATION é 50300. A integração com outros sistemas e ferramentas pode exigir portas adicionais.  
  
<!-- MISSING LINKS ## See Also  
[HDInsight Firewall Configuration &#40;Analytics Platform System&#41;](hdinsight-firewall-configuration.md)
-->
  
