---
title: Monitorar com o SCOM
description: Use o System Center Operations Manager (SCOM) para monitorar o dispositivo de sistema de plataforma de análise (APS).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 0b244d85e601e46fe778298e723c0a7d01e669bb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74400976"
---
# <a name="monitor-with-system-center-operations-manager---analytics-platform-system"></a>Monitorar com o sistema de plataforma System Center Operations Manager-Analytics
Use o System Center Operations Manager (SCOM) para monitorar o dispositivo de sistema de plataforma de análise (APS).
  
## <a name="before-you-begin"></a>Antes de começar  
  
### <a name="prerequisites"></a>Pré-requisitos  
  
1.  System Center Operations Manager 2007 R2, 2012 ou 2012 SP1 devem estar instalados e em execução.  
  
2.  SQL Server 2008 R2 Native Client ou SQL Server Native Client 2012 deve estar instalado.  
  
3.  Os pacotes de gerenciamento a serem monitorados SQL Server PDW devem ser instalados, importados e configurados. Use os artigos a seguir para obter instruções sobre como executar essas tarefas.  
  
    -   [Instalar os pacotes de gerenciamento do SCOM &#40;o sistema de plataforma de análise&#41;](install-the-scom-management-packs.md)  
  
    -   [Importar o pacote de gerenciamento do SCOM para o PDW &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-pdw.md) 
    
    -   [Configurar o SCOM para monitorar o sistema de plataforma de análise &#40;Analytics Platform System&#41;](configure-scom-to-monitor-analytics-platform-system.md)
  
<!-- MISSING LINKS    -   [Import the SCOM Management Pack for HDInsight &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-hdinsight.md)  -->  
   
  
## <a name="to-monitor-sql-server-pdw-with-scom"></a>Para monitorar SQL Server PDW com o SCOM  
Depois de configurar os pacotes de gerenciamento do SCOM, clique no painel Monitoramento do SCOM e faça uma busca detalhada até **SQL Server dispositivo** e, em seguida, **Microsoft SQL Server Parallel Data Warehouse**. Sob Microsoft SQL Server Parallel Data Warehouse, há quatro opções: alertas, dispositivos, diagrama de dispositivo e nós.  
  
### <a name="alerts"></a>Alertas  
Alertas são onde você pode encontrar os alertas atuais a serem gerenciados.  
  
![Alertas](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM.png "SCOM_SCOM")  
  
### <a name="appliances"></a>Eletrodomésticos  
Os dispositivos são onde você encontrará os dispositivos SQL Server PDW atualmente descobertos e monitorados em seu ambiente. Se um dispositivo não aparecer aqui e você tiver criado a conexão ODBC para ele, pode haver algo errado com sua conta do PDWWatcher. Se eles aparecerem como "não monitorado", pode haver algo errado com sua conta do PDWMonitor. Seja paciente, pois o SCOM não faz alterações em tempo real, mas periodicamente verifica se os novos dispositivos monitoram e enviam periodicamente consultas a dispositivos para monitoramento.  
  
![Dispositivos](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM2.png "SCOM_SCOM2")  
  
### <a name="appliances-diagram"></a>Diagrama de dispositivos  
A página de diagrama de dispositivos é onde você pode dar uma olhada na integridade do seu dispositivo com um modo de exibição de árvore:  
  
![Diagrama de aplicativos](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM3.png "SCOM_SCOM3")  
  
### <a name="nodes"></a>Nós  
Por fim, a exibição nós permite que você veja a integridade do seu dispositivo por meio de cada nó:  
  
![Nós](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM4.png "SCOM_SCOM4")  
  
## <a name="see-also"></a>Consulte Também  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Noções básicas sobre alertas do console de administração &#40;Analytics Platform System&#41;](understanding-admin-console-alerts.md)  
  
