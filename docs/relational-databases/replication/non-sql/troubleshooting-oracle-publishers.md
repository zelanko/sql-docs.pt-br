---
title: Solução de problemas de Publicadores Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], troubleshooting
- troubleshooting [SQL Server replication], Oracle publishing
ms.assetid: be94f1c1-816b-4b1d-83f6-2fd6f5807ab7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3edd60a47ac4cebcdea3f70a0658ce837e3d63ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68095654"
---
# <a name="troubleshooting-oracle-publishers"></a>Solucionando problemas de Publicadores Oracle
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico lista diversos problemas que poderiam surgir ao configurar e usar um Publicador Oracle.  
  
## <a name="an-error-is-raised-regarding-oracle-client-and-networking-software"></a>É gerado um erro relativo ao software de rede e de cliente Oracle  
 A conta sob a qual o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é executado no Distribuidor deve receber permissões de leitura e execução para o diretório (e todos os subdiretórios) em que o software de rede cliente Oracle está instalado. Se as permissões não forem concedidas ou os componentes de cliente Oracle não estiverem adequadamente instalados, você receberá a seguinte mensagem de erro:  
  
 "Falha na conexão ao servidor com [Microsoft OLE DB Provider for Oracle]. Cliente Oracle e componentes de rede não foram localizados. Esses componentes são fornecidos pela Oracle Corporation e são parte da instalação de software de cliente Oracle Versão 7.3.3 ou posterior. O provedor está incapaz de funcionar até que esses componentes estejam instalados."  
  
 Se um cliente Oracle apropriado houver sido instalado no Distribuidor, certifique-se de que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] foi interrompido e reiniciado depois que a instalação do cliente estiver concluída. Isso é requerido para que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] reconheça os componentes de cliente.  
  
 Se você houver se certificado de que as permissões foram concedidas e que os componentes foram instalados corretamente, mas esse erro persiste, verifique se as configurações de registro em HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDTC\MTxOCI estão corretas:  
  
-   Para Oracle 10g, as configurações corretas são  
  
    -   OracleOciLib = oci.dll  
  
    -   OracleSqlLib = orasql10.dll  
  
    -   OracleXaLib = oraclient10.dll  
  
-   Para Oracle 9i, as configurações corretas são  
  
    -   OracleOciLib = oci.dll  
  
    -   OracleSqlLib = orasql9.dll  
  
    -   OracleXaLib = oraclient9.dll  
  
## <a name="the-sql-server-distributor-cannot-connect-to-the-oracle-database-instance"></a>O Distribuidor do SQL Server não pode se conectar à instância do banco de dados Oracle  
 Se o Distribuidor do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não pode se conectar ao Publicador Oracle, certifique-se de que:  
  
-   O software Oracle necessário esteja instalado no Distribuidor.  
  
-   O banco de dados de Oracle esteja online e você possa conectar-se a ele usando uma ferramenta como SQL*Plus.  
  
-   A replicação de logon usada para se conectar ao Publicador Oracle tenha permissões adequadas. Para obter mais informações, consulte [Configure an Oracle Publisher](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md) (Configurar um publicador do Oracle).  
  
-   Os nomes TNS definidos durante a configuração de Publicador Oracle estejam listados no arquivo tnsnames.ora.  
  
-   O Oracle Home e o caminho corretos estejam sendo usados. Mesmo se você tiver um conjunto de binários Oracle instalados no Distribuidor do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , certifique-se de que as variáveis do ambiente relacionadas ao Oracle Home tenham sido adequadamente configuradas. Se você alterar valores de variáveis do ambiente, deverá parar e reiniciar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para que a alteração entre em vigor.  
  
 Para obter maiores informações sobre como configurar e testar a conectividade, consulte “Instalando e configurando software de rede de cliente Oracle no Distribuidor do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]“, em [Configurar um Publicador Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
## <a name="the-oracle-publisher-is-associated-with-another-distributor"></a>O Publicador Oracle está associado a outro Distribuidor  
 Um Publicador Oracle só pode estar associado a um Distribuidor do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Se um Distribuidor diferente estiver associado ao Publicador Oracle, ele deve ser descartado antes que o outro Distribuidor possa ser usado. Se o Distribuidor não for descartado primeiro, você receberá uma das seguintes mensagens de erro:  
  
-   “Instância do servidor Oracle ' \<*OraclePublisherName*>' foi configurado anteriormente para usar '\<*SQLServerDistributorName*>' como Distribuidor. Para começar a usar '\<*NewSQLServerDistributorName*>' como Distribuidor, você deve remover a configuração de replicação atual na instância de servidor Oracle, o que excluirá todas as publicações nessa instância de servidor."  
  
-   “Servidor Oracle '\<*OracleServerName*>' já está definido como publicador '\<*OraclePublisherName*>' no distribuidor '\<*SQLServerDistributorName*>. *\<DistributionDatabaseName>* '. Remova o publicador ou o sinônimo público ' *\<SynonymName>* ' para recriar.”  
  
 Quando um Publicador Oracle é descartado, os objetos de replicação no banco de dados Oracle são automaticamente limpos. No entanto, a limpeza manual dos objetos de replicação Oracle é necessária em alguns casos. Para limpar manualmente objetos de replicação Oracle criados por replicação:  
  
1.  Conecte-se ao Publicador Oracle com permissões DBA.  
  
2.  Emita o comando SQL `DROP PUBLIC SYNONYM MSSQLSERVERDISTRIBUTOR;`.  
  
3.  Emita o comando SQL `DROP USER <replication_administrative_user_schema>``CASCADE;`.  

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="sql-server-error-21663-is-raised-regarding-the-lack-of-a-primary-key"></a>É gerado o erro SQL Server 21663, relativo à falta de uma chave primária  
 Os artigos em publicações transacionais devem ter uma chave primária válida. Se não tiverem uma chave primária válida, você receberá a seguinte mensagem de erro ao tentar adicionar um artigo:  
  
 “Nenhuma chave primária válida foi encontrada para a tabela de origem [\<*TableOwner*>].[\<*TableName*>]”  
  
 Para obter informações sobre requisitos para chaves primárias, consulte a seção "Índices e Restrições Exclusivos" no tópico [Design Considerations and Limitations for Oracle Publishers](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md).  
  
## <a name="sql-server-error-21642-is-raised-regarding-a-duplicate-linked-server-login"></a>É gerado o erro SQL Server 21642, relativo a um logon de servidor vinculado duplicado  
 Quando um Publicador Oracle é configurado inicialmente, uma entrada de servidor vinculado é criada para a conexão entre o Publicador e o Distribuidor. O servidor vinculado tem o mesmo nome que o serviço TNS Oracle. Se você tentar criar um servidor vinculado com o mesmo nome, a seguinte mensagem de erro será mostrada:  
  
 "Os publicadores heterogêneos exigem um servidor vinculado. Um servidor vinculado chamado ' *\<LinkedServerName>* ' já existe. Remova o servidor vinculado ou escolha um nome de publicador diferente."  
  
 Esse erro pode ocorrer se você tentar criar o servidor vinculado diretamente ou se tiver previamente descartado a relação entre o Publicador Oracle e o Distribuidor do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e estiver agora tentando reconfigurá-lo. Se receber esse erro ao tentar reconfigurar o Publicador, remova o servidor vinculado com [sp_dropserver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md).  
  
 Se você precisar se conectar ao Publicador Oracle usando uma conexão de servidor vinculado, crie outro nome de serviço TNS e use esse nome ao chamar [sp_addlinkedserver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md). Para obter informações sobre como criar nomes de serviço TNS, consulte a documentação do Oracle.  
  
## <a name="sql-server-error-21617-is-raised"></a>É gerado o erro SQL Server 21617  
 A publicação Oracle usa o aplicativo SQL*PLUS Oracle para baixar o pacote de código de suporte do Publicador para o banco de dados Oracle. Antes de tentar configurar o Publicador Oracle, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] verifica se SQL\*PLUS está acessível através do caminho do sistema no Distribuidor. Se o SQL\*PLUS não puder ser carregado, a seguinte mensagem de erro será mostrada:  
  
 "Não é possível executar o SQL*PLUS. Certifique-se de que uma versão atual do código de cliente Oracle esteja instalada no distribuidor."  
  
 Tente localizar o SQL\*PLUS no Distribuidor. Para uma instalação de cliente Oracle 10g, o nome desse executável é sqlplus.exe. Normalmente, ele é instalado em %ORACLE_HOME%/bin. Para verificar se o caminho do SQL\*PLUS aparece no caminho do sistema, examine o valor da variável do sistema **Caminho**:  
  
1.  Clique com o botão direito do mouse em **Meu Computador**e, em seguida, clique em **Propriedades**.  
  
2.  Clique na guia **Avançado** e clique em **Variáveis de Ambiente**.  
  
3.  Na caixa de diálogo **Variáveis de Ambiente** , na lista **Variáveis de Sistema** , selecione a variável **Caminho** e, então, clique em **Editar**.  
  
4.  Na caixa de diálogo **Editar Variável de Sistema** : se o caminho para a pasta que contém sqlplus.exe não estiver presente na caixa de texto **Valor de Variável** , edite a cadeia para incluí-lo.  
  
5.  Clique em **OK** em cada caixa de diálogo aberta para sair e salvar as alterações.  
  
 Se você não puder localizar sqlplus.exe no Distribuidor, instale uma versão atual do software de cliente Oracle no Distribuidor. Para obter mais informações, consulte [Configure an Oracle Publisher](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md) (Configurar um publicador do Oracle).  
  
## <a name="sql-server-error-21620-is-raised"></a>É gerado o erro SQL Server 21620  
 Se você estiver se conectando a um banco de dados Oracle anterior à versão 8.1, a publicação Oracle requer que o software de cliente Oracle instalado no Distribuidor seja da versão 9. Se você estiver se conectando a um banco de dados Oracle que seja da versão 8.1 ou posterior, recomendamos que o software de cliente Oracle seja da versão 10 ou posterior.  
  
 Antes de tentar configurar o Publicador Oracle, a publicação Oracle verifica se a versão de SQL*PLUS acessível através do caminho do sistema no Distribuidor é a versão 9 ou posterior. Caso não seja, a seguinte mensagem de erro é mostrada:  
  
 A versão de SQL*PLUS acessível através da variável Caminho do Sistema não é atual o suficiente para oferecer suporte à publicação Oracle. Certifique-se de que uma versão atual do código de cliente Oracle esteja instalada no distribuidor."  
  
 Se você tem múltiplas versões de software de cliente Oracle instaladas no Distribuidor, certifique-se de que a versão mais recente seja pelo menos a versão 9 e que a variável Caminho do Sistema se refira primeiro a esta versão (referências a outras versões podem constar, desde que a mais recente apareça primeiro). Para obter mais informações sobre edição da variável Caminho do Sistema, consulte a seção "É gerado o erro SQL Server 21617", acima, neste tópico.  
  
## <a name="sql-server-error-21624-or-error-21629-is-raised"></a>É gerado o erro SQL Server 21624 ou 21629  
 Para Distribuidores de 64 bits, a publicação Oracle usa o Provedor OLEDB Oracle para Oracle (OraOLEDB.Oracle). Certifique-se de que o provedor OLEDB Oracle esteja instalado e registrado no Distribuidor. Se o provedor não estiver instalado e registrado, uma ou ambas as seguintes mensagens de erro serão mostradas:  
  
-   "Não foi possível localizar o provedor OLEDB Oracle, OraOLEDB.Oracle, registrado no distribuidor '%s.' Certifique-se de que uma versão atual do provedor OLEDB Oracle esteja instalada e registrada no distribuidor."  
  
-   "A chave do Registro CLSID que indica que o Provedor OLEDB Oracle para Oracle, OraOLEDB.Oracle, foi registrado e não está presente no distribuidor. Certifique-se de que o provedor OLEDB Oracle esteja instalado e registrado no distribuidor."  
  
 Se você estiver usando software de cliente Oracle versão 10g, o provedor é OraOLEDB10.dll; para a versão 9i, é OraOLEDB.dll. O provedor é instalado em %ORACLE_HOME%\BIN (por exemplo, C:\oracle\product\10.1.0\Client_1\bin). Se você verificar que o provedor OLEDB Oracle não está instalado no Distribuidor, instale-o a partir do disco de instalação de software de cliente Oracle fornecido pela Oracle. Para obter mais informações, consulte [Configure an Oracle Publisher](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md) (Configurar um publicador do Oracle).  
  
 Se o provedor OLEDB Oracle estiver instalado, certifique-se de que esteja registrado. Para registrar o provedor DLL, execute o seguinte comando a partir do diretório em que o DLL está instalado e, então, pare e reinicie a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
1.  `regsvr32 OraOLEDB10.dll` ou `regsvr32 OraOLEDB.dll`.  
  
## <a name="sql-server-error-21626-or-error-21627-is-raised"></a>É gerado o erro SQL Server 21626 ou 21627  
 Para verificar se o ambiente de publicação Oracle está adequadamente configurado, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tenta conectar o Publicador Oracle com as credenciais de logon que você especificou durante a configuração. Se o Distribuidor do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não puder conectar-se ao Publicador Oracle, a seguinte mensagem de erro será mostrada:  
  
-   "Não foi possível conectar-se ao servidor do banco de dados Oracle '%s' usando o provedor OLEDB Oracle OraOLEDB.Oracle."  
  
 Se essa mensagem de erro for mostrada, verifique a conectividade ao banco de dados Oracle executando SQL*PLUS diretamente usando o mesmo logon e senha especificados durante a configuração do Publicador Oracle. Para obter mais informações, consulte a seção "O Distribuidor do SQL Server não pode se conectar à instância de banco de dados Oracle", acima, neste tópico.  
  
## <a name="sql-server-error-21628-is-raised"></a>É gerado o erro SQL Server 21628  
 Para Distribuidores de 64 bits, a publicação Oracle usa o Provedor OLEDB Oracle para Oracle (OraOLEDB.Oracle). O[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cria uma entrada de registro para permitir que o provedor Oracle seja executado em processo com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se houver um problema ao ler ou gravar essa entrada de registro, a seguinte mensagem de erro será mostrada:  
  
 "Não foi possível atualizar o registro de distribuidor '%s' para permitir que o provedor OLEDB Oracle OraOLEDB.Oracle seja executado em processo com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Certifique-se de que o logon atual esteja autorizado para modificar chaves de registro pertencentes ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ."  
  
 A publicação Oracle requer que a entrada de registro exista e seja definida como **1** para Distribuidores de 64 bits. Se a entrada não existir, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tentará criá-la. Se a entrada existe, mas estiver definida como **0**, a configuração não será alterada; haverá falha na configuração do Publicador Oracle.  
  
 Para exibir e modificar a configuração de registro:  
  
1.  Clique em **Iniciar**e em **Executar**.  
  
2.  Na caixa de diálogo **Executar** , digite **regedit**e, então, clique em **OK**.  
  
3.  Navegue até HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\ *\<InstanceName>* \Providers.  
  
     Incluída em Provedores deve haver uma pasta nomeada OraOLEDB.Oracle. Dentro dessa pasta deve haver o nome do valor DWORD **AllowInProcess**, com valor **1**.  
  
4.  Se você verificar que **AllowInProcess** está definido como **0**, atualize a entrada de registro para **1**:  
  
    1.  Clique com o botão direito do mouse na entrada e, então, clique em **Modificar**.  
  
    2.  Na caixa de diálogo **Editar Cadeia** , digite **1** no campo **Dados do Valor** .  
  
## <a name="sql-server-error-21684-is-raised"></a>É gerado o erro SQL Server 21684  
 Se a conta de usuário administrativo não tiver privilégios suficientes, a seguinte mensagem de erro será mostrada:  
  
 "As permissões associadas com o logon de administrador para o publicador Oracle '% s' não é suficiente."  
  
 Para verificar as permissões concedidas ao usuário, execute a seguinte consulta: `SELECT * from session_privs`. A saída deve ser semelhante ao seguinte:  
  
 `PRIVILEGE`  
  
 `------------------`  
  
 `CREATE SESSION`  
  
 `CREATE TABLE`  
  
 `CREATE PUBLIC SYNONYM`  
  
 `DROP PUBLIC SYNONYM`  
  
 `CREATE VIEW`  
  
 `CREATE SEQUENCE`  
  
 `CREATE PROCEDURE`  
  
 `CREATE TRIGGER`  
  
## <a name="you-encounter-permissions-issues-for-the-replication-user-schema"></a>Você encontra problemas de permissões para o esquema de usuário de replicação  
 O esquema de usuário de replicação deve ter as permissões descritas em “Criando o esquema de usuário manualmente” em [Configurar um Publicador Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
## <a name="oracle-error-ora-01000"></a>Erro Oracle ORA-01000  
 A replicação usa cursores no Publicador Oracle durante o processo de adicionar artigos a uma publicação. É possível exceder o número máximo de cursores disponíveis no Publicador durante esse processo. Se isso acontecer, o seguinte erro será gerado:  
  
 "ORA-01000: máximo de cursores abertos excedido"  
  
 Para evitar esse problema, certifique-se de que a configuração **max_open_cursors** no banco de dados Oracle esteja definida como um número suficientemente alto (pelo menos 1000). Para obter mais informações sobre essa configuração, consulte a documentação Oracle.  
  
## <a name="oracle-error-ora-01555"></a>Erro Oracle ORA-01555  
 O seguinte erro de banco de dados Oracle não está relacionado à replicação instantânea; está relacionado ao modo como o Oracle constrói exibições de dados de leitura consistente:  
  
 "ORA-01555: Instantâneo muito antigo"  
  
 Usando objetos conhecidos como segmentos de reversão, o Oracle constrói exibições de dados de leitura consistente no point-in-time em que uma instrução SQL é emitida. Um erro "instantâneo muito antigo" pode ocorrer quando uma informação de reversão é substituída por outras sessões simultâneas. Antes do Oracle 9i, o método recomendado para reduzir a frequência desse erro era aumentar o tamanho e/ou o número de segmentos de reversão e atribuir grandes transações a um segmento de reversão específico.  
  
 No Oracle 9i, a Oracle introduziu o conceito de espaço de tabela UNDO, que substitui o segmento de reversão. Para prevenir o erro "instantâneo muito antigo" no Oracle 9i, recomenda-se:  
  
-   Criar um espaço de tabela UNDO com uma quantidade adequada de espaço livre.  
  
-   Definir a garantia de retenção no espaço de tabela (Oracle 10G e maior).  
  
-   Configurar os parâmetros de inicialização Oracle UNDO_MANAGEMENT e UNDO_RETENTION.  
  
 Para obter detalhes adicionais sobre como evitar o erro "instantâneo muito antigo", consulte a documentação do Oracle.  
  
## <a name="oracle-error-ora-22285"></a>Erro Oracle ORA-22285  
 Se uma tabela inclui uma coluna BFILE, os dados para a coluna são armazenados no sistema de arquivos. A conta de usuário administrativo da replicação deve dispor de acesso ao diretório no qual os dados estão armazenados, usando a seguinte sintaxe:  
  
 `GRANT READ ON DIRECTORY <directory_name> TO <replication_administrative_user_schema>`  
  
 Se o acesso não for concedido, o seguinte erro será gerado pelo Log Reader Agent:  
  
 "ORA-22285: diretório ou arquivo inexistente para a operação FILEOPEN"  
  
## <a name="changes-are-made-that-require-reconfiguration-of-the-publisher"></a>São feitas alterações que requerem reconfiguração do publicador  
 Alterações às tabelas de metadados de replicação ou a procedimentos requerem que você descarte e reconfigure o Publicador. Para reconfigurar o Publicador, você deve descartar e configurá-lo novamente usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], Transact-SQL ou RMO. Para obter informações sobre como configurar o Publicador, consulte [Configurar um Publicador Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
 **Para descartar um Publicador Oracle (** SQL Server Management Studio **)**  
  
1.  Conecte-se ao Distribuidor para o Publicador Oracle no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] e expanda o nó do servidor.  
  
2.  Clique com o botão direito do mouse na pasta **Replicação**e, então, clique em **Propriedades do Distribuidor**.  
  
3.  Na página **Publicadores** da caixa de diálogo **Propriedades do Distribuidor** , desmarque a caixa de seleção para o Publicador Oracle.  
  
4.  Clique em **OK**.  
  
 **Para descartar um Publicador Oracle (Transact-SQL)**  
  
-   Execute **sp_dropdistpublisher**. Para obter mais informações, consulte [sp_dropdistpublisher &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar um Publicador Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Visão geral da publicação do Oracle](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
