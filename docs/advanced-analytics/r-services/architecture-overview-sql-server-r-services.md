---
title: "Vis&#227;o geral da arquitetura (SQL Server R Services) | Microsoft Docs"
ms.custom: ""
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6c4a4f66-ea3e-4a73-acf2-6c8aeafc94b0
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 9
---
# Vis&#227;o geral da arquitetura (SQL Server R Services)
Esta seção fornece uma visão geral da arquitetura do [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], incluindo segurança, novos componentes adicionados no mecanismo de banco de dados do SQL Server para componentes de suporte a R e interoperabilidade de scripts de código-fonte aberto R em execução no SQL Server.


## Metas


A arquitetura do [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] é projetado para oferecer suporte a linguagem de código-fonte aberto R. Os usuários atuais do R devem ser capazes de portar seu código R e executá-lo em T-SQL com relativamente pequenas modificações.

No entanto, o SQL Server R Services também oferece inovações que fornecem maior desempenho e integração mais próxima do banco de dados para a linguagem R, para permitir a transferência de dados e processamento mais rápido e para reduzir as barreiras para o desenvolvimento de empresa de soluções de R. Essas inovações incluem o código-fonte aberto e proprietários componentes desenvolvidos pela Microsoft.


São os objetivos principais da integração com o SQL Server fornecer melhor desempenho e escalabilidade para R, enquanto o gerenciamento de dados com segurança. Para esse objetivo, serviços do SQL Server R fornece uma infra-estrutura de vários processo que oferece suporte à autenticação integrada do Windows e logons do SQL com base em senha. 

+ [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] Fornece uma distribuição de base de R, junto com os pacotes ScaleR e a capacidade de executar tarefas de R em paralelo.
+ Novos componentes do SQL Server fornecem uma estrutura segura e de alto desempenho para a execução de scripts externos.
+ Executarem tarefas de R fora do processo do SQL Server, para fornecer segurança e maior capacidade de gerenciamento.
+ [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] gerencia a segurança de todos os processos de R. 

Para ajudá-lo a otimizar o código R existente e tirar proveito desses aprimoramentos, os tópicos desta seção descrevem a nova arquitetura em detalhes. Sobre como o processamento de dados e análise é tratada pelo [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], você pode fazer escolhas apropriadas sobre como realizar a ingestão de dados, a forma mais eficiente executar engenharia de recursos e como consumir os resultados.
 

## Nesta seção
+ [Interoperabilidade de R](../../advanced-analytics/r-services/r-interoperability-in-sql-server-r-services.md)
+ [Novos componentes do SQL Server para serviços de R](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r-services.md)
+ [Visão geral de segurança](../../advanced-analytics/r-services/security-overview-sql-server-r-services.md)

## Consulte também
[Tutoriais de serviços de R](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)
