---
title: Configurando o espelhamento de banco de dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
ms.assetid: da45efed-55eb-4c71-be34-ac2589dfce8d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 43c964db4c0231d15101f58b7af088bc239fe152
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68048091"
---
# <a name="setting-up-database-mirroring-sql-server"></a>Configurando o espelhamento de banco de dados (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta seção descreve os pré-requisitos, as recomendações e as etapas para configuração do espelhamento de banco de dados. Para obter uma introdução ao espelhamento de banco de dados, consulte [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
> [!IMPORTANT]  
>  É recomendável configurar um espelhamento de banco de dados fora do horário de pico, pois a configuração pode afetar o desempenho.  
  
  
##  <a name="PrepareInstances"></a> Preparando uma instância de servidor para hospedar um servidor espelho  
 Para cada sessão de espelhamento de banco de dados:  
  
1.  O servidor principal, o servidor espelho e o servidor testemunha, se houver, devem ser hospedadas por instâncias de servidor separadas que devem estar em sistemas host separados. Cada instância de servidor exige um ponto de extremidade de espelhamento de banco de dados. Se você precisar criar um ponto de extremidade de espelhamento de banco de dados, verifique se está acessível a outras instâncias de servidor.  
  
     A forma de autenticação usada para o espelhamento de banco de dados por uma instância do servidor é uma propriedade do ponto de extremidade de espelhamento de banco de dados. Dois tipos de segurança de transporte estão disponíveis para o espelhamento de banco de dados: Autenticação do Windows ou autenticação baseada em certificado. Para obter mais informações, consulte [Segurança de transporte para espelhamento de banco de dados e grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md).  
  
     Os requisitos de acesso à rede são específicos ao formulário de autenticação, da seguinte maneira:  
  
    -   **Se estiver usando a Autenticação do Windows**  
  
         Se as instâncias de servidor estiverem sendo executadas em contas do usuário de domínio diferentes, cada uma exigirá um logon no banco de dados **mestre** dos outros. Se o logon não existir, você deve criá-lo. Para obter mais informações, consulte [Permitir o acesso à rede a um ponto de extremidade de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-allow-network-access-windows-authentication.md).  
  
    -   **Se estiver usando certificados**  
  
         Para habilitar a autenticação de certificado para espelhamento de banco de dados em uma determinada instância do servidor, o administrador do sistema deve configurar cada instância do servidor para usar certificados nas conexões de saída e de entrada. As conexões de saída devem ser configuradas primeiro. Para obter mais informações, consulte [Usar certificados para um ponto de extremidade do espelhamento de banco de dados &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md).  
  
2.  Verifique se existem logons no servidor espelho para todos os usuários do banco de dados. Para obter mais informações, consulte [Configurar contas de logon para espelhamento de banco de dados ou para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/database-mirroring/set-up-login-accounts-database-mirroring-always-on-availability.md).  
  
3.  Na instância de servidor que hospedará o banco de dados espelho, configure o restante do ambiente que é necessário para o banco de dados espelhado. Para obter mais informações, consulte [Gerenciar metadados ao disponibilizar um banco de dados em outra instância do servidor &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).  
  
##  <a name="EstablishUsingWinAuthentication"></a> Visão geral: estabelecer uma sessão de espelhamento de banco de dados  
 As etapas básicas para estabelecer uma sessão de espelhamento são as seguintes:  
  
1.  Crie o banco de dados espelho restaurando os seguintes backups, usando RESTORE WITH NORECOVERY em cada operação de restauração:  
  
    1.  Restaure um backup completo recente do banco de dados principal, depois de ter certeza de que o banco de dados principal já estava usando o modelo de recuperação completa quando o backup foi realizado. O banco de dados espelho deve ter o mesmo nome que o banco de dados principal.  
  
    2.  Se você tiver feito qualquer backup diferencial do banco de dados desde o backup completo restaurado, restaure seu backup diferencial mais recente.  
  
    3.  Restaure todos os backups de log feitos desde o backup completo ou diferencial do banco de dados.  
  
     Para obter mais informações, veja [Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md).  
  
    > [!IMPORTANT]  
    >  Conclua as etapas de configuração restantes o mais rápido possível depois de fazer o backup do banco de dados principal. Antes de iniciar o espelhamento nos parceiros, você deve criar um backup do log atual no banco de dados original e restaurá-lo no futuro banco de dados espelho.  
  
2.  Você pode configurar usando [!INCLUDE[tsql](../../includes/tsql-md.md)] ou o Assistente de Espelhamento de Banco de Dados. Para obter mais informações, consulte um dos seguintes itens:  
  
    -   [Estabelecer uma sessão de espelhamento de banco de dados com a Autenticação do Windows &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-establish-session-windows-authentication.md)  
  
    -   [Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
3.  Por padrão, uma sessão é definida como segurança de transação completa (SAFETY é definido como FULL), que inicia a sessão no modo síncrono de segurança alta, sem failover automático. Você pode reconfigurar a sessão para ser executada em modo de segurança alta com failover automático ou em modo assíncrono de alto desempenho, como se segue:  
  
    -   **Modo de segurança alta com failover automático**  
  
         Se você quiser que uma sessão de modo de segurança alta dê suporte a failover automático, acrescente uma instância do servidor testemunha.  
  
         **Para adicionar uma testemunha**  
  
        -   [Adicionar uma testemunha de espelhamento de banco de dados usando a Autenticação do Windows &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)  
  
        -   [Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
        > [!NOTE]  
        >  O proprietário do banco de dados pode desativar a testemunha de um banco de dados a qualquer momento. A desativação da testemunha equivale a não ter nenhuma testemunha, e não pode ocorrer failover automático.  
  
    -   **Modo de alto desempenho**  
  
         Alternativamente, se você não quiser failover automático e preferir enfatizar o desempenho em vez da disponibilidade, desative a segurança de transação. Para obter mais informações, consulte [Alterar a segurança da transação em uma sessão de espelhamento de banco de dados &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/change-transaction-safety-in-a-database-mirroring-session-transact-sql.md).  
  
        > [!NOTE]  
        >  Em modo de alto desempenho, WITNESS precisa ser definido como OFF. Para obter mais informações, confira [Quorum: Como uma testemunha afeta a disponibilidade do banco de dados &#40;Espelhamento de Banco de Dados&#41;](../../database-engine/database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md).  
  
> [!NOTE]  
>  Para obter um exemplo do uso do [!INCLUDE[tsql](../../includes/tsql-md.md)] para configurar o espelhamento de banco de dados usando a Autenticação do Microsoft Windows, veja [Exemplo: Configurando o espelhamento de banco de dados usando a Autenticação do Windows &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/example-setting-up-database-mirroring-using-windows-authentication-transact-sql.md).  
>   
>  Para obter um exemplo do uso do [!INCLUDE[tsql](../../includes/tsql-md.md)] para configurar o espelhamento de banco de dados usando a segurança baseada em certificado, veja [Exemplo: Configurar o espelhamento de banco de dados usando certificados &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/example-setting-up-database-mirroring-using-certificates-transact-sql.md).  
  
  
##  <a name="InThisSection"></a> Nesta seção  
 [Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)  
 Resume as etapas para criar ou preparar um banco de dados espelho antes de retomar uma sessão suspensa. Fornece também links para tópicos de instruções.  
  
 [Especificar um endereço de rede do servidor &#40;Espelhamento de banco de dados&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)  
 Descreve a sintaxe de um endereço de rede de servidor, como o endereço identifica o ponto de extremidade do espelhamento de banco de dados da instância do servidor e como encontrar o nome de domínio totalmente qualificado de um sistema.  
  
 [Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
 Descreve como usar o Assistente para Configurar Segurança de Espelhamento de Banco de Dados para iniciar o espelhamento de banco de dados em um banco de dados.  
  
 [Estabelecer uma sessão de espelhamento de banco de dados com a Autenticação do Windows &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-establish-session-windows-authentication.md)  
 Descreve as etapas [!INCLUDE[tsql](../../includes/tsql-md.md)] de configuração do espelhamento de banco de dados.  
  
 [Exemplo: configurar o espelhamento de banco de dados usando a Autenticação do Windows &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/example-setting-up-database-mirroring-using-windows-authentication-transact-sql.md)  
 Contém um exemplo de todas as fases necessárias para criar uma sessão de espelhamento de banco de dados com uma testemunha, usando a Autenticação do Windows.  
  
 [Exemplo: Configurar o espelhamento de banco de dados usando certificados &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/example-setting-up-database-mirroring-using-certificates-transact-sql.md)  
 Contém um exemplo de todas as fases necessárias para criar uma sessão de espelhamento de banco de dados com uma testemunha, usando a autenticação baseada em certificado.  
  
 [Configurar contas de logon para espelhamento de banco de dados ou para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/database-mirroring/set-up-login-accounts-database-mirroring-always-on-availability.md)  
 Descreve como criar um logon para uma instância de servidor remoto usando uma conta diferente da instância de servidor local.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **SQL Server Management Studio**  
  
-   [Iniciar o Assistente para Configurar Segurança de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
-   [Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
 **Transact-SQL**  
  
-   [Permitir o acesso à rede a um ponto de extremidade de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-allow-network-access-windows-authentication.md)  
  
-   [Permitir que um ponto de extremidade de espelhamento de banco de dados use certificados para conexões de saída &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
-   [Permitir que um ponto de extremidade de espelhamento de banco de dados use certificados para conexões de entrada &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-inbound-connections.md)  
  
-   [Criar um ponto de extremidade de espelhamento de banco de dados para a Autenticação do Windows &#40;SQL Server&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Estabelecer uma sessão de espelhamento de banco de dados com a Autenticação do Windows &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-establish-session-windows-authentication.md)  
  
-   [Adicionar uma testemunha de espelhamento de banco de dados usando a Autenticação do Windows &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)  
  
-   [Configurar um banco de dados espelho para usar a propriedade confiável &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/set-up-a-mirror-database-to-use-the-trustworthy-property-transact-sql.md)  
  
 **Transact-SQL/SQL Server Management Studio**  
  
-   [Atualização de Instâncias Espelhadas](../../database-engine/database-mirroring/upgrading-mirrored-instances.md)  
  
-   [Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)  
  
-   [Solução de problemas de configuração de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)  
  
  
## <a name="see-also"></a>Consulte Também  
 [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Espelhamento de banco de dados: Interoperabilidade e Coexistência &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-interoperability-and-coexistence-sql-server.md)   
 [Segurança de transporte para espelhamento de banco de dados e grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [Especificar um endereço de rede do servidor &#40;Espelhamento de banco de dados&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)  
  
  
