---
title: "Considera&#231;&#245;es sobre seguran&#231;a para o tempo de execu&#231;&#227;o de R no SQL Server | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "04/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d5065197-69e6-4fce-9654-00acaecc148b
caps.latest.revision: 15
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 15
---
# Considera&#231;&#245;es sobre seguran&#231;a para o tempo de execu&#231;&#227;o de R no SQL Server
  Este tópico fornece uma visão geral das considerações de segurança para trabalhar com [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] em [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Para obter mais informações sobre como gerenciar o serviço e sobre como provisionar as contas de usuário usadas para executar scripts R, consulte [Configurar e gerenciar extensões de análise avançada](../../advanced-analytics/r-services/configure-and-manage-advanced-analytics-extensions.md).  
  
## Usar o firewall para restringir o acesso à rede por R  
 No método de instalação sugerido, uma regra de Firewall do Windows é usada para bloquear todo o acesso à rede de saída dos processos de tempo de execução de R. Regras de firewall devem ser criadas para impedir que o processo de tempo de execução de R baixe pacotes ou faça outras chamadas de rede que podem ser potencialmente mal-intencionados.  
  
 É altamente recomendável que você ativa o Firewall do Windows (ou outro firewall de sua escolha) para bloquear o acesso à rede pelo tempo de execução de R.  
  
 Se você estiver usando um programa de firewall diferente, também pode criar regras para bloquear conexões de rede de saída para o tempo de execução de R, definindo regras para as contas de usuário local ou para o grupo representado pelo pool de contas de usuário.   
Para saber mais, confira [Configure and Manage Advanced Analytics Extensions](../../advanced-analytics/r-services/configure-and-manage-advanced-analytics-extensions.md).  
  
## Métodos de autenticação com suporte para contextos de computação remota 
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] agora oferece suporte a logons de autenticação integrada do Windows e SQL ao criar conexões entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e um cliente de ciência de dados remotos. 
  
 Por exemplo, se você estiver desenvolvendo uma solução de R em seu laptop e executar cálculos no computador do SQL Server, você precisará criar uma fonte de dados do SQL Server no R, usando o **rx** funções e definindo uma cadeia de conexão com base em suas credenciais do Windows. Quando você altera o _computação contexto_ do seu laptop para o computador do SQL Server, se sua conta do Windows tem as permissões necessárias, todo o código R será executado no computador do SQL Server. Além disso, todas as consultas SQL executadas como parte do código R serão executadas com suas credenciais também. 
 
 Embora um logon do SQL também pode ser usado na cadeia de conexão para uma fonte de dados do SQL Server, o uso de um logon requer que a instância do SQL Server permitir autenticação de modo misto.
 
 ### Autenticação implícita
  
 Em geral o [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] inicia o tempo de execução de R e executa scripts R em sua própria conta. No entanto, se o script R faz uma chamada ODBC, o [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] representará as credenciais do usuário que enviou o comando para garantir que a chamada ODBC não falhe. Isso é chamado de *autenticação implícita*. 
 
 > [!IMPORTANT] 
 >
 > Para a autenticação seja bem-sucedida, o grupo de usuários do Windows que contém as contas de trabalho implícita (por padrão, **SQLRUser**) deve ter uma conta no banco de dados mestre para a instância e esta conta devem receber permissões para se conectar à instância.  
  
## Não há suporte para criptografia em repouso  
 Não há suporte para o Transparent Data Encryption para dados enviados ou recebidos do tempo de execução de R. Como conseqüência, a criptografia em repouso **não** ser aplicado a todos os dados que você usar scripts de R, todos os dados salvos em disco ou persistentes resultados intermediários.  
 
 ## Consulte também
 [Insira aqui a descrição do link](../../advanced-analytics/r-services/configuration-sql-server-r-services.md) 
  