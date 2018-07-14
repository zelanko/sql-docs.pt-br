---
title: Configurar um publicador Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], configuring
ms.assetid: 240c8416-c8e5-4346-8433-07e0f779099f
caps.latest.revision: 58
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 66bd7f7e6bc67856a3c5f6e231a2c554a3eb4b29
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37264422"
---
# <a name="configure-an-oracle-publisher"></a>Configurar um publicador Oracle
  As publicações dos Editores Oracle são criadas da mesma forma que são criados os instantâneos e as publicações transacionais mas, antes de criar uma publicação de um Publicador Oracle, você deverá completar as etapas a seguir (etapas um, três e quatro que estão detalhadamente descritas neste tópico):  
  
1.  Crie um usuário administrativo de replicação no banco de dados do Oracle, usando o script fornecido.  
  
2.  Para as tabelas que você publicará, conceda a permissão SELECT diretamente em cada uma delas (não através de uma função) ao usuário administrativo Oracle que você criou na etapa 1.  
  
3.  Instale o software do cliente Oracle e o provedor OLE DV no Distribuidor [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e, em seguida, pare e reinicie a instância [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Se o Distribuidor estiver executando em uma plataforma de 64-bit, você deverá usar a versão de 64 bits do provedor OLE DB do Oracle.  
  
4.  Configure o banco de dados Oracle como um Publicador no Distribuidor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Para obter uma lista de objetos que podem ser publicados em um banco de dados Oracle, consulte [Considerações de design e limitações para Publicadores Oracle](design-considerations-and-limitations-for-oracle-publishers.md).  
  
> [!NOTE]  
>  Você deve ser um membro da função de servidor fixa **sysadmin** para habilitar um Publicador ou Distribuidor e para criar uma publicação Oracle ou uma assinatura de uma publicação Oracle.  
  
## <a name="creating-the-replication-administrative-user-schema-within-the-oracle-database"></a>Criando o esquema de usuários administrativo de replicação no banco de dados Oracle  
 Os agentes de replicação se conectam ao banco de dados Oracle, e executam operações no contexto de um esquema de usuário que você deve criar. Um número de permissões deve ser concedido ao esquema, os quais estão listados na próxima seção. Esse esquema contém todos os objetos criados pelo processo de replicação [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Publicador Oracle, com a exceção de um sinônimo público, **MSSQLSERVERDISTRIBUTOR**. Para obter mais informações sobre os objetos criados no banco de dados Oracle, consulte [Objects Created on the Oracle Publisher](objects-created-on-the-oracle-publisher.md).  
  
> [!NOTE]  
>  Remover o sinônimo público **MSSQLSERVERDISTRIBUTOR** e o usuário de replicação Oracle configurado com a opção **CASCADE** fará com que todos os objetos de replicação do Publicador Oracle sejam removidos.  
  
 Um script de amostra foi fornecido para ajudar na instalação do esquema de usuário de replicação Oracle. O script está disponível no seguinte diretório após a instalação de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: *\<unidade>*:\\\Arquivos de Programas\Microsoft SQL Server\\*\<InstanceName>* \MSSQL\Install\oracleadmin.sql. Também está incluído no tópico [Script to Grant Oracle Permissions](script-to-grant-oracle-permissions.md).  
  
 Conecte-se ao banco de dados Oracle usando uma conta com privilégios DBA e execute o script. Os prompts de script do usuário e senha para o esquema de usuário administrativo de replicação, assim como o espaço de tabela padrão, no qual os objetos serão criados (o espaço de tabela já deve existir no banco de dados Oracle). Para obter informações sobre como especificar outros espaços de tabela para objetos, consulte [Gerenciar espaços de tabela Oracle](manage-oracle-tablespaces.md). Escolha um nome de usuário e uma senha forte e anote ambas as informações, pois serão solicitadas depois que o banco de dados Oracle estiver configurado como um Publicador. É recomendado que o esquema seja usado apenas para objetos exigidos pelo aplicativo, não crie tabelas para serem publicadas nesse esquema.  
  
### <a name="creating-the-user-schema-manually"></a>Criando manualmente o esquema de usuário  
 Se você criar manualmente o esquema de usuário de replicação, é necessário conceder ao esquema as permissões a seguir, diretamente ou através de uma função de banco de dados.  
  
-   CREATE PUBLIC SYNONYM e DROP PUBLIC SYNONYM  
  
-   CREATE PROCEDURE  
  
-   CREATE SEQUENCE  
  
-   CREATE SESSION  
  
 Também será necessário conceder as seguintes permissões ao usuário diretamente (não por uma função):  
  
-   CREATE ANY TRIGGER. Isso é necessário somente na replicação transacional e de instantâneos.  
  
-   CREATE TABLE  
  
-   CREATE VIEW  
  
## <a name="installing-and-configuring-oracle-client-networking-software-on-the-sql-server-distributor"></a>Instalando e configurando o software de rede cliente Oracle no SQL Server Distributor  
 Você deve instalar e configurar o software de rede cliente Oracle e o provedor Oracle OLE DB no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Distributor, para que o Distributor possa fazer as conexões com o Publicador Oracle. Após instalar o software, defina as permissões adequadas nas pastas onde o software está instalado, e então, pare e reinicie a instância [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para garantir que todas as instâncias serão atualizadas (as permissões serão descritas a seguir, na seção "Definindo permissões de diretório").  
  
> [!NOTE]  
>  O cliente de rede cliente Oracle deve ser a versão mais recente disponível. A Oracle recomenda que os usuários instalem as mais recentes versões do software cliente. O software cliente é, portanto, muitas vezes uma versão mais recente do que o software do banco de dados.  
  
 A maneira mais prática para instalar e configurar o software de rede cliente, é usar o Oracle Universal Installer e o Net Configuration Assistant nos disco do Oracle Client.  
  
 No Instalador Universal Oracle, você deverá fornecer as seguintes informações:  
  
|Informações|Description|  
|-----------------|-----------------|  
|Oracle Home|Esse é o caminho para diretório de instalação do software Oracle. Aceite o padrão (C:\oracle\ora90 ou semelhante) ou digite outro caminho. Para obter mais informações sobre o Oracle Home, consulte a seção "Considerações sobre o Oracle Home" mais adiante neste tópico.|  
|Nome do Oracle home|Um alias para o caminho do Oracle home.|  
|Tipo de instalação|No Oracle 10g, selecione a opção de instalação **Administrador** .|  
  
 Após a conclusão do Instalador Universal Oracle, use o Assistente de Configuração Net para configurar a conectividade da rede. Você deve fornecer quatro informações para configurar a conectividade de rede. O administrador do banco de dados Oracle configura a configuração de rede quando define o banco de dados e o ouvinte e, se você não tiver essas informações, elas deverão ser fornecidas pelo administrador. Você deve fazer o seguinte:  
  
|Ação|Description|  
|------------|-----------------|  
|Identificar o banco de dados|Há dois métodos para identificar o banco de dados. O primeiro método usa o Sistema Identificador Oracle (SID) e está disponível em todas as versões do Oracle. O segundo método usa o nome de serviço, que está disponível a partir da versão 8.0 do Oracle. Ambos os métodos usam um valor que é configurado quando o banco de dados é criado, e é importante que a configuração de rede cliente use o mesmo método de nomenclatura que o administrador usou ao configurar o ouvinte para o banco de dados.|  
|Identificar um alias de rede para o banco de dados|Você deve especificar um alias de rede que será usado para acessar o banco de dados Oracle. Você também fornece esse alias quando identifica o banco de dados Oracle como um Publicador no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Distributor. O alias de rede é essencialmente um ponteiro para o SID remoto ou o nome de serviço que foi configurado quando o banco de dados foi criado, ele foi referenciado por diversos nomes em diferentes versões e produtos Oracle, incluindo o nome de serviço Net e o alias TNS. O SQL*Plus solicita esse alias como o parâmetro "Cadeia de caracteres de Host" ao efetuar logon.|  
|Selecionar o protocolo de rede|Selecione os protocolos apropriados que você gostaria de ter suporte. A maioria dos aplicativos usa o TCP.|  
|Especificar as informações de host para identificar o ouvinte de banco de dados|O host é o nome ou alias de DNS do computador no qual o ouvinte Oracle está executando, que costuma geralmente ser o mesmo computador no qual o banco de dados reside. Para alguns protocolos, você deve fornecer informações adicionais. Por exemplo, se você selecionar o TCP, deve fornecer a porta na qual o ouvinte está escutando as solicitações de conexão para o banco de dados de destino. A configuração do TCP padrão usa a porta 1521.|  
  
### <a name="setting-directory-permissions"></a>Definindo permissões de diretório  
 A conta sob a qual o serviço [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Distributor executa, deve receber permissões de gravação e leitura para o diretório (e todos os subdiretórios) no qual o software de rede cliente Oracle está instalado.  
  
### <a name="testing-connectivity-between-the-sql-server-distributor-and-the-oracle-publisher"></a>Testando conectividade entre o SQL Server Distributor e o Publicador Oracle  
 Quando estiver concluindo o Net Configuration Assistant deverá existir uma opção que irá testar a conexão do Publicador Oracle. Antes de você testar a conexão, garanta que a instância do banco de dados Oracle esteja on-line e que o Oracle Listener esteja executando. Se o teste for malsucedido, entre em contato com o DBA da Oracle, responsável pelo banco de dados ao qual você está tentando se conectar.  
  
 Após você ter feito uma conexão bem sucedida com o Publicador Oracle tente fazer logon no banco de dados, usando a conta e senha associadas com o esquema de usuário administrativo de replicação que você criou. Enquanto estiver executando na mesma conta do Windows que o serviço [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa, realize o seguinte:  
  
1.  Clique em **Iniciar**e em **Executar**.  
  
2.  Digite `cmd` e clique em **OK**.  
  
3.  No prompt de comando, digite:  
  
     `sqlplus <UserSchemaLogin>/<UserSchemaPassword>@<NetServiceName>`  
  
     Por exemplo: `sqlplus replication/$tr0ngPasswerd@Oracle90Server`  
  
4.  Se a configuração de redes foi bem-sucedida, o logon terá sucesso e você visualizará um prompt `SQL` .  
  
5.  Se você enfrentar problemas ao se conectar com o banco de dados Oracle, consulte a seção "O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Distributor não pode se conectar à instância do banco de dados Oracle" em [Troubleshooting Oracle Publishers](troubleshooting-oracle-publishers.md).  
  
### <a name="considerations-for-oracle-home"></a>Considerações sobre o Oracle Home  
 O Oracle oferece suporte à instalação lado a lado de binários aplicativos, mas apenas um conjunto de binários pode ser usado por replicação em um determinado momento. Cada conjunto de binários é associado a um Oracle Home; os binários estão no diretório %ORACLE_HOME%\bin. É necessário certificar-se de que o conjunto correto de binários (especificamente a versão mais recente do software de rede cliente) seja usado quando a replicação fizer as conexões com o Publicador Oracle.  
  
 Efetue o logon no Distribuidor com as contas usadas pelo serviço [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e o serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent e defina as variáveis de ambiente apropriadas. A variável %ORACLE_HOME% deve ser definida para fazer referência ao ponto de instalação que você especificou na instalação do software de rede cliente. O %PATH% deve incluir o diretório %ORACLE_HOME% \bin como a primeira entrada Oracle que for encontrada. Para obter mais informações sobre como definir as variáveis de ambiente, consulte a documentação do Windows.  
  
## <a name="configuring-the-oracle-database-as-a-publisher-at-the-sql-server-distributor"></a>Configurando o banco de dados Oracle como um Publicador no SQL Server Distributor  
 Editores Oracle sempre usam um Distribuidor remoto e é necessário configurar uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para agir como um Distribuidor para o Publicador Oracle (um Publicador Oracle pode usar apenas um Distribuidor mas, um único Distribuidor pode efetuar serviços em mais de um Publicador Oracle). Após configurar um Distribuidor, identifique a instância do banco de dados Oracle como sendo um Publicador no Distribuidor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] através do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], Transact-SQL ou do RMO (Replication Management Objects). Para obter mais informações sobre como configurar um Distribuidor, consulte [Configurar a distribuição](../configure-distribution.md).  
  
> [!NOTE]  
>  Um Publicador Oracle não pode ter o mesmo nome do Distribuidor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou o mesmo nome de um dos Editores [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , usando o mesmo Distribuidor.  
  
 Quando você identifica o banco de dados Oracle como sendo um Publicador, é necessário escolher uma opção de edição Oracle: Completa ou Oracle Gateway. Depois que um Publicador é identificado, essa opção não pode ser alterada sem descartar e reconfigurar o Publicador. A opção Completa é projetada para fornecer instantâneos e publicações transacionais com o conjunto completo de recursos com suporte para publicações Oracle. A opção Gateway fornece otimizações de projeto específicas para aprimorar o desempenho de casos em que a replicação serve como um gateway entre sistemas.  
  
 Após o Publicador Oracle ser identificado no Distribuidor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , a replicação cria um servidor vinculado com o mesmo nome como o nome do serviço TNS do banco de dados Oracle. Esse servidor vinculado só pode ser usado por replicação. Se você precisar se conectar ao Publicador Oracle usando uma conexão de servidor vinculado, crie outro nome de serviço TNS e use esse nome ao chamar [sp_addlinkedserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql).  
  
 Para configurar um Publicador Oracle e criar uma publicação, consulte [Create a Publication from an Oracle Database](../publish/create-a-publication-from-an-oracle-database.md).  
  
## <a name="see-also"></a>Consulte também  
 [Considerações administrativas sobre Publicadores Oracle](administrative-considerations-for-oracle-publishers.md)   
 [Mapeamento de tipo de dados para Publicadores Oracle](data-type-mapping-for-oracle-publishers.md)   
 [Glossário de termos para publicações Oracle](glossary-of-terms-for-oracle-publishing.md)   
 [Visão geral da publicação do Oracle](oracle-publishing-overview.md)  
  
  
