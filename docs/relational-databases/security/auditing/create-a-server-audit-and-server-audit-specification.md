---
title: Criar uma auditoria de servidor e uma especificação de auditoria de servidor | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.SWB.SQLAUDIT.FILTER.F1
- sql13.swb.sqlaudit.general.f1
- sql13.swb.sqlaudit.srvaudit.general.f1
helpviewer_keywords:
- server audit [SQL Server]
- audits [SQL Server], specification
ms.assetid: 6624b1ab-7ec8-44ce-8292-397edf644394
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 5eefebaf1d68a29a654bb407c46ad5871164d2d0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68095188"
---
# <a name="create-a-server-audit-and-server-audit-specification"></a>Criar uma auditoria de servidor e uma especificação de auditoria de servidor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como criar uma especificação de auditoria de servidor no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. *Auditar* uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] envolve eventos de rastreamento e de log que ocorrem no sistema. O objeto *SQL Server Audit* coleta uma instância única de ações no nível do servidor e/ou do banco de dados e grupos de ações a serem monitoradas. A auditoria está no nível de instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Você pode ter várias auditorias por instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . O objeto *Especificação da Auditoria do Servidor* pertence a uma auditoria. É possível criar uma especificação de auditoria de servidor por auditoria, já que ambas são criadas no escopo da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para criar uma auditoria de servidor e uma especificação de auditoria de servidor usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Deve existir uma auditoria antes da criação de uma especificação de auditoria de servidor para ela. Quando uma especificação de auditoria de servidor é criada, ela fica em um estado desabilitado.  
  
-   A instrução CREATE SERVER AUDIT está no escopo de uma transação. Se a transação for revertida, a instrução também será revertida.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
  
-   Para criar, alterar ou descartar uma auditoria de servidor, as entidades devem ter a permissão ALTER ANY SERVER AUDIT ou CONTROL SERVER.  
  
-   Os usuários que têm a permissão ALTER ANY SERVER AUDIT podem criar especificações de auditoria de servidor e associá-las a qualquer auditoria.  
  
-   Depois que uma especificação de auditoria de servidor é criada, ela pode ser exibida por entidades que tenham a permissão CONTROL SERVER ou ALTER ANY SERVER AUDIT, com a conta sysadmin, ou por entidades que tenham acesso explícito à auditoria.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-create-a-server-audit"></a>Para criar uma auditoria de servidor  
  
1.  No Pesquisador de Objetos, expanda a pasta **Segurança** .  
  
2.  Clique com o botão direito do mouse na pasta **Auditorias** e selecione **Nova Auditoria...** .  
  
     As opções a seguir estão disponíveis na página **Geral** da caixa de diálogo **Criar Auditoria** :  
  
     **Nome da auditoria**  
     O nome da auditoria. Esse nome é gerado automaticamente quando você cria uma nova auditoria, mas é editável.  
  
     **Atraso de fila (em milissegundos)**  
     Especifica o período máximo, em milissegundos, que pode decorrer antes de as ações de auditorias serem forçadas a serem processadas.  Um valor 0 indica entrega síncrona. O valor padrão mínimo é **1000** (1 segundo). O máximo é 2.147.483.647 (2.147.483.647 segundos ou 24 dias, 20 horas, 31 minutos, 23.647 segundos).  
  
     **Em caso de falha de log de auditoria:**  
     **Continue**  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] As operações continuam. Os registros de auditoria não são retidos. A auditoria retomará tentando registrar eventos em log e será retomada se a condição de falha for resolvida. A seleção da opção **Continuar** pode permitir atividade não auditada, o que pode violar suas políticas de segurança. Selecionar essa opção ao continuar a operação do [!INCLUDE[ssDE](../../../includes/ssde-md.md)] é mais importante do que manter uma auditoria completa. Essa é a seleção padrão.  
  
     **Desligar servidor**  
     Força o desligamento de um servidor quando a instância do servidor que grava no destino não puder gravar dados no destino de auditoria. O logon que emite isso deve ter a permissão **SHUTDOWN** . Se o logon não tiver essa permissão, essa função apresentará falha e será exibida uma mensagem de erro. Não ocorre nenhum evento auditado. Selecione essa opção quando uma falha de auditoria puder comprometer a segurança ou a integridade do sistema.  
  
     **Operação com falha**  
     Em casos onde o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit não pode gravar no log de auditoria, essa opção provocará falha nas ações de banco de dados se elas forem, de outra forma, provocar eventos auditados. Não ocorre nenhum evento auditado. As ações que não provocam eventos auditados podem continuar. A auditoria retomará tentando registrar eventos em log e será retomada se a condição de falha for resolvida. Selecione essa opção quando manter uma auditoria completa for mais importante do que o acesso total ao [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
    > [!IMPORTANT]  
    >  Quando a auditoria estiver em um estado com falha, a Conexão de administrador dedicada poderá continuar executando eventos auditados.  
  
     Lista**Destino da auditoria**  
     Especifica o destino para dados de auditoria. As opções disponíveis são um arquivo binário, o log de aplicativos do Windows ou o log de segurança do Windows. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não poderá gravar no log de segurança do Windows se não forem definidas configurações adicionais no Windows. Para obter mais informações, veja [Gravar eventos de auditoria do SQL Server no log de segurança](../../../relational-databases/security/auditing/write-sql-server-audit-events-to-the-security-log.md).  
  
     **Caminho do arquivo**  
     Especifica a localização da pasta em que os dados de auditoria serão gravados quando o **Destino da auditoria** for um arquivo.  
  
     **Reticências (...)**  
     Abre a caixa de diálogo **Localizar Pasta -** _server\_name_ para especificar um caminho de arquivo ou criar uma pasta na qual o arquivo de auditoria é gravado.  
  
     **Audite o limite máximo de arquivo:**  
     **Máximo de arquivos de substituição**  
     Especifica que, quando o número máximo de arquivos de auditoria é atingido, os arquivos de auditoria mais antigos são substituídos por novo conteúdo de arquivo.  
  
     **Máximo de arquivos**  
     Especifica que, quando o número máximo de arquivos de auditoria for atingido, haverá falha com um erro em qualquer ação que provoque a geração de eventos de auditoria adicionais.  
  
     Caixa de seleção**Ilimitado**  
     Quando a caixa de seleção **Ilimitado** sob **Máximo de arquivos de substituição** for marcada, não haverá nenhum limite imposto para o número de arquivos de auditoria a serem criados. A caixa de seleção **Ilimitado** é marcada por padrão e se aplica às seleções **Máximo de arquivos de substituição** e **Máximo de arquivos** .  
  
     Caixa**Número de arquivos**  
     Especifica o número de arquivos de auditoria a serem criados, até 2.147.483.647. Essa opção estará disponível somente se **Ilimitado** estiver desmarcado.  
  
     **Tamanho máximo de arquivo**  
     Especifica o tamanho máximo para um arquivo de auditoria em megabytes (MB), gigabytes (GB) ou terabytes (TB). Você pode especificar entre 1024 MB e 2.147.483.647 TB. Marcar a caixa de seleção **Ilimitado** não estabelece um limite para o tamanho do arquivo. A especificação de um valor abaixo de 1024 MB falhará, gerando um erro. A caixa de seleção **Ilimitada** fica marcada por padrão.  
  
     Caixa de seleção**Reservar espaço em disco**  
     Especifica o espaço pré-alocado no disco que é igual ao tamanho de arquivo máximo especificado. Essa configuração pode ser usada se a caixa de seleção **Ilimitada** sob **Tamanho máximo do arquivo** não for marcada. Essa caixa de seleção não é marcada por padrão.  
  
3.  Opcionalmente, na página **Filtro** , insira um predicado ou a cláusula `WHERE` , para a auditoria de servidor para especificar opções adicionais não disponíveis da página **Geral** . Inclua o predicado em parênteses; por exemplo: `(object_name = 'EmployeesTable')`.  
  
4.  Quando terminar de selecionar as opções, clique em **OK**.  
  
#### <a name="to-create-a-server-audit-specification"></a>Para criar uma especificação de auditoria de servidor  
  
1.  No Pesquisador de Objetos, clique no sinal de mais para expandir a pasta **Segurança** .  
  
2.  Clique com o botão direito do mouse na pasta **Especificações de Auditoria de Servidor** e selecione **Nova Especificação de Auditoria de Servidor...** .  
  
     As opções a seguir estão disponíveis na caixa de diálogo **Criar Especificação de Auditoria de Servidor** .  
  
     **Nome**  
     O nome da especificação de auditoria de servidor. Esse nome é gerado automaticamente quando você cria uma nova especificação de auditoria de servidor, mas é editável.  
  
     **Auditoria**  
     O nome de uma auditoria de servidor existente. Digite o nome da auditoria ou selecione-o na lista.  
  
     **Tipo de Ação de Auditoria**  
     Especifica os grupos de ação de auditoria no nível de servidor e as ações de auditoria a capturar. Para a lista de grupos de ação de auditoria no nível de servidor, ações de auditoria e uma descrição dos eventos que eles contêm, veja [Ações e grupos de ações de auditoria do SQL Server](../../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md).  
  
     **Esquema de Objeto**  
     Exibe o esquema para **Object Name**especificado.  
  
     **Object Name**  
     Nome do objeto a ser auditado. Isso só está disponível para ações de auditoria e não se aplica a grupos de auditoria.  
  
     **Reticências (...)**  
     Abre a caixa de diálogo **Selecionar Objetos** para procurar e selecionar um objeto disponível, com base no **Tipo de Ação de Auditoria**especificado.  
  
     **Nome Principal**  
     A conta para filtrar a auditoria para o objeto que está sendo auditado.  
  
     **Reticências (...)**  
     Abre a caixa de diálogo **Selecionar Objetos** para procurar e selecionar um objeto disponível, com base no **Nome do Objeto**especificado.  
  
3.  Quando terminar, clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-create-a-server-audit"></a>Para criar uma auditoria de servidor  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- Creates a server audit called "HIPAA_Audit" with a binary file as the target and no options.  
    CREATE SERVER AUDIT HIPAA_Audit  
        TO FILE ( FILEPATH ='\\SQLPROD_1\Audit\' );  
    ```  
  
#### <a name="to-create-a-server-audit-specification"></a>Para criar uma especificação de auditoria de servidor  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    /*Creates a server audit specification called "HIPAA_Audit_Specification" that audits failed logins for the SQL Server audit "HIPAA_Audit" created above.  
    */  
  
    CREATE SERVER AUDIT SPECIFICATION HIPAA_Audit_Specification  
    FOR SERVER AUDIT HIPAA_Audit  
        ADD (FAILED_LOGIN_GROUP);  
    GO  
    -- Enables the audit.   
  
    ALTER SERVER AUDIT HIPAA_Audit  
    WITH (STATE = ON);  
    GO  
    ```  
  
 Para obter mais informações, veja [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-audit-transact-sql.md) e [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-audit-specification-transact-sql.md).  
  
  
