---
title: Configuração de firewall PDW - Analytics Platform System | Microsoft Docs
description: A página firewall do SQL Server PDW Configuration Manager permite que você habilite ou desabilite as regras de firewall que permitem ou impedem o acesso a portas específicas no dispositivo Analytics Platform System.
aauthor: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 8ccfd60aee7647c2421870a09ab5fa9b2653b99d
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
ms.locfileid: "31539376"
---
# <a name="parallel-data-warehouse-firewall-configuration-in-analytics-platform-system"></a>Configuração do firewall do Data Warehouse paralela no sistema de plataforma de análise
O **Firewall** página do SQL Server PDW Configuration Manager permite que você habilite ou desabilite as regras de firewall que permitem ou impedem o acesso a portas específicas no dispositivo Analytics Platform System.  
  
## <a name="to-manage-ports-and-firewall-rules-for-appliance-nodes"></a>Gerenciar portas e regras de firewall para nós de dispositivo  
  
1.  Inicie o Gerenciador de configuração. Para obter mais informações, consulte [iniciar o Gerenciador de configuração &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md).  
  
2.  No painel esquerdo do Configuration Manager, expanda **topologia de depósito de dados paralela**e, em seguida, clique em **Firewall**.  
  
3.  Localize a regra de porta ou um firewall para atualizar a lista de configuração e, em seguida, marque ou desmarque a caixa ao lado desse item. Somente opções configuráveis pelo administrador do SQL Server PDW são mostradas nesta lista, incluindo abrindo e fechando portas no externo em nós.  
  
4.  Clique em **aplicar** para salvar suas alterações.  
  
![DWConfig Appliance PDW Firewall](./media/pdw-firewall-configuration/SQL_Server_PDW_DWConfig_ApplPDWFirewall.png "SQL_Server_PDW_DWConfig_ApplPDWFirewall")  
  
## <a name="external-ports"></a>Portas externas  
As seguintes portas estão abertas para conexões de clientes provenientes de fora do PDW.  
  
|Finalidade|N º de porta|Nós|  
|-----------|-----------|---------|  
|Acesso de cliente SQL para PDW (TDS)|17001|CTL|  
|Acesso de cliente carregador (dwloader & SSIS)|8001|CTL|  
|Acesso de área de trabalho remoto|3389|LISTA DE CERTIFICADOS CONFIÁVEIS, CMP|  
|BinaryLoaderDataChannel do SSIS|16551|CTL|  
|dwloader BinaryLoaderDataChannel|16551|CMP|  
|SSL criptografadas conexões (para comunicações internas, para acessar o Console de administração e para acessar os serviços de cluster do HDInsight)|443|Todos os nós|  
|Fluxo de controle de carregamento do SQL Server PDW - credenciais do Windows|8002|CTL|  
|Kerberos|88|AD01 e AD02,|  
|filtros|389|AD01 e AD02|  
  
## <a name="internal-ports"></a>Portas internas  
As seguintes portas são usadas pelo PDW para comunicação interna, mas não estão abertas para conexões provenientes de fora do dispositivo de PDW.  
  
|Finalidade|N º de porta|Nós|  
|-----------|-----------|---------|  
|Tráfego do canal de controle DMS|16450|LISTA DE CERTIFICADOS CONFIÁVEIS, CMP|  
|Tráfego do canal de dados DMS|16550|LISTA DE CERTIFICADOS CONFIÁVEIS, CMP|  
|Diagnósticos internos|16650|LISTA DE CERTIFICADOS CONFIÁVEIS, CMP|  
|Status de failover (DMS)|15000|LISTA DE CERTIFICADOS CONFIÁVEIS, CMP|  
|Status de failover (Engine)|15001|CMP|  
|Intervalo de portas dinâmicas de (efêmeras)|20000-65535|LISTA DE CERTIFICADOS CONFIÁVEIS, CMP|  
|Intervalos de porta do SQL Server (TDS)|1433, 1500-1508|LISTA DE CERTIFICADOS CONFIÁVEIS, CMP|  
  
> [!NOTE]  
> Criando tabelas externas ou fontes de dados externos usa a porta TCP 8020 por padrão. Essas instruções podem ser configuradas para usar outras portas em vez disso. A porta padrão Hortonworks JOB_TRACKER_LOCATION é 50300. Integração com outros sistemas e ferramentas pode exigir portas adicionais.  
  
<!-- MISSING LINKS ## See Also  
[HDInsight Firewall Configuration &#40;Analytics Platform System&#41;](hdinsight-firewall-configuration.md)  -->  
  
