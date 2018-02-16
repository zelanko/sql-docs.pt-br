---
title: Conjuntos de linhas do esquema OLE DB | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- schema rowsets [OLE DB]
- schema rowsets [Analysis Services], OLE DB
- OLE DB schema rowsets
- rowsets [Analysis Services], OLE DB
ms.assetid: ca2ee87a-ba04-4501-9125-33934c58ab31
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 59d17cb1345f7ba32a2cbaac27f5ec002aadfa40
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="ole-db-schema-rowsets"></a>Conjuntos de linhas do esquema OLE DB
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
Os conjuntos de linhas do esquema OLE DB a seguir são suportados pelo provedor de XMLA (XML for Analysis) do [!INCLUDE[msCoName](../../../includes/msconame-md.md)]. Use o **DISCOVER_ENUMERATORS** conjunto de linhas com o [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) método para verificar se um provedor de fonte de dados específico oferece suporte a um conjunto de linhas.  
  
 Você também poderá encontrar informações detalhadas sobre esses conjuntos de linhas pesquisando o tópico (Conjuntos de linhas do esquema" na parte de referência do programador de OLE DB da MSDN® Library, no site do [!INCLUDE[msCoName](../../../includes/msconame-md.md)].  
  
 A tabela a seguir descreve este conjunto de linhas do esquema.  
  
|Conjunto de linhas|Description|  
|------------|-----------------|  
|**DBSCHEMA_ASSERTIONS**|Identifica as asserções definidas no catálogo e que são propriedade de um determinado usuário.|  
|[DBSCHEMA_CATALOGS Rowset](../../../analysis-services/schema-rowsets/ole-db/dbschema-catalogs-rowset.md) <sup>1</sup>|Identifica os atributos físicos associados a catálogos acessíveis do sistema de gerenciamento de banco de dados (DBMS). Para alguns sistemas, como o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Access, só pode haver um catálogo. Para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], esse conjunto de linhas enumera todos os catálogos (bancos de dados) definidos no banco de dados do sistema.|  
|**DBSCHEMA_CHARACTER_SETS**|Identifica os conjuntos de caracteres definidos no catálogo e acessíveis para um determinado usuário.|  
|**DBSCHEMA_CHECK_CONSTRAINTS**|Identifica as restrições de verificação definidas no catálogo e que são propriedade de um determinado usuário.|  
|**DBSCHEMA_CHECK_CONSTRAINTS_BY_TABLE**|Identifica as restrições de verificação para uma determinada tabela, definidas em um catálogo que é propriedade de um determinado usuário.|  
|**DBSCHEMA_COLLATIONS**|Identifica os agrupamentos de caracteres definidos no catálogo e acessíveis para um determinado usuário.|  
|**DBSCHEMA_COLUMN_DOMAIN_USAGE**|Identifica as colunas definidas no catálogo dependentes em um domínio definido no catálogo e que são propriedade de um determinado usuário.|  
|**DBSCHEMA_COLUMN_PRIVILEGES**|Identifica os privilégios em colunas de tabelas definidas no catálogo e que estão disponíveis para um determinado usuário ou que foram concedidos por ele.|  
|[DBSCHEMA_COLUMNS Rowset](../../../analysis-services/schema-rowsets/ole-db/dbschema-columns-rowset.md) <sup>1</sup>|Oferece informações de coluna por todas as colunas que atendem aos critérios de restrição fornecidos.|  
|**DBSCHEMA_CONSTRAINT_COLUMN_USAGE**|Identifica as colunas usadas por restrições referenciais, restrições exclusivas, restrições de verificação e asserções definidas no catálogo e que são propriedade de um determinado usuário.|  
|**DBSCHEMA_CONSTRAINT_TABLE_USAGE**|Identifica as tabelas usadas por restrições referenciais, restrições exclusivas, restrições de verificação e asserções definidas no catálogo e que são propriedade de um determinado usuário.|  
|**DBSCHEMA_FOREIGN_KEYS**|Identifica as colunas de chave estrangeira definidas no catálogo por um determinado usuário. Esse conjunto de linhas do esquema é compilado em várias exibições do esquema ISO como uma conveniência ao programador de linguagens diferentes de SQL. Se suportado, esse conjunto de linhas do esquema deverá ser sincronizado com as exibições ISO relacionadas (**REFERENTIAL_CONSTRAINTS** e **CONSTRAINT_COLUMN_USAGE**).|  
|**DBSCHEMA_INDEXES**|Identifica os índices definidos no catálogo e que são propriedade de um determinado usuário.|  
|**DBSCHEMA_KEY_COLUMN_USAGE**|Identifica as colunas definidas no catálogo e que são restringidas como chaves por um determinado usuário.|  
|**DBSCHEMA_PRIMARY_KEYS**|Identifica as colunas de chave primária definidas no catálogo por um determinado usuário. Esse conjunto de linhas de esquema é compilado em uma exibição de esquema ISO como uma conveniência para o programador de linguagens diferentes de SQL. Se suportado, esse conjunto de linhas de esquema deve ser sincronizado com a exibição ISO relacionada (**CONSTRAINT_COLUMN_USAGE**).|  
|**DBSCHEMA_PROCEDURE_COLUMNS**|Retorna informações sobre as colunas de conjuntos de linhas retornadas por procedimentos.|  
|**DBSCHEMA_PROCEDURE_PARAMETERS**|Retorna informações sobre os parâmetros e códigos de retorno de procedimentos.|  
|**DBSCHEMA_PROCEDURES**|Identifica os procedimentos definidos no catálogo e que são propriedade de um determinado usuário. É uma extensão OLE DB.|  
|[DBSCHEMA_PROVIDER_TYPES Rowset](../../../analysis-services/schema-rowsets/ole-db/dbschema-provider-types-rowset.md) <sup>1</sup>|Identifica os tipos de dados (base) suportados pelo provedor de dados.|  
|**DBSCHEMA_REFERENTIAL_CONSTRAINTS**|Identifica as restrições referenciais definidas no catálogo e que são propriedade de um determinado usuário.|  
|**DBSCHEMA_SCHEMATA**|Identifica os esquemas que são propriedade de um determinado usuário.|  
|**DBSCHEMA_SQL_LANGUAGES**|Identifica os níveis de conformidade, as opções e os dialetos suportados pela implementação de SQL que processa os dados definidos no catálogo.|  
|**DBSCHEMA_STATISTICS**|Identifica as estatísticas definidas no catálogo e que são propriedade de um determinado usuário.<br /><br /> Esta tabela não está relacionada ao **TABLE_STATISTICS** conjunto de linhas.|  
|**DBSCHEMA_TABLE_CONSTRAINTS**|Identifica as restrições de tabela definidas no catálogo e que são propriedade de um determinado usuário.|  
|**DBSCHEMA_TABLE_PRIVILEGES**|Identifica os privilégios em tabelas definidas no catálogo e que estão disponíveis para um determinado usuário ou que foram concedidos por ele.|  
|**DBSCHEMA_TABLE_STATISTICS**|Descreve o conjunto de estatísticas disponível em tabelas no provedor.<br /><br /> Esse conjunto de linhas não está relacionado ao **estatísticas** conjunto de linhas.|  
|[DBSCHEMA_TABLES Rowset](../../../analysis-services/schema-rowsets/ole-db/dbschema-tables-rowset.md) <sup>1</sup>|Identifica os grupos de medidas e dimensões expostos como tabelas no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|**DBSCHEMA_TABLES_INFO** <sup>1</sup>|Identifica as tabelas (incluindo as exibições) definidas no catálogo e acessíveis a um determinado usuário.|  
|**DBSCHEMA_TRANSLATIONS**|Identifica as traduções de caracteres definidas no catálogo e acessíveis para um determinado usuário.|  
|**DBSCHEMA_TRUSTEE**|Enumera os objetos de confiança para uma fonte de dados.|  
|**DBSCHEMA_USAGE_PRIVILEGES**|Identifica o **uso** privilégios em objetos que são definidos no catálogo e estão disponíveis para ou concedido por um determinado usuário.|  
|**DBSCHEMA_VIEW_COLUMN_USAGE**|Identifica as exibições definidas no catálogo e acessíveis para um determinado usuário.|  
|**DBSCHEMA_VIEW_TABLE_USAGE**|Identifica as tabelas das quais as tabelas exibidas, definidas no catálogo e que são propriedade de um determinado usuário, são dependentes.|  
|**DBSCHEMA_VIEWS**|Identifica as exibições definidas no catálogo e acessíveis para um determinado usuário.|  
  
 <sup>1</sup> indica conjuntos de linhas do esquema suportados pelo provedor de fonte de dados MSOLAP para o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] provedor XMLA.  
  
## <a name="see-also"></a>Consulte também  
 [Conjunto de linhas DISCOVER_ENUMERATORS](../../../analysis-services/schema-rowsets/xml/discover-enumerators-rowset.md)   
 [Conjuntos de linhas do esquema do Analysis Services](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
