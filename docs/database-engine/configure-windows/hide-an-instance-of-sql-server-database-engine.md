---
title: Ocultar uma instância do Mecanismo de Banco de Dados do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 08/19/2015
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], hiding instances
- hiding instances of Database Engine
ms.assetid: 392de21a-57fa-4a69-8237-ced8ca86ed1d
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 5401e5b731f09de89dedeef8308b7118299fbc9b
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66785271"
---
# <a name="hide-an-instance-of-sql-server-database-engine"></a>Ocultar uma instância do Mecanismo de Banco de Dados do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como ocultar uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o SQL Server Configuration Manager. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa o serviço de navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para enumerar instâncias do [!INCLUDE[ssDE](../../includes/ssde-md.md)] instaladas no computador. Isso permite que aplicativos cliente naveguem por um servidor e ajuda os clientes a distinguirem entre várias instâncias do [!INCLUDE[ssDE](../../includes/ssde-md.md)] no mesmo computador. Você pode usar o procedimento a seguir para evitar que o serviço SQL Server Browser exponha uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] a computadores cliente que tentam localizar a instância usando o botão **Procurar** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Configuration Manager  
  
#### <a name="to-hide-an-instance-of-the-sql-server-database-engine"></a>Ocultar uma instância do Mecanismo de Banco de Dados do SQL Server  
  
1.  No **SQL Server Configuration Manager**, expanda **Configuração de Rede do SQL Server**, clique com o botão direito do mouse em **Protocolos de** *\<server instance>* e, depois, selecione **Propriedades**.  
  
2.  Na guia **Sinalizadores** , na caixa **Ocultar Instância** , selecione **Sim**e clique em **OK** para fechar a caixa de diálogo. A alteração entra em vigor imediatamente para conexões novas.  
  
## <a name="remarks"></a>Remarks  
 Se você ocultar uma instância nomeada, terá de fornecer o número da porta na cadeia de conexão para se conectar à instância oculta, mesmo se o navegador estiver em execução. Recomendamos que use uma porta estática em vez de uma porta dinâmica para a instância oculta nomeada.  
  Para obter mais informações, veja [Configurar um servidor para escuta em uma porta TCP específica &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md).  
  
### <a name="clustering"></a>Clustering  
 Se você ocultar uma instância nomeada clusterizada, o serviço de cluster poderá não se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Isso fará com que a verificação da instância de cluster **IsAlive** falhe e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ficará offline. É recomendável que você crie um alias em todos os nós da instância clusterizada para refletir a porta estática configurada para a instância.  
 Para obter mais informações, consulte [Criar ou excluir um alias de servidor para ser usado por um cliente &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md).  
  
 Se você ocultar uma instância nomeada clusterizada, o serviço de cluster poderá não se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se a chave do Registro **LastConnect** (**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SNI11.0\LastConnect**) tiver uma porta diferente da porta de escuta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se o serviço de cluster não puder fazer uma conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você poderá ver um erro semelhante ao seguinte:  
**ID do evento: 1001: Nome do evento: Deadlock de recursos de clustering de failover.**  
  
## <a name="see-also"></a>Consulte Também  
 [Configuração de rede do servidor](../../database-engine/configure-windows/server-network-configuration.md)   
 [Descrição das conexões de cliente do Servidor Virtual SQL](https://support.microsoft.com/kb/273673)   
 [Como atribuir uma porta estática a uma instância nomeada do SQL Server – e evitar uma armadilha comum](https://blogs.msdn.com/b/arvindsh/archive/2012/09/08/how-to-assign-a-static-port-to-a-sql-server-named-instance-and-avoid-a-common-pitfall.aspx)  
  
  
