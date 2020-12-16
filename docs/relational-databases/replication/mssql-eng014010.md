---
description: MSSQL_ENG014010
title: MSSQL_ENG014010 | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014010 error
ms.assetid: 6ea84f2f-e7a2-4028-9ea9-af0d2eba660e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 3b925d1a587203a5f2072e601f23fb0a14b5c115
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475797"
---
# <a name="mssql_eng014010"></a>MSSQL_ENG014010
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|14010|  
|Origem do Evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|O servidor '%s' não está definido como um servidor de assinatura.|  
  
## <a name="explanation"></a>Explicação  
 A replicação espera que todos os servidores em uma topologia sejam registrados usando o nome do computador com um nome da instância opcional (no caso de uma instância clusterizada, o nome do servidor virtual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com o nome da instância opcional). Para que a replicação funcione corretamente, o valor retornado pelo `SELECT @@SERVERNAME` para cada servidor na topologia deve corresponder ao nome do computador ou ao nome do servidor virtual com o nome da instância opcional.  
  
 Não haverá suporte para replicação se você tiver registrado qualquer uma das instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pelo endereço IP ou FQDN (nome de domínio totalmente qualificado). Se qualquer das instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiver registrada por endereço IP ou por FQDN no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] quando a replicação tiver sido configurada, esse erro poderá ocorrer.  
  
## <a name="user-action"></a>Ação do usuário  
 Certifique-se de que todas as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na topologia foram registradas corretamente. Se o nome de rede do computador e o nome da instância do SQL Server forem diferentes:  
  
-   Adicione o nome da instância do SQL Server como um nome de rede válido. Um método para definir um nome de rede alternativo é adicionar isto ao arquivo de hosts local. O arquivo de hosts local fica por padrão situado em WINDOWS\system32\drivers\etc ou WINNT\system32\drivers\etc. Para obter mais informações, consulte a documentação do Windows.  
  
     Por exemplo, se o nome do computador for comp1 e o computador possui um endereço IP 10.193.17.129, e o nome de instância for inst1/instname, adicione a entrada a seguir para os arquivos de host:  
  
     10.193.17.129 inst1  
  
-   Remova a replicação, registre cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e, depois, restabeleça a replicação. Se o valor @@SERVERNAME não estiver correto em uma instância não clusterizada, siga estas etapas:  
  
    ```  
    sp_dropserver '<old_name>', 'droplogins'  
    go  
    sp_addserver '<new_name>', 'local'  
    go  
    ```  
  
     Depois de executar o procedimento armazenado [sp_addserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md), você deverá reiniciar o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que a alteração no @@SERVERNAME entre em vigor.  
  
     Se o valor @@SERVERNAME não estiver correto em uma instância clusterizada, você deverá alterar o nome usando o Administrador de Cluster. Para obter mais informações, consulte [Instâncias do cluster de failover do AlwaysOn &#40;SQL Server&#41;](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).  
  
## <a name="see-also"></a>Consulte Também  
 [@@SERVERNAME &#40;Transact-SQL&#41;](../../t-sql/functions/servername-transact-sql.md)   
 [Referência de erros e eventos &#40;Replicação&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
