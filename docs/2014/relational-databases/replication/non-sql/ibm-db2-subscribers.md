---
title: Assinantes do IBM DB2 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- non-SQL Server Subscribers, IBM DB2
- data types [SQL Server replication], non-SQL Server Subscribers
- IBM DB2 Subscribers
- mapping data types [SQL Server replication]
- heterogeneous Subscribers, IBM DB2
ms.assetid: a1a27b1e-45dd-4d7d-b6c0-2b608ed175f6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 54263e75c0f4c7da7c6d9c24ea499c202372aa64
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068616"
---
# <a name="ibm-db2-subscribers"></a>Assinantes do IBM DB2
  O[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oferece suporte a assinaturas push para IBM DB2/AS 400, DB2/MVS e DB2/Universal Database por meio dos provedores OLE DB fornecidos com o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Host Integration Server.  
  
## <a name="configuring-an-ibm-db2-subscriber"></a>Configurando um Assinante IBM DB2  
 Para configurar um Assinante IBM DB2, siga estas etapas:  
  
1.  Instale a versão mais recente do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] OLE DB Provider para DB2 no Distribuidor:  
  
    -   Se você estiver usando o [!INCLUDE[ssEnterpriseEd11](../../../includes/ssenterpriseed11-md.md)], na página da Web [Downloads do SQL Server 2008](https://go.microsoft.com/fwlink/?LinkId=149256) , na seção **Downloads relacionados** , clique no link para a versão mais recente do Microsoft SQL Server 2008 Feature Pack. Na página da Web do **Microsoft SQL Server 2008 Feature Pack** , pesquise por **Microsoft OLE DB Provider for DB2**.  
  
    -   Se você estiver usando o [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Standard, instale a versão mais recente do servidor [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Host [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] (HIS), que inclui o provedor.  
  
     Além de instalar o provedor, recomendamos que você instale o Data Access Tool, que é usado na próxima etapa (é instalado por padrão com o download do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Enterprise). Para obter mais informações sobre a instalação e uso de Data Access Tool, consulte a documentação do provedor ou a documentação HIS.  
  
2.  Crie uma cadeia de conexão para o Assinante. A cadeia de conexão pode ser criada em qualquer editor de texto, mas recomendamos que você use o Data Access Tool. Para criar a cadeia de caracteres no Data Access Tool:  
  
    1.  Clique em **Iniciar**, **Programas**, **Microsoft OLE DB Provider para DB2**e, então, **Data Access Tool**.  
  
    2.  No **Data Access Tool**, siga as etapas para prover informações sobre o servidor de DB2. Quando você concluir a ferramenta, um UDL (vínculo de dados universal) é criado com uma cadeia de conexão associada (o UDL não é usado de fato pela replicação, mas a cadeia de conexão é).  
  
    3.  Acesse a cadeia de conexão: clique com o botão direito em UDL no Data Access Tool e selecione **Exibir Cadeia de Conexão**.  
  
     A cadeia de conexão será semelhante a (quebras de linha são para legibilidade):  
  
    ```  
    Provider=DB2OLEDB;Initial Catalog=MY_SUBSCRIBER_DB;Network Transport Library=TCP;Host CCSID=1252;  
    PC Code Page=1252;Network Address=MY_SUBSCRIBER;Network Port=50000;Package Collection=MY_PKGCOL;  
    Default Schema=MY_SCHEMA;Process Binary as Character=False;Units of Work=RUW;DBMS Platform=DB2/NT;  
    Persist Security Info=False;Connection Pooling=True;  
    ```  
  
     A maioria das opções na cadeia de caracteres é específica para o servidor DB2 que você está configurando, mas a opção `Process Binary as Character` deve sempre ser definida como `False`. Um valor é necessário para a opção `Initial Catalog` para identificar o banco de dados de assinatura. A cadeia de conexão será inserida no Assistente para Nova Assinatura quando você criar a assinatura.  
  
3.  Crie um instantâneo ou uma publicação transacional, habilite-o para Assinantes não[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e, em seguida, crie uma assinatura push para o Assinante. Para obter mais informações, consulte [Criar uma assinatura para um Assinante não SQL Server](../create-a-subscription-for-a-non-sql-server-subscriber.md).  
  
4.  Opcionalmente, especifique um script de criação personalizado para um ou mais artigos. Quando uma tabela é publicada, um script CREATE TABLE é criado para aquela tabela. Para Assinantes não[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , o script é criado no dialeto [!INCLUDE[tsql](../../../includes/tsql-md.md)] e, depois, é convertido para um dialeto SQL mais genérico pelo Agente de Distribuição antes de ser aplicado ao Assinante. Para especificar um script de criação personalizado, modifique o script [!INCLUDE[tsql](../../../includes/tsql-md.md)] existente ou crie um script completo que usa o dialeto SQL DB2; se for criado um script DB2, use a diretiva **bypass_translation** para que o Agente de Distribuição aplique o script no Assinante sem conversão.  
  
     Os scripts podem ser modificados por diversas razões, porém a razão mais comum é alterar mapeamentos de tipo de dados. Para obter mais informações, consulte a seção "Considerações para o mapeamento de tipo de dados" neste tópico. Se você modificar o script [!INCLUDE[tsql](../../../includes/tsql-md.md)] , as alterações deverão ficar restritas a alterações de mapeamento de tipo de dados (e o script não deverá conter nenhum comentário). Se mais alterações significativas forem requeridas, crie um script DB2.  
  
     **Para modificar um script de artigo e fornecê-lo como um script de criação personalizado**  
  
    1.  Depois que o instantâneo for gerado para a publicação, navegue para a pasta de instantâneo da publicação.  
  
    2.  Localize o arquivo .sch com o mesmo nome do artigo, por exemplo, MyArticle.sch.  
  
    3.  Abra o arquivo usando o Bloco de Notas ou outro editor de textos.  
  
    4.  Modifique o arquivo e salve-o em um diretório diferente.  
  
    5.  Execute sp_changearticle, especificando o caminho e o nome do arquivo para a propriedade *creation_script*. Para obter mais informações, consulte [sp_changearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql).  
  
     **Para criar um script de artigo e fornecê-lo como um script de criação personalizado**  
  
    1.  Crie um script de artigo usando o dialeto DB2 SQL. Certifique-se que a primeira linha do arquivo seja **bypass_translation**, com nada mais na linha.  
  
    2.  Execute sp_changearticle, especificando o caminho e o nome do arquivo para a propriedade *creation_script*.  
  
## <a name="considerations-for-ibm-db2-subscribers"></a>Considerações sobre os Assinantes IBM DB2  
 Além das considerações abrangidas no tópico [Non-SQL Server Subscribers](non-sql-server-subscribers.md), considere os assuntos a seguir ao replicar para os Assinantes DB2:  
  
-   Os dados e índices para cada tabela replicada são atribuídos para um espaço de tabela de DB2. O tamanho de página de um espaço de tabela DB2 controla o número máximo de colunas e o tamanho máximo da linha das tabelas pertencentes ao espaço de tabela. Verifique se o espaço de tabela associado com tabelas replicadas é baseado apropriadamente no número de colunas replicadas e no tamanho máximo das linhas das tabelas.  
  
-   Não publique tabelas para Assinantes DB2 usando replicação transacional se uma ou mais colunas de chave primária na tabela forem do tipo de dados DECIMAL(32-38, 0-38) ou NUMERIC(32-38, 0-38). A replicação transacional identifica linhas usando a chave primária; isso poderá resultar em falhas porque estes tipos de dados são mapeados para VARCHAR(41) no Assinante. Tabelas com chaves primárias que usam estes tipos de dados podem ser publicadas usando replicação de instantâneo.  
  
-   Se você quer pré-criar tabelas no Assinante, em vez da replicação criá-las, use a opção somente suporte para replicação. Para obter mais informações, consulte [Initialize a Transactional Subscription Without a Snapshot](../initialize-a-transactional-subscription-without-a-snapshot.md).  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permite nomes de tabela e nomes de coluna mais longos que DB2:  
  
    -   Se o banco de dados da publicação incluir tabelas com nomes mais longos daqueles suportados na versão DB2 do Assinante, especifique um nome alternativo para a propriedade de artigo destination_table. Para mais informações sobre como configurar propriedades ao criar uma publicação, consulte [Criar uma publicação](../publish/create-a-publication.md) e [Definir um artigo](../publish/define-an-article.md).  
  
    -   Não é possível especificar nomes de coluna alternativos. Você deve se assegurar de que as tabelas publicadas não incluam colunas mais longas do que as que têm suporte na versão DB2 do Assinante.  
  
## <a name="mapping-data-types-from-sql-server-to-ibm-db2"></a>Mapear tipos de dados do SQL Server para IBM DB2  
 A tabela a seguir exibe os mapeamentos dos tipos de dados usados quando os dados são replicados para um Assinante que executa IBM DB2.  
  
|Tipo de dados do SQL Server|Tipo de dados IBM DB2|  
|--------------------------|-----------------------|  
|`bigint`|DECIMAL(19,0)|  
|`binary(1-254)`|CHAR(1-254) FOR BIT DATA|  
|`binary(255-8000)`|VARCHAR(255-8000) FOR BIT DATA|  
|`bit`|SMALLINT|  
|`char(1-254)`|CHAR(1-254)|  
|`char(255-8000)`|VARCHAR(255-8000)|  
|`date`|DATE|  
|`datetime`|timestamp|  
|`datetime2(0-7)`|VARCHAR(27)|  
|`datetimeoffset(0-7)`|VARCHAR(34)|  
|`decimal(1-31, 0-31)`|DECIMAL(1-31, 0-31)|  
|`decimal(32-38, 0-38)`|VARCHAR(41)|  
|`float(53)`|DOUBLE|  
|`float`|FLOAT|  
|`geography`|IMAGEM|  
|`geometry`|IMAGEM|  
|`hierarchyid`|IMAGEM|  
|`image`|VARCHAR (0) para dados de BIT<sup>1</sup>|  
|`into`|INT|  
|`money`|DECIMAL(19,4)|  
|`nchar(1-4000)`|VARCHAR(1-4000)|  
|`ntext`|VARCHAR (0)<sup>1</sup>|  
|`numeric(1-31, 0-31)`|DECIMAL(1-31, 0-31)|  
|`numeric(32-38, 0-38)`|VARCHAR(41)|  
|`nvarchar(1-4000)`|VARCHAR(1-4000)|  
|`nvarchar(max)`|VARCHAR (0)<sup>1</sup>|  
|`real`|REAL|  
|`smalldatetime`|timestamp|  
|`smallint`|SMALLINT|  
|`smallmoney`|DECIMAL(10,4)|  
|`sql_variant`|N/D|  
|`sysname`|VARCHAR(128)|  
|`text`|VARCHAR (0)<sup>1</sup>|  
|`time(0-7)`|VARCHAR(16)|  
|`timestamp`|CHAR(8) FOR BIT DATA|  
|`tinyint`|SMALLINT|  
|`uniqueidentifier`|CHAR(38)|  
|`varbinary(1-8000)`|VARCHAR(1-8000) FOR BIT DATA|  
|`varchar(1-8000)`|VARCHAR(1-8000)|  
|`varbinary(max)`|VARCHAR (0) para dados de BIT<sup>1</sup>|  
|`varchar(max)`|VARCHAR (0)<sup>1</sup>|  
|`xml`|VARCHAR (0)<sup>1</sup>|  
  
 <sup>1</sup> consulte a próxima seção para obter mais informações sobre mapeamentos para varchar (0).  
  
### <a name="data-type-mapping-considerations"></a>Considerações sobre mapeamento de tipo de dados  
 Considere os seguintes problemas de mapeamento de tipo de dados ao replicar para Assinantes DB2:  
  
-   Ao mapear [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] `char` , `varchar` , `binary` e `varbinary` para DB2 CHAR, varchar, char para dados bit e VARCHAR para dados de bit, respectivamente, a replicação define o comprimento do tipo de dados DB2 como o mesmo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo.  
  
     Isto permite que a tabela gerada seja criada com êxito no Assinante, desde que a restrição de tamanho da página DB2 seja ampla o suficiente para acomodar o tamanho máximo da linha. Assegure-se de que o logon usado para acessar o banco de dados do DB2 tenha permissões para acessar espaços de tabela de tamanho suficiente para as tabelas que estão sendo replicadas para DB2.  
  
-   O DB2 pode suportar colunas VARCHAR de até 32 KB (kilobytes); portanto, é possível que algumas colunas grandes de objeto [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] possam ser mapeadas apropriadamente para colunas DB2 VARCHAR. Porém, o provedor OLE DB que a replicação usa para DB2 não suporta mapear objetos grandes [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para objetos grandes DB2. Por esse motivo, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] `text` `varchar(max)` as colunas,, `ntext` e `nvarchar(max)` são mapeadas para varchar (0) nos scripts de criação gerados. O valor de comprimento de 0 deve ser alterado para um valor apropriado antes de aplicar o script ao Assinante. Se o comprimento de tipo de dado não for alterado, o DB2 gerará o erro 604 quando a criação de tabela for tentada no Assinante DB2 (o erro 604 indica que o atributo de precisão ou comprimento de um tipo de dado não é válido).  
  
     Baseado sobre seu conhecimento da tabela de origem que você está replicando, determine se é apropriado mapear um objeto grande [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para um item DB2 de comprimento variável e especifique um comprimento máximo apropriado em um script de criação personalizado. Para obter informações sobre especificar um script de criação personalizado, consulte a etapa 5 na seção "Configurando um Assinante de IBM DB2" neste tópico.  
  
    > [!NOTE]  
    >  O comprimento especificado para o tipo DB2, quando combinado com outros comprimentos de coluna, não pode exceder o tamanho máximo de linha baseado no espaço de tabela DB2 ao qual os dados de tabela são atribuídos.  
  
     Se não houver mapeamento apropriado para uma coluna de objeto grande, considere usar filtragem de coluna no artigo para que a coluna não seja replicada. Para obter mais informações, consulte [Filter Published Data](../publish/filter-published-data.md) (Filtrar dados publicados).  
  
-   Ao replicar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] `nchar` e `nvarchar` para DB2 CHAR e varchar, a replicação usa o mesmo especificador de comprimento para o tipo DB2 como para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo. Porém, o comprimento de tipo de dados pode ser muito pequeno para a tabela DB2 gerada.  
  
     Em alguns ambientes DB2, um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] `char` item de dados não é restrito a caracteres de byte único; o comprimento de um item char ou varchar deve levar isso em conta. Você deve levar também em conta o *mover para dentro* e *mover para fora* de caracteres se forem necessários. Se você estiver replicando tabelas com `nchar` `nvarchar` colunas e, talvez seja necessário especificar um comprimento máximo maior para o tipo de dados em um script de criação personalizado. Para obter informações sobre especificar um script de criação personalizado, consulte a etapa 5 na seção "Configurando um Assinante de IBM DB2" neste tópico.  
  
## <a name="see-also"></a>Consulte Também  
 [Non-SQL Server Subscribers](non-sql-server-subscribers.md)   
 [Subscribe to Publications](../subscribe-to-publications.md)  
  
  
