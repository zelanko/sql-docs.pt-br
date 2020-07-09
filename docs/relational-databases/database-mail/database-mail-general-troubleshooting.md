---
title: Solução de problemas gerais do Database Mail
ms.date: 06/03/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- architecture [SQL Server], Database Mail
- Database Mail [SQL Server], architecture
- Database Mail [SQL Server], components
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-dt-2019
ms.openlocfilehash: 92496d6c02903ad6c7c14c5b2fd134797f608997
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85726510"
---
# <a name="general-database-mail-troubleshooting-steps"></a>Etapas de solução de problemas gerais do Database Mail 
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

Solucionar problemas do Database Mail requer verificar as áreas gerais a seguir do sistema do Database Mail. Esses procedimentos são apresentados em uma ordem lógica, mas podem ser avaliados em qualquer ordem.

## <a name="permissions"></a>Permissões

Você deve ser membro da função de servidor fixa sysadmin para solucionar problemas de todos os aspectos do Database Mail. Usuários que não são membros da função de servidor fixa sysadmin podem, apenas, obter informações sobre os emails que tentam enviar, e não sobre emails enviados por outros.

## <a name="is-database-mail-enabled"></a>O Database Mail está habilitado

1. No SQL Server Management Studio, conecte-se a uma instância do SQL Server usando uma janela do editor de consulta e então execute o seguinte código:

    ```sql
    sp_configure 'show advanced', 1; 
    GO
    RECONFIGURE;
    GO
    sp_configure;
    GO
    ```

   No painel de resultados, confirme se o run_value para [Database Mail XPs](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md) está definido como 1.
   Se o run_value não é 1, o Database Mail não está habilitado. O Database Mail não é habilitado automaticamente para reduzir o número de recursos disponíveis para a investida de um usuário mal-intencionado. Para obter mais informações, veja [Compreender a configuração da área da superfície](../security/surface-area-configuration.md).

1. Se você decidir que é apropriado habilitar o Database Mail, execute o seguinte código:

    ```sql
    sp_configure 'Database Mail XPs', 1; 
    GO
    RECONFIGURE;
    GO
    ```

1. Para restaurar o procedimento sp_configure ao seu estado padrão, que não mostra opções avançadas, execute o seguinte código:

    ```sql 
    sp_configure 'show advanced', 0; 
    GO
    RECONFIGURE;
    GO
    ```

## <a name="are-users-properly-configured-to-send-mail"></a>Os usuários estão configurados corretamente para enviar emails

1. Para enviar Database Mail, os usuários devem ser membros da função de banco de dados DatabaseMailUserRole no banco de dados msdb. Membros da função de servidor fixa sysadmin e da função db_owner do msdb tornam-se automaticamente membros de DatabaseMailUserRole. Para listar todos os outros membros de DatabaseMailUserRole, execute a seguinte instrução:

    ```sql
    EXEC msdb.sys.sp_helprolemember 'DatabaseMailUserRole';
    ```

1. Para adicionar usuários à função DatabaseMailUserRole, use a seguinte instrução:

    ```sql
    USE msdb;
    GO
    
    sp_addrolemember @rolename = 'DatabaseMailUserRole'
    ,@membername = '<database user>';
    ```

1. Para enviar Database Mail, os usuários devem ter acesso a, pelo menos, um perfil do Database Mail. Para listar os usuários (entidades) e os perfis aos quais eles têm acesso, execute a instrução a seguir.

    ```sql
    EXEC msdb.dbo.sysmail_help_principalprofile_sp;
    ```

1. Use o Assistente para Configuração do Database Mail para criar perfis e conceder acesso a eles aos usuários.
 
## <a name="is-database-mail-started"></a>O database mail é iniciado

1. O [Programa Externo do Database Mail](database-mail-external-program.md) é ativado quando há mensagens de email a serem processadas. Quando não há nenhuma mensagem a enviar no tempo limite especificado, o programa é encerrado. Para confirmar se a ativação do Database Mail foi iniciada, execute a instrução a seguir:

    ```sql
    EXEC msdb.dbo.sysmail_help_status_sp;
    ```
1. Se a ativação do Database Mail tiver sido iniciada, execute a seguinte instrução para iniciá-la:

    ```sql
    EXEC msdb.dbo.sysmail_start_sp;
    ```

1. Se o programa externo do Database Mail tiver sido iniciado, verifique o status da fila de emails com a seguinte instrução:

    ```sql
    EXEC msdb.dbo.sysmail_help_queue_sp @queue_type = 'mail';
    ```
  
   A fila de emails deve ter o estado de RECEIVES_OCCURRING. O status da fila pode variar a todo instante. Se o estado da fila de email não for RECEIVES_OCCURRING, tente reiniciar a fila. Interrompa a fila usando a instrução a seguir:
   
```sql
EXEC msdb.dbo.sysmail_stop_sp;
```

Então inicie a fila usando a instrução a seguir:

```sql
EXEC msdb.dbo.sysmail_start_sp;
```

  > [!NOTE]
  >  Use a coluna length do conjunto de resultados de sysmail_help_queue_sp para determinar o número de emails na fila.

## <a name="do-problems-affect-some-or-all-accounts"></a>Problemas afetam a algumas ou todas as contas

1. Caso tenha determinado que apenas alguns perfis estão conseguindo enviar emails, pode haver algum problema com as contas do Database Mail utilizadas pelos perfis problemáticos. Para determinar quais contas estão conseguindo enviar email, execute a seguinte instrução:

    ```sql
    SELECT sent_account_id, sent_date FROM msdb.dbo.sysmail_sentitems;
    ```

1. Se um perfil não em funcionando não usar nenhuma das contas listadas, é possível que todas as contas disponíveis ao perfil não estejam funcionando adequadamente. Para testar as contas separadamente, use o Assistente para Configuração do Database Mail para criar um novo perfil com uma única conta e, em seguida, use a caixa de diálogo Enviar Email de Teste para enviar um email usando a nova conta. 
1. Para exibir as mensagens de erro retornadas pelo Database Mail, execute a seguinte instrução:

    ```sql
    SELECT * FROM msdb.dbo.sysmail_event_log;
    ```

   > [!NOTE]
   > O Database Mail considera a mensagem enviada quando consegue entregá-la a um servidor de email SMTP. Erros subsequentes, como um endereço de email destinatário inválido, podem impedir que a mensagem seja entregue, mas não são inseridos no log do Database Mail.

## <a name="retry-mail-delivery"></a>Tentar novamente a entrega de emails

1. Caso tenha determinado que o Database Mail está falhando porque não está sendo possível alcançar confiavelmente o servidor SMTP, você poderá aumentar a taxa de êxito na entrega de emails aumentado o número de vezes que o Database Mail tenta enviar cada mensagem. Inicie o Assistente para Configuração do Database Mail e selecione a opção Exibir ou alterar parâmetros do sistema. Alternativamente, você pode associar mais contas ao perfil, de modo que, diante da ocorrência de falha na conta primária, o Database Mail use a conta de failover para enviar os emails.
1. Na página Configurar Parâmetros do Sistema, os valores padrão de cinco vezes para Tentativas de Repetição de Conta e de 60 segundos para Atraso na Repetição de Conta significam que a entrega da mensagem falhará se o servidor SMTP não puder ser alcançado em 5 minutos. Aumente esses parâmetros para aumentar o tempo antes de a entrega da mensagem falhar.

    > [!NOTE]
    > Quando um grande número de mensagens é enviado, valores padrão grandes podem aumentar a confiabilidade, porém aumentarão substancialmente o uso de recursos à medida que seguidas tentativas de entregar a mensagem forem sendo feitas. Trate a raiz do problema, resolvendo a condição da rede ou do servidor SMTP que está impedindo o Database Mail de contatar prontamente o servidor SMTP.



##  <a name="see-also"></a><a name="RelatedContent"></a> Confira também
  
-   [Objetos de configuração do Database Mail](../../relational-databases/database-mail/database-mail-configuration-objects.md)  
  
-   [Objetos do sistema de mensagens do Database Mail](../../relational-databases/database-mail/database-mail-messaging-objects.md)  
  
-   [Programa externo do Database Mail](../../relational-databases/database-mail/database-mail-external-program.md)  
  
-   [Log e auditoria do Database Mail](../../relational-databases/database-mail/database-mail-log-and-audits.md)  
  
-   [Configurar o SQL Server Agent Mail para usar o Database Mail](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)  
  
  
  
