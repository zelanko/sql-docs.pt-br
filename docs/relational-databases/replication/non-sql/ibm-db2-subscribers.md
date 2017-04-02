---
title: "Assinantes do IBM DB2 | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Assinantes não SQL Server, IBM DB2"
  - "tipos de dados [replicação do SQL Server], assinantes não-SQL Server"
  - "Assinantes do IBM DB2"
  - "mapeando tipos de dados [replicação do SQL Server]"
  - "Assinantes heterogêneos, IBM DB2"
ms.assetid: a1a27b1e-45dd-4d7d-b6c0-2b608ed175f6
caps.latest.revision: 74
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 73
---
# Assinantes do IBM DB2
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] suporta o assinaturas push para IBM DB2/AS 400, DB2/MVS e DB2/Universal Database por meio dos provedores OLE DB que acompanham [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Host Integration Server.  
  
## Configurando um Assinante IBM DB2  
 Para configurar um Assinante IBM DB2, siga estas etapas:  
  
1.  Instale a versão mais recente do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] OLE DB Provider para DB2 no Distribuidor:  
  
    -   Se você estiver usando [!INCLUDE[ssEnterpriseEd11](../../../includes/ssenterpriseed11-md.md)], no [Downloads do SQL Server 2008](http://go.microsoft.com/fwlink/?LinkId=149256) página da Web, no **Downloads relacionados** seção, clique no link para a versão mais recente do Microsoft SQL Server 2008 Feature Pack. Sobre o **Microsoft SQL Server 2008 Feature Pack** página da Web, procure **Microsoft OLE DB Provider for DB2**.  
  
    -   Se você estiver usando o [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Standard, instale a versão mais recente do servidor [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Host [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] (HIS), que inclui o provedor.  
  
     Além de instalar o provedor, recomendamos que você instale a ferramenta de acesso de dados, que é usado na próxima etapa (ele é instalado por padrão com o download do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Enterprise). Para obter mais informações sobre a instalação e uso de Data Access Tool, consulte a documentação do provedor ou a documentação HIS.  
  
2.  Crie uma cadeia de conexão para o Assinante. A cadeia de conexão pode ser criada em qualquer editor de texto, mas recomendamos que você use o Data Access Tool. Para criar a cadeia de caracteres no Data Access Tool:  
  
    1.  Clique em **Iniciar**, **programas**, **Microsoft OLE DB Provider for DB2**, e então **ferramenta de acesso a dados**.  
  
    2.  No **Data Access Tool**, siga as etapas para fornecer informações sobre o servidor DB2. Quando você concluir a ferramenta, um UDL (vínculo de dados universal) é criado com uma cadeia de conexão associada (o UDL não é usado de fato pela replicação, mas a cadeia de conexão é).  
  
    3.  Acessar a cadeia de conexão: UDL na ferramenta de acesso a dados e selecione **Exibir cadeia de conexão**.  
  
     A cadeia de conexão será semelhante a (quebras de linha são para legibilidade):  
  
    ```  
    Provider=DB2OLEDB;Initial Catalog=MY_SUBSCRIBER_DB;Network Transport Library=TCP;Host CCSID=1252;  
    PC Code Page=1252;Network Address=MY_SUBSCRIBER;Network Port=50000;Package Collection=MY_PKGCOL;  
    Default Schema=MY_SCHEMA;Process Binary as Character=False;Units of Work=RUW;DBMS Platform=DB2/NT;  
    Persist Security Info=False;Connection Pooling=True;  
    ```  
  
     A maioria das opções na cadeia de caracteres é específica para o servidor DB2 que você está configurando, mas a opção `Process Binary as Character` deve sempre ser definida como `False`. Um valor é necessário para a opção `Initial Catalog` para identificar o banco de dados de assinatura. A cadeia de conexão será inserida no Assistente para Nova Assinatura quando você criar a assinatura.  
  
3.  Crie um instantâneo ou uma publicação transacional, habilite-o para Assinantes não [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e, em seguida, crie uma assinatura push para o Assinante. Para obter mais informações, consulte [criar uma assinatura para um assinante não-SQL Server](../../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md).  
  
4.  Opcionalmente, especifique um script de criação personalizado para um ou mais artigos. Quando uma tabela é publicada, um script CREATE TABLE é criado para aquela tabela. Para Assinantes não [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o script é criado no dialeto [!INCLUDE[tsql](../../../includes/tsql-md.md)] e, depois, é convertido para um dialeto SQL mais genérico pelo Agente de Distribuição antes de ser aplicado ao Assinante. Para especificar um script de criação personalizado, modifique os existentes [!INCLUDE[tsql](../../../includes/tsql-md.md)] script ou criar um script completo que usa o dialeto SQL DB2; se for criado um script DB2, use o **bypass_translation** diretiva para que o agente de distribuição aplique o script no assinante sem conversão.  
  
     Os scripts podem ser modificados por diversas razões, porém a razão mais comum é alterar mapeamentos de tipo de dados. Para obter mais informações, consulte a seção "Considerações para o mapeamento de tipo de dados" neste tópico. Se você modificar o script [!INCLUDE[tsql](../../../includes/tsql-md.md)], as alterações deverão ficar restritas a alterações de mapeamento de tipo de dados (e o script não deverá conter nenhum comentário). Se mais alterações significativas forem requeridas, crie um script DB2.  
  
     **Para modificar um script de artigo e fornecê-lo como um script de criação personalizado**  
  
    1.  Depois que o instantâneo for gerado para a publicação, navegue para a pasta de instantâneo da publicação.  
  
    2.  Localize o arquivo .sch com o mesmo nome do artigo, por exemplo, MyArticle.sch.  
  
    3.  Abra o arquivo usando o Bloco de Notas ou outro editor de textos.  
  
    4.  Modifique o arquivo e salve-o em um diretório diferente.  
  
    5.  Execute sp_changearticle, especificando o caminho do arquivo e nome para o *creation_script* propriedade. Para obter mais informações, consulte [sp_changearticle & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md).  
  
     **Para criar um script de artigo e fornecê-lo como um script de criação personalizado**  
  
    1.  Crie um script de artigo usando o dialeto DB2 SQL. Certifique-se de que a primeira linha do arquivo é **bypass_translation**, com nada mais na linha.  
  
    2.  Execute sp_changearticle, especificando o caminho do arquivo e nome para o *creation_script* propriedade.  
  
## Considerações sobre os Assinantes IBM DB2  
 Além das considerações abordados neste tópico [assinantes não-SQL Server](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md), considere as seguintes questões ao replicar para assinantes do DB2:  
  
-   Os dados e índices para cada tabela replicada são atribuídos para um espaço de tabela de DB2. O tamanho de página de um espaço de tabela DB2 controla o número máximo de colunas e o tamanho máximo da linha das tabelas pertencentes ao espaço de tabela. Verifique se o espaço de tabela associado com tabelas replicadas é baseado apropriadamente no número de colunas replicadas e no tamanho máximo das linhas das tabelas.  
  
-   Não publique tabelas para Assinantes DB2 usando replicação transacional se uma ou mais colunas de chave primária na tabela forem do tipo de dados DECIMAL(32-38, 0-38) ou NUMERIC(32-38, 0-38). A replicação transacional identifica linhas usando a chave primária; isso poderá resultar em falhas porque estes tipos de dados são mapeados para VARCHAR(41) no Assinante. Tabelas com chaves primárias que usam estes tipos de dados podem ser publicadas usando replicação de instantâneo.  
  
-   Se você quer pré-criar tabelas no Assinante, em vez da replicação criá-las, use a opção somente suporte para replicação. Para obter mais informações, consulte [inicializar um transacional assinatura sem um instantâneo](../../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permite que mais nomes de tabela e nomes de coluna que DB2:  
  
    -   Se o banco de dados da publicação incluir tabelas com nomes mais longos daqueles suportados na versão DB2 do Assinante, especifique um nome alternativo para a propriedade de artigo destination_table. Para obter mais informações sobre como definir propriedades ao criar uma publicação, consulte [criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md) e [definir um artigo](../../../relational-databases/replication/publish/define-an-article.md).  
  
    -   Não é possível especificar nomes de coluna alternativos. Você deve se assegurar de que as tabelas publicadas não incluam colunas mais longas do que as que têm suporte na versão DB2 do Assinante.  
  
## Mapear tipos de dados do SQL Server para IBM DB2  
 A tabela a seguir exibe os mapeamentos dos tipos de dados usados quando os dados são replicados para um Assinante que executa IBM DB2.  
  
|Tipo de dados do SQL Server|Tipo de dados IBM DB2|  
|--------------------------|-----------------------|  
|**bigint**|DECIMAL(19,0)|  
|**binary(1-254)**|CHAR(1-254) FOR BIT DATA|  
|**binary(255-8000)**|VARCHAR(255-8000) FOR BIT DATA|  
|**bit**|smallint|  
|**char(1-254)**|CHAR(1-254)|  
|**char(255-8000)**|VARCHAR(255-8000)|  
|**date**|DATE|  
|**datetime**|TIMESTAMP|  
|**datetime2(0-7)**|VARCHAR(27)|  
|**DateTimeOffset(0-7)**|VARCHAR(34)|  
|**decimal (1-31, 0-31)**|DECIMAL(1-31, 0-31)|  
|**decimal (32-38, 0-38)**|VARCHAR(41)|  
|**float(53)**|DOUBLE|  
|**float**|FLOAT|  
|**geografia**|IMAGE|  
|**geometria**|IMAGE|  
|**hierarchyid**|IMAGE|  
|**image**|VARCHAR(0) FOR BIT DATA*|  
|**into**|INT|  
|**money**|DECIMAL(19,4)|  
|**nchar(1-4000)**|VARCHAR(1-4000)|  
|**ntext**|VARCHAR(0)*|  
|**numérico (1-31, 0-31)**|DECIMAL(1-31, 0-31)|  
|**numérico (32-38, 0-38)**|VARCHAR(41)|  
|**nvarchar(1-4000)**|VARCHAR(1-4000)|  
|**nvarchar(max)**|VARCHAR(0)*|  
|**real**|REAL|  
|**smalldatetime**|TIMESTAMP|  
|**smallint**|smallint|  
|**smallmoney**|DECIMAL(10,4)|  
|**sql_variant**|N/A|  
|**sysname**|VARCHAR(128)|  
|**text**|VARCHAR(0)*|  
|**Time(0-7)**|VARCHAR(16)|  
|**timestamp**|CHAR(8) FOR BIT DATA|  
|**tinyint**|smallint|  
|**uniqueidentifier**|CHAR(38)|  
|**varbinary(1-8000)**|VARCHAR(1-8000) FOR BIT DATA|  
|**varchar(1-8000)**|VARCHAR(1-8000)|  
|**varbinary(max)**|VARCHAR(0) FOR BIT DATA*|  
|**varchar(max)**|VARCHAR(0)*|  
|**xml**|VARCHAR(0)*|  
  
 *Confira a próxima seção para obter mais informações sobre mapeamentos para VARCHAR(0).  
  
### Considerações sobre mapeamento de tipo de dados  
 Considere os seguintes problemas de mapeamento de tipo de dados ao replicar para Assinantes DB2:  
  
-   Ao mapear [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **char**, **varchar**, **binário** e **varbinary** para DB2 CHAR, VARCHAR, CHAR FOR BIT DATA e VARCHAR FOR BIT DATA, respectivamente, a replicação define o comprimento do tipo de dados DB2 para ser o mesmo que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo.  
  
     Isto permite que a tabela gerada seja criada com êxito no Assinante, desde que a restrição de tamanho da página DB2 seja ampla o suficiente para acomodar o tamanho máximo da linha. Assegure-se de que o logon usado para acessar o banco de dados do DB2 tenha permissões para acessar espaços de tabela de tamanho suficiente para as tabelas que estão sendo replicadas para DB2.  
  
-   O DB2 pode suportar colunas VARCHAR de até 32 KB (kilobytes); portanto, é possível que algumas colunas grandes de objeto [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] possam ser mapeadas apropriadamente para colunas DB2 VARCHAR. Porém, o provedor OLE DB que a replicação usa para DB2 não suporta mapear objetos grandes [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para objetos grandes DB2. Por esse motivo, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **texto**, **varchar (max)**, **ntext**, e **nvarchar (max)** colunas são mapeadas para VARCHAR(0) nos scripts de criação gerados. O valor de comprimento de 0 deve ser alterado para um valor apropriado antes de aplicar o script ao Assinante. Se o comprimento de tipo de dado não for alterado, o DB2 gerará o erro 604 quando a criação de tabela for tentada no Assinante DB2 (o erro 604 indica que o atributo de precisão ou comprimento de um tipo de dado não é válido).  
  
     Baseado sobre seu conhecimento da tabela de origem que você está replicando, determine se é apropriado mapear um objeto grande [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para um item DB2 de comprimento variável e especifique um comprimento máximo apropriado em um script de criação personalizado. Para obter informações sobre especificar um script de criação personalizado, consulte a etapa 5 na seção "Configurando um Assinante de IBM DB2" neste tópico.  
  
    > [!NOTE]  
    >  O comprimento especificado para o tipo DB2, quando combinado com outros comprimentos de coluna, não pode exceder o tamanho máximo de linha baseado no espaço de tabela DB2 ao qual os dados de tabela são atribuídos.  
  
     Se não houver mapeamento apropriado para uma coluna de objeto grande, considere usar filtragem de coluna no artigo para que a coluna não seja replicada. Para obter mais informações, consulte [Filtrar dados publicados](../../../relational-databases/replication/publish/filter-published-data.md).  
  
-   Ao replicar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **nchar** e **nvarchar** para DB2 CHAR e VARCHAR, a replicação usa o mesmo especificador de tamanho para o tipo DB2 do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo. Porém, o comprimento de tipo de dados pode ser muito pequeno para a tabela DB2 gerada.  
  
     Em alguns ambientes DB2, um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **char** item de dados não está restrito a caracteres de byte único; o comprimento de um item CHAR ou VARCHAR deve levar isso em conta. Você também deve levar em conta *Deslocar* e *shift-out* caracteres se forem necessários. Se você estiver replicando tabelas com **nchar** e **nvarchar** colunas, talvez seja necessário especificar um comprimento máximo maior para o tipo de dados em um script de criação personalizado. Para obter informações sobre especificar um script de criação personalizado, consulte a etapa 5 na seção "Configurando um Assinante de IBM DB2" neste tópico.  
  
## Consulte também  
 [Assinantes não SQL Server](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [Assinar publicações](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  