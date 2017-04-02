---
title: "Modificar o pool de contas de usu&#225;rio para o SQL Server R Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 58b79170-5731-46b5-af8c-21164d28f3b0
caps.latest.revision: 19
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# Modificar o pool de contas de usu&#225;rio para o SQL Server R Services
  Como parte do processo de instalação para [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], um novo Windows *pool da conta de usuário* é criado para oferecer suporte à execução de tarefas pelo [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] service. O objetivo dessas contas de trabalho é isolar a execução simultânea de Scripts de R por diferentes usuários SQL.
  
  O número de contas de usuário nesse pool determina quantas sessões de R podem estar ativas simultaneamente.   Se o mesmo usuário executa vários scripts de R simultaneamente, todas as sessões executadas pelo usuário usará a mesma conta de trabalho. Como conseqüência, um único usuário pode ter 100 scripts de R diferentes em execução simultaneamente, desde que permitem recursos.

## Configuração padrão   
-   Em uma instância padrão, o nome do grupo é **SQLRUserGroup**. 
-   Em uma instância nomeada, o nome do grupo padrão é sufixado com o nome da instância: por exemplo, **SQLRUserGroupMyInstanceName**. 
-   Contas: Por padrão, o pool de conta de usuário contém 20 contas de usuário, denominadas **MSSQLSERVER01** por meio de **MSSQLSERVER20** para a instância padrão.  
-   Para uma instância nomeada, as contas de usuário são nomeadas usando o nome da instância: por exemplo, **MyInstanceName01** por meio de **MyInstanceName20**.  


## Gerenciando o grupo de usuários para cada instância
O grupo de conta do Windows é criado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalação para cada instância em que R Services está instalado, então se você tiver instalado várias instâncias que dão suporte a R, haverá vários grupos de usuários.
No entanto, cada grupo de usuários está associado com o [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] de serviço em uma instância específica e não oferece suporte a trabalhos em R que são executados em outras instâncias.

Por padrão, o grupo não **não** ter permissões de logon a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância à qual ele está associado. Se for necessário para habilitar a execução de scripts de R pelos usuários, o administrador de banco de dados deve fornecer esse grupo com **se conectem** permissões.  

### Alterando o número de contas de trabalho no grupo de usuário do Windows

Para modificar o número de usuários no pool de conta, você deve editar as propriedades do [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] de serviço conforme descrito abaixo.  
  
As senhas associadas a cada conta de usuário são geradas aleatoriamente, mas você pode alterá-las posteriormente, depois que as contas são criadas.  
  
1. Abra o SQL Server Configuration Manager e selecione **SQL Server Services**.
2. Clique duas vezes o serviço Launchpad do SQL Server e interromper o serviço se ele está em execução. 
3.  Sobre o **Service** guia, certifique-se de que o modo de inicialização está definido como automático. Scripts de R falhará se a barra inicial não está em execução.
4.  Clique o **Avançado** guia e editar o valor de **contagem de usuários externos** se necessário. Essa configuração controla quantos usuários diferentes do SQL pode executar consultas simultaneamente em R. O padrão é 20 contas, que na maioria dos casos é mais do que adequado para oferecer suporte a sessões de R.
5. Opcionalmente, você pode definir a opção **Redefinir a senha de usuários externos** para _Sim_ se sua organização tiver uma diretiva que exija a alteração de senhas a cada 90 dias. Isso regenerará as senhas criptografadas que mantém a barra inicial para as contas de usuário.    
6.  Reinicie o serviço.  

## Permissões adicionais necessárias para a execução de Script remoto
Se você executar scripts R com o computador do SQL Server como um remoto computação contexto, esse grupo de trabalho precisa de permissão para fazer logon na instância do SQL Server onde R scripts serão executados.

Para obter mais informações, consulte [Perguntas freqüentes sobre a atualização e instalação](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md). 

  
## Consulte também  
 [Configuração (SQL Server R Services)](../../advanced-analytics/r-services/configuration-sql-server-r-services.md)
  