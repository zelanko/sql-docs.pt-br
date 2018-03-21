---
title: "Exibições | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: views
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-views
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- views [SQL Server], about views
ms.assetid: ada83c28-e8b7-45d9-b53c-b3d67c8820c8
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: de1be71afd708fab6f380daf4b60a0aeb87b2665
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2018
---
# <a name="views"></a>exibições
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]
  Uma exibição é uma tabela virtual cujos conteúdos são definidos por uma consulta. Como uma tabela, uma exibição consiste em um conjunto de colunas nomeadas e linhas de dados. Exceto se indexada, uma exibição não existe como um conjunto armazenado de valores de dados em um banco de dados. As linhas e colunas dos dados vêm de tabelas referidas em consultas que definem a exibição e são produzidas, dinamicamente, quando a exibição é referenciada.  
  
 Uma exibição atua como um filtro nas tabelas subjacentes na exibição. A consulta que define a exibição pode ser de uma ou mais tabelas ou de outras exibições dos bancos de dados atuais ou outros. As consultas distribuídas podem também ser usadas para definir as exibições que usam os dados de diversas fontes heterogêneas. Isso é útil, por exemplo, se você deseja combinar dados estruturados de forma semelhante de diferentes servidores, cada um dos quais armazena dados para uma região diferente de sua organização.  
  
 As exibições são geralmente usadas para focalizar, simplificar e personalizar a percepção que cada usuário tem do banco de dados. As exibições podem ser usadas como mecanismos de segurança para permitir que usuários acessem dados por meio da exibição, sem conceder-lhes permissões para acessarem diretamente as tabelas base subjacentes da exibição. As exibições podem ser usadas para fornecer uma interface compatível com versões anteriores para emular uma tabela que costumava existir, mas cujo esquema foi alterado. As exibições também podem ser usadas quando você copia dados para e de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para melhorar o desempenho e particionar dados.  
  
## <a name="types-of-views"></a>Tipos de exibições  
 Além da função padrão de exibições básicas definidas pelo usuário, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece os seguintes tipos de exibições que servem para propósitos especiais em um banco de dados:  
  
 Exibições indexadas  
 Uma exibição indexada é uma exibição que foi materializada. Isto significa que a definição de exibição foi computada e os dados resultantes foram armazenaram como uma tabela. Você indexa uma exibição criando um índice com cluster exclusivo nela. As exibições indexadas podem melhorar sensivelmente o desempenho de alguns tipos de consultas. As exibições indexadas funcionam melhor para consultas que agregam muitas linhas. Eles não são muito apropriadas para conjuntos de dados subjacentes atualizados com frequência.  
  
 Exibições particionadas  
 Uma exibição particionada associa dados particionados horizontalmente de um conjunto de tabelas membro em um ou mais servidores. Isso faz com que os dados pareçam ser provenientes de uma tabela. Uma exibição que associa tabelas membro na mesma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é uma exibição particionada local.  
  
 Exibições do sistema  
 Exibições do sistema expõem metadados de catálogo. Você pode usar exibições do sistema para retornar informações sobre a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou os objetos definidos na instância. Por exemplo, você pode consultar a exibição de catálogo de sys.databases para retornar informações sobre os bancos de dados definidos pelo usuário disponível na instância. Para obter mais informações, veja [Exibições do sistema &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
## <a name="common-view-tasks"></a>Tarefas de exibição comuns  
 A tabela a seguir fornece links a tarefas comuns associadas à criação ou modificação de uma exibição.  
  
|Tarefas de exibição|Tópico|  
|----------------|-----------|  
|Descreve como criar uma exibição.|[Criar exibições](../../relational-databases/views/create-views.md)|  
|Descreve como criar uma exibição indexada.|[Criar exibições indexadas](../../relational-databases/views/create-indexed-views.md)|  
|Descreve como modificar a definição de exibição.|[Modificar exibições](../../relational-databases/views/modify-views.md)|  
|Descreve como modificar dados por uma exibição.|[Modificar dados por meio de uma exibição](../../relational-databases/views/modify-data-through-a-view.md)|  
|Descreve como excluir uma exibição.|[Excluir exibições](../../relational-databases/views/delete-views.md)|  
|Descreve como retornar informações sobre uma exibição como a definição de exibição.|[Obter informações sobre uma exibição](../../relational-databases/views/get-information-about-a-view.md)|  
|Descreve como renomear uma exibição.|[Renomear exibições](../../relational-databases/views/rename-views.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Criar exibições sobre colunas XML](../../relational-databases/xml/create-views-over-xml-columns.md)   
 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)  
  
  
