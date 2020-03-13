---
title: Transparent Data Encryption
description: A TDE (Transparent Data Encryption) para o PDW (Parallel data warehouse) executa a criptografia e a descriptografia de e/s em tempo real dos arquivos de log de dados e de transações e dos arquivos de log de PDW especiais. "
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: e75230ed175c6fbf1b0a2492265bbe12067060ca
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79289744"
---
# <a name="transparent-data-encryption"></a>Criptografia de Dados Transparente
Você pode adotar várias precauções para ajudar a proteger o banco de dados, como a criação de um sistema seguro, a criptografia de ativos confidenciais e a criação de um firewall em torno de servidores de bancos de dados. No entanto, para um cenário no qual a mídia física (como unidades ou fitas de backup) seja roubada, uma parte mal-intencionada pode apenas restaurar ou anexar o banco de dados e procurar os mesmos. Uma solução é criptografar dados confidenciais no banco de dados e proteger as chaves usadas para criptografar os dados com um certificado. Isso impede que alguém sem as chaves use os dados, mas esse tipo de proteção deve ser planejado antecipadamente.  
  
A TDE ( *Transparent Data Encryption* ) executa a criptografia e a descriptografia de e/s em tempo real dos arquivos de log de transações e de dados e dos arquivos de log do PDW especiais. A criptografia usa uma chave de criptografia de banco de dados (DEK), que é armazenada no registro de inicialização do banco de dados para disponibilidade durante a recuperação. O DEK é uma chave simétrica protegida usando um certificado armazenado no banco de dados mestre do SQL Server PDW. A TDE protege os dados “em repouso”, ou seja, os dados e arquivos de log. Fornece a capacidade de se adequar a muitas leis, regulamentos e diretrizes estabelecidos em vários setores. Esse recurso permite que os desenvolvedores de software criptografem dados usando algoritmos de criptografia AES e 3DES sem alterar os aplicativos existentes.  
  
> [!IMPORTANT]  
> O TDE não fornece criptografia para dados que trafegam entre o cliente e o PDW. Para obter mais informações sobre como criptografar dados entre o cliente e o SQL Server PDW, consulte [provisionar um certificado](provision-certificate.md).  
>   
> TDE não criptografa dados enquanto está sendo movido ou está em uso. O tráfego interno entre os componentes do PDW dentro do SQL Server PDW não é criptografado. Os dados armazenados temporariamente nos buffers de memória não são criptografados. Para atenuar esse risco, controle o acesso físico e as conexões com o SQL Server PDW.  
  
Depois de protegido, o banco de dados pode ser restaurado usando o certificado correto.  
  
> [!NOTE]  
> Ao criar um certificado para TDE, você deve fazer o backup imediatamente, junto com a chave privada associada. Se em algum momento o certificado ficar indisponível ou caso você deseje restaurar ou anexar o banco de dados a outro servidor, você precisará dos backups do certificado e da chave privada ou não será possível abrir o banco de dados. O certificado de criptografia deve ser retido até mesmo se o TDE já não estiver habilitado no banco de dados. Mesmo que o banco de dados não seja criptografado, partes do log de transações ainda poderão permanecer protegidas e talvez o certificado seja necessário para algumas operações até a realização do backup completo do banco de dados. Um certificado que excedeu sua data de validade ainda pode ser usado para criptografar e descriptografar dados com TDE.  
  
A criptografia do arquivo de banco de dados é executada em nível de página. As páginas em um banco de dados criptografado são criptografadas antes de serem gravadas no disco e descriptografadas quando lidas na memória. A TDE não aumenta o tamanho do banco de dados criptografado.  
  
A ilustração a seguir mostra a hierarquia de chaves para criptografia TDE:  
  
![Exibe a hierarquia](media/tde-architecture.png "TDE_Architecture")  
  
## <a name="using-tde"></a>Usando Transparent Data Encryption  
Para usar a TDE, execute estes procedimentos. As três primeiras etapas são feitas apenas uma vez, ao preparar SQL Server PDW para dar suporte a TDE.  
  
1.  Crie uma chave mestra no banco de dados mestre.  
  
2.  Use **sp_pdw_database_encryption** para habilitar TDE no SQL Server PDW. Essa operação modifica os bancos de dados temporários para garantir a proteção de futuros data temporários e falhará se for tentada quando houver sessões ativas que tenham tabelas temporárias. **sp_pdw_database_encryption** ativa o mascaramento de dados do usuário em logs do sistema PDW. (Para obter mais informações sobre máscara de dados do usuário em logs do sistema PDW, consulte [sp_pdw_log_user_data_masking](../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md).)  
  
3.  Use [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) para criar uma credencial que possa autenticar e gravar no compartilhamento em que o backup do certificado será armazenado. Se já existir uma credencial para o servidor de armazenamento pretendido, você poderá usar a credencial existente.  
  
4.  No banco de dados mestre, crie um certificado protegido pela chave mestra.  
  
5.  Faça backup do certificado no compartilhamento de armazenamento.  
  
6.  No banco de dados do usuário, crie uma chave de criptografia de banco de dados e proteja-a pelo certificado armazenado no banco de dados mestre.  
  
7.  Use a `ALTER DATABASE` instrução para criptografar o banco de dados usando TDE.  
  
O exemplo a seguir ilustra a criptografia `AdventureWorksPDW2012` do banco de dados usando `MyServerCert`um certificado chamado, criado no SQL Server PDW.  
  
**Primeiro: habilite TDE no SQL Server PDW.** Essa ação é necessária apenas uma vez.  
  
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
  
**Segundo: Crie e faça backup de um certificado no banco de dados mestre.** Essa ação é necessária apenas uma vez. Você pode ter um certificado separado para cada banco de dados (recomendado), ou você pode proteger vários bancos com um certificado.  
  
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
  
**Último: Crie o DEK e use ALTER DATABASE para criptografar um banco de dados de usuário.** Essa ação é repetida para cada banco de dados protegido pelo TDE.  
  
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
  
As operações de criptografia e descriptografia são agendadas em threads em segundo plano por SQL Server. Você pode exibir o status dessas operações usando as exibições de catálogo e de gerenciamento dinâmico na lista que aparece mais adiante neste artigo.  
  
> [!CAUTION]  
> Os arquivos de backup de bancos de dados com TDE habilitada também são criptografados usando a chave de criptografia do banco de dados. Como resultado, quando você restaura esses backups, o certificado que protege a chave de criptografia do banco de dados deve estar disponível. Isso significa que, além de fazer backup do banco de dados, você deve assegurar que os backups dos certificados de servidor sejam mantidos para evitar perda de dados. Se o certificado não estiver mais disponível, haverá perda de dados.  
  
## <a name="commands-and-functions"></a>Comandos e funções  
Os certificados da TDE devem ser criptografados pela chave mestra do banco de dados para serem aceitos pelas instruções a seguir.  
  
A tabela a seguir fornece links e explicações de comandos e funções da TDE.  
  
|Comando ou função|Finalidade|  
|-----------------------|-----------|  
|[CREATE DATABASE ENCRYPTION KEY](../t-sql/statements/create-database-encryption-key-transact-sql.md)|Cria uma chave usada para criptografar um banco de dados.|  
|[ALTERAR CHAVE DE CRIPTOGRAFIA DO BANCO DE DADOS](../t-sql/statements/alter-database-encryption-key-transact-sql.md)|Altera a chave usada para criptografar um banco de dados.|  
|[REMOVER CHAVE DE CRIPTOGRAFIA DO BANCO DE DADOS](../t-sql/statements/drop-database-encryption-key-transact-sql.md)|Remove a chave usada para criptografar um banco de dados.|  
|[ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)|Explica a opção **ALTER DATABASE** usada para habilitar a TDE.|  
  
## <a name="catalog-views-and-dynamic-management-views"></a>Exibições do catálogo e exibições de gerenciamento dinâmico  
A tabela a seguir mostra exibições do catálogo de TDE e exibições de gerenciamento dinâmico.  
  
|Exibição do catálogo ou exibição de gerenciamento dinâmico|Finalidade|  
|-------------------------------------------|-----------|  
|[sys.databases](../relational-databases/system-catalog-views/sys-databases-transact-sql.md)|Exibição do catálogo que exibe informações do banco de dados.|  
|[sys.certificates](../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)|Exibição do catálogo que mostra os certificados em um banco de dados.|  
|[sys.dm_pdw_nodes_database_encryption_keys](../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql.md)|Exibição de gerenciamento dinâmico que fornece informações para cada nó, sobre as chaves de criptografia usadas em um banco de dados e o estado de criptografia de um banco de dados.|  
  
## <a name="permissions"></a>Permissões  
Cada recurso e comando da TDE têm requisitos individuais de permissões, descritos nas tabelas anteriores.  
  
A exibição dos metadados envolvidos com TDE requer `CONTROL SERVER` a permissão.  
  
## <a name="considerations"></a>Considerações  
Quando um exame de recriptografia para uma operação de criptografia de banco de dados está em andamento, as operações de manutenção no banco de dados são desabilitadas.  
  
Você pode encontrar o estado da criptografia de banco de dados usando a exibição de gerenciamento dinâmico **Sys. dm_pdw_nodes_database_encryption_keys** . Para obter mais informações, consulte a seção *exibições de catálogo e exibições de gerenciamento dinâmico* anteriormente neste artigo.  
  
### <a name="restrictions"></a>Restrições  
As operações a seguir não são permitidas `CREATE DATABASE ENCRYPTION KEY`durante `ALTER DATABASE ENCRYPTION KEY`as `DROP DATABASE ENCRYPTION KEY`instruções, `ALTER DATABASE...SET ENCRYPTION` , ou.  
  
-   Descartando o banco de dados.  
  
-   Usando um `ALTER DATABASE` comando.  
  
-   Iniciando um backup de banco de dados.  
  
-   Iniciando uma restauração de banco de dados.  
  
As seguintes operações ou condições impedirão `CREATE DATABASE ENCRYPTION KEY`as `ALTER DATABASE ENCRYPTION KEY`instruções `DROP DATABASE ENCRYPTION KEY`,, `ALTER DATABASE...SET ENCRYPTION` ou.  
  
-   Um `ALTER DATABASE` comando está em execução.  
  
-   Algum backup de dados está sendo executado.  
  
Durante a criação de arquivos de banco de dados, a inicialização instantânea do arquivo não está disponível quando a TDE está habilitada.  
  
### <a name="areas-not-protected-by-tde"></a>Áreas não protegidas por TDE  
TDE não protege tabelas externas.  
  
O TDE não protege as sessões de diagnóstico. Os usuários devem ter cuidado para não consultar os parâmetros confidenciais enquanto as sessões de diagnóstico estiverem em uso. As sessões de diagnóstico que revelam informações confidenciais devem ser descartadas assim que não forem mais necessárias.  
  
Os dados protegidos pelo TDE são descriptografados quando colocados na memória SQL Server PDW. Os despejos de memória são criados quando determinados problemas ocorrem no dispositivo. Os arquivos de despejo representam o conteúdo da memória no momento da aparência do problema e podem conter dados confidenciais em um formato não criptografado. O conteúdo dos despejos de memória deve ser revisado antes que eles sejam compartilhados com outras pessoas.  
  
O banco de dados mestre não é protegido pelo TDE. Apesar de o banco de dados mestre não contiver dado de usuário, ele contém informações como nomes de logon.  
  
### <a name="transparent-data-encryption-and-transaction-logs"></a>Transparent Data Encryption e logs de transação  
Habilitar um banco de dados para usar TDE tem o efeito de zerar a parte restante do log de transações virtuais para forçar o próximo log de transações virtuais. Isso garante que nenhum texto não criptografado seja deixado nos logs de transações depois que o banco de dados for definido para criptografia. Você pode encontrar o status da criptografia do arquivo de log em cada nó do PDW exibindo a `encryption_state` coluna `sys.dm_pdw_nodes_database_encryption_keys` na exibição, como neste exemplo:  
  
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
SQL Server PDW mantém um conjunto de logs destinados à solução de problemas. (Observe que esse não é o log de transações, o log de erros do SQL Server ou o log de eventos do Windows.) Esses logs de atividade do PDW podem conter instruções completas em texto não criptografado, alguns dos quais podem conter dados do usuário. Exemplos típicos são instruções **Insert** e **Update** . A máscara de dados do usuário pode ser ativada ou desativada explicitamente usando **sp_pdw_log_user_data_masking**. Habilitar a criptografia em SQL Server PDW automaticamente ativa o mascaramento de dados do usuário em logs de atividade do PDW para protegê-los. **sp_pdw_log_user_data_masking** também pode ser usado para mascarar instruções quando não estiver usando TDE, mas isso não é recomendado porque reduz significativamente a capacidade da equipe de suporte da Microsoft analisar problemas.  
  
### <a name="transparent-data-encryption-and-the-tempdb-system-database"></a>Transparent Data Encryption e o banco de dados do sistema tempdb  
O banco de dados do sistema tempdb é criptografado quando a criptografia é habilitada usando [sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md). Isso é necessário antes que qualquer banco de dados possa usar TDE. Isso pode ter um efeito de desempenho para bancos de dados não criptografados na mesma instância do SQL Server PDW.  
  
## <a name="key-management"></a>Gerenciamento de chaves  
A DEK (chave de criptografia de banco de dados) é protegida pelos certificados armazenados no banco de dados mestre. Esses certificados são protegidos pela DMK (chave mestra de banco de dados) do banco de dados mestre. O DMK precisa ser protegido pela SMK (chave mestra de serviço) para ser usado para TDE.  
  
O sistema pode acessar as chaves sem exigir intervenção humana (como fornecer uma senha). Se o certificado não estiver disponível, o sistema produzirá um erro explicando que o DEK não pode ser descriptografado até que o certificado apropriado esteja disponível.  
  
Ao mover um banco de dados de um dispositivo para outro, o certificado usado para proteger seu ' DEK ' deve ser restaurado primeiro no servidor de destino. Em seguida, o banco de dados pode ser restaurado como de costume. Para obter mais informações, consulte a documentação padrão do SQL Server, em [mover um banco de dados protegido por TDE para outro SQL Server](https://technet.microsoft.com/library/ff773063.aspx).  
  
Os certificados usados para criptografar DEKs devem ser retidos desde que haja backups de banco de dados que os utilizem. Os backups de certificado devem incluir a chave privada do certificado, porque sem a chave privada, um certificado não pode ser usado para a restauração do banco de dados. Esses backups de chave privada de certificado são armazenados em um arquivo separado, protegido por uma senha que deve ser fornecida para a restauração do certificado.  
  
## <a name="restoring-the-master-database"></a>Restaurando o banco de dados mestre  
O banco de dados mestre pode ser restaurado usando **DWConfig**, como parte da recuperação de desastre.  
  
-   Se o nó de controle não foi alterado, ou seja, se o banco de dados mestre for restaurado no mesmo dispositivo e não alterado do qual o backup do banco de dados mestre foi obtido, o DMK e todos os certificados serão legíveis sem ação adicional.  
  
-   Se o banco de dados mestre for restaurado em um dispositivo diferente, ou se o nó de controle tiver sido alterado desde o backup do banco de dados mestre, serão necessárias etapas adicionais para gerar novamente o DMK.  
  
    1.  Abra o DMK:  
  
        ```sql  
        OPEN MASTER KEY DECRYPTION BY PASSWORD = '<password>';  
        ```  
  
    2.  Adicione a criptografia por SMK:  
  
        ```sql  
        ALTER MASTER KEY   
            ADD ENCRYPTION BY SERVICE MASTER KEY;  
        ```  
  
    3.  Reinicie o dispositivo.  
  
## <a name="upgrade-and-replacing-virtual-machines"></a>Atualizar e substituir máquinas virtuais  
Se um DMK existir no dispositivo no qual a VM de atualização ou substituição foi executada, a senha do DMK deverá ser fornecida como um parâmetro.  
  
Exemplo da ação de atualização. Substitua `**********` pela sua senha do DMK.  
  
`setup.exe /Action=ProvisionUpgrade ... DMKPassword='**********'`  
  
Exemplo da ação para substituir uma máquina virtual.  
  
`setup.exe /Action=ReplaceVM ... DMKPassword='**********'`  
  
Durante a atualização, se um banco de usuários do usuário estiver criptografado e a senha DMK não for fornecida, a ação de atualização falhará. Durante a substituição, se a senha correta não for fornecida quando existir uma DMK, a operação ignorará a etapa de recuperação DMK. Todas as outras etapas serão concluídas no final da ação substituir VM, no entanto, a ação relatará falha no final para indicar que etapas adicionais são necessárias. Nos logs de instalação (localizados em **\ProgramData\Microsoft\Microsoft SQL Server Parallel Data Warehouse\100\Logs\Setup\\<carimbo de hora> \detail-setup**), o seguinte aviso será mostrado próximo ao final.  
  
`*** WARNING \*\*\* DMK is detected in master database, but could not be recovered automatically! The DMK password was either not provided or is incorrect!`
  
Execute essas instruções manualmente no PDW e reinicie o dispositivo depois disso para recuperar o DMK:  
  
```sql
OPEN MASTER KEY DECRYPTION BY PASSWORD = '<DMK password>';  
ALTER MASTER KEY ADD ENCRYPTION BY SERVICE MASTER KEY;  
```
  
Use as etapas no parágrafo **restaurando o banco de dados mestre** para recuperar o banco de dados e reinicie o dispositivo.  
  
Se o DMK existia antes, mas não foi recuperado após a ação, a seguinte mensagem de erro será gerada quando um banco de dados for consultado.  
  
```sql
Msg 110806;  
A distributed query failed: Database '<db_name>' cannot be opened due to inaccessible files or insufficient memory or disk space. See the SQL Server errorlog for details.
```  
  
## <a name="performance-impact"></a>Impacto do Desempenho  
O impacto no desempenho do TDE varia de acordo com o tipo de dados que você tem, como ele é armazenado e o tipo de atividade de carga de trabalho no SQL Server PDW. Quando protegido por TDE, a e/s de leitura e descriptografia de dados ou a criptografia e a gravação de dados é uma atividade intensiva de CPU e terá mais impacto quando outras atividades com uso intensivo de CPU estiverem ocorrendo ao mesmo tempo. Como o TDE criptografa `tempdb`, o TDE pode afetar o desempenho dos bancos de dados que não estão criptografados. Para obter uma ideia precisa do desempenho, você deve testar todo o sistema com os dados e a atividade de consulta.  
  
## <a name="related-content"></a>Conteúdo relacionado  
Os links a seguir contêm informações gerais sobre como SQL Server gerencia a criptografia. Esses artigos podem ajudá-lo a entender SQL Server criptografia, mas esses artigos não têm informações específicas para SQL Server PDW e discutem recursos que não estão presentes no SQL Server PDW.  
  
-   [Criptografia do SQL Server](../relational-databases/security/encryption/sql-server-encryption.md)  
  
-   [Hierarquia de criptografia](../relational-databases/security/encryption/encryption-hierarchy.md)  
  
-   [Chaves de criptografia de banco de dados SQL Server e](../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)  

  
## <a name="see-also"></a>Consulte Também  
[ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)  
[CREATE MASTER KEY](../t-sql/statements/create-master-key-transact-sql.md)  
[CREATE DATABASE ENCRYPTION KEY](../t-sql/statements/create-database-encryption-key-transact-sql.md)  
[BACKUP CERTIFICATE](../t-sql/statements/backup-certificate-transact-sql.md)  
[sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
[sp_pdw_database_encryption_regenerate_system_keys](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
[sp_pdw_log_user_data_masking](../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
[sys.certificates](../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)  
[sys.dm_pdw_nodes_database_encryption_keys](../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql.md)  
  
