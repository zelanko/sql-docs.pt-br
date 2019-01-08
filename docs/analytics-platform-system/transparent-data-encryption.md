---
title: Criptografia de dados transparente - Parallel Data Warehouse | Microsoft Docs
description: Transparent data encryption (TDE) para o Parallel Data Warehouse (PDW) executa criptografia de e/s em tempo real e a descriptografia dos dados e arquivos de log de transações e os arquivos de log especiais do PDW."
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: ea15a8fc5eaf066b5a64cf73192f64dd0078434e
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52534086"
---
# <a name="transparent-data-encryption"></a>Criptografia de Dados Transparente
Você pode tomar várias precauções para ajudar a proteger o banco de dados como, por exemplo, projetando um sistema seguro, criptografando ativos confidenciais e criando um firewall em torno dos servidores de banco de dados. No entanto, para um cenário em que a mídia física (como unidades ou fitas de backup) é roubada, um terceiro mal-intencionado pode simplesmente restaurar ou anexar o banco de dados e procurar os dados. Uma solução é criptografar dados confidenciais no banco de dados e proteger as chaves usadas para criptografar os dados com um certificado. Isso impede que alguém sem as chaves use os dados, mas esse tipo de proteção deve ser planejado antecipadamente.  
  
*A Transparent data encryption* (TDE) executa criptografia de e/s em tempo real e a descriptografia dos dados e arquivos de log de arquivos de log de transação e o PDW especial. A criptografia usa uma DEK (chave de criptografia do banco de dados), que é armazenada no registro de inicialização do banco de dados para disponibilidade durante a recuperação. A DEK é uma chave simétrica protegida usando um certificado armazenado no banco de dados mestre do SQL Server PDW. A TDE protege os dados “em repouso”, ou seja, os dados e arquivos de log. Fornece a capacidade de se adequar a muitas leis, regulamentos e diretrizes estabelecidos em vários setores. Esse recurso permite que os desenvolvedores de software criptografem dados usando algoritmos de criptografia AES e 3DES, sem alterar os aplicativos existentes.  
  
> [!IMPORTANT]  
> TDE não fornece criptografia para dados que trafegam entre o cliente e o PDW. Para obter mais informações sobre como criptografar dados entre o cliente e o SQL Server PDW, consulte [provisionar um certificado](provision-certificate.md).  
>   
> A TDE criptografa os dados enquanto ele está se movendo ou em uso. O tráfego interno entre os componentes do PDW dentro do SQL Server PDW não é criptografado. Dados armazenados temporariamente nos buffers de memória não são criptografados. Para reduzir esse risco, controle o acesso físico e conexões com o SQL Server PDW.  
  
Depois de protegido, o banco de dados pode ser restaurado usando o certificado correto.  
  
> [!NOTE]  
> Quando você cria um certificado para a TDE, você deve imediatamente fazer backup dele, junto com a chave privada associada. Se em algum momento o certificado ficar indisponível ou caso você deseje restaurar ou anexar o banco de dados a outro servidor, você precisará dos backups do certificado e da chave privada ou não será possível abrir o banco de dados. O certificado de criptografia deve ser retido até mesmo se o TDE já não estiver habilitado no banco de dados. Mesmo que o banco de dados não seja criptografado, partes do log de transações ainda poderão permanecer protegidas e talvez o certificado seja necessário para algumas operações até a realização do backup completo do banco de dados. Um certificado que excedeu sua data de validade ainda pode ser usado para criptografar e descriptografar dados com TDE.  
  
A criptografia do arquivo de banco de dados é executada no nível de página. As páginas em um banco de dados criptografado são criptografadas antes de serem gravadas no disco e descriptografadas quando lidas na memória. A TDE não aumenta o tamanho do banco de dados criptografado.  
  
A ilustração a seguir mostra a hierarquia de chaves de criptografia de TDE:  
  
![Exibe a hierarquia](media/tde-architecture.png "TDE_Architecture")  
  
## <a name="using-tde"></a>Usando Transparent Data Encryption  
Para usar a TDE, execute estes procedimentos. As três primeiras etapas são feitas somente uma vez, durante a preparação do SQL Server PDW para dar suporte a TDE.  
  
1.  Crie uma chave mestra de banco de dados mestre.  
  
2.  Use **sp_pdw_database_encryption** para habilitar a TDE no SQL Server PDW. Esta operação modifica os bancos de dados temporários para garantir a proteção de dados temporários de futuros e falhará se você tentar quando existem quaisquer sessões ativas que têm tabelas temporárias. **sp_pdw_database_encryption** ativa de mascaramento de dados de usuário nos logs de sistema do PDW. (Para obter mais informações sobre o mascaramento de dados de usuário nos logs de sistema do PDW, consulte [sp_pdw_log_user_data_masking](../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md).)  
  
3.  Use [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) para criar uma credencial que pode autenticar e gravar no compartilhamento onde o backup do certificado será armazenado. Se já existir uma credencial para o servidor de armazenamento pretendida, você pode usar a credencial existente.  
  
4.  Banco de dados mestre, crie um certificado protegido pela chave mestra.  
  
5.  Faça backup do certificado para o compartilhamento de armazenamento.  
  
6.  No banco de dados de usuário, crie uma chave de criptografia de banco de dados e proteja-a com o certificado que é armazenado no banco de dados mestre.  
  
7.  Use o `ALTER DATABASE` instrução para criptografar o banco de dados usando TDE.  
  
O exemplo a seguir ilustra a criptografar o `AdventureWorksPDW2012` banco de dados usando um certificado chamado `MyServerCert`, criada no SQL Server PDW.  
  
**Primeiro: Habilite a TDE no SQL Server PDW.** Esta ação só é necessária uma vez.  
  
```sql  
USE master;  
GO  
  
-- Create a database master key in the master database  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<UseStrongPasswordHere>';  
GO  
  
-- Enable encryption for PDW  
EXEC sp_pdw_database_encryption 1;  
GO  
  
-- Add a credential that can write to the share  
-- A credential created for a backup can be used if you wish  
EXEC sp_pdw_add_network_credentials 'SECURE_SERVER', '<domain>\<Windows_user>', '<password>';  
```  
  
**Segundo: Criar e fazer backup de um certificado no banco de dados mestre.** Esta ação só é necessário uma vez. Você pode ter um certificado separado para cada banco de dados (recomendado) ou você pode proteger vários bancos de dados com um certificado.  
  
```sql  
-- Create certificate in master  
CREATE CERTIFICATE MyServerCert WITH SUBJECT = 'My DEK Certificate';  
GO  
  
-- Back up the certificate with private key  
BACKUP CERTIFICATE MyServerCert   
    TO FILE = '\\SECURE_SERVER\cert\MyServerCert.cer'  
    WITH PRIVATE KEY   
    (   
        FILE = '\\SECURE_SERVER\cert\MyServerCert.key',  
        ENCRYPTION BY PASSWORD = '<UseStrongPasswordHere>'   
    )   
GO  
```  
  
**Último: Criar a DEK e use ALTER DATABASE para criptografar um banco de dados do usuário.** Essa ação é repetida para cada banco de dados protegido por TDE.  
  
```sql  
USE AdventureWorksPDW2012;  
GO  
  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_128  
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;  
GO  
  
ALTER DATABASE AdventureWorksPDW2012 SET ENCRYPTION ON;  
GO  
```  
  
As operações de criptografia e descriptografia são agendadas em threads em segundo plano pelo SQL Server. Você pode exibir o status dessas operações usando exibições do catálogo e exibições de gerenciamento dinâmico na lista que aparece mais adiante neste artigo.  
  
> [!CAUTION]  
> Os arquivos de backup de bancos de dados com TDE habilitada também são criptografados usando a chave de criptografia do banco de dados. Como resultado, quando você restaura esses backups, o certificado que protege a chave de criptografia do banco de dados deve estar disponível. Isso significa que, além de fazer backup do banco de dados, você deve assegurar que os backups dos certificados de servidor sejam mantidos para evitar perda de dados. Se o certificado não estiver mais disponível, haverá perda de dados.  
  
## <a name="commands-and-functions"></a>Comandos e funções  
Os certificados da TDE devem ser criptografados pela chave mestra do banco de dados para serem aceitos pelas instruções a seguir.  
  
A tabela a seguir fornece links e explicações de comandos e funções da TDE.  
  
|Comando ou função|Finalidade|  
|-----------------------|-----------|  
|[CRIAR CHAVE DE CRIPTOGRAFIA DE BANCO DE DADOS](../t-sql/statements/create-database-encryption-key-transact-sql.md)|Cria uma chave usada para criptografar um banco de dados.|  
|[ALTERAR CHAVE DE CRIPTOGRAFIA DE BANCO DE DADOS](../t-sql/statements/alter-database-encryption-key-transact-sql.md)|Altera a chave usada para criptografar um banco de dados.|  
|[DROP DATABASE ENCRYPTION KEY](../t-sql/statements/drop-database-encryption-key-transact-sql.md)|Remove a chave usada para criptografar um banco de dados.|  
|[ALTERAR BANCO DE DADOS](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)|Explica a opção **ALTER DATABASE** usada para habilitar a TDE.|  
  
## <a name="catalog-views-and-dynamic-management-views"></a>Exibições do catálogo e exibições de gerenciamento dinâmico  
A tabela a seguir mostra exibições do catálogo de TDE e exibições de gerenciamento dinâmico.  
  
|Exibição do catálogo ou exibição de gerenciamento dinâmico|Finalidade|  
|-------------------------------------------|-----------|  
|[sys.databases](../relational-databases/system-catalog-views/sys-databases-transact-sql.md)|Exibição do catálogo que exibe informações do banco de dados.|  
|[sys.certificates](../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)|Exibição do catálogo que mostra os certificados em um banco de dados.|  
|[sys.dm_pdw_nodes_database_encryption_keys](../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql.md)|Exibição de gerenciamento dinâmico que fornece informações para cada nó, sobre as chaves de criptografia usado em um banco de dados e o estado da criptografia de banco de dados.|  
  
## <a name="permissions"></a>Permissões  
Cada recurso e comando da TDE têm requisitos individuais de permissões, descritos nas tabelas anteriores.  
  
Exibição de metadados envolvidos com TDE requer a `CONTROL SERVER` permissão.  
  
## <a name="considerations"></a>Considerações  
Quando um exame de recriptografia para uma operação de criptografia de banco de dados está em andamento, as operações de manutenção no banco de dados são desabilitadas.  
  
Você pode descobrir o estado de criptografia de banco de dados usando o **sys.dm_pdw_nodes_database_encryption_keys** exibição de gerenciamento dinâmico. Para obter mais informações, consulte o *exibições do catálogo e exibições de gerenciamento dinâmico* seção neste artigo.  
  
### <a name="restrictions"></a>Restrictions  
As seguintes operações não são permitidas durante o `CREATE DATABASE ENCRYPTION KEY`, `ALTER DATABASE ENCRYPTION KEY`, `DROP DATABASE ENCRYPTION KEY`, ou `ALTER DATABASE...SET ENCRYPTION` instruções.  
  
-   Descartando o banco de dados.  
  
-   Usando um `ALTER DATABASE` comando.  
  
-   Iniciando um backup de banco de dados.  
  
-   Iniciando uma restauração de banco de dados.  
  
As seguintes operações ou condições impedirá que o `CREATE DATABASE ENCRYPTION KEY`, `ALTER DATABASE ENCRYPTION KEY`, `DROP DATABASE ENCRYPTION KEY`, ou `ALTER DATABASE...SET ENCRYPTION` instruções.  
  
-   Um `ALTER DATABASE` comando está em execução.  
  
-   Algum backup de dados está sendo executado.  
  
Durante a criação de arquivos de banco de dados, a inicialização instantânea do arquivo não está disponível quando a TDE está habilitada.  
  
### <a name="areas-not-protected-by-tde"></a>Áreas não protegidas por TDE  
A TDE não protege a tabelas externas.  
  
A TDE não protege as sessões de diagnóstico. Os usuários devem ter cuidado para não consultas com parâmetros confidenciais enquanto sessões de diagnóstico estão em uso. Sessões de diagnóstico que revelam informações confidenciais devem ser descartadas, assim que eles não são mais necessários.  
  
Dados protegidos por TDE são descriptografados quando colocado na memória do SQL Server PDW. Despejos de memória são criados quando ocorrem determinados problemas no dispositivo. Despejar arquivos representam o conteúdo da memória no momento da aparência do problema e pode conter dados confidenciais de forma descriptografada. O conteúdo de despejos de memória deve ser revisado antes que eles são compartilhados com outras pessoas.  
  
O banco de dados mestre não está protegido por TDE. Embora o banco de dados mestre não contém dados de usuário, ele contêm informações como nomes de logon.  
  
### <a name="transparent-data-encryption-and-transaction-logs"></a>Transparent Data Encryption e logs de transação  
Habilitar um banco de dados usar TDE tem o efeito de anulação a parte restante do log de transações virtuais para forçar o próximo log de transações virtuais. Isso garante que nenhum texto não criptografado seja deixado nos logs de transações depois que o banco de dados for definido para criptografia. Você pode localizar o status da criptografia de arquivo de log em cada nó do PDW por meio da exibição a `encryption_state` coluna o `sys.dm_pdw_nodes_database_encryption_keys` modo de exibição, como neste exemplo:  
  
```sql  
WITH dek_encryption_state AS   
(  
    SELECT ISNULL(db_map.database_id, dek.database_id) AS database_id, encryption_state  
    FROM sys.dm_pdw_nodes_database_encryption_keys AS dek  
        INNER JOIN sys.pdw_nodes_pdw_physical_databases AS node_db_map  
           ON dek.database_id = node_db_map.database_id AND dek.pdw_node_id = node_db_map.pdw_node_id  
        LEFT JOIN sys.pdw_database_mappings AS db_map  
            ON node_db_map .physical_name = db_map.physical_name  
        INNER JOIN sys.dm_pdw_nodes AS nodes  
            ON nodes.pdw_node_id = dek.pdw_node_id  
    WHERE dek.encryptor_thumbprint <> 0x  
)  
SELECT TOP 1 encryption_state  
       FROM dek_encryption_state  
       WHERE dek_encryption_state.database_id = DB_ID('AdventureWorksPDW2012 ')  
       ORDER BY (CASE encryption_state WHEN 3 THEN -1 ELSE encryption_state END) DESC;  
```  
  
Todos os dados gravados no log de transações antes de uma alteração na chave de criptografia do banco de dados serão criptografados usando a chave de criptografia do banco de dados anterior.  
  
### <a name="pdw-activity-logs"></a>Logs de atividade do PDW  
SQL Server PDW mantém um conjunto de logs para solucionar problemas. (Observe isso não é o log de transações, o log de erros do SQL Server ou o log de eventos do Windows.) Esses logs de atividade do PDW podem conter instruções completas em texto não criptografado, algumas das quais podem conter dados de usuário. São exemplos típicos **inserir** e **atualização** instruções. Mascaramento de dados do usuário pode ser explicitamente ativado ou desativado usando **sp_pdw_log_user_data_masking**. Habilitar a criptografia no SQL Server PDW automaticamente ativa o mascaramento de dados do usuário nos logs de atividade do PDW para protegê-los. **sp_pdw_log_user_data_masking** também pode ser usado para mascarar instruções quando não estiver usando a TDE, mas que não é recomendado porque reduz significativamente a capacidade da equipe de suporte da Microsoft para analisar problemas.  
  
### <a name="transparent-data-encryption-and-the-tempdb-system-database"></a>Transparent Data Encryption e o banco de dados do sistema tempdb  
O banco de dados do sistema tempdb é criptografado quando a criptografia é habilitada por meio [sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md). Isso é necessário antes de qualquer banco de dados pode usar a TDE. Isso pode ter um efeito de desempenho para bancos de dados não criptografados na mesma instância do SQL Server PDW.  
  
## <a name="key-management"></a>Gerenciamento de chaves  
A chave de criptografia de banco de dados (DEK) é protegida por certificados armazenados no banco de dados mestre. Esses certificados são protegidos pela chave mestra do banco de dados (DMK) do banco de dados mestre. A DMK precisa ser protegido pela chave mestra de serviço (SMK) para ser usado para a TDE.  
  
O sistema pode acessar as chaves sem a necessidade de intervenção humana (como fornecer uma senha). Se o certificado não estiver disponível, o sistema produzirá um erro explicando que não é possível descriptografar a DEK até que o certificado apropriado esteja disponível.  
  
Ao mover um banco de dados de um dispositivo para outro, o certificado usado para proteger seu ' DEK deve ser restaurado primeiro no servidor de destino. Em seguida, o banco de dados pode ser restaurado como de costume. Para obter mais informações, consulte a documentação do SQL Server standard, em [mover um banco de dados protegido por TDE para outro SQL Server](https://technet.microsoft.com/library/ff773063.aspx).  
  
Certificados usados para criptografar os DEKs devem ser mantidos enquanto houver backups de banco de dados que usá-los. Backups do certificado devem incluir a chave privada do certificado, porque um certificado sem a chave privada não pode ser usado para a restauração de banco de dados. Esses backups de chave privada do certificado são armazenadas em um arquivo separado, protegido por senha que deve ser fornecida para restauração de certificado.  
  
## <a name="restoring-the-master-database"></a>Restaurando o banco de dados mestre  
O banco de dados mestre pode ser restaurado usando **DWConfig**, como parte da recuperação de desastre.  
  
-   Se o nó de controle não for alterado, que é que se o banco de dados mestre é restaurado no dispositivo do mesmo e inalterado do qual foi feito o backup do banco de dados mestre, a DMK e todos os certificados poderão ser lidos sem ação adicional.  
  
-   Se o banco de dados mestre é restaurado em um dispositivo diferente, ou se o nó de controle foi alterado desde o backup do banco de dados mestre, etapas adicionais serão necessárias para regenerar a DMK.  
  
    1.  Abra a DMK:  
  
        ```sql  
        OPEN MASTER KEY DECRYPTION BY PASSWORD = '<password>';  
        ```  
  
    2.  Adicione a criptografia por SMK:  
  
        ```sql  
        ALTER MASTER KEY   
            ADD ENCRYPTION BY SERVICE MASTER KEY;  
        ```  
  
    3.  Reinicie o dispositivo.  
  
## <a name="upgrade-and-replacing-virtual-machines"></a>Atualização e substituição de máquinas virtuais  
Se existir uma DMK no dispositivo em que o Upgrade ou substitua VM foi executada, a senha DMK deve ser fornecida como um parâmetro.  
  
Exemplo de ação de atualização. Substitua `**********` com sua senha DMK.  
  
`setup.exe /Action=ProvisionUpgrade ... DMKPassword='**********'  `  
  
Exemplo da ação para substituir uma máquina virtual.  
  
`setup.exe /Action=ReplaceVM ... DMKPassword='**********'  `  
  
Durante a atualização, se um usuário de banco de dados é criptografado e a senha da DMK não for fornecida, a ação de atualização falhará. Durante a substituição, se a senha correta não for fornecida quando existe uma DMK, a operação irá ignorar a etapa de recuperação DMK. Todas as outras etapas serão concluídas no final da operação de substituição VM, no entanto, a ação reportará a falha no final para indicar que são necessárias etapas adicionais. Nos logs de instalação (localizado em **\ProgramData\Microsoft\Microsoft SQL Server Parallel Data Warehouse\100\Logs\Setup\\\Detail-Setup < carimbo de hora >**), o seguinte aviso será exibido próximo ao final.  
  
`*** WARNING \*\*\* DMK is detected in master database, but could not be recovered automatically! The DMK password was either not provided or is incorrect!  `
  
Execute esses instrução manualmente no PDW e reiniciar o dispositivo depois disso para recuperar a DMK:  
  
```sql
OPEN MASTER KEY DECRYPTION BY PASSWORD = '<DMK password>';  
ALTER MASTER KEY ADD ENCRYPTION BY SERVICE MASTER KEY;  
```
  
Use as etapas na **restaurar banco de dados mestre** de parágrafo para recuperar o banco de dados e, em seguida, reiniciar o dispositivo.  
  
Se a DMK existia antes, mas não foi recuperada após a ação, a seguinte mensagem de erro será gerada quando um banco de dados é consultado.  
  
```sql
Msg 110806;  
A distributed query failed: Database '<db_name>' cannot be opened due to inaccessible files or insufficient memory or disk space. See the SQL Server errorlog for details.
```  
  
## <a name="performance-impact"></a>Impacto de desempenho  
O impacto no desempenho da TDE varia de acordo com o tipo de dados que você tem, como ele é armazenado e o tipo de atividade de carga de trabalho sobre o SQL Server PDW. Quando protegido por TDE, a e/s de leitura e, em seguida, descriptografar os dados ou a criptografia e, em seguida, a gravação de dados é uma atividade com uso intensivo de CPU e terá maior impacto quando outras atividades de uso intensivo de CPU estão ocorrendo ao mesmo tempo. Porque a TDE criptografa `tempdb`, TDE pode afetar o desempenho de bancos de dados que não estão criptografados. Para obter uma ideia precisa de desempenho, você deve testar todo o sistema com a sua atividade de dados e consultas.  
  
## <a name="related-content"></a>Conteúdo relacionado  
Os links a seguir contêm informações gerais sobre como o SQL Server gerencia criptografia. Esses artigos podem ajudar você a entender a criptografia do SQL Server, mas estes artigos não têm informações específicas para o SQL Server PDW e eles discutem os recursos que não estão presentes no SQL Server PDW.  
  
-   [Criptografia do SQL Server](../relational-databases/security/encryption/sql-server-encryption.md)  
  
-   [Hierarquia de criptografia](../relational-databases/security/encryption/encryption-hierarchy.md)  
  
-   [Chaves de criptografia do SQL Server e do banco de dados](../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)  

  
## <a name="see-also"></a>Consulte também  
[ALTERAR BANCO DE DADOS](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)  
[CRIAR CHAVE MESTRA](../t-sql/statements/create-master-key-transact-sql.md)  
[CRIAR CHAVE DE CRIPTOGRAFIA DE BANCO DE DADOS](../t-sql/statements/create-database-encryption-key-transact-sql.md)  
[BACKUP CERTIFICATE](../t-sql/statements/backup-certificate-transact-sql.md)  
[sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
[sp_pdw_database_encryption_regenerate_system_keys](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
[sp_pdw_log_user_data_masking](../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
[sys.certificates](../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)  
[sys.dm_pdw_nodes_database_encryption_keys](../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql.md)  
  
