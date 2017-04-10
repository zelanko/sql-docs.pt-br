---
title: "MSSQL_ENG014117 | Microsoft Docs"
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
  - "erro MSSQL_ENG014117"
ms.assetid: e5906a76-9511-4c47-8826-8c765b58a39d
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# MSSQL_ENG014117
    
## Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|14117|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|'%s' não está configurado como um banco de dados de distribuição.|  
  
## Explicação  
 Esse erro poderá acontecer se uma ou ambas as situações forem verdadeiras:  
  
-   A entrada para o banco de dados de distribuição especificado está ausente no **msdb... MSdistributiondbs**.  
  
-   Não há uma entrada para o servidor local no **mestre** banco de dados ou a entrada está incorreto.  
  
     A replicação espera que todos os servidores em uma topologia sejam registrados usando o nome do computador com um nome da instância opcional (no caso de uma instância clusterizada, o nome do servidor virtual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com o nome da instância opcional). Para que a replicação funcione corretamente, o valor retornado pelo `SELECT @@SERVERNAME` para cada servidor na topologia deve corresponder ao nome do computador ou ao nome do servidor virtual com o nome da instância opcional.  
  
     Não haverá suporte para replicação se você tiver registrado qualquer uma das instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pelo endereço IP ou FQDN (nome de domínio totalmente qualificado). Se você tinha qualquer das instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registrada pelo endereço IP ou FQDN no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] quando configurou a replicação, esse erro pode ocorrer.  
  
## Ação do usuário  
 Certifique-se de que a instância do Distribuidor esteja corretamente registrada. Se o nome de rede do computador e o nome da instância do SQL Server forem diferentes:  
  
-   Adicione o nome da instância do SQL Server como um nome de rede válido. Um método para definir um nome de rede alternativo é adicionar isto ao arquivo de hosts local. O arquivo de hosts local fica por padrão situado em WINDOWS\system32\drivers\etc ou WINNT\system32\drivers\etc. Para obter mais informações, consulte a documentação do Windows.  
  
     Por exemplo, se o nome do computador for comp1 e o computador possui um endereço IP 10.193.17.129, e o nome de instância for inst1/instname, adicione a entrada a seguir para os arquivos de host:  
  
     10.193.17.129 inst1  
  
-   Desabilite a distribuição, registre a instância e restabeleça a distribuição. Se o valor @@SERVERNAME não estiver correto para uma instância não clusterizada, siga as seguintes etapas:  
  
    ```  
    sp_dropserver '<old_name>', 'droplogins'  
    go  
    sp_addserver '<new_name>', 'local'  
    go  
    ```  
  
     Depois de executar o [sp_addserver & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md) procedimento armazenado, você deve reiniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço para que a alteração @@SERVERNAME entrem em vigor.  
  
     Se o valor @@SERVERNAME não estiver correto para uma instância clusterizada, será necessário alterar o nome usando o Administrador de Cluster. Para obter mais informações, consulte [instâncias de Cluster de Failover do AlwaysOn & #40. SQL Server & 41;](../Topic/AlwaysOn%20Failover%20Cluster%20Instances%20\(SQL%20Server\).md).  
  
 Depois de verificar se a instância do distribuidor está registrada corretamente, verifique se o banco de dados de distribuição está listado em **msdb... MSdistributiondbs**. Se não estiver listado:  
  
1.  Gere um script para a configuração de distribuição. Para obter mais informações, consulte [Scripting Replication](../../relational-databases/replication/scripting-replication.md).  
  
2.  Desabilite a distribuição e habilite-a novamente. Para obter mais informações, consulte [Configurar distribuição](../../relational-databases/replication/configure-distribution.md).  
  
## Consulte também  
 [Erros e eventos referência & #40. Replicação e 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  