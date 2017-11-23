---
title: Bancos de dados independentes | Microsoft Docs
ms.custom: 
ms.date: 08/24/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- contained database
- database_uncontained_usage event
- partially contained database
- contained database, understanding
ms.assetid: 36af59d7-ce96-4a02-8598-ffdd78cdc948
caps.latest.revision: "37"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: c39632f5d9580b652f57cec05000649af7591fc2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="contained-databases"></a>Bancos de dados independentes
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Um *banco de dados independente* é um banco de dados isolado de outros bancos de dados e da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda o banco de dados.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ajuda o usuário a isolar seu banco de dados da instância de 4 maneiras.  
  
-   A maioria dos metadados que descrevem um banco de dados é mantida no banco de dados. (Além de, ou em vez de, manter os metadados no banco de dados mestre.)  
  
-   Todo os metadados são definidos usando o mesmo agrupamento.  
  
-   A autenticação de usuário pode ser executada pelo banco de dados, reduzindo a dependência dos bancos de dados dos logons da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   O ambiente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (DMVs, XEvents etc.) relata e pode agir sobre as informações de contenção.  
  
 Alguns recursos de bancos de dados parcialmente independentes, como armazenar metadados no banco de dados, aplicam-se a todos os bancos de dados do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Alguns benefícios dos bancos de dados parcialmente independentes, como autenticação no nível de banco de dados e agrupamento de catálogos, devem ser habilitados antes de serem disponibilizados. A contenção parcial é habilitada usando as instruções **CREATE DATABASE** e **ALTER DATABASE** ou usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações sobre como habilitar a contenção parcial de bancos de dados, consulte [Migrate to a Partially Contained Database](../../relational-databases/databases/migrate-to-a-partially-contained-database.md).  
  
##  <a name="Concepts"></a> Conceitos de banco de dados parcialmente independente  
 Um banco de dados totalmente independente inclui todas as configurações e metadados necessários para definir o banco de dados e não tem nenhuma dependência de configuração da instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] onde o banco de dados está instalado. Em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], separar um banco de dados da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderia ser demorado e exigir conhecimento detalhado da relação entre o banco de dados e a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os bancos de dados parcialmente independentes facilitam a separação de um banco de dados de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e de outros bancos de dados.  
  
 O banco de dados independente considera recursos em relação à contenção. Qualquer entidade definida pelo usuário que confie apenas em funções que residem no banco de dados é considerada totalmente contida. Qualquer entidade definida pelo usuário que confie apenas em funções que residem fora do banco de dados é considerada não contida. (Para obter mais informações, consulte a seção [Contenção](#containment) mais adiante neste tópico.)  
  
 Os termos a seguir se aplicam ao modelo de banco de dados independente.  
  
 Limite de banco de dados  
 O limite entre um banco de dados e a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O limite entre um banco de dados e outros bancos de dados.  
  
 Contida  
 Um elemento que existe completamente no limite de banco de dados.  
  
 Não contida  
 Um elemento que cruza o limite de banco de dados.  
  
 Banco de dados dependente  
 Um banco de dados com contenção definida como **NONE**. Todos os bancos de dados em versões anteriores ao [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] são dependentes. Por padrão, todos os bancos de dados do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posteriores têm um conjunto de contenção definido como **NONE**.  
  
 Banco de dados parcialmente contido  
 Um banco de dados parcialmente independente é um banco de dados independente que permite que alguns recursos cruzem o limite de banco de dados. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inclui a capacidade de determinar quando o limite de retenção é cruzado.  
  
 Usuário contido  
 Há dois tipos de usuários de bancos de dados independentes.  
  
-   **Usuário de banco de dados independente com senha**  
  
     Usuários de banco de dados independente com senhas são autenticados pelo banco de dados. Para obter mais informações, consulte [Usuários de bancos de dados independentes – Tornando seu banco de dados portátil](../../relational-databases/security/contained-database-users-making-your-database-portable.md).  
  
-   **entidades de segurança do Windows**  
  
     Usuários autorizados do Windows e membros de grupos autorizados do Windows podem conectar-se diretamente ao banco de dados e não precisam de logons no banco de dados **mestre** . O banco de dados confia na autenticação pelo Windows.  
  
 Os usuários baseados em logons no banco de dados **mestre** podem receber acesso a um banco de dados independente, mas isso cria uma dependência na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Portanto, criar usuários com base em logons permite ver comentários sobre bancos de dados parcialmente independentes.  
  
> [!IMPORTANT]  
>  Habilitar delegados de bancos de dados parcialmente independentes controla o acesso à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para os proprietários do banco de dados. Para saber mais, veja [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md).  
  
 Limite de banco de dados  
 Como os bancos de dados parcialmente independentes separam a funcionalidade do banco de dados das funcionalidades da instância, há uma linha claramente definida entre esses dois elementos chamada de *limite de banco de dados*.  
  
 Dentro do limite de banco de dados está o *modelo de banco de dados*, onde os bancos de dados são desenvolvidos e gerenciados. Exemplos de entidades localizadas dentro do modelo do banco de dados incluem tabelas do sistema, como **sys.tables**, usuários com senhas de bancos de dados independentes e tabelas de usuário no banco de dados atual referenciadas por um nome de duas partes.  
  
 Fora do limite de banco de dados está o *modelo de gerenciamento*que pertence às funções e ao gerenciamento em nível da instância. Exemplos de entidades localizadas fora do limite de banco de dados incluem tabelas do sistema, como **sys.endpoints**, usuários mapeados para logons e tabelas de usuário em outro banco de dados referenciadas por um nome de três partes.  
  
##  <a name="containment"></a> Contenção  
 Entidades de usuário que residem inteiramente dentro do banco de dados são consideradas *contidas*. Qualquer entidade que resida fora do banco de dados ou que dependa da interação com funções fora do banco de dados é considerada como *não contida*.  
  
 Em geral, entidades de usuário entram nas seguintes categorias de contenção:  
  
-   Entidades de usuário totalmente contidas (que nunca cruzam o limite de banco de dados), por exemplo sys.indexes. Qualquer código que use esses recursos ou qualquer objeto que faça referência apenas a essas entidades também é totalmente contido.  
  
-   Entidades de usuário não contidas (que cruzam o limite de banco de dados), por exemplo, sys.server_principals ou a própria entidade de servidor (logon). Qualquer código que use essas entidades ou qualquer função que faça referência a essas entidades não é contido.  
  
###  <a name="partial"></a> Partially Contained Database  
 O recurso de banco de dados independente está disponível atualmente apenas em um estado parcialmente contido. Um banco de dados parcialmente contido é um banco de dados independente que permite o uso de recursos não contidos.  
  
 Use as exibições [sys.dm_db_uncontained_entities](../../relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql.md) e [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) para retornar informações sobre objetos ou recursos não contidos. Por meio da determinação do status da contenção dos elementos de seu banco de dados, é possível descobrir quais objetos ou recursos devem ser substituídos os alterados para promover a contenção.  
  
> [!IMPORTANT]  
>  Como determinados objetos têm uma configuração de contenção padrão de **NONE**, essa exibição pode retornar falsos positivos.  
  
 O comportamento de bancos de dados parcialmente independentes difere muito distintamente do comportamento de bancos de dados dependentes em termos de agrupamento. Para obter mais informações sobre problemas de agrupamento, consulte [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md).  
  
##  <a name="benefits"></a> Benefícios do uso de bancos de dados parcialmente independentes  
 Há problemas e complicações associadas aos bancos de dados dependentes que podem ser resolvidos por meio de um banco de dados parcialmente independente.  
  
### <a name="database-movement"></a>Movimentação do banco de dados  
 Um dos problemas que ocorre ao mover bancos de dados é que algumas informações importantes podem não estar disponíveis quando um banco de dados é movido de uma instância a outra. Por exemplo, as informações de logon são armazenadas na instância e não no banco de dados. Quando você move um banco de dados dependente de uma instância para outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essas informações são deixadas para trás. Você deve identificar as informações ausentes e movê-las com seu banco de dados para a nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esse processo pode ser difícil e demorado.  
  
 O banco de dados parcialmente independente pode armazenar informações importantes no banco de dados para que o banco de dados ainda contenha as informações depois de ser movido.  
  
> [!NOTE]  
>  Um banco de dados parcialmente independente pode fornecer documentação que descreve os recursos que são usados por um banco de dados que não pode ser separado da instância. Isso inclui uma lista de outros bancos de dados relacionados, configurações do sistema exigidas pelo banco de dados, mas que não podem ser contidas, e assim por diante.  
  
### <a name="benefit-of-contained-database-users-with-always-on"></a>Benefício de usuários de banco de dados independentes com AlwaysOn  
 Reduzindo as associações à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], bancos de dados parcialmente independentes podem ser úteis durante o failover quando o [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]é usado.  
  
 Criar os usuários independentes permite que o usuário se conecte diretamente no banco de dados independente. Este é um recurso muito significativo em cenários de alta disponibilidade e recuperação de desastres como em uma solução AlwaysOn. Se os usuários forem independentes, no caso de failover, as pessoas podem ser capazes de se conectar ao secundário sem criar logons na instância que hospeda o secundário. Isto fornece um benefício imediato. Para obter mais informações, consulte [Visão geral dos Grupos de Disponibilidade AlwaysOn (SQL Server)](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md) e [Pré-requisitos, restrições e recomendações para Grupos de Disponibilidade AlwaysOn (SQL Server)](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
### <a name="initial-database-development"></a>Desenvolvimento inicial de bancos de dados  
 Como um desenvolvedor talvez não saiba onde um novo banco de dados será implantado, a limitação dos impactos no ambiente implantados no banco de dados reduz o trabalho e a preocupação do desenvolvedor. No modelo não contido, o desenvolvedor deve considerar os possíveis impactos no ambiente no novo banco de dados e programa de maneira correspondente. No entanto, ao usar bancos de dados parcialmente independentes, os desenvolvedores podem detectar impactos de nível de instância no banco de dados e preocupações de nível de instância para o desenvolvedor.  
  
### <a name="database-administration"></a>Administração de banco de dados  
 Manter as configurações de banco de dados no banco de dados, e não no banco de dados mestre, permite que o proprietário de cada banco de dados tenha mais controle sobre seu banco de dados, sem conceder a eles a permissão **sysadmin** .  
  
##  <a name="Limitations"></a> Limitações  
 Bancos de dados parcialmente independentes não permitem os recursos a seguir.  
  
-   Os bancos de dados parcialmente independentes não podem usar replicação, Change Data Capture ou controle de alterações.  
  
-   Procedimentos numerados  
  
-   Objetos associados a esquema que dependem de funções internas com alterações de agrupamento  
  
-   Alteração de associação resultante de alterações de agrupamento, inclusive referências a objetos, colunas, símbolos ou tipos.  
  
-   Replicação, captura de dados de alteração e controle de alterações.  
  
> [!WARNING]  
>  Os procedimentos armazenados temporários são permitidos no momento. Como os procedimentos armazenados temporários violam a retenção, não se espera que eles tenham suporte em versões futuras de bancos de dados independentes.  
  
##  <a name="Identifying"></a> Identificando a contenção do banco de dados  
 Há duas ferramentas para facilitar a identificação do status de contenção do banco de dados. O [sys.dm_db_uncontained_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql.md) é uma exibição que mostra todas as entidades potencialmente não contidas no banco de dados. O evento database_uncontained_usage ocorre quando qualquer entidade não contida real é identificada em tempo de execução.  
  
### <a name="sysdmdbuncontainedentities"></a>sys.dm_db_uncontained_entities  
 Esta exibição mostra as entidades do banco de dados que têm potencial para não serem contidas, como aquelas que cruzam o limite de banco de dados. Isso inclui as entidades de usuário que possam usar objetos fora do modelo de banco de dados. Porém, como a contenção de algumas entidades (por exemplo, as que usam SQL dinâmico) não pode ser determinada até o tempo de execução, a exibição poderá mostrar algumas entidades que não estão contidas realmente. Para obter mais informações, consulte [sys.dm_db_uncontained_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql.md).  
  
### <a name="databaseuncontainedusage-event"></a>evento database_uncontained_usage  
 Esse XEvent ocorre sempre que uma entidade não contida é identificada no momento de execução. Isso inclui entidades originadas no código de cliente. Esse XEvent ocorrerá somente para entidades reais não contidas. No entanto, o evento ocorre somente no momento de execução. Portanto, qualquer entidade de usuário não contida não executada não será identificada por esse XEvent.  
  
## <a name="see-also"></a>Consulte também  
 [Recursos modificados &#40;Banco de Dados Contidos&#41;](../../relational-databases/databases/modified-features-contained-database.md)   
 [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md)   
 [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md)   
 [Migrate to a Partially Contained Database](../../relational-databases/databases/migrate-to-a-partially-contained-database.md)   
 [Usuários de bancos de dados independentes – Tornando seu banco de dados portátil](../../relational-databases/security/contained-database-users-making-your-database-portable.md)  
  
  
