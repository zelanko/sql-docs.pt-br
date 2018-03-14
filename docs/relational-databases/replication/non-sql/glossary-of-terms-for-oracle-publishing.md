---
title: "Glossário de termos para publicações Oracle | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Oracle publishing [SQL Server replication], glossary
ms.assetid: e21dfa4b-6144-4be7-9cbf-ca2709b2bd9f
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 89626fd3666456bb8770eb07d1767be749032722
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2018
---
# <a name="glossary-of-terms-for-oracle-publishing"></a>Glossário de termos para publicações Oracle
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Você deve estar familiarizado com os seguintes termos da Oracle ao configurar e administrar publicações Oracle. Para uma lista completa de termos da Oracle, consulte a documentação online da Oracle.  
  
 Tabelas organizadas por índice (IOT)  
 Uma tabela cujos dados estão classificados fisicamente em disco por ordem de índice; é semelhante a uma tabela com índice clusterizado do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Uma IOT é reproduzida a um Assinante como uma tabela com um índice cluster.  
  
 Instância  
 Um banco de dados Oracle é associado a uma instância. A instância inclui os processos de memória e plano de fundo que fornecem suporte ao banco de dados. Uma instância Oracle sempre mapeia em um único banco de dados, enquanto uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pode conter muitos bancos de dados. Há circunstâncias nas quais um banco de dados Oracle pode ter várias instâncias.  
  
 Ouvinte Oracle  
 Gerencia o tráfego de entrada de rede para uma instância de banco de dados Oracle. Ao configurar a conectividade da rede de um banco de dados Oracle, você especifica o protocolo por meio do qual o tráfego é enviado e a porta pela qual o Ouvinte ouve o tráfego. O Ouvinte é geralmente configurado para ser executado no mesmo computador da instância de banco de dados Oracle e pode ser configurado para servir a uma ou mais instâncias.  
  
 ROWID  
 Um ponteiro para a localização de uma linha específica em um banco de dados. Como é mais rápido recuperar linhas usando o ROWID do que usando um exame da tabela ou um índice, a replicação usa o ROWID temporariamente ao processar as alterações a tabelas publicadas.  
  
 Sequência  
 Um objeto de banco de dados usado para gerar números exclusivos. A replicação usa sequências para ordenar alterações feitas a tabelas publicadas.  
  
 SQL\*Plus  
 Um aplicativo usado para acessar e consultar bancos de dados Oracle. É semelhante ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **sqlcmd**.  
  
 Sinônimo  
 Um alias para um objeto. O sinônimo público especial **MSSQLSERVERDISTRIBUTOR** é criado automaticamente quando um Editor Oracle é configurado. O sinônimo usa como referência a tabela **HREPL_Distributor** e fornece um ponteiro lógico ao Distribuidor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que serve ao Editor.  
  
 Após publicar um banco de dados Oracle, as tentativas subsequentes para configurar seu Editor para usar um outro Distribuidor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] apresentarão falha, pois esse sinônimo público identifica o Distribuidor específico já configurado para servir ao Editor.  
  
 Espaço de tabela  
 Uma unidade de armazenamento de banco de dados que é aproximadamente equivalente a um grupo de arquivos no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Nome do serviço TNS  
 O TNS (Substrato Transparente de Rede) é uma camada de comunicação usada pelos bancos de dados Oracle. O nome de serviço do TNS é o nome pelo qual uma instância do banco de dados Oracle é identificada em uma rede. Você atribui um nome de serviço ao TNS quando for configurar a conectividade do banco de dados Oracle. A replicação usa o nome de serviço do TNS para identificar o Editor e estabelecer conexões.  
  
 Esquema de usuário  
 Um esquema de usuário pode ser considerado como um usuário de banco de dados que possui um conjunto particular de objetos de banco de dados. O esquema do usuário administrativo da replicação possui todos os objetos criados pelo processo de replicação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no banco de dados Oracle, exceto o sinônimo público **MSSQLSERVERDISTRIBUTOR** .  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar um Publicador Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Objetos criados no Publicador Oracle](../../../relational-databases/replication/non-sql/objects-created-on-the-oracle-publisher.md)   
 [Publicadores não SQL Server](../../../relational-databases/replication/non-sql/non-sql-server-publishers.md)   
 [Oracle Publishing Overview](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
