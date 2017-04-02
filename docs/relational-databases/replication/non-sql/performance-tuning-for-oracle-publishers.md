---
title: "Ajuste de desempenho para Editores Oracle | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "publicação Oracle [replicação do SQL Server], ajuste de desempenho"
ms.assetid: 32c0b4ec-c166-45a3-b41e-38a30fd56813
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# Ajuste de desempenho para Editores Oracle
  Arquitetura de publicação é semelhante ao Oracle o [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] publicação arquitetura; portanto, a primeira etapa na replicação do Oracle para desempenho de ajuste requer seguir as recomendações de ajuste gerais encontrado no [melhorar o desempenho geral de replicação](../../../relational-databases/replication/administration/enhance-general-replication-performance.md).  
  
 Além disso há duas opções para Editores Oracle que estão relacionadas ao desempenho:  
  
-   Especificando a opção de publicação apropriada: Oracle ou Oracle Gateway.  
  
-   Configurando o trabalho de conjunto da transação para processar alterações no Publicador em um intervalo apropriado.  
  
## Especificando a opção Appropriate Publishing  
 A opção Oracle Gateway fornece desempenho melhorado em relação à opção Oracle Complete; entretanto, essa opção não pode ser usada para publicar a mesma tabela em várias publicações transacionais. Uma tabela pode aparecer no máximo em uma publicação transacional e em qualquer número de publicações de instantâneo. Se você precisa publicar a mesma tabela em várias publicações transacionais, escolha a opção Oracle Complete. Especifique essa opção ao identificar o Editor Oracle no Distribuidor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [Create a Publication from an Oracle Database](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md).  
  
## Configurando o trabalho de conjunto da transação  
 As alterações em tabelas Oracle publicadas são processadas em grupos chamados conjuntos de transação. Para assegurar consistência transacional, cada conjunto de transação é confirmado como uma única transação no banco de dados de distribuição. Se o conjunto de transação ficar muito grande, não poderá ser processado eficazmente como uma única transação.  
  
 Por padrão, conjuntos de transação só são criados pelo Log Reader Agent. Se durante períodos da atividade de alta alteração,o Log Reader Agent não executar ou não conectar-se pelo Distribuidor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ao Editor Oracle, os conjuntos da transação podem estar muito grandes. Para evitar esse problema, certifique-se que os conjuntos da transação são criados em intervalos regulares, mesmo se o Log Reader Agent não executar ou não puder conectar-se ao Editor Oracle.  
  
 Os conjuntos de transação podem ser criados com o trabalho de Xactset (um trabalho de banco de dados Oracle instalado por replicação), que usa o mesmo mecanismo que o Log Reader Agent usa para criar conjuntos. Cada vez que o trabalho for executado, uma nova transação será criada. Na próxima vez em que o Log Reader Agent for executado, o agente processará o conjunto que foi criado. Se ainda existir alterações pendentes após todos os conjuntos de transações terem sido processados, o Log Reader Agent cria e processa um ou mais conjuntos de transações adicionais.  
  
 Para configurar o trabalho de conjunto de transação, consulte [Configurar o trabalho de conjunto de transação para um editor Oracle e 40; Programação Transact-SQL de replicação e 41;](../../../relational-databases/replication/administration/configure the transaction set job for an oracle publisher.md).  
  
## Consulte também  
 [Configurar um publicador Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Visão geral da Publicação Oracle](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  