---
title: MSSQLSERVER_1418 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1418 (Database Engine error)
ms.assetid: 6e9c7241-0201-44e0-9f8b-b3c4e293f0f6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c8f238589f0f9b6641095a4ccb65a4665300a28b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68023169"
---
# <a name="mssqlserver1418"></a>MSSQLSERVER_1418
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|1418|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBM_PARTNERNOTFOUND|  
|Texto da mensagem|O endereço de rede do servidor "%.*ls" não pode ser acessado ou não existe. Verifique o nome do endereço de rede e se as portas de pontos de extremidade local e remoto estão em operação.|  
  
## <a name="explanation"></a>Explicação  
Os pontos de extremidade de rede do servidor não responderam porque o endereço especificado de rede do servidor não pode ser acessado ou não existe.  
  
> [!NOTE]  
> Por padrão, o sistema operacional [!INCLUDE[msCoName](../../includes/msconame-md.md)] bloqueia todas as portas.  
  
## <a name="user-action"></a>Ação do usuário  
Verifique o nome de endereço de rede e envie o comando novamente.  
  
A ação corretiva pode ser necessária em ambos os parceiros. Por exemplo, se essa mensagem for gerada quando você estiver tentando executar SET PARTNER na instância do servidor principal, a mensagem poderá indicar que você precisa apenas realizar a ação corretiva na instância do servidor espelho. Contudo, ações corretivas podem ser necessárias em ambos os parceiros.  
  
### <a name="additional-corrective-actions"></a>Ações corretivas adicionais  
  
-   Verifique se o banco de dados espelho está pronto para espelhamento.  
  
-   Verifique se o nome e a porta da instância do servidor espelho estão corretos.  
  
-   Verifique se a instância do servidor espelho de destino não está protegida por um firewall.  
  
-   Verifique se a instância do servidor principal não está protegida por um firewall.  
  
-   Verifique se os pontos de extremidade são iniciados nos parceiros usando a coluna **state** ou **state_desc** da exibição do catálogo **sys.database_mirroring_endpoints**. Se algum ponto de extremidade não foi iniciado, execute uma instrução ALTER ENDPOINT para iniciá-lo.  
  
-   Verifique se a instância do servidor principal está escutando na porta atribuída a seu ponto de extremidade de espelhamento de banco de dados e se a instância do servidor de espelho está escutando em sua porta. Para obter mais informações, consulte "Verificando a disponibilidade da porta", posteriormente neste tópico. Se um parceiro não estiver escutando em sua porta designada, modifique o ponto de extremidade de espelhamento de banco de dados para escutar em uma porta diferente.  
  
    > [!IMPORTANT]  
    > A segurança configurada incorretamente pode causar uma mensagem de erro de configuração geral. Normalmente, a instância do servidor descarta a solicitação incorreta de conexão sem responder. Para o chamador, um erro de configuração de segurança pode ocorrer por diversos motivos, como banco de dados espelho em um estado ruim ou inexistente, permissões incorretas e assim por diante.  
  
### <a name="using-the-error-log-file-for-diagnosis"></a>Usando o arquivo de log de erros para diagnóstico  
Em alguns casos, os arquivos de log de erros estão disponíveis para investigação. Nesses casos, determine se o log de erros contém a mensagem de erro 26023 para a porta TCP do ponto de extremidade de espelhamento de banco de dados. Esse erro, de severidade 16, pode indicar que o ponto de extremidade de espelhamento de banco de dados não foi iniciado. Essa mensagem pode ocorrer mesmo que o **sys.database_mirroring_endpoints** mostre o estado do ponto de extremidade como iniciado.  
  
Depois de resolver os problemas encontrados, execute novamente a instrução SET PARTNER do ALTER DATABASE *database_name* no servidor de entidade.  
  
### <a name="verifying-port-availability"></a>Verificando a disponibilidade da porta  
Quando estiver configurando a rede para uma sessão de espelhamento de banco de dados, verifique se o ponto de extremidade de espelhamento de banco de dados de cada instância do servidor é usado apenas pelo processo de espelhamento de banco de dados. Se outro processo estiver escutando na porta atribuída a um ponto de extremidade de espelhamento de banco de dados, os processos de espelhamento de banco de dados das outras instâncias de servidor não poderão se conectar ao ponto de extremidade.  
  
Para exibir todas as portas escutadas por um servidor baseado no Windows, use o utilitário de prompt de comando **netstat**. A sintaxe de **netstat** depende da versão do sistema operacional Windows. Para obter mais informações, consulte a documentação do sistema operacional.  
  
#### <a name="windows-server-2003-service-pack-1-sp1"></a>Windows Server 2003 Service Pack 1 (SP1)  
Para listar as portas de escuta e os processos que abriram essas portas, insira o seguinte comando no prompt de comando do Windows:  
  
**netstat -abn**  
  
#### <a name="windows-server-2003-pre-sp1"></a>Windows Server 2003 (pre-SP1)  
Para identificar as portas de escuta e os processos que abriram essas portas, siga estas etapas:  
  
1.  Obtenha a ID do processo.  
  
    Para saber a ID do processo de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], conecte-se àquela instância e use a seguinte instrução do [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
    ```  
    SELECT SERVERPROPERTY('ProcessID')   
    ```  
  
    Para obter mais informações, consulte "SERVERPROPERTY (Transact-SQL)" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Faça a correspondência da ID do processo à saída do seguinte comando **netstat**:  
  
    **netstat -ano**  
  
## <a name="see-also"></a>Consulte Também  
[ALTER ENDPOINT &#40;Transact-SQL&#41;](~/t-sql/statements/alter-endpoint-transact-sql.md)  
[O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](~/database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
[Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](~/database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)  
[SERVERPROPERTY &#40;Transact-SQL&#41;](~/t-sql/functions/serverproperty-transact-sql.md)  
[Especificar um endereço de rede do servidor &#40;espelhamento de banco de dados&#41;](~/database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)  
[sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)  
[Solução de problemas de configuração de espelhamento de banco de dados &#40;SQL Server&#41;](~/database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)  
  
