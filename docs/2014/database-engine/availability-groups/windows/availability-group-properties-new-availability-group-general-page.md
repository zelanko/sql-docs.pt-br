---
title: Propriedades do grupo de disponibilidade e novo grupo de disponibilidade (página Geral) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroupproperties.general.f1
ms.assetid: 9af5379f-91b8-4729-9f75-4a80242a30e9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 248ffe57906052c0d7dafcd187bb1b2b34cd6e64
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62815649"
---
# <a name="availability-group-properties-and-new-availability-group-general-page"></a>Propriedades do Grupo de Disponibilidade e Novo Grupo de Disponibilidade (página geral)
   Este tópico se aplica à guia **Geral** da caixa de diálogo **Novo Grupo de Disponibilidade** e da caixa de diálogo **Propriedades do Grupo de Disponibilidade**.  A caixa de diálogo **Novo Grupo de Disponibilidade** permite criar um novo grupo de disponibilidade sem usar o [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)]. A caixa de diálogo **Propriedades do Grupo de Disponibilidade** permite exibir e alterar a configuração de um grupo de disponibilidade existente.  
  
 **Para exibir as propriedades do grupo de disponibilidade**  
  
-   [Exibir as propriedades do grupo de disponibilidade &#40;SQL Server&#41;](view-availability-group-properties-sql-server.md)  
  
-   [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Nome do grupo de disponibilidade**  
 O nome do grupo de disponibilidade. Esse é um nome especificado pelo usuário que deve ser exclusivo no WSFC (Windows Server Failover Cluster).  
  
## <a name="availability-databases"></a>Bancos de dados de disponibilidade  
 **Nome do banco de dados**  
 O nome de um banco de dados que foi adicionado ao grupo de disponibilidade.  
  
 **Adicionar**  
 Clique para adicionar um banco de dados ao grupo de disponibilidade.  
  
 **Remover**  
 Clique para remover um banco de dados selecionado do grupo de disponibilidade.  
  
## <a name="availability-replicas"></a>Réplicas de Disponibilidade  
 **Instância do servidor**  
 O nome de servidor da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda essa réplica e, para uma instância não padrão, seu nome de instância.  
  
 **Função**  
 **Primary**  
 Atualmente a réplica primária.  
  
 **Secundário**  
 Atualmente uma réplica secundária.  
  
 **Resolvendo**  
 Atualmente, a função de réplica está no processo de ser resolvida para a função primária ou secundária.  
  
 **Modo de disponibilidade**  
 O modo de disponibilidade da réplica. Pode ser:  
  
 **Confirmação assíncrona**  
 A réplica primária pode confirmar transações sem esperar que a réplica secundária grave o log no disco.  
  
 **Confirmação síncrona**  
 A réplica primária espera para confirmar uma determinada transação até que a réplica secundária tenha gravado a transação em disco.  
  
 Para obter mais informações, consulte [modos de disponibilidade (grupos de disponibilidade AlwaysOn)](availability-modes-always-on-availability-groups.md).  
  
 **Modo de Failover**  
 O modo de failover da réplica, um dos seguintes:  
  
 **Automático**  
 Failover automático. A réplica é um destino para failovers automáticos. Essa opção terá suporte apenas se o modo de disponibilidade estiver definido como confirmação síncrona.  
  
 **Manual**  
 Failover manual. O failover da réplica pode ser feito apenas manualmente pelo administrador do banco de dados.  
  
 **Conexões na função primária**  
 O tipo de conexões de cliente com suporte quando a réplica possui a função primária.  
  
 **Permitir todas as conexões**  
 Todas as conexões são permitidas com os bancos de dados na réplica primária. Essa é a configuração padrão.  
  
 **Permitir conexões de leitura/gravação**  
 Conexões em que a propriedade de conexão da tentativa de aplicativo está definida como **ReadOnly** não são permitidas. Quando a propriedade de tentativa de aplicativo é definida como **ReadWrite** ou a propriedade de conexão de tentativa de aplicativo não está definida, a conexão é permitida. Para obter mais informações sobre a propriedade de conexão Tentativa de Aplicativo, consulte [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 **Secundário legível**  
 Se uma réplica de disponibilidade que está executando a função primária (isto é, está atuando como uma réplica secundária) pode aceitar conexões de clientes, um dos seguintes:  
  
 **Não**  
 Nenhuma conexão direta é permitida para bancos de dados secundários desta réplica. Eles não estão disponíveis para acesso de leitura. Essa é a configuração padrão.  
  
 **Tentativa de leitura somente**  
 Somente conexões diretas somente leitura são permitidas para bancos de dados secundários desta réplica. Os bancos de dados secundários estão disponíveis para acesso de leitura.  
  
 **Sim**  
 Todas as conexões são permitidas para os bancos de dados secundários desta réplica, mas somente para acesso de leitura. Os bancos de dados secundários estão disponíveis para acesso de leitura.  
  
 **Tempo limite da sessão (segundos)**  
 O número de segundos do período de tempo limite de sessão nesta réplica.  
  
 **URL do Ponto de Extremidade**  
 A URL do ponto de extremidade. Para obter informações sobre o formato dessas URLs, veja [Especificar a URL do ponto de extremidade ao adicionar ou modificar uma réplica de disponibilidade &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md).  
  
 **Adicionar**  
 Clique para adicionar uma réplica secundária ao grupo de disponibilidade.  
  
 **Remover**  
 Clique para remover uma réplica secundária especificada do grupo de disponibilidade.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  
