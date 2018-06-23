---
title: Ajuste de desempenho para Publicadores Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Oracle publishing [SQL Server replication], performance tuning
ms.assetid: 32c0b4ec-c166-45a3-b41e-38a30fd56813
caps.latest.revision: 33
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 523d1f40d27778b8aaa45f6b71873cf3cb69cc34
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121459"
---
# <a name="performance-tuning-for-oracle-publishers"></a>Ajuste de desempenho para Editores Oracle
  A arquitetura de publicação Oracle é semelhante à arquitetura de publicação do [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , entretanto, a primeira etapa é ajustar a replicação Oracle para requisitos de desempenho, seguindo as recomendações gerais de ajuste encontradas em [Enhance General Replication Performance](../administration/enhance-general-replication-performance.md).  
  
 Além disso há duas opções para Editores Oracle que estão relacionadas ao desempenho:  
  
-   Especificando a opção de publicação apropriada: Oracle ou Oracle Gateway.  
  
-   Configurando o trabalho de conjunto da transação para processar alterações no Publicador em um intervalo apropriado.  
  
## <a name="specifying-the-appropriate-publishing-option"></a>Especificando a opção Appropriate Publishing  
 A opção Oracle Gateway fornece desempenho melhorado em relação à opção Oracle Complete; entretanto, essa opção não pode ser usada para publicar a mesma tabela em várias publicações transacionais. Uma tabela pode aparecer no máximo em uma publicação transacional e em qualquer número de publicações de instantâneo. Se você precisa publicar a mesma tabela em várias publicações transacionais, escolha a opção Oracle Complete. Especifique essa opção ao identificar o Editor Oracle no Distribuidor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [Create a Publication from an Oracle Database](../publish/create-a-publication-from-an-oracle-database.md).  
  
## <a name="configuring-the-transaction-set-job"></a>Configurando o trabalho de conjunto da transação  
 As alterações em tabelas Oracle publicadas são processadas em grupos chamados conjuntos de transação. Para assegurar consistência transacional, cada conjunto de transação é confirmado como uma única transação no banco de dados de distribuição. Se o conjunto de transação ficar muito grande, não poderá ser processado eficazmente como uma única transação.  
  
 Por padrão, conjuntos de transação só são criados pelo Log Reader Agent. Se durante períodos da atividade de alta alteração,o Log Reader Agent não executar ou não conectar-se pelo Distribuidor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ao Editor Oracle, os conjuntos da transação podem estar muito grandes. Para evitar esse problema, certifique-se que os conjuntos da transação são criados em intervalos regulares, mesmo se o Log Reader Agent não executar ou não puder conectar-se ao Editor Oracle.  
  
 Os conjuntos de transação podem ser criados com o trabalho de Xactset (um trabalho de banco de dados Oracle instalado por replicação), que usa o mesmo mecanismo que o Log Reader Agent usa para criar conjuntos. Cada vez que o trabalho for executado, uma nova transação será criada. Na próxima vez em que o Log Reader Agent for executado, o agente processará o conjunto que foi criado. Se ainda existir alterações pendentes após todos os conjuntos de transações terem sido processados, o Log Reader Agent cria e processa um ou mais conjuntos de transações adicionais.  
  
 Para configurar o trabalho do conjunto de transações, consulte [Configurar um Publicador Oracle no trabalho do conjunto de transações &#40;programação de Transact-SQL de replicação&#41;](../administration/configure-the-transaction-set-job-for-an-oracle-publisher.md).  
  
## <a name="see-also"></a>Consulte também  
 [Configurar um Publicador Oracle](configure-an-oracle-publisher.md)   
 [Visão geral da publicação do Oracle](oracle-publishing-overview.md)  
  
  