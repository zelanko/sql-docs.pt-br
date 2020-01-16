---
title: Criar um ponto de extremidade do espelhamento de banco de dados (Transact-SQL)
description: Use o Transact-SQL para criar um ponto de extremidade de espelhamento de banco de dados usando a Autenticação do Windows.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- database mirroring [SQL Server], endpoint
- endpoints [SQL Server], database mirroring
- Windows authentication [SQL Server]
- database mirroring [SQL Server], security
ms.assetid: baf1a4b1-6790-4275-b261-490bca33bdb9
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 11b3c1d06c74f8d5c19aa95ba8de20fbce67d3dd
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75259040"
---
# <a name="create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql"></a>Criar um ponto de extremidade de espelhamento de banco de dados para a Autenticação do Windows (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como criar um ponto de extremidade de espelhamento de banco de dados que usa a Autenticação do Windows no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para oferecer suporte ao espelhamento de banco de dados ou ao [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] , cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exige um ponto de extremidade de espelhamento de banco de dados. Uma instância do servidor só pode ter em um ponto de extremidade do espelhamento de banco de dados, que tem uma porta única. Um ponto de extremidade do espelhamento de banco de dados poderá usar qualquer porta que estiver disponível no sistema local quando o ponto de extremidade for criado. Todas as sessões de espelhamento de banco de dados em uma instância do servidor escutam aquela porta e todas as conexões que chegam para o espelhamento de banco de dados usam aquela porta.  
  
> [!IMPORTANT]  
>  Se um ponto de extremidade do espelhamento de banco de dados existe e já está em uso, é recomendável usar esse ponto de extremidade. O descarte de um ponto de extremidade em uso interrompe sessões existentes.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  [Segurança](#Security)  
  
-   **Para criar um ponto de extremidade de espelhamento de banco de dados usando:**  [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
 Os métodos de autenticação e de criptografia da instância do servidor são estabelecidos pelo administrador do sistema.  
  
> [!IMPORTANT]  
>  O algoritmo RC4 é preterido. [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Recomendamos usar AES.  
  
####  <a name="Permissions"></a> Permissões  
 Exige a permissão CREATE ENDPOINT ou a associação na função de servidor fixa sysadmin. Para obter mais informações, consulte [Permissões GRANT do ponto de extremidade &#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md).  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-create-a-database-mirroring-endpoint-that-uses-windows-authentication"></a>Para criar um ponto de extremidade do espelhamento de banco de dados que usa a Autenticação do Windows  
  
1.  Conecte-se à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na qual você deseja criar um ponto de extremidade do espelhamento de banco de dados.  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Determine se um ponto de extremidade de espelhamento de banco de dados já existe usando a seguinte instrução:  
  
    ```  
    SELECT name, role_desc, state_desc FROM sys.database_mirroring_endpoints;   
    ```  
  
    > [!IMPORTANT]  
    >  Se um ponto de extremidade do espelhamento de banco de dados já existir para a instância do servidor, use aquele ponto de extremidade para qualquer outra sessão que você estabelecer na instância do servidor.  
  
4.  Para usar o Transact-SQL para criar um ponto de extremidade para ser usado com a Autenticação do Windows, use uma instrução CREATE ENDPOINT. A instrução leva o seguinte formato geral:  
  
     CREATE ENDPOINT *\<endpointName>*  
  
     STATE=STARTED  
  
     AS TCP ( LISTENER_PORT = *\<listenerPortList>* )  
  
     FOR DATABASE_MIRRORING  
  
     (  
  
     [ AUTHENTICATION = **WINDOWS** [ *\<authorizationMethod>* ]  
  
     ]  
  
     [ [ **,** ] ENCRYPTION = **REQUIRED**  
  
     [ ALGORITHM { *\<algorithm>* } ]  
  
     ]  
  
     [ **,** ] ROLE = *\<role>*  
  
     )  
  
     onde  
  
    -   *\<endpointName>* é um nome exclusivo do ponto de extremidade de espelhamento de banco de dados da instância de servidor.  
  
    -   STARTED especifica que o ponto de extremidade deve ser iniciado e começar a escutar conexões. Um ponto de extremidade do espelhamento de banco de dados é normalmente criado no estado STARTED. Alternativamente, você pode iniciar uma sessão em um estado STOPPED (o padrão) ou no estado DISABLED.  
  
    -   *\<listenerPortList>* é um único número de porta (*nnnn*) no qual você deseja que o servidor escute mensagens de espelhamento de banco de dados. Só o TCP é permitido; se qualquer outro protocolo for especificado causará um erro.  
  
         Um número de porta só pode ser usado uma vez por um sistema de computador. Um ponto de extremidade do espelhamento de banco de dados poderá usar qualquer porta que estiver disponível no sistema local quando o ponto de extremidade for criado. Para identificar as portas que estão sendo usadas atualmente pelos pontos de extremidade de TCP no sistema, use a seguinte instrução Transact-SQL:  
  
        ```  
        SELECT name, port FROM sys.tcp_endpoints;  
        ```  
  
        > [!IMPORTANT]  
        >  Cada instância do servidor requer uma e apenas uma porta do ouvinte exclusiva.  
  
    -   Para a Autenticação do Windows, a opção AUTHENTICATION é opcional, a menos que você deseje que o ponto de extremidade use apenas NTLM ou Kerberos para autenticar conexões. *\<authorizationMethod>* especifica o método usado para autenticar conexões como um dos seguintes: NTLM, KERBEROS ou NEGOTIATE. O padrão, NEGOTIATE, faz o ponto de extremidade usar o protocolo de negociação Windows para escolher NTLM ou Kerberos. A negociação habilita conexões com ou sem autenticação, dependendo do nível de autenticação do ponto de extremidade oposto.  
  
    -   ENCRYPTION é definido como REQUIRED por padrão. Isso especifica que todas as conexões para esse ponto de extremidade devem usar criptografia. Porém, você pode desabilitar a criptografia ou deixá-la opcional em um ponto de extremidade. As alternativas são como segue:  
  
        |Valor|Definição|  
        |-----------|----------------|  
        |DISABLED|Especifica que os dados enviados em uma conexão não estão criptografados.|  
        |SUPPORTED|Especifica que os dados só serão criptografados se o ponto de extremidade oposto especificar SUPPORTED ou REQUIRED.|  
        |REQUIRED|Especifica que os dados enviados em uma conexão devem ser criptografados.|  
  
         Se um ponto de extremidade requisitar criptografia, o outro ponto de extremidade deve ter ENCRYPTION definido como SUPPORTED ou REQUIRED.  
  
    -   *\<algorithm>* fornece a opção de especificar os padrões de criptografia para o ponto de extremidade. O valor de *\<algorithm>* pode ser um dos seguintes algoritmos ou combinações de algoritmos: RC4, AES, AES RC4 ou RC4 AES.  
  
         AES RC4 especifica que esse ponto de extremidade negociará um algoritmo de criptografia, dando preferência ao algoritmo AES. RC4 AES especifica que esse ponto de extremidade negociará um algoritmo de criptografia, dando preferência ao algoritmo RC4. Se ambos os ponto de extremidade especificarem ambos os algoritmos, mas em ordens diferentes, vence o ponto de extremidade que aceita a conexão.  
  
        > [!NOTE]  
        >  O algoritmo RC4 é preterido. [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Recomendamos usar AES.  
  
    -   *\<role>* define a função ou as funções que o servidor pode executar. Especificar ROLE é necessário. Entretanto, a função do ponto de extremidade é relevante apenas para o espelhamento de banco de dados. Para [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], a função do ponto de extremidade é ignorada.  
  
         Para permitir que uma instância do servidor sirva como uma função em uma sessão de espelhamento de banco de dados e uma função diferente em outra sessão, especifique ROLE=ALL. Para restringir uma instância do servidor como sendo um parceiro ou uma testemunha, especifique ROLE=PARTNER ou ROLE=WITNESS, respectivamente.  
  
        > [!NOTE]  
        >  Para obter mais informações sobre opções de Espelhamento de Banco de Dados para diferentes edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
     Para obter uma descrição completa da sintaxe CREATE ENDPOINT, veja [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md).  
  
    > [!NOTE]  
    >  Para alterar um ponto de extremidade existente, use [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md).  
  
###  <a name="TsqlExample"></a> Exemplo: criar pontos de extremidade compatíveis com espelhamento de banco de dados (Transact-SQL)  
 O seguinte exemplo cria pontos de extremidade do espelhamento de banco de dados para as instâncias de servidor padrão em três sistemas de computador separados:  
  
|Função da instância de servidor|Nome do computador host|  
|-----------------------------|---------------------------|  
|Parceiro (inicialmente na função principal)|`SQLHOST01\.`|  
|Parceiro (inicialmente na função espelho)|`SQLHOST02\.`|  
|Witness (testemunha)|`SQLHOST03\.`|  
  
 Neste exemplo, todos os três pontos de extremidade usam o número da porta 7022, entretanto qualquer número de porta disponível funcionaria. A opção AUTHENTICATION é desnecessária, porque os pontos de extremidade usam o tipo padrão, Autenticação do Windows. A opção ENCRYPTION também é desnecessária, porque todos os pontos de extremidade são feitos para negociar o método de autenticação de uma conexão, que é o comportamento padrão para a Autenticação do Windows. Também, todos os pontos de extremidade requerem a criptografia, que é o comportamento padrão.  
  
 Toda instância do servidor está limitada para servir como parceiro ou testemunha, e o ponto de extremidade de cada servidor especifica expressamente qual a função (ROLE=PARTNER ou ROLE=WITNESS).  
  
> [!IMPORTANT]  
>  Cada instância do servidor só pode ter um ponto de extremidade. Então, se você quiser que uma instância do servidor seja parceiro em algumas sessões e testemunha em outras, especifique ROLE=ALL.  
  
```  
--Endpoint for initial principal server instance, which  
--is the only server instance running on SQLHOST01.  
CREATE ENDPOINT endpoint_mirroring  
    STATE = STARTED  
    AS TCP ( LISTENER_PORT = 7022 )  
    FOR DATABASE_MIRRORING (ROLE=PARTNER);  
GO  
--Endpoint for initial mirror server instance, which  
--is the only server instance running on SQLHOST02.  
CREATE ENDPOINT endpoint_mirroring  
    STATE = STARTED  
    AS TCP ( LISTENER_PORT = 7022 )  
    FOR DATABASE_MIRRORING (ROLE=PARTNER);  
GO  
--Endpoint for witness server instance, which  
--is the only server instance running on SQLHOST03.  
CREATE ENDPOINT endpoint_mirroring  
    STATE = STARTED  
    AS TCP ( LISTENER_PORT = 7022 )  
    FOR DATABASE_MIRRORING (ROLE=WITNESS);  
GO  
```  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para configurar um ponto de extremidade de espelhamento de banco de dados**  
  
-   [Criar um ponto de extremidade de espelhamento de banco de dados para grupos de disponibilidade AlwaysOn &#40;SQL Server PowerShell&#41;](../../database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Usar certificados para um ponto de extremidade de espelhamento de banco de dados &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
    -   [Permitir que um ponto de extremidade de espelhamento de banco de dados use certificados para conexões de saída &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
    -   [Permitir que um ponto de extremidade de espelhamento de banco de dados use certificados para conexões de entrada &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-inbound-connections.md)  
  
-   [Especificar um endereço de rede do servidor &#40;Espelhamento de banco de dados&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)  
  
-   [Especificar a URL do ponto de extremidade ao adicionar ou modificar uma réplica de disponibilidade &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
 **Para exibir informações sobre o ponto de extremidade de espelhamento de banco de dados**  
  
-   [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [Escolher um algoritmo de criptografia](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [Especificar um endereço de rede do servidor &#40;espelhamento de banco de dados&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)   
 [Exemplo: configurar o espelhamento de banco de dados usando a Autenticação do Windows &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/example-setting-up-database-mirroring-using-windows-authentication-transact-sql.md)   
 [O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
  
  

