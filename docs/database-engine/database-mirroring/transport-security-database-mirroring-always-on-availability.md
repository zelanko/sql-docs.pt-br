---
title: Segurança do transporte – espelhamento de banco de dados – disponibilidade AlwaysOn | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: database-mirroring
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- sessions [SQL Server], database mirroring
- cryptography [SQL Server], database mirroring
- certificates [SQL Server], database mirroring
- encryption [SQL Server], database mirroring
- Windows authentication [SQL Server]
- authentication [SQL Server], database mirroring
- transport security
- database mirroring [SQL Server], security
ms.assetid: 49239d02-964e-47c0-9b7f-2b539151ee1b
caps.latest.revision: 59
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ccd011f25b06e4eac42ce408b97ed7c5a801095d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="transport-security---database-mirroring---always-on-availability"></a>Segurança do transporte – espelhamento de banco de dados – disponibilidade AlwaysOn
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  A segurança de transporte envolve autenticação e, como opção, criptografia de mensagens trocadas entre os bancos de dados. Para o espelhamento de banco de dados e [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], a autenticação e a criptografia são configuradas no ponto de extremidade do espelhamento de banco de dados. Para obter uma introdução aos pontos de extremidade de espelhamento de banco de dados, consulte [O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md).  
  
 **Neste tópico:**  
  
-   [Autenticação](#Authentication)  
  
-   [Criptografia de dados](#DataEncryption)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="Authentication"></a> Autenticação  
 Autenticação é o processo de verificar se um usuário é quem o usuário diz ser. Conexões entre pontos de extremidade espelhamento de banco de dados requerem autenticação. Exigências de conexão de um parceiro ou testemunha, se existir, devem ser autenticadas.  
  
 O tipo de autenticação usado por uma instância do servidor para o espelhamento de banco de dados ou [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] é uma propriedade do ponto de extremidade do espelhamento de banco de dados. Dois tipos de segurança de transporte estão disponíveis para pontos de extremidade do espelhamento de banco de dados: Autenticação do Windows (SSPI) e autenticação baseada em certificado.  
  
### <a name="windows-authentication"></a>Autenticação do Windows  
 Sob autenticação do Windows, cada instância de servidor faz o logon para o outro lado usando as credenciais da conta de usuário do Windows sob o qual o processo está sendo executado. A Autenticação do Windows pode exigir configuração manual de contas de logon, como segue:  
  
-   Se as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] forem executadas como serviços sob a mesma conta de domínio, nenhuma configuração adicional será necessária.  
  
-   Se as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] forem executadas como serviços em diferentes contas de domínio (nos mesmos domínios ou em domínios confiáveis), o logon de cada conta deverá ser criado no **mestre** em cada uma das outras instâncias de servidor, e esse logon deverá receber permissões CONNECT no ponto de extremidade.  
  
-   Se as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] forem executadas como a conta de Serviço de Rede, o logon da conta de cada computador host (*DomainName***\\***ComputerName$*) deverá ser criado no **mestre** em cada um dos outros servidores e esse logon deverá receber permissões CONNECT no ponto de extremidade. Isso é porque uma instância de servidor em execução sob a conta de serviço de rede é autenticada usando a conta de domínio do computador host.  
  
> [!NOTE]  
>  Para obter um exemplo de como configurar a sessão de espelhamento de banco de dados usando a Autenticação do Windows, consulte [Exemplo: Configurando o espelhamento de banco de dados usando a Autenticação do Windows &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/example-setting-up-database-mirroring-using-windows-authentication-transact-sql.md).  
  
### <a name="certificates"></a>Certificados  
 Em algumas situações, como quando as instâncias de servidor não estão em domínios confiáveis ou quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver executando como um serviço local, a Autenticação do Windows é indisponível. Em tais casos, em vez de credenciais de usuário, são exigidos certificados para autenticar solicitações de conexão. O ponto de extremidade do espelhamento de cada instância de servidor deve ser configurado com seu próprio certificado localmente criado.  
  
 O método de criptografia é estabelecido quando o certificado é criado. Para obter mais informações, consulte [Permitir que um ponto de extremidade de espelhamento de banco de dados use certificados para conexões de saída &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md). Administre cuidadosamente os certificados que você usa.  
  
 Uma instância de servidor usa a chave privada de seu próprio certificado para estabelecer sua identidade ao configurar uma conexão. A instância de servidor que recebe a solicitação de conexão usa a chave pública do certificado do remetente para autenticar a identidade do remetente. Por exemplo, considere duas instâncias de servidor, Server_A e Server_B. Server_A usa sua chave privada para criptografar o cabeçalho da conexão antes de enviar uma solicitação de conexão a Server_B. Server_B usa a chave pública do certificado de Server_A para descriptografar o cabeçalho da conexão. Se o cabeçalho descriptografado estiver correto, Server_B saberá que o cabeçalho foi criptografado por Server_A, e a conexão é autenticada. Se o cabeçalho descriptografado estiver incorreto, Server_B saberá que a solicitação de conexão não é autêntica e recusará a conexão.  
  
##  <a name="DataEncryption"></a> Criptografia de dados  
 Por padrão, um ponto de extremidade de espelhamento de banco de dados solicita a criptografia de dados enviados por conexões de espelhamento. Neste caso, os pontos de extremidade podem se conectar apenas a pontos de extremidade que também usam criptografia. A menos que você possa garantir que sua rede está segura, recomendamos que você solicite criptografia para suas conexões de espelhamento de banco de dados. Porém, você pode desabilitar a criptografia ou torná-la suportável, mas não obrigatória. Se a criptografia estiver desabilitada, nunca serão criptografados dados e os pontos de extremidade não poderão se conectar a um ponto de extremidade que solicita criptografia. Se a criptografia for suportada, só serão criptografados dados se o ponto de extremidade suportar ou solicitar criptografia.  
  
> [!NOTE]  
>  Os pontos de extremidade de espelhamento criados por [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] são criados com criptografia obrigatória ou desabilitada. Para alterar a configuração de criptografia para SUPPORTED, use a instrução ALTER ENDPOINT [!INCLUDE[tsql](../../includes/tsql-md.md)] . Para obter mais informações, consulte [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md).  
  
 Opcionalmente, você pode controlar os algoritmos de criptografia que podem ser usados por um ponto de extremidade, especificando um dos seguintes valores para a opção de ALGORITHM em uma instrução CREATE ENDPOINT ou instrução ALTER ENDPOINT:  
  
|Valor de ALGORITHM|Description|  
|---------------------|-----------------|  
|RC4|Especifica que o ponto de extremidade deve usar o algoritmo RC4. Esse é o padrão.<br /><br /> **\*\* Aviso \*\*** O algoritmo RC4 é preterido. [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Recomendamos usar AES.|  
|AES|Especifica que o ponto de extremidade deve usar o algoritmo AES.|  
|AES RC4|Especifica que o dois pontos de extremidade negociarão por um algoritmo de criptografia com esse ponto de extremidade, dando preferência ao algoritmo AES.|  
|RC4 AES|Especifica que o dois pontos de extremidade negociarão por um algoritmo de criptografia com esse ponto de extremidade, dando preferência ao algoritmo RC4.|  
  
 Se os pontos de extremidade especificarem ambos os algoritmos, mas em ordens diferentes, vence o ponto de extremidade que aceita a conexão.  
  
> [!NOTE]  
>  O algoritmo RC4 tem suporte somente para compatibilidade com versões anteriores. O novo material só pode ser criptografado por meio do algoritmo RC4 ou RC4_128 quando o banco de dados está no nível de compatibilidade 90 ou 100. (Não recomendável.) Use um algoritmo mais recente; por exemplo, um dos algoritmos AES. No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versões posteriores, o material criptografado por meio do algoritmo RC4 ou RC4_128 pode ser descriptografado em qualquer nível de compatibilidade.  
>   
>  Embora consideravelmente mais rápido que o AES, o RC4 é um algoritmo relativamente fraco, enquanto o AES é um algoritmo relativamente forte. Portanto, nós recomendamos que você use o algoritmo AES.  
  
 Para obter informações sobre a sintaxe [!INCLUDE[tsql](../../includes/tsql-md.md)] para especificar criptografia, consulte [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md).  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para configurar a segurança de transporte para o ponto de extremidade do espelhamento de banco de dados**  
  
-   [Criar um ponto de extremidade de espelhamento de banco de dados para a Autenticação do Windows &#40;SQL Server&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [Criar um ponto de extremidade de espelhamento de banco de dados para a Autenticação do Windows &#40;SQL Server&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Permitir que um ponto de extremidade de espelhamento de banco de dados use certificados para conexões de saída &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Escolher um algoritmo de criptografia](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [DROP ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-endpoint-transact-sql.md)   
 [Central de segurança do Mecanismo de Banco de Dados do SQL Server e Banco de Dados SQL do Azure](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)   
 [Gerenciar metadados ao disponibilizar um banco de dados em outra instância do servidor &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)   
 [O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)   
 [sys.dm_db_mirroring_connections &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-mirroring-sys-dm-db-mirroring-connections.md)   
 [Solução de problemas de configuração de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)   
 [Solução de problemas de configuração de Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
  
