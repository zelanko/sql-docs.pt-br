---
description: Referência do Transact-SQL (Mecanismo de Banco de Dados)
title: Referência do Transact-SQL (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 04/29/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- sql13.tsqlref.f1
- devlang-tsql
helpviewer_keywords:
- Transact-SQL
ms.assetid: dbba47d7-e08e-4435-b876-35dced1f325d
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 727dc40389d803cc81bb07011f799bc2d44365a0
ms.sourcegitcommit: 1126792200d3b26ad4c29be1f561cf36f2e82e13
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/14/2020
ms.locfileid: "90076663"
---
# <a name="transact-sql-reference-database-engine"></a>Referência do Transact-SQL (Mecanismo de Banco de Dados)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]

Este tópico fornece as noções básicas de como encontrar e usar os tópicos de referência do Microsoft [!INCLUDE[tsql](../includes/tsql-md.md)] (T-SQL). O T-SQL é fundamental para a utilização dos serviços e produtos do Microsoft SQL. Todas as ferramentas e todos os aplicativos que se comunicam com um Banco de Dados SQL desempenham essa função ao enviar comandos do T-SQL.  

## <a name="t-sql-compliance-to-sql-standard"></a>Conformidade do T-SQL com o Padrão SQL
Para ver documentos técnicos detalhados sobre como determinados padrões são implementados no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], confira a [Documentação de Suporte a Padrões do Microsoft SQL Server](https://docs.microsoft.com/openspecs/sql_standards/ms-sqlstandlp/89fb00b1-4b9e-4296-92ce-a2b3f7ca01d2).

## <a name="tools-that-use-t-sql"></a>Ferramentas que utilizam o T-SQL
Algumas das ferramentas da Microsoft que emitem comandos do T-SQL são:

- [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)
- [SSDT (SQL Server Data Tools)](../ssdt/download-sql-server-data-tools-ssdt.md)
- [sqlcmd](../tools/sqlcmd-utility.md)
- [Azure Data Studio](../azure-data-studio/what-is.md)
  
## <a name="locate-the-transact-sql-reference-topics"></a>Localizar os tópicos de referência do Transact-SQL  
Para encontrar os tópicos do T-SQL, utilize a pesquisa na parte superior direita ou o índice à esquerda desta página. Você também pode digitar uma palavra-chave do T-SQL na janela do Editor de Consultas do Management Studio e pressionar F1. 
  
## <a name="find-system-views"></a>Encontrar exibições do sistema
Para encontrar tabelas, exibições, funções e procedimentos do sistema, consulte esses links que estão na seção [Using relational databases](../relational-databases/database-features.md) (Usando bancos de dados relacionais) na documentação do SQL.

- [Exibições de catálogo do sistema](../relational-databases/system-catalog-views/catalog-views-transact-sql.md)
- [Exibições de compatibilidade do sistema](../relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)
- [Exibições de gerenciamento dinâmico do sistema](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
- [Funções do sistema](../relational-databases/system-functions/system-functions-category-transact-sql.md)
- [Exibições do esquema de informações do sistema](../relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)
- [Procedimentos armazenados do sistema](../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)
- [Tabelas do sistema](../relational-databases/system-tables/system-tables-transact-sql.md)

## <a name="applies-to-references"></a>Referências de "Aplica-se a"  
 Os tópicos de referência do T-SQL abrangem várias versões do SQL Server, começando com a versão 2008, bem como outros serviços do SQL do Azure. Próximo à parte superior de cada tópico há uma seção que indica quais produtos e serviços são compatíveis com o assunto do tópico. 

Por exemplo, este tópico é aplicável a todas as versões e tem o rótulo a seguir. 
  
 [!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]   

No próximo exemplo, o rótulo a seguir indica um tópico que é aplicável apenas ao Azure Synapse Analytics e ao Parallel Data Warehouse.

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../includes/applies-to-version/asa-pdw.md)]

Em alguns casos, o tópico é utilizado por um produto ou serviço, mas nem todos os argumentos são compatíveis. Nesse caso, seções **Aplica-se a** adicionais são inseridas em descrições de argumento apropriado no corpo do tópico.  
 
## <a name="get-help-from-microsoft-q--a"></a>Obtenha ajuda do P e R da Microsoft  
Para obter ajuda online, confira o [Fórum do Transact-SQL de P e R da Microsoft](https://docs.microsoft.com/answers/topics/sql-server-transact-sql.html).  
 
## <a name="see-other-language-references"></a>Consulte outras referências de linguagem
Os documentos do SQL incluem essas outras referências de linguagem:
  
- [Referência de linguagem do XQuery](../xquery/xquery-language-reference-sql-server.md)
- [Referência de Linguagem do Integration Services](../integration-services/integration-services-language-reference.md)
- [Referência de linguagem de replicação](../relational-databases/replication/replication-language-reference.md)
- [Referência de linguagem do Analysis Services](../mdx/analysis-services-language-reference.md)  

## <a name="next-steps"></a>Próximas etapas
Agora que já sabe como encontrar os tópicos de referência do T-SQL, você está pronto para:

- Trabalho por meio de um breve tutorial sobre como gravar o T-SQL, confira [Tutorial: Escrevendo instruções Transact-SQL](../t-sql/tutorial-writing-transact-sql-statements.md). 
- Exibir as [Convenções de sintaxe&#40;Transact-SQL&#41;](../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  

  
  
