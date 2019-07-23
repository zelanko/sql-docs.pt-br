---
title: Mapear portas TCP/IP para nós NUMA (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- NUMA
- memory [SQL Server], NUMA
- affinity NUMA
- ports [SQL Server], working with NUMA
- CPU [SQL Server], NUMA support
- NUMA, How to map a port to a NUMA node
- NUMA affinity
- TCP/IP [SQL Server], NUMA support
- non-uniform memory access
ms.assetid: 07727642-0266-4cbc-8c55-3c367e4458ca
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 48c645bd85034f226650cf5e98ddd18a6b8efa9e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67997978"
---
# <a name="map-tcp-ip-ports-to-numa-nodes-sql-server"></a>Mapear portas TCP/IP para nós NUMA (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como mapear portas TCP/IP para nós NUMA (acesso não uniforme a memória) usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager. Na inicialização, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] grava as informações de nó no log de erros.  
  
 Para determinar o número de nó do nó que você quer usar, leia as informações do nó de log de erros ou da exibição **sys.dm_os_schedulers** . Para definir um endereço de TCP/IP e portar para nós únicos ou múltiplos, acrescente um bitmap de identificação de nó (uma máscara de afinidade) em parênteses depois do número da porta. Podem ser especificados nós em formato decimal ou hexadecimal. Para criar o bitmap, primeiro numere os nós da direita para a esquerda iniciando com zero, como em 76543210. Crie uma representação binária da lista de nós, provendo 1 para os nós que você quer usar e 0 para os nós que você não quer usar. Por exemplo, para usar nós NUMA 0, 2 e 5, especifique 00100101.  
  
|||  
|-|-|  
|Número de nó NUMA|76543210|  
|Mascare 0, 2 e 5 contando da direita|00100101|  
  
 Converta a representação binária (00100101) em `[37]`decimal, ou `[0x25]`hexadecimal. Para escutar em todos os nós, não forneça nenhum identificador de nó.  
  
 Se uma porta for mapeada para mais de um nó NUMA, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atribuirá conexões para nós numa forma de rodízio sem tentar equilibrar carga pelos nós.  
  
> [!NOTE]  
>  Para habilitar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para escutar várias portas TCP para cada endereço IP, consulte [Configurar o Mecanismo de Banco de Dados para escutar em várias portas TCP](../../database-engine/configure-windows/configure-the-database-engine-to-listen-on-multiple-tcp-ports.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Configuration Manager  
  
#### <a name="to-map-a-tcpip-port-to-a-numa-node"></a>Para mapear uma porta de TCP/IP para um nó NUMA  
  
1.  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, expanda **Configuração de Rede do SQL Server** e, depois, clique em **Protocolos de** *\<instance name>* .  
  
2.  No painel de detalhes, clique duas vezes no **TCP/IP**.  
  
3.  Na guia **IP Addresses** , na seção que corresponde ao endereço de IP para configurar, na caixa **TCP Port** , adicione o identificador do nó NUMA em parênteses depois do número da porta. Por exemplo, para TCP porta 1500 e nós 0, 2 e 5, use **1500 [37]** ou **1500 [0x25]** .  
  
## <a name="see-also"></a>Consulte Também  
 [Soft-NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)  
  
  
