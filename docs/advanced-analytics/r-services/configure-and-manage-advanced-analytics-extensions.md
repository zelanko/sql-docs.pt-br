---
title: "Configurar e gerenciar Extens&#245;es de An&#225;lise Avan&#231;ada | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "11/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8d73fd98-0c61-4a62-94bb-75658195f2a6
caps.latest.revision: 21
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 20
---
# Configurar e gerenciar Extens&#245;es de An&#225;lise Avan&#231;ada
  Depois de ter instalado o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], você poderá fazer pequenas alterações na configuração do tempo de execução R e outros serviços associados ao [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] .  
  
  
 **Neste tópico**  
  
-   [Provisionando contas de usuário para SQL Server R Services](#bkmk_Provisioning)  
  
-   [Gerenciando o uso de memória por processos de R](#bkmk_ManagingMemory)  
  
-   [Alterando os padrões de serviço usando o arquivo de configuração](#bkmk_ChangingConfig) 

-   [Modificando a conta de serviço Launchpad](#bkmk_Launchpad) 
  
##  <a name="bkmk_Provisioning"></a> Provisionando contas de usuário para SQL Server R Services  
 Tempo de execução de R processa em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executados no contexto de contas de usuário locais com poucos privilégios. A execução de processos de tempo de execução de R em contas individuais de poucos privilégios tem os seguintes benefícios:  
  
-   Reduzir os privilégios dos processos de tempo de execução de R em execução no computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
  
-   Fornecer isolamento entre as sessões de tempo de execução de R  
  
 Como parte do processo de instalação em [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], um novo Windows *pool da conta de usuário* é criado que contém as contas de usuário local necessárias para executar o processo de tempo de execução de R. Você pode modificar o número de usuários se necessário para dar suporte a R. O administrador de banco de dados também deve fornecer a esse grupo permissão para se conectar a qualquer instância em que os serviços de R foi habilitado. Para obter mais informações, consulte [modifique o Pool de conta de usuário para serviços do SQL Server R](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md).  
  
 No entanto, uma lista de controle de acesso (ACL) pode ser definida para recursos confidenciais sobre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para negar acesso a esse grupo para evitar que o processo de tempo de execução de R obtenham acesso aos recursos.  
  
-   O pool de conta de usuário está vinculado a uma instância específica.  Para cada instância em que R script foi habilitado, um pool separado de trabalho contas são criadas. Contas não podem ser compartilhadas entre instâncias.
  
-   Nomes de conta de usuário no pool estão no formato SQLInstanceName*nn*. Por exemplo, se você estiver usando a instância padrão de seu servidor R, o pool de contas de usuário oferece suporte a nomes de conta como MSSQLSERVER01, MSSQLSERVER02 e assim por diante.  
  
-   O tamanho do pool de conta de usuário é estático e o valor padrão é 20. O número de sessões de tempo de execução de R que podem ser iniciadas simultaneamente é limitado pelo tamanho desse pool de conta de usuário. No entanto, esse limite pode ser alterado por um administrador usando o SQL Server Configuration Manager.  
  
  
 Para saber mais sobre como fazer alterações para o pool de contas de usuário, veja [Modify the User Account Pool for SQL Server R Services](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md).  
  
##  <a name="bkmk_ManagingMemory"></a> Gerenciando o uso de memória por processos de R  
 Por padrão, os processos de tempo de execução de R associados a [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] está limitado a usar não mais do que 20% da memória total do computador. No entanto, esse limite pode ser aumentado pelo administrador, se isso for necessário.  
  
 Geralmente, esse valor será inadequado para tarefas de R grave como modelo de treinamento ou prever em várias linhas de dados. Talvez você precise reduzir a quantidade de memória reservada para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (ou para outros serviços) e usar o Resource Governor para definir um pool de recursos externos ou pools e alocar. Para obter mais informações, consulte [governança de recursos para serviços de R](../../advanced-analytics/r-services/resource-governance-for-r-services.md).  
  
##  <a name="bkmk_ChangingConfig"></a> Alterar opções de serviço avançadas usando o arquivo de configuração  
 
Você pode controlar algumas propriedades avançadas do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] editando o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] arquivo de configuração. Esse arquivo é criado durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e por padrão é salvo como um arquivo de texto sem formatação no seguinte local:  
 
```  
<instance path>\binn\rlauncher.config  
```  
  
 Você deve ser um administrador no computador que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para fazer alterações nesse arquivo. Se você editar o arquivo, é recomendável que você faça uma cópia de backup antes de salvar as alterações.  
  
 Por exemplo, para usar o Bloco de Notas para abrir o arquivo de configuração para a instância padrão (MSSQLSERVER), abra um prompt de comando como administrador e digite o seguinte comando:  
  
```  
C:\>Notepad.exe "%programfiles%\Microsoft SQL Server\MSSQL13.MSSQLSERVER\mssql\binn\rlauncher.config"  
  
```  
  
###  <a name="bkmk_properties"></a> Propriedades de configuração  
 Todas as configurações assumem a forma de um par chave-valor, com cada configuração em uma linha separada. Por exemplo, esta propriedade especifica que no máximo 20 por cento da memória do sistema pode ser usada pelos processos do R:  
  
 Padrão: `MEMORY_LIMIT_PERCENT=20`  
  
 A tabela a seguir lista cada uma das configurações com suporte para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], com os valores permitidos.  
  
|Nome da configuração|Tipo de valor|Default|Descrição|  
|------------------|----------------|-------------|-----------------|  
|JOB_CLEANUP_ON_EXIT|Integer<br /><br /> 0 = Desabilitado<br /><br /> 1 = Habilitado|1<br /><br /> Arquivos de log são removidos ao sair|Especifica se a pasta de trabalho temporária criada para cada sessão R deve ser limpa após a sessão de R. Essa configuração é útil para depuração.<br /><br /> Observação: Esta é uma configuração interna apenas, não altere esse valor.|  
|TRACE_LEVEL|Integer<br /><br /> 1 = Erro<br /><br /> 2 = desempenho<br /><br /> 3 = Aviso<br /><br /> 4 = informações|1<br /><br /> Somente os avisos de saída|Configura o nível de detalhamento do rastreamento do iniciador do R (MSSQLLAUNCHPAD) para fins de depuração. Esta configuração afeta o detalhamento dos rastreamentos armazenados nos seguintes arquivos de rastreamento, que estão localizados no caminho especificado pela configuração LOG_DIRECTORY:<br /><br /> **rlauncher.log**: O arquivo de rastreamento gerado para sessões de R iniciadas por consultas do T-SQL.<br /><br /> Para obter mais informações sobre esse cenário, consulte [Data Exploration and Predictive Modeling with R](../../advanced-analytics/r-services/data-exploration-and-predictive-modeling-with-r.md).|  

## <a name="bkmk_Launchpad"></a>Modificando a conta de serviço Launchpad

Um separado [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] serviço é criado para cada instância em que você configurou [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]. 

Por padrão, a barra inicial é configurada para ser executado usando a conta NT Service\MSSQLLaunchpad, que é configurado com todas as permissões necessárias para executar scripts R. No entanto, se você alterar essa conta, a barra inicial não poderá iniciar ou acessar a instância do SQL Server onde os scripts R devem ser executados.
 
  Se você modificar a conta de serviço, certifique-se de usar o **política de segurança Local** aplicativo e atualizar as permissões em cada serviço de conta para incluir essas permissões:
  + Ajustar cotas de memória para um processo (SeIncreaseQuotaPrivilege)
  + Ignorar verificação completa (SeChangeNotifyPrivilege)
  + Fazer logon como um serviço (SeServiceLogonRight)
  + Substituir um token de nível de processo (SeAssignPrimaryTokenPrivilege)

Para obter mais informações sobre permissões necessárias para executar serviços do SQL Server, consulte [Configurar contas de serviço do Windows e permissões](https://msdn.microsoft.com/library/ms143504.aspx#Windows).
   
## Consulte também  
 [Introdução ao SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
  
  