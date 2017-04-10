---
title: "Gerenciando e monitorando solu&#231;&#245;es R | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "06/24/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d455f22a-190f-4a28-9088-98a843cd5db2
caps.latest.revision: 15
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 15
---
# Gerenciando e monitorando solu&#231;&#245;es R
  Os administradores de banco de dados devem integrar projetos e prioridades concorrentes em um único ponto de contato: o servidor de banco de dados. Eles devem fornecer acesso aos dados não apenas aos cientistas de dados, mas a vários desenvolvedores de relatório, analistas de negócios e consumidores de dados comerciais, mantendo a integridade dos repositórios de dados operacionais e de relatórios. Na empresa, o DBA é uma parte fundamental da criação e implantação de uma infraestrutura eficiente para ciência de dados. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] fornece muitos benefícios para o administrador de banco de dados que oferece suporte à função de ciência de dados.  
  
-   **Segurança.** A arquitetura do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] protege seus bancos de dados e isola a execução de sessões de R da operação da instância do banco de dados.  
  
     Você pode especificar quem tem permissão para executar os scripts R e certificar-se de que os dados usados em trabalhos de R sejam gerenciados com as mesmas funções de segurança definidas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Confiabilidade.** Sessões de R são executadas em um processo separado a fim de garantir que o servidor continue a executar como de costume, mesmo que a sessão de R encontre problemas. Contas de usuário físico de baixo privilégio são usadas para conter e isolar instâncias de R.   
  
-   **Administração do recursos.** Você pode controlar a quantidade de recursos alocados ao tempo de execução de R, para evitar que cálculos muito intensos prejudiquem o desempenho geral do servidor.  
  
  
## Nesta seção  
 [Monitorar os serviços de R](../../advanced-analytics/r-services/monitoring-r-services.md)
 
 [Governança de recursos para serviços de R](../../advanced-analytics/r-services/resource-governance-for-r-services.md)
 
[Instalar e gerenciar pacotes de R](../../advanced-analytics/r-services/installing-and-managing-r-packages.md)
  
[Configuração](../../advanced-analytics/r-services/configuration-sql-server-r-services.md) 

+ [Configurar e gerenciar Extensões de Análise Avançada](../../advanced-analytics/r-services/configure-and-manage-advanced-analytics-extensions.md)  
  
+  [Modificar o pool de contas de usuário para o SQL Server R Services](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)  

 [Considerações sobre segurança para o tempo de execução de R no SQL Server](../../advanced-analytics/r-services/security-considerations-for-the-r-runtime-in-sql-server.md)  
  
 
  
## Consulte também  
 [Recursos e tarefas do SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)  
  
  