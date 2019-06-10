---
title: Especificar um endereço de rede do servidor (espelhamento de banco de dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- database mirroring [SQL Server], endpoint
- endpoints [SQL Server], database mirroring
- server network addresses [SQL Server]
ms.assetid: a64d4b6b-9016-4f1e-a310-b1df181dd0c6
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 630df054d6025d70e2dcc2b90d339d1499dbc237
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66795177"
---
# <a name="specify-a-server-network-address-database-mirroring"></a>Especificar um endereço de rede do servidor (Espelhamento de banco de dados)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A configuração de uma sessão de espelhamento de banco de dados requer um endereço de rede de servidor para cada uma das instâncias de servidor. O endereço de rede de servidor de uma instância de servidor deve identificar a instância de forma inequívoca fornecendo um endereço de sistema e número de porta na qual a instância está escutando.  
  
 Antes de você poder especificar uma porta em um endereço de rede de servidor, deve existir o ponto de extremidade do espelhamento de banco de dados na instância de servidor. Para obter mais informações, veja [Criar um ponto de extremidade de espelhamento de banco de dados para a Autenticação do Windows &#40;SQL Server&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md).  
  
  
##  <a name="Syntax"></a> Sintaxe para um endereço de rede de servidor  
 A sintaxe para um endereço de rede de servidor é do formato:  
  
 TCP<strong>://</strong> *\<system-address>* <strong>:</strong> *\<port>*  
  
 onde  
  
-   *\<system-address>* é uma cadeia de caracteres que identifica sem ambiguidade o sistema de computador de destino. Normalmente, o endereço de servidor é um nome de sistema (se os sistemas estiverem no mesmo domínio), um nome de domínio completamente qualificado ou um endereço de IP.  
  
    -   Se os sistemas estiverem no mesmo domínio, você poderá usar o nome do sistema de computador; por exemplo, `SYSTEM46`.  
  
    -   Para usar um endereço IP, ele deve ser exclusivo em seu ambiente. Recomendamos que você use um endereço IP somente se ele for estático. O endereço IP pode ser o IP Versão 4 (IPv4) ou IP Versão 6 (IPv6). Um endereço IPv6 deve estar entre colchetes. Por exemplo: **[** _<IPv6_address>_ **]** .  
  
         Para saber o endereço IP de um sistema, no prompt de comando do Windows, digite no comando **ipconfig** .  
  
    -   O nome de domínio completamente qualificado tem seu funcionamento garantido. Esta é uma cadeia de caracteres de endereço definida localmente de formatos diferentes em lugares diferentes. Frequentemente, mas não sempre, um nome de domínio completamente qualificado é um nome composto que inclui o nome do computador e uma série de segmentos de domínio separados por pontos no formato:  
  
         _computer_name_ **.** _domain_segment_[... **.** _domain_segment_]  
  
         em que *computer_name i*é o nome de rede do computador que executa a instância de servidor e *domain_segment*[... **.** _domain_segment_] são as informações restantes de domínio do servidor; por exemplo: `localinfo.corp.Adventure-Works.com`.  
  
         O conteúdo e número de segmentos de domínio são determinados dentro da companhia ou organização. Se você não conhecer o nome de domínio completamente qualificado do seu servidor, consulte seu administrador de sistema.  
  
        > [!NOTE]  
        >  Para obter informações sobre como achar um nome de domínio completamente qualificado, consulte "Encontrando o nome de domínio completamente qualificado", mais abaixo neste tópico.  
  
-   *\<port>* é o número da porta usada pelo ponto de extremidade de espelhamento da instância de servidor parceiro. Para obter informações sobre como especificar um ponto de extremidade, veja [Criar um ponto de extremidade de espelhamento de banco de dados para a Autenticação do Windows &#40;SQL Server&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md).  
  
     Um ponto de extremidade de espelhamento de banco de dados pode usar qualquer porta disponível no sistema do computador. Cada número de porta em um sistema de computador deve estar associado a somente um ponto de extremidade e cada ponto de extremidade está associado a uma única instância de servidor; e assim, diferentes instâncias de servidor no mesmo servidor escutam em diferentes pontos de extremidade com portas diferentes. Por isso, a porta que você especifica no endereço de rede de servidor quando você configura uma sessão de espelhamento de banco de dados sempre dirigirá a sessão à instância de servidor cujo ponto de extremidade está associado a essa porta.  
  
     No endereço de rede de servidor de uma instância de servidor, somente o número da porta associado a seu ponto de extremidade de espelhamento distingue essa instância de qualquer outra instância no computador. A figura a seguir ilustra os endereços de rede de servidor de duas instâncias de servidor em um único computador. A instância padrão usa a porta `7022` e a instância nomeada usa a porta `7033`. O endereço de rede de servidor para estas duas instâncias de servidor é, respectivamente: `TCP://MYSYSTEM.Adventure-works.MyDomain.com:7022` e `TCP://MYSYSTEM.Adventure-works.MyDomain.com:7033`. Note que o endereço não contém o nome da instância de servidor.  
  
     ![Endereços de rede do servidor de uma instância padrão](../../database-engine/availability-groups/windows/media/dbm-2-instances-ports-1-system.gif "Endereços de rede do servidor de uma instância padrão")  
  
     Para identificar a porta associada atualmente com o ponto de extremidade de espelhamento de banco de dados de uma instância de servidor, use a seguinte instrução do [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
    ```  
    SELECT type_desc, port FROM sys.tcp_endpoints  
    ```  
  
     Encontre a fila cujo valor **type_desc** é "DATABASE_MIRRORING" e use o número da porta correspondente.  
  
### <a name="examples"></a>Exemplos  
  
#### <a name="a-using-a-system-name"></a>A. Usando um nome de sistema  
 O endereço de rede de servidor a seguir especifica um nome de sistema, `SYSTEM46`e a porta `7022`.  
  
```  
ALTER DATABASE AdventureWorks SET PARTNER ='tcp://SYSTEM46:7022';  
```  
  
#### <a name="b-using-a-fully-qualified-domain-name"></a>B. Usando um nome de domínio completamente qualificado  
 O endereço de rede de servidor a seguir especifica um nome de domínio completamente qualificado, `DBSERVER8.manufacturing.Adventure-Works.com`e a porta `7024`.  
  
```  
ALTER DATABASE AdventureWorks SET PARTNER ='tcp://DBSERVER8.manufacturing.Adventure-Works.com:7024';  
```  
  
#### <a name="c-using-ipv4"></a>C. Usando IPv4  
 O endereço de rede de servidor a seguir especifica um endereço IPv4, `10.193.9.134`e a porta `7023`.  
  
```  
ALTER DATABASE AdventureWorks SET PARTNER ='tcp://10.193.9.134:7023';  
```  
  
#### <a name="d-using-ipv6"></a>D. Usando IPv6  
 O endereço de servidor de rede a seguir contém um endereço IPv6, `2001:4898:23:1002:20f:1fff:feff:b3a3`, e a porta `7022`.  
  
```  
ALTER DATABASE AdventureWorks SET PARTNER ='tcp://[2001:4898:23:1002:20f:1fff:feff:b3a3]:7022';  
```  
  
## <a name="finding-the-fully-qualified-domain-name"></a>B. Encontrando o nome de domínio completamente qualificado  
 Para encontrar o nome de domínio completamente qualificado de um sistema, no prompt de comando do Windows desse sistema, digite:  
  
 **IPCONFIG /ALL**  
  
 Para formar o nome de domínio totalmente qualificado, concatene os valores de *<host_name>* e *<Primary_Dns_Suffix>* da seguinte forma:  
  
 _<host_name>_ **.** _<Primary_Dns_Suffix>_  
  
 Por exemplo, a configuração IP  
  
 `Host Name  .  .  .  .  .  .  : MYSERVER`  
  
 `Primary Dns Suffix  .  .  .  : mydomain.Adventure-Works.com`  
  
 se equipara ao nome de domínio completamente qualificado a seguir:  
  
 `MYSERVER.mydomain.Adventure-Works.com`  
  
##  <a name="Examples"></a> Exemplos  
 O exemplo a seguir mostra o endereço de rede de servidor para uma instância de servidor em um sistema de computador nomeado `REMOTESYSTEM3` em outro domínio. As informações de domínio são `NORTHWEST.ADVENTURE-WORKS.COM`e a porta do ponto de extremidade de espelhamento de banco de dados é `7025`. Tendo estes exemplos de componentes determinados, o endereço de rede de servidor é.  
  
 `TCP://REMOTESYSTEM3.NORTHWEST.ADVENTURE-WORKS.COM:7025`  
  
 O exemplo a seguir exibe o endereço de rede de servidor para uma instância de servidor em um sistema de computador nomeado `DBSERVER1`. Este sistema está no domínio local e é identificado sem-ambiguidade por seu nome de sistema. A porta do ponto de extremidade de espelhamento de banco de dados é `7022`.  
  
 `TCP://DBSERVER1:7022`  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Criar um ponto de extremidade de espelhamento de banco de dados para a Autenticação do Windows &#40;SQL Server&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
  
  
