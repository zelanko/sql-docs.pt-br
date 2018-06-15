---
title: Bancos de dados do sistema | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- system databases [SQL Server]
- displaying system database data
- modifying system data
- viewing system database data
ms.assetid: 30468a7c-4225-4d35-aa4a-ffa7da4f1282
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d5bf6819d26ff105113292162c3302d54460a6e1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32931531"
---
# <a name="system-databases"></a>Bancos de dados do sistema
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inclui os seguintes bancos de dados do sistema.  
  
|Banco de dados do sistema|Description|  
|---------------------|-----------------|  
|[Banco de dados mestre](../../relational-databases/databases/master-database.md)|Registra toda a informações de nível de sistema por uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Banco de dados msdb](../../relational-databases/databases/msdb-database.md)|É usado pelo SQL Server Agent para programar alertas e trabalhos.|  
|[Banco de dados modelo](../../relational-databases/databases/model-database.md)|É usado como modelo de todos os bancos de dados criados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. As modificações feitas no banco de dados **modelo** , como tamanho, agrupamento, modelo de recuperação, e outras opções de bancos de dados, são aplicadas a qualquer banco de dados criados em seguida.|  
|[Banco de dados de recursos](../../relational-databases/databases/resource-database.md)|É um banco de dados do tipo somente leitura que contém objetos de sistema incluídos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os objetos de sistema são fisicamente persistentes no banco de dados **Recurso** , mas aparecem logicamente no esquema **sys** de todo banco de dados.|  
|[Banco de dados tempdb](../../relational-databases/databases/tempdb-database.md)|É um espaço de trabalho para reter objetos temporários ou conjuntos de resultados intermediários.|  

> [!IMPORTANT]
> Para o Banco de Dados SQL do Azure, somente se aplicam o banco de dados mestre e o banco de dados tempdb. Para saber o conceito de servidor lógico e banco de dados mestre lógico, confira [O que é um servidor lógico do SQL Azure?](https://docs.microsoft.com/azure/sql-database/sql-database-servers-databases#what-is-an-azure-sql-logical-server). Para obter uma discussão sobre o tempdb no contexto do Banco de Dados SQL do Azure, confira [Banco de dados tempdb no Banco de Dados SQL do Azure](tempdb-database.md#tempdb-database-in-sql-database).
  
## <a name="modifying-system-data"></a>modificando dados do sistema  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não oferece suporte aos usuários diretamente na atualização de informações de objetos do sistema como tabelas de sistema, procedimentos armazenados do sistema  e exibições de catálogo. Em lugar disso, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece um conjunto completo de ferramentas administrativas que permitem aos usuários administrar totalmente seus sistemas e gerenciar todos os usuários e objetos de um banco de dados. Entre elas estão as seguintes:  
  
-   Utilitários de administração, como o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
-   SQL-SMO API. Isso permite que os programadores incluam a funcionalidade completa para administrar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em seus aplicativos.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] . Podem usar procedimentos armazenados do sistema e instruções DDL [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
 Essas ferramentas protegem os aplicativos das alterações nos objetos de sistema. Por exemplo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] algumas vezes precisa alterar as tabelas de sistema em novas versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para dar suporte a nova funcionalidade adicionada nessa versão. Os aplicativos que emitem instruções SELECT que diretamente referenciam tabelas do sistema são frequentemente dependentes do formato antigo das tabelas do sistema. Possivelmente, os sites só serão capazes de fazer a atualizar para uma nova versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] após regravarem os aplicativos que estão sendo selecionados nas tabelas do sistema. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera os procedimentos armazenados do sistema, a DDL e as interfaces publicadas SQL-SMO, e trabalha para manter a compatibilidade com as versões anteriores dessas interfaces.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não oferece suporte a gatilhos definidos nas tabelas do sistema, pois eles podem modificar a operação do sistema.  
  
> [!NOTE]  
>  Bancos de dados do sistema não podem residir em diretórios de compartilhamento UNC.  
  
## <a name="viewing-system-database-data"></a>exibindo dados de sistema do banco de dados  
 Você não deve codificar instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que fazem consulta diretamente nas tabelas do sistema, a menos que seja a única maneira de obter as informações exigidas pelo aplicativo. Em lugar disso, os aplicativos devem obter informações de catálogos e do sistema usando o seguinte:  
  
-   Exibições de catálogo do sistema  
  
-   SQL-SMO  
  
-   Interface de Instrumentação de Gerenciamento do Windows (WMI)  
  
-   Funções de catálogo, métodos, atributos, ou propriedades das API de dados usados no aplicativo, como ADO, OLE DB, ou ODBC.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimentos armazenados do sistema e funções internas.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Fazer backup e restaurar bancos de dados do sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [Ocultar objetos do sistema no Pesquisador de Objetos](http://msdn.microsoft.com/library/c01d8804-838c-4f75-b78c-80e41e4fffdc)  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
 [Bancos de dados](../../relational-databases/databases/databases.md)  
  
  
