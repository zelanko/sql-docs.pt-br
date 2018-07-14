---
title: Especifique a URL de ponto de extremidade ao adicionar ou modificar uma réplica de disponibilidade (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- endpoints [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], endpoint
- Endpoint URLs (HADR)
ms.assetid: d7520c13-a8ee-4ddc-9e9a-54cd3d27ef1c
caps.latest.revision: 19
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 571ffb7537474343cd595445af77a4ecae48d3e6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37222616"
---
# <a name="specify-the-endpoint-url-when-adding-or-modifying-an-availability-replica-sql-server"></a>Especifique a URL do Ponto de Extremidade Ao Adicionar ou Modificando uma Réplica de disponibilidade (SQL Server)
  Para hospedar uma réplica de disponibilidade para um grupo de disponibilidade, uma instância de servidor deve ter um ponto de extremidade de espelhamento de banco de dados. A instância de servidor usa este ponto de extremidade para escutar mensagens de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] de réplicas de disponibilidade hospedadas por outras instâncias de servidor. Para definir uma réplica de disponibilidade para um grupo de disponibilidade, você deve especificar a URL de ponto de extremidade da instância de servidor que hospedará a réplica. A *URL de ponto de extremidade* identifica o protocolo de transporte do ponto de extremidade de espelhamento de banco de dados — TCP, o endereço do sistema da instância de servidor e o número de porta associado ao ponto de extremidade.  
  
> [!NOTE]  
>  O termo "URL de ponto de extremidade" é sinônimo do termo "endereço de rede de servidor" usado pela interface do usuário e pela documentação de espelhamento de banco de dados.  
  
-   [Sintaxe para uma URL de ponto de extremidade](#SyntaxOfURL)  
  
-   [Encontrando o nome de domínio completamente qualificado de um sistema](#Finding_FQDN)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
-   [Conteúdo relacionado](#RelatedContent)  
  
##  <a name="SyntaxOfURL"></a> Sintaxe para uma URL de ponto de extremidade  
 A sintaxe para uma URL de ponto de extremidade é do seguinte formato:  
  
 TCP**://***\<system-address>***:***\<port>*  
  
 onde  
  
-   *\<system-address>* é uma cadeia de caracteres que identifica sem ambiguidade o sistema de computador de destino. Normalmente, o endereço de servidor é um nome de sistema (se os sistemas estiverem no mesmo domínio), um nome de domínio completamente qualificado ou um endereço de IP.  
  
    -   Como os nós do cluster WSFC (Windows Server Failover Clustering) são do mesmo domínio, você pode usar o nome do sistema de computador; por exemplo, `SYSTEM46`.  
  
    -   Para usar um endereço IP, ele deve ser exclusivo em seu ambiente. Recomendamos que você use um endereço IP somente se ele for estático. O endereço IP pode ser o IP Versão 4 (IPv4) ou IP Versão 6 (IPv6). Um endereço IPv6 deve estar entre colchetes. Por exemplo: **[***<IPv6_address>***]**.  
  
         Para saber o endereço IP de um sistema, no prompt de comando do Windows, digite no comando **ipconfig** .  
  
    -   O nome de domínio completamente qualificado tem seu funcionamento garantido. Esta é uma cadeia de caracteres de endereço definida localmente de formatos diferentes em lugares diferentes. Frequentemente, mas não sempre, um nome de domínio completamente qualificado é um nome composto que inclui o nome do computador e uma série de segmentos de domínio separados por pontos no formato:  
  
         *computer_name* **.** *domain_segment*[...**.***domain_segment*]  
  
         em que *computer_name* é o nome de rede do computador que executa a instância de servidor e *domain_segment*[...**.***domain_segment*] são as informações restantes de domínio do servidor; por exemplo: `localinfo.corp.Adventure-Works.com`.  
  
         O conteúdo e número de segmentos de domínio são determinados dentro da companhia ou organização. Para obter mais informações, consulte [Encontrando o nome de domínio completamente qualificado](#Finding_FQDN), posteriormente neste tópico.  
  
-   *\<port>* é o número da porta usada pelo ponto de extremidade de espelhamento da instância de servidor parceiro.  
  
     Um ponto de extremidade de espelhamento de banco de dados pode usar qualquer porta disponível no sistema do computador. Cada número de porta deve estar associado a somente um ponto de extremidade e cada ponto de extremidade está associado a uma única instância de servidor; e assim, diferentes instâncias de servidor no mesmo servidor escutam em diferentes pontos de extremidade com portas diferentes. Por isso, a porta que você especifica na URL de ponto de extremidade quando você especifica uma réplica de disponibilidade sempre direcionará mensagens de entrada para a instância de servidor cujo ponto de extremidade está associado a essa porta.  
  
     Na URL do ponto de extremidade, somente o número da porta identifica a instância de servidor que está associada ao ponto de extremidade de espelhamento no computador de destino. A figura a seguir ilustra as URL de ponto de extremidade de duas instâncias de servidor em um único computador. A instância padrão usa a porta `7022` e a instância nomeada usa a porta `7033`. As URLs de ponto de extremidade para estas duas instâncias de servidor são, respectivamente: `TCP://MYSYSTEM.Adventure-works.MyDomain.com:7022` e `TCP://MYSYSTEM.Adventure-works.MyDomain.com:7033`. Note que o endereço não contém o nome da instância de servidor.  
  
     ![Endereços de rede do servidor de uma instância padrão](../../media/dbm-2-instances-ports-1-system.gif "Endereços de rede do servidor de uma instância padrão")  
  
     Para identificar a porta associada atualmente com o ponto de extremidade de espelhamento de banco de dados de uma instância de servidor, use a seguinte instrução do [!INCLUDE[tsql](../../../includes/tsql-md.md)] :  
  
    ```  
    SELECT type_desc, port FROM sys.TCP_endpoints  
    ```  
  
     Encontre a fila cujo valor **type_desc** é "DATABASE_MIRRORING" e use o número da porta correspondente.  
  
### <a name="examples"></a>Exemplos  
  
#### <a name="a-using-a-system-name"></a>A. Usando um nome de sistema  
 A URL de ponto de extremidade a seguir especifica um nome de sistema, `SYSTEM46`e a porta `7022`.  
  
 `TCP://SYSTEM46:7022`  
  
#### <a name="b-using-a-fully-qualified-domain-name"></a>B. Usando um nome de domínio completamente qualificado  
 A URL de ponto de extremidade a seguir especifica um nome de domínio completamente qualificado, `DBSERVER8.manufacturing.Adventure-Works.com`e a porta `7024`.  
  
 `TCP://DBSERVER8.manufacturing.Adventure-Works.com:7024`  
  
#### <a name="c-using-ipv4"></a>C. Usando IPv4  
 A URL de ponto de extremidade a seguir especifica um endereço IPv4, `10.193.9.134`e a porta `7023`.  
  
 `TCP://10.193.9.134:7023`  
  
#### <a name="d-using-ipv6"></a>D. Usando IPv6  
 A URL de ponto de extremidade a seguir contém um endereço IPv6, `2001:4898:23:1002:20f:1fff:feff:b3a3`, e a porta `7022`.  
  
 `TCP://[2001:4898:23:1002:20f:1fff:feff:b3a3]:7022`  
  
##  <a name="Finding_FQDN"></a> Encontrando o nome de domínio completamente qualificado de um sistema  
 Para encontrar o nome de domínio completamente qualificado de um sistema, no prompt de comando do Windows desse sistema, digite:  
  
 **IPCONFIG /ALL**  
  
 Para formar o nome de domínio totalmente qualificado, concatene os valores de *<host_name>* e *<Primary_Dns_Suffix>* da seguinte forma:  
  
 *<host_name>* **.** *<Primary_Dns_Suffix>*  
  
 Por exemplo, a configuração IP  
  
 `Host Name  .  .  .  .  .  .  : MYSERVER`  
  
 `Primary Dns Suffix  .  .  .  : mydomain.Adventure-Works.com`  
  
 se equipara ao nome de domínio completamente qualificado a seguir:  
  
 `MYSERVER.mydomain.Adventure-Works.com`  
  
> [!NOTE]  
>  Se você precisar de mais informações sobre um nome de domínio completamente qualificado, consulte seu administrador de sistema.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para configurar um ponto de extremidade de espelhamento de banco de dados**  
  
-   [Criar um ponto de extremidade de espelhamento para grupos de disponibilidade AlwaysOn do banco de dados &#40;SQL Server PowerShell&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Criar um ponto de extremidade de espelhamento de banco de dados para a Autenticação do Windows &#40;SQL Server&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Usar certificados para um ponto de extremidade de espelhamento de banco de dados &#40;Transact-SQL&#41;](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
    -   [Permitir que um ponto de extremidade de espelhamento de banco de dados use certificados para conexões de saída &#40;Transact-SQL&#41;](../../database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
    -   [Permitir que um ponto de extremidade de espelhamento de banco de dados use certificados para conexões de entrada &#40;Transact-SQL&#41;](../../database-mirroring/database-mirroring-use-certificates-for-inbound-connections.md)  
  
-   [Especificar um endereço de rede do servidor &#40;Espelhamento de banco de dados&#41;](../../database-mirroring/specify-a-server-network-address-database-mirroring.md)  
  
-   [Solucionar problemas de configuração de grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;excluído](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
 **Para exibir informações sobre o ponto de extremidade de espelhamento de banco de dados**  
  
-   [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)  
  
 **Para adicionar uma réplica de disponibilidade**  
  
-   [Adicionar uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Unir uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [Guia de soluções do Microsoft SQL Server AlwaysOn para alta disponibilidade e recuperação de desastres](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
## <a name="see-also"></a>Consulte também  
 [Criação e configuração de grupos de disponibilidade &#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)   
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql)  
  
  
