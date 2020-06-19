---
title: Sobre o acesso de conexão de cliente a réplicas de disponibilidade (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], readable secondary replicas
- active secondary replicas [SQL Server], read-only access to
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], client connectivity
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: 29027e46-43e4-4b45-b650-c4cdeacdf552
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: bc978cd0280c9885fe7d4d4b499d01adc8f540cb
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84937267"
---
# <a name="about-client-connection-access-to-availability-replicas-sql-server"></a>Sobre Acesso de conexão de cliente a réplicas de disponibilidade (SQL Server)
  Em um grupo de disponibilidade AlwaysOn, você pode configurar uma ou mais réplicas de disponibilidade para permitir conexões somente leitura quando elas estiverem sendo executadas na função secundária (ou seja, executando como uma réplica secundária). Você também pode configurar cada réplica de disponibilidade para permitir ou excluir conexões somente leitura quando ela estiver sendo executada na função primária (ou seja, em execução como uma réplica primária).  
  
 Para facilitar o acesso de clientes aos bancos de dados primário ou secundário de um determinado grupo de disponibilidade, você deve definir um ouvinte de grupo de disponibilidade. Por padrão, o ouvinte do grupo de disponibilidade direciona as conexões de entrada para a réplica primária. No entanto, você pode configurar um grupo de disponibilidade para suportar o roteamento somente leitura que permite que seu ouvinte de grupo de disponibilidade redirecione as solicitações de conexão de aplicativos de tentativa de leitura a uma réplica secundária legível. Para obter informações, veja [Configurar o roteamento somente leitura para um grupo de disponibilidade &#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md).  
  
 Durante um failover, uma réplica secundária faz a transição para a função primária e a réplica primária antiga faz a transição para a réplica secundária. Durante o processo de failover, todas as conexões de cliente com a réplica primária e as réplicas secundárias são terminadas. Após o failover, quando um cliente se reconecta ao ouvinte de grupo de disponibilidade, o ouvinte reconecta o cliente à nova réplica primária, com exceção de uma solicitação conexão de tentativa de leitura. Se o roteamento somente leitura estiver configurado nas instâncias de cliente e de servidor que hospedam a nova réplica primária e pelo menos em uma réplica secundária legível, as solicitações de conexão de tentativa de leitura serão redirecionadas a uma réplica secundária com suporte para o tipo de acesso de conexão exigido pelo cliente. Para garantir uma experiência de cliente amigável depois de um failover, é importante configurar o acesso de conexão para as funções secundárias e primária de cada réplica de disponibilidade.  
  
> [!NOTE]  
>  Para obter informações sobre o ouvinte do grupo de disponibilidade, que manipula as solicitações de conexão do cliente, consulte [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativo &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md).  
  
 **Neste tópico:**  
  
-   [Tipos de acesso de conexão com suporte da função secundária](#ConnectAccessForSecondary)  
  
-   [Tipos de acesso de conexão com suporte da função primária](#ConnectAccessForPrimary)  
  
-   [Como a configuração de acesso de conectividade afeta a conectividade de clientes](#HowConnectionAccessAffectsConnectivity)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
-   [Conteúdo relacionado](#RelatedContent)  
  
##  <a name="types-of-connection-access-supported-by-the-secondary-role"></a><a name="ConnectAccessForSecondary"></a>Tipos de acesso de conexão com suporte da função secundária  
 A função secundária dá suporte a três alternativas para conexões de cliente, da seguinte maneira:  
  
 Nenhuma conexão  
 Nenhuma conexão de usuário é permitida. Os bancos de dados secundários não estão disponíveis para acesso de leitura. Esse é o comportamento padrão na função secundária.  
  
 Conexões somente de intenção de leitura  
 Os bancos de dados secundários estão disponíveis somente para conexão para a qual a `Application Intent` propriedade de conexão está definida como `ReadOnly` (conexões de*intenção de leitura*).  
  
 Para obter mais informações sobre essa propriedade de conexão, consulte [Suporte do SQL Server Native Client à alta disponibilidade e recuperação de desastre](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).  
  
 Permitir qualquer conexão somente leitura  
 Todos os bancos de dados secundários estão disponíveis para conexões de acesso de leitura. Essa opção permite a conexão de clientes com versão inferior.  
  
 Para obter mais informações, consulte [Configurar o acesso somente leitura em uma réplica de disponibilidade &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md).  
  
##  <a name="types-of-connection-access-supported-by-the-primary-role"></a><a name="ConnectAccessForPrimary"></a>Tipos de acesso de conexão com suporte da função primária  
 A função primária dá suporte a duas alternativas para conexões de cliente, da seguinte maneira:  
  
 Todas as conexões são permitidas  
 As conexões de leitura/gravação e somente leitura são permitidas nos bancos de dados primários. Esse é o comportamento padrão para a função primária.  
  
 Permitir apenas conexões de leitura/gravação  
 Quando a `Application Intent` propriedade de conexão é definida como **ReadWrite** ou não está definida, a conexão é permitida. Conexões para as quais a `Application Intent` palavra-chave da cadeia de conexão está definida `ReadOnly` não são permitidas. Permitir apenas conexões de leitura/gravação pode ajudar a impedir que os clientes conectem uma carga de trabalho de intenção de leitura à réplica primária por engano.  
  
 Para obter mais informações sobre essa propriedade de conexão, consulte [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Para obter mais informações, consulte [Configurar o acesso somente leitura em uma réplica de disponibilidade &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md).  
  
##  <a name="how-the-connection-access-configuration-affects-client-connectivity"></a><a name="HowConnectionAccessAffectsConnectivity"></a>Como a configuração de acesso de conexão afeta a conectividade do cliente  
 As configurações de acesso de conexão de uma réplica determinam se uma tentativa de conexão é reprovada ou tem êxito. A tabela a seguir resume quando uma determinada tentativa de conexão é reprovada ou tem êxito para cada configuração de acesso de conexão.  
  
|Função da Réplica|Acesso de conexão com suporte na réplica|Tentativa de conexão|Resultado da tentativa de conexão|  
|------------------|--------------------------------------------|-----------------------|--------------------------------|  
|Secundário|Todos|Intenção de leitura, leitura/gravação ou nenhuma intenção de conexão especificada|Sucesso|  
|Secundário|Nenhum (este é o comportamento padrão da função secundária).|Intenção de leitura, leitura/gravação ou nenhuma intenção de conexão especificada|Falha|  
|Secundário|Tentativa de leitura somente|Intenção de leitura|Sucesso|  
|Secundário|Tentativa de leitura somente|Intenção de leitura/gravação ou nenhuma intenção de conexão especificada|Falha|  
|Primário|Tudo (esse é o comportamento padrão da função primária).|Intenção de somente leitura, leitura/gravação ou nenhuma intenção de conexão especificada|Sucesso|  
|Primário|Leitura-gravação|Tentativa de leitura somente|Falha|  
|Primário|Leitura-gravação|Intenção de leitura/gravação ou nenhuma intenção de conexão especificada|Sucesso|  
  
 Para obter informações sobre como configurar um grupo de disponibilidade para aceitar conexões de cliente às suas réplicas, consulte [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativo &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md).  
  
### <a name="example-connection-access-configuration"></a>Exemplo de configuração de acesso de conexão  
 Dependendo de como as diferentes réplicas de disponibilidade são configuradas para acesso de conexão, o suporte para conexões de clientes pode ser alterado depois que um grupo de disponibilidade sofre failover. Por exemplo, considere um grupo de disponibilidade para o qual o relatório é executado em réplicas secundárias de confirmação assíncrona remotas. Todos os aplicativos somente leitura dos bancos de dados deste grupo de disponibilidade definem a propriedade de conexão `Application Intent` como `ReadOnly`, de forma que todas as conexões somente leitura são conexões de intenção de leitura.  
  
 Este grupo de disponibilidade de exemplo possui duas réplicas da confirmação síncrona no centro de computação principal e duas réplicas da confirmação assíncrona em um site de satélite. Para a função primária, todas as réplicas são configuradas para acesso de leitura/gravação, o que impede conexões de intenção de leitura com a réplica primária em todas as situações. A função secundária de confirmação síncrona usa a configuração de acesso de conexão padrão ("nenhuma"), que impede todas as conexões de cliente sob a função secundária.  Em comparação, as réplicas de confirmação assíncronas são configuradas para permitir conexões de intenção de leitura sob a função secundária. A tabela a seguir resume essa configuração de exemplo:  
  
|Réplica|Modo de confirmação|Função inicial|Acesso de conexão para a função secundária|Acesso de conexão para a função primária|  
|-------------|-----------------|------------------|------------------------------------------|----------------------------------------|  
|Replica1|Síncrona|Primário|Nenhum|Leitura-gravação|  
|Replica2|Síncrona|Secundário|Nenhum|Leitura-gravação|  
|Replica3|Assíncrona|Secundário|Somente tentativa de leitura|Leitura-gravação|  
|Replica4|Assíncrona|Secundário|Tentativa de leitura somente|Leitura-gravação|  
  
 Normalmente, neste cenário de exemplo, os failovers ocorrem apenas entre as réplicas de confirmação síncrona e imediatamente após o failover, os aplicativos de tentativa de leitura podem se reconectar a uma das réplicas secundárias de confirmação assíncrona. No entanto, quando ocorre um desastre no centro de computação principal, as duas réplicas de confirmação síncrona são perdidas. O administrador de banco de dados no site de satélite responde executando um failover manual forçado em uma réplica secundária da confirmação assíncrona. Os bancos de dados secundários na réplica secundária restante são suspensos pelo failover forçado, tornando-os indisponíveis para cargas de trabalho somente leitura. A nova réplica primária, que está configurada para conexões de leitura/gravação, impede que a carga de trabalho de intenção de leitura erudita compita com a carga de trabalho de leitura/gravação. Isso significa que, até que o administrador de banco de dados retome os bancos de dados secundários na réplica secundária restante de confirmação assíncrona, os clientes com intenção de leitura não podem se conectar a qualquer réplica de disponibilidade.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Configurar o acesso somente leitura em uma réplica de disponibilidade &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Configurar o roteamento somente leitura para um grupo de disponibilidade &#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [Monitorar grupos de disponibilidade &#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md)  
  
-   [Exibir as propriedades da réplica de disponibilidade &#40;SQL Server&#41;](view-availability-replica-properties-sql-server.md)  
  
-   [Usar a caixa de diálogo Novo Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [Guia de soluções AlwaysOn do Microsoft SQL Server para alta disponibilidade e recuperação de desastre](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [Blog da equipe do AlwaysOn do SQL Server: blog oficial da equipe do SQL Server AlwaysOn](https://blogs.msdn.com/b/sqlalwayson/)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativo &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [Estatísticas](../../../relational-databases/statistics/statistics.md)  
  
  
