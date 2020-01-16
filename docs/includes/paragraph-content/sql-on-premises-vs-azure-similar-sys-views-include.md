
<!--
### Code examples for Azure cloud differ slightly from on-premises
  Or.....
### Code examples can differ for Azure SQL Database
-->

Alguns exemplos de código Transact-SQL escritos para SQL Server locais precisam de pequenas alterações para serem executados no serviço de Banco de Dados SQL do Azure na nuvem. Uma categoria desses exemplos de código envolve exibições do sistema cujos prefixos de nome diferem ligeiramente entre os dois sistemas de banco de dados:

- **servidor\_** &nbsp; - &nbsp; _prefixo para local_
- **banco de dados\_** &nbsp; - &nbsp; _prefixo para o serviço do BD SQL do Azure na nuvem_

Para ilustração, a tabela a seguir lista e compara dois subconjuntos de exibições do sistema. Para resumir, os subconjuntos estão restritos aos nomes de exibição que também contêm a cadeia de caracteres `_event`. Os subconjuntos têm prefixos de nome diferentes porque eles vêm de dois sistemas de banco de dados diferentes.

| Nome do 2017 local | Nome do serviço de nuvem |
| :------------------------- | :---------------------- |
| server_event_notifications<br />server_event_session_actions<br />server_event_session_events<br />server_event_session_fields<br />server_event_session_targets<br />server_event_sessions<br />server_events<br />server_trigger_events | database_event_session_actions<br />database_event_session_events<br />database_event_session_fields<br />database_event_session_targets<br />database_event_sessions |
| &nbsp; | &nbsp; |

As duas listas na tabela anterior são precisas em junho de 2019. Mas o conteúdo da tabela aqui pode ficar desatualizado, pois seu conteúdo não será mantido aqui. Para obter listas precisas, execute a seguinte instrução T-SQL SELECT. Execute SELECT duas vezes, uma vez em cada sistema de banco de dados.

```sql
SELECT name
    FROM sys.all_objects
    WHERE
        (name LIKE 'database\_%' { ESCAPE '\' } OR
         name LIKE 'server\_%' { ESCAPE '\' })
        AND name LIKE '%\_event%' { ESCAPE '\' }
        AND type = 'V'
    ORDER BY name;
```

<!--
The creation of this docs/includes/ file was prompted by Issue 2211 (https://github.com/MicrosoftDocs/sql-docs/issues/2211).
Initial PR was PR 10427 (https://github.com/MicrosoftDocs/sql-docs-pr/pull/10427).
The complaint was that a specific T-SQL code block failed on Azure SQL Database.

GeneMi  ,  2019/05/28
-->
