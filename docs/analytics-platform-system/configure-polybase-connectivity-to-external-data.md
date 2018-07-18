---
title: Configurar a conectividade do PolyBase - Analytics Platform System | Microsoft Docs
description: Explica como configurar o PolyBase no Parallel Data Warehouse para se conectar ao Hadoop ou no Microsoft Azure storage blob fontes de dados externas. Usar o PolyBase para executar consultas que integram dados de várias fontes, incluindo Hadoop, o armazenamento de BLOBs do Azure e Parallel Data Warehouse.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 26eeffb1d2a27ee49f01114b015ab4051b145d64
ms.sourcegitcommit: 731c5aed039607a8df34c63e780d23a8fac937e1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/07/2018
ms.locfileid: "37909866"
---
# <a name="configure-polybase-connectivity-to-external-data"></a>Configurar a conectividade do PolyBase para dados externos
Explica como configurar o PolyBase no Parallel Data Warehouse para se conectar ao Hadoop ou no Microsoft Azure storage blob fontes de dados externas. Usar o PolyBase para executar consultas que integram dados de várias fontes, incluindo Hadoop, o armazenamento de BLOBs do Azure e Parallel Data Warehouse.  
  
### <a name="to-configure-connectivity"></a>Para configurar a conectividade  
  
1.  Abra uma ferramenta de consulta, como sqlcmd ou o SQL Server Data Tools (SSDT) e executar sp_configure para exibir as configurações atuais de 'conectividade do hadoop'.  
  
    ![configuração de conectividade do Hadoop](./media/configure-polybase-connectivity-to-external-data/APS_PDW_sp_configure.png "APS_PDW_sp_configure")  
  
2.  Decida qual configuração você necessidade e se você precisa alterar a configuração atual de conectividade do Hadoop. Essa opção se aplica a toda a região PDW do SQL Server. Para obter uma lista completa das definições de configuração e versões, consulte [sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
3.  Para alterar a configuração de conectividade do hadoop, execute sp_configure com RECONFIGURE. Aqui estão alguns exemplos.  
  
    ```sql  
    --Enable connectivity to Hortonworks Data Platform for Windows Server (HDP) or HDInsight’s Microsoft Azure blob storage  
    EXEC sp_configure 'hadoop connectivity', 4;   
    RECONFIGURE;  
  
    -- Enable connectivity to Hortonworks Data Platform (HDP)for Linux   
    EXEC sp_configure 'hadoop connectivity', 5;   
    RECONFIGURE;  
  
    -- Enable connectivity to Cloudera CDH for Linux   
    EXEC sp_configure 'hadoop connectivity', 3;   
    RECONFIGURE;  
  
    -- Disable the Hadoop connectivity option   
    EXEC sp_configure 'hadoop connectivity', 0;  
    RECONFIGURE;  
    ```  
  
    Sp_configure em execução com RECONFIGURE define o valor de config. Reiniciar a região é necessária para definir o valor de execução. Uma vez que uma reinicialização também é necessária após a parada seguinte, você não precisa fazer a reinicialização até que a próxima etapa, que altera o core-site.  
  
4.  Para habilitar o armazenamento de BLOBs do Microsoft Azure como uma fonte de dados externa, adicione um ou mais chaves de acesso de conta de armazenamento Microsoft Azure ao arquivo de core-site. XML do PDW. Para adicionar uma chave:  
  
    1.  Encontre seu nome de conta de armazenamento do Microsoft Azure. Para exibir suas contas de armazenamento, o logon para o[portal do Azure](https://portal.azure.com) e clique em **contas de armazenamento (clássico)**.  
  
        ![Nome de conta de armazenamento do Windows Azure](./media/configure-polybase-connectivity-to-external-data/APS_PDW_AzureStorageAccountName.png "APS_PDW_AzureStorageAccountName")  
  
    2.  Encontre sua chave de acesso da conta de armazenamento do Azure. Para fazer isso, clique em seu nome de conta de armazenamento e, na folha configurações, clique em **chaves**. Isso mostra as chaves de armazenamento e o nome da conta.  
  
        ![Chaves de acesso da conta de armazenamento do Windows Azure](./media/configure-polybase-connectivity-to-external-data/APS_PDW_AzureStorageAccountAccessKey.png "APS_PDW_AzureStorageAccountAccessKey")  
  
    3.  Abra uma conexão de área de trabalho remota ao nó de controle do PDW.  
  
    4.  Abra o arquivo C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf\core-site.xml.  
  
    5.  Adicione a seguinte propriedade com atributos de nome e valor para o core-site.  
  
        ```xml  
        <property>  
          <name>fs.azure.account.key.<your storage account name>.blob.core.windows.net</name>  
          <value><your storage account access key></value>  
        </property>  
        ```  
  
        Este exemplo usa a chave de acesso e o nome de conta mostrada anteriormente.  
  
        ```xml  
        <property>  
          <name>fs.azure.account.key.CustomerX.blob.core.windows.net</name>  
          <value>yyeTfCxxxxxxxxQ5WdnapXw77W+FwzHUhX/p/f26fIpnNFGtewzyRN90e1/qmTOl1xxxxxxxxa0goG71LsNcw==</value>  
        </property>  
        ```  
  
        > [!CAUTION]  
        > Tome precauções de segurança antes de armazenar a chave de acesso no core-site. Qualquer usuário que tenha a permissão CONTROL SERVER ou ALTER ANY EXTERNAL DATA SOURCE pode criar uma fonte de dados externa que acesse essa conta. Depois de criar a fonte de dados externa, todos os usuários do SQL Server PDW com permissões de CREATE TABLE podem criar uma tabela externa que acessa a conta de armazenamento. Os usuários podem acessar dados da conta e consomem recursos na conta.  
  
    6.  Salve as alterações ao core-site.  
  
5.  Adicione propriedade de classpath e os valores para o arquivo yarn-site. XML.  
  
    Ignore esta etapa se você estiver se conectando a um 1.3 Hadoop externo.  
  
    Começando com o Hadoop 2.0, o arquivo de yarn-site. XML contém as definições de configuração para o framework do YARN do Hadoop. Esse arquivo está localizado no nó de controle, sob **C:\program files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf\\**.  
  
    Para executar consultas do PolyBase em um Cluster de 2.0 externa do Hadoop no Windows ou Linux, você precisará configurar a propriedade de classpath e os valores sejam consistentes com as configurações de yarn-site. XML em seu Hadoop Cluster externo. Essa configuração é necessária mesmo que seu Hadoop Cluster externo usa as configurações padrão.  
  
    Exemplo de configurações padrão:  
  
    ```xml  
    <property>  
        <name>yarn.application.classpath</name>  
        <value>  
          %HADOOP_CONF_DIR%,  
          %HADOOP_COMMON_HOME%/share/hadoop/common/*,  
          %HADOOP_COMMON_HOME%/share/hadoop/common/lib/*,  
          %HADOOP_HDFS_HOME%/share/hadoop/hdfs/*,  
          %HADOOP_HDFS_HOME%/share/hadoop/hdfs/lib/*,  
          %HADOOP_YARN_HOME%/share/hadoop/yarn/*,  
          %HADOOP_YARN_HOME%/share/hadoop/yarn/lib/*  
         </value>  
      </property>  
    ```  
  
    Quando qualquer propriedade é definida no yarn-site. XML, o PolyBase usa essas configurações de propriedade quando ele executa consultas em relação a Hadoop. Se você planeja executar consultas do PolyBase em relação ao Blob de armazenamento do Azure e um Cluster de 2.0 externa do Hadoop no Windows, deve haver consistência entre todos os arquivos yarn-site. XML, caso contrário haverá falha nas consultas do PolyBase.  
   
6.  Reinicie a região PDW. Para fazer isso, use a ferramenta Configuration Manager. Ver [iniciar o Configuration Manager &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md).  
  
7.  Verifique se as configurações de segurança para conexões do Hadoop. Se o **autenticação fraca** no Hadoop lado é habilitada usando `dfs.permission = true`, você deve criar um usuário do Hadoop **pdw_user** conceda leitura completa e permissões de gravação para este usuário. SQL Server PDW e as chamadas correspondentes do SQL Server PDW sempre são emitidas como **pdw_user**.  Isso é um nome de usuário fixa e não pode ser alterado nesta versão de conectividade do Hadoop e a versão do SQL Server PDW. Se a segurança no Hadoop é desabilitada usando `dfs.permission = false`, em seguida, nenhuma ação adicional precisa ser executada.  
  
8.  Decida quais usuários podem criar uma fonte de dados externa para o armazenamento de BLOBs do Microsoft Azure. Dê o nome da conta de armazenamento a cada um desses usuários e também **ALTER ANY EXTERNAL DATA SOURCE** ou **CONTROL SERVER** permissão.  
  
9. Para conexões do Hadoop, decida quais usuários podem criar uma fonte de dados externa para o Hadoop. Dê a cada um desses usuários o número de porta e endereço IP de cada nó de nome do Hadoop e dar-lhes **ALTER ANY EXTERNAL DATA SOURCE** ou **CONTROL SERVER** permissão.  
  
10. Conectar-se para o WASB também requer o encaminhamento de DNS a ser configurado no dispositivo. Para configurar o encaminhamento de DNS, consulte [usar um encaminhador DNS para resolver nomes de DNS não são de dispositivo &#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md).  
  
Os usuários autorizados agora podem criar fontes de dados externas, formatos de arquivo externo e tabelas externas. Eles podem usá-los para integrar dados de várias fontes, incluindo Hadoop, armazenamento de BLOBs do Microsoft Azure e SQL Server PDW.  

## <a name="kerberos-configuration"></a>Configuração do Kerberos  
Observe que quando PolyBase se autentica em um cluster protegido por Kerberos, a configuração de Hadoop deve ser definida para autenticação. Isso faz com que a comunicação de dados entre os nós do Hadoop não seja criptografada. 

 Para se conectar a um cluster Hadoop protegido por Kerberos [usando MIT KDC]:
   
  
1.  Localize o diretório de configuração do Hadoop no caminho de instalação no nó de controle:  
  
    ```  
    C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf
    ```  
  
2.  Localize o valor de configuração do lado do Hadoop nas chaves de configuração listadas na tabela. (No computador do Hadoop, localize os arquivos no diretório da configuração do Hadoop.)  
  
3.  Copie os valores de configuração para a propriedade de valor nos arquivos correspondentes no nó de controle.  
  
    |**#**|**Arquivo de configuração**|**Chave de configuração**|**Ação**|  
    |------------|----------------|---------------------|----------|   
    |1|core-site.xml|polybase.kerberos.kdchost|Especifique o nome de host do KDC. Por exemplo: kerberos.your-realm.com.|  
    |2|core-site.xml|polybase.kerberos.realm|Especifique o realm do Kerberos. Por exemplo: YOUR-REALM.COM|  
    |3|core-site.xml|hadoop.security.authentication|Localize a configuração do lado do Hadoop e copie a máquina do SQL Server. Por exemplo: KERBEROS<br></br>**Observação de segurança:** KERBEROS deve ser escrito em letras maiúsculas. Se for escrito em letras minúsculas, talvez ele não seja ativado.|   
    |4|hdfs-site.xml|dfs.namenode.kerberos.principal|Localize a configuração do lado do Hadoop e copie a máquina do SQL Server. Por exemplo: hdfs/_HOST@YOUR-REALM.COM|  
    |5|mapred-site.xml|mapreduce.jobhistory.principal|Localize a configuração do lado do Hadoop e copie a máquina do SQL Server. Por exemplo: mapred/_HOST@YOUR-REALM.COM|  
    |6|mapred-site.xml|mapreduce.jobhistory.address|Localize a configuração do lado do Hadoop e copie a máquina do SQL Server. Por exemplo: 10.193.26.174:10020|  
    |7|yarn-site.xml yarn.|yarn.resourcemanager.principal|Localize a configuração do lado do Hadoop e copie a máquina do SQL Server. Por exemplo: yarn/_HOST@YOUR-REALM.COM|  
  
4. Crie um objeto de credencial com escopo de banco de dados para especificar as informações de autenticação de cada usuário do Hadoop. Veja [Objetos T-SQL do PolyBase](../relational-databases/polybase/polybase-t-sql-objects.md).  

5. Reinicie a região PDW. Para fazer isso, use a ferramenta Configuration Manager. Ver [iniciar o Configuration Manager &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md).
 
## <a name="see-also"></a>Consulte também  
[Configuração de dispositivo &#40;Analytics Platform System&#41;](appliance-configuration.md)  
<!-- MISSING LINKS [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  -->  
  
