---
title: FILESTREAM e FileTable com Grupos de Disponibilidade AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FileTables [SQL Server], Availability Groups
- FILESTREAM [SQL Server], Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: fdceda9a-a9db-4d1d-8745-345992164a98
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: cdd5119460d5b982c30c3e04e924e9a6b501f559
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="filestream-and-filetable-with-always-on-availability-groups-sql-server"></a>FILESTREAM e FileTable com grupos de disponibilidade AlwaysOn (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico contém informações sobre como o usar os recursos FILESTREAM e FileTable com o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
 Todas as funcionalidades FILESTREAM têm suporte. Depois de um failover, os dados de FILESTREAM podem ser acessados em ambas as réplicas secundárias legíveis e no novo primário.  
  
 A funcionalidade FileTable tem suporte parcial. Depois de um failover, os dados de FileTable estarão acessíveis na réplica primária, mas os dados de FileTable não estarão acessíveis em réplicas secundárias legíveis.  
  
 **Neste tópico:**  
  
-   [Pré-requisitos](#Prerequisites)  
  
-   [Usando VNNs (nomes de rede virtual) para acesso FILESTREAM e FileTable](#vnn)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
-   [Conteúdo relacionado](#RelatedContent)  
  
##  <a name="Prerequisites"></a> Pré-requisitos  
  
-   Antes de adicionar um banco de dados que usa FILESTREAM, com ou sem FileTable, a um grupo de disponibilidade, verifique se o FILESTREAM está habilitado em toda instância de servidor que hospeda uma réplica de disponibilidade do grupo de disponibilidade. Para obter mais informações, consulte [Enable and Configure FILESTREAM](../../../relational-databases/blob/enable-and-configure-filestream.md).  
  
##  <a name="vnn"></a> Usando VNNs (nomes de rede virtual) para acesso FILESTREAM e FileTable  
 Ao habilitar o FILESTREAM em uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], um compartilhamento de nível de instância é criado para fornecer acesso aos dados FILESTREAM. Você acessa esse compartilhamento usando o nome do computador no seguinte formato:  
  
 `\\<computer_name>\<filestream_share_name>`  
  
 Em um grupo de disponibilidade AlwaysOn, porém, o nome do computador é virtualizado usando um nome de rede virtual ou VNN. Quando o computador for a réplica primária em um grupo de disponibilidade, e os bancos de dados do grupo de disponibilidade contiverem dados FILESTREAM, um compartilhamento de escopo definido por VNN também será criado para fornecer acesso aos dados FILESTREAM. Isso não afeta o acesso do Transact-SQL aos dados FILESTREAM. No entanto, os aplicativos que usam as APIs do sistema de arquivos têm de usar o compartilhamento de escopo definido por VNN, que tem um caminho no seguinte formato:  
  
 `\\<VNN>\<filestream_share_name>`  
  
 Esse compartilhamento de escopo definido por VNN é criado quando ocorre um dos eventos a seguir.  
  
-   Você adiciona um banco de dados que contém dados FILESTREAM a um grupo de disponibilidade AlwaysOn na réplica primária. Nesse caso, o compartilhamento `\\<computer_name>\<filestream_share_name>` já existe. O compartilhamento `\\<VNN>\<filestream_share_name>` será criado.  
  
-   Você habilita o FILESTREAM para acesso de transmissão de E/S de arquivos em uma réplica primária com grupos de disponibilidade. Os seguintes compartilhamentos serão criados:  
  
    1.  `\\<computer_name>\<filestream_share_name>`  
  
    2.  `\\<VNN1>\<filestream_share_name>` para o grupo de disponibilidade 1.  
  
    3.  `\\<VNN2>\<filestream_share_name>` para o grupo de disponibilidade 2.  
  
 Esses compartilhamentos de escopo definido por VNN também serão propagados para todas as réplicas secundárias.  
  
 Quando o banco de dados que contém dados FILESTREAM ou FileTable pertence a um grupo de disponibilidade AlwaysOn:  
  
-   As funções FILESTREAM e FileTable aceitam ou retornam VNNs (nomes de rede virtual) em vez de nomes de computadores. Para obter mais informações sobre essas funções, veja [Funções Filestream e FileTable &#40;Transact-SQL&#41;](../../../relational-databases/system-functions/filestream-and-filetable-functions-transact-sql.md).  
  
-   Todo o acesso aos dados FILESTREAM ou FileTable pelas APIs do sistema de arquivos deve usar VNNs em vez de nomes de computadores.  
  
 Se seu aplicativo tentar acessar o compartilhamento usando o nome do computador no formato `\\<computer_name>\<filestream_share_name>` quando o banco de dados fizer parte de um grupo de disponibilidade, ocorrerá um erro.  
  
 Se seu aplicativo tentar acessar o compartilhamento usando o caminho de escopo definido por VNN quando o banco de dados não fizer parte de um grupo de disponibilidade, a solicitação poderá ser bem-sucedida. Nesse caso, o nome de rede virtual será resolvido como nome do computador. No entanto, esse uso não é recomendado, pois o caminho de escopo definido por VNN deixará de funcionar se o grupo de disponibilidade for descartado.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Enable and Configure FILESTREAM](../../../relational-databases/blob/enable-and-configure-filestream.md)  
  
-   [Habilitar os pré-requisitos para FileTable](../../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)  
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
 Nenhum.  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  

