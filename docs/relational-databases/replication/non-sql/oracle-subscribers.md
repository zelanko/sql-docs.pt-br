---
title: Assinantes Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- data types [SQL Server replication], non-SQL Server Subscribers
- Oracle Subscribers [SQL Server replication]
- non-SQL Server Subscribers, Oracle
- heterogeneous Subscribers, Oracle
- mapping data types [SQL Server replication]
ms.assetid: 591c0313-82ce-4689-9fc1-73752ff122cf
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8e7ee336c9f81c8d4258e16cf09aa9ffec177e0f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68110948"
---
# <a name="oracle-subscribers"></a>Assinantes Oracle
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Iniciando como o [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tem suporte para as assinaturas push do Oracle por meio do provedor Oracle OLE DB fornecido pela Oracle.  
  
## <a name="configuring-an-oracle-subscriber"></a>Configurando um Assinante Oracle  
 Para configurar um Assinante Oracle, siga estas etapas:  
  
1.  Instale e configure o software de rede cliente Oracle e o provedor Oracle OLE DB no Distribuidor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , para que o Distribuidor possa realizar as conexões ao Assinante Oracle. O software de rede cliente Oracle deve ter a versão mais recente disponível. A Oracle recomenda que os usuários instalem as mais recentes versões do software cliente. O software cliente é, portanto, muitas vezes uma versão mais recente do que o software do banco de dados. A maneira mais prática para instalar o software é usar o Instalador Universal Oracle no disco do Oracle Cliente. No Instalador Universal Oracle, você deverá fornecer as seguintes informações:  
  
    |Informações|Descrição|  
    |-----------------|-----------------|  
    |Oracle Home|Esse é o caminho para diretório de instalação do software Oracle. Aceite o padrão (C:\oracle\ora90 ou semelhante) ou digite outro caminho. Para obter mais informações sobre o Oracle Home, consulte a seção "Considerações sobre o Oracle Home" mais adiante neste tópico.|  
    |Nome do Oracle home|Um alias para o caminho do Oracle home.|  
    |Tipo de instalação|No Oracle 10g, selecione a opção de instalação **Tempo de Execução** ou **Administrador** .|  
  
2.  Crie um nome de TNS para o Assinante. O TNS (Substrato Transparente de Rede) é uma camada de comunicação usada pelos bancos de dados Oracle. O nome de serviço do TNS é o nome pelo qual uma instância do banco de dados Oracle é identificada em uma rede. Você atribui um nome de serviço ao TNS quando for configurar a conectividade do banco de dados Oracle. A replicação usa o nome de serviço do TNS para identificar o Assinante e estabelecer conexões.  
  
     Após a conclusão do Instalador Universal Oracle, use o Assistente de Configuração Net para configurar a conectividade da rede. Você deve fornecer quatro informações para configurar a conectividade de rede. O administrador do banco de dados Oracle configura a configuração de rede quando define o banco de dados e o ouvinte e, se você não tiver essas informações, elas deverão ser fornecidas pelo administrador. Você deve fazer o seguinte:  
  
    |Ação|Descrição|  
    |------------|-----------------|  
    |Identificar o banco de dados|Há dois métodos para identificar o banco de dados. O primeiro método usa o Sistema Identificador Oracle (SID) e está disponível em todas as versões do Oracle. O segundo método usa o nome de serviço, que está disponível a partir da versão 8.0 do Oracle. Ambos os métodos usam um valor que é configurado quando o banco de dados é criado, e é importante que a configuração de rede cliente use o mesmo método de nomenclatura que o administrador usou ao configurar o ouvinte para o banco de dados.|  
    |Identificar um alias de rede para o banco de dados|Você deve especificar um alias de rede que será usado para acessar o banco de dados Oracle. O alias de rede é essencialmente um ponteiro para o SID remoto ou o nome de serviço que foi configurado quando o banco de dados foi criado, ele foi referenciado por diversos nomes em diferentes versões e produtos Oracle, incluindo o nome de serviço Net e o alias TNS. O SQL*Plus solicita esse alias como o parâmetro "Cadeia de caracteres de Host" ao efetuar logon.|  
    |Selecionar o protocolo de rede|Selecione os protocolos apropriados que você gostaria de ter suporte. A maioria dos aplicativos usa o TCP.|  
    |Especificar as informações de host para identificar o ouvinte de banco de dados|O host é o nome ou alias de DNS do computador no qual o ouvinte Oracle está executando, que costuma geralmente ser o mesmo computador no qual o banco de dados reside. Para alguns protocolos, você deve fornecer informações adicionais. Por exemplo, se você selecionar o TCP, deve fornecer a porta na qual o ouvinte está escutando as solicitações de conexão para o banco de dados de destino. A configuração do TCP padrão usa a porta 1521.|  
  
3.  Crie um instantâneo ou uma publicação transacional, habilite-o para Assinantes não[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e, em seguida, crie uma assinatura push para o Assinante. Para obter mais informações, consulte [Criar uma assinatura para um Assinante não SQL Server](../../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md).  

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

### <a name="setting-directory-permissions"></a>Definindo permissões de diretório  
 A conta sob a qual o serviço [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Distribuidor executa deve receber permissões de gravação e executar para o diretório (e todos os subdiretórios) onde o software de rede cliente Oracle está instalado.  
  
### <a name="testing-connectivity-between-the-sql-server-distributor-and-the-oracle-publisher"></a>Testando a conectividade entre o SQL Server Distributor e o Publicador Oracle  
 Próximo do fim do Assistente de Configuração Net deve haver uma opção para testar a conexão ao Assinante Oracle. Antes de você testar a conexão, garanta que a instância do banco de dados Oracle esteja on-line e que o Oracle Listener esteja executando. Se o teste for malsucedido, entre em contato com o DBA da Oracle, responsável pelo banco de dados ao qual você está tentando se conectar.  
  
 Após ter feito uma conexão bem-sucedida com o Assinante Oracle, tente fazer o logon no banco de dados usando a mesma conta e senha configuradas para o Agente de Distribuição da assinatura.  
  
1.  Clique em **Iniciar**e em **Executar**.  
  
2.  Digite `cmd` e clique em **OK**.  
  
3.  No prompt de comando, digite:  
  
     `sqlplus <UserSchemaLogin>/<UserSchemaPassword>@<NetServiceName>`  
  
     Por exemplo: `sqlplus replication/$tr0ngPasswerd@Oracle90Server`  
  
4.  Se a configuração de redes foi bem-sucedida, o logon terá sucesso e você visualizará um prompt `SQL` .  
  
### <a name="considerations-for-oracle-home"></a>Considerações sobre o Oracle Home  
 O Oracle oferece suporte à instalação lado a lado de binários aplicativos, mas apenas um conjunto de binários pode ser usado por replicação em um determinado momento. Cada conjunto de binários é associado a um Oracle Home; os binários estão no diretório %ORACLE_HOME%\bin. Você deve garantir que o conjunto correto de binários (especificamente a versão mais recente do software de rede cliente) seja usado quando a replicação fizer as conexões com o Assinante Oracle.  
  
 Efetue o logon no Distribuidor com as contas usadas pelo serviço [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e o serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent e defina as variáveis de ambiente apropriadas. A variável %ORACLE_HOME% deve ser definida para fazer referência ao ponto de instalação que você especificou na instalação do software de rede cliente. O %PATH% deve incluir o diretório %ORACLE_HOME% \bin como a primeira entrada Oracle que for encontrada. Para obter mais informações sobre como definir as variáveis de ambiente, consulte a documentação do Windows.  
  
> [!NOTE]  
>  Se tiver mais de um Oracle home no Distribuidor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , garanta que o Agente de Distribuição esteja usando o provedor Oracle OLE DB mais recente. Em alguns casos, a Oracle não atualiza o provedor OLE DB por padrão quando você atualiza os componentes do cliente no Distribuidor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Desinstale o provedor OLE DB antigo e instale o mas recente provedor OLE DB. Para obter mais informações sobre como instalar e desinstalar o provedor, consulte a documentação do Oracle.  
  
## <a name="considerations-for-oracle-subscribers"></a>Considerações sobre os Assinantes Oracle  
 Além das considerações cobertas no tópico [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md), considere os assuntos a seguir quando for replicar para os Assinantes Oracle:  
  
-   O Oracle trata as cadeias de caracteres vazias e os valores NULOS como NULOS. Isto é importante se for definir uma coluna [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como NÃO NULA e estiver replicando a coluna para um Assinante Oracle. Para evitar falhas quando for aplicar alterações ao Assinante Oracle, você deve fazer um dos seguintes:  
  
    -   Garantir que cadeias de caracteres vazias não estejam inseridas na tabela publicada como valores de colunas.  
  
    -   Usar o parâmetro **-SkipErrors** para o Agente de Distribuição caso seja aceitável ser notificado das falhas no log do histórico do Agente de Distribuição e continuar com o processamento. Especifique o código de erro Oracle 1400 ( **-SkipErrors1400**).  
  
    -   Modifique o script de criação de tabela gerado, removendo o atributo NOT NULL das colunas de caracteres que talvez tenham cadeias de caracteres vazias associadas e forneça o script modificado como um script de criação personalizado para o artigo usando o parâmetro @creation_script de [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).  
  
-   Os Assinantes Oracle têm suporte para uma opção de esquemas de 0x4071. Para obter mais informações sobre opções de esquema, consulte [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).  
  
## <a name="mapping-data-types-from-sql-server-to-oracle"></a>Mapeando os tipos de dados do SQL Server para o Oracle  
 A tabela a seguir mostra os mapeamentos dos tipos de dados usados quando esses são replicados em Assinante executando em Oracle.  
  
|Tipo de dados do SQL Server|Tipo de dados do Oracle|  
|--------------------------|----------------------|  
|**bigint**|NUMBER(19,0)|  
|**binary(1-2000)**|RAW(1-2000)|  
|**binary(2001-8000)**|BLOB|  
|**bit**|NUMBER(1)|  
|**char(1-2000)**|CHAR(1-2000)|  
|**char(2001-4000)**|VARCHAR2(2001-4000)|  
|**char(4001-8000)**|CLOB|  
|**date**|DATE|  
|**datetime**|DATE|  
|**datetime2(0-7)**|TIMESTAMP (7) para Oracle 9 e Oracle 10; VARCHAR (27) para Oracle 8|  
|**datetimeoffset(0-7)**|TIMESTAMP(7) WITH TIME ZONE para Oracle 9 e Oracle 10; VARCHAR(34) para Oracle 8|  
|**decimal(1-38, 0-38)**|NUMBER(1-38, 0-38)|  
|**float(53)**|FLOAT|  
|**float**|FLOAT|  
|**geografia**|BLOB|  
|**geometria**|BLOB|  
|**hierarchyid**|BLOB|  
|**imagem**|BLOB|  
|**int**|NUMBER(10,0)|  
|**money**|NUMBER(19,4)|  
|**nchar(1-1000)**|CHAR(1-1000)|  
|**nchar(1001-4000)**|NCLOB|  
|**ntext**|NCLOB|  
|**numeric(1-38, 0-38)**|NUMBER(1-38, 0-38)|  
|**nvarchar(1-1000)**|VARCHAR2(1-2000)|  
|**nvarchar(1001-4000)**|NCLOB|  
|**nvarchar(max)**|NCLOB|  
|**real**|real|  
|**smalldatetime**|DATE|  
|**smallint**|NUMBER(5,0)|  
|**smallmoney**|NUMBER(10,4)|  
|**sql_variant**|N/A|  
|**sysname**|VARCHAR2(128)|  
|**text**|CLOB|  
|**time(0-7)**|VARCHAR(16)|  
|**timestamp**|RAW(8)|  
|**tinyint**|NUMBER(3,0)|  
|**uniqueidentifier**|CHAR(38)|  
|**varbinary(1-2000)**|RAW(1-2000)|  
|**varbinary(2001-8000)**|BLOB|  
|**varchar(1-4000)**|VARCHAR2(1-4000)|  
|**varchar(4001-8000)**|CLOB|  
|**varbinary(max)**|BLOB|  
|**varchar(max)**|CLOB|  
|**xml**|NCLOB|  
  
## <a name="see-also"></a>Consulte Também  
 [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [Assinar publicações](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  
