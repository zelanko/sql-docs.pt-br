---
title: Referência do arquivo de entrada XML (Orientador de Otimização do Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Database Engine Tuning Advisor [SQL Server], XML input files
- input file reference [Database Engine Tuning Advisor]
- XML input files [Database Engine Tuning Advisor]
ms.assetid: 05e5e5f0-d6df-4336-b18e-e9bc2835a766
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4dfcae2c6d18b295919a3b843efe2edd95062d01
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48126186"
---
# <a name="xml-input-file-reference-database-engine-tuning-advisor"></a>Referência do arquivo de entrada XML (Orientador de Otimização do Mecanismo de Banco de Dados)
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] pode usar um arquivo de entrada XML para ajustar o banco de dados Este arquivo XML define os bancos de dados, tabelas, arquivos ou tabelas da carga de trabalho e as opções a serem usadas na sessão de ajuste. Você também pode usar este arquivo para indicar uma configuração específica de usuário a fim de realizar uma análise hipotética.  
  
 O arquivo de entrada do Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] contém uma hierarquia de elementos XML, cada qual contendo um texto ou outros elementos que especificam os parâmetros da sessão de ajuste. O arquivo de entrada XML do Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve seguir os padrões do XML bem formado para que todos os nomes dos elementos diferenciem letras maiúsculas e minúsculas. Os elementos são especificados usando a caixa Pascal, o que significa que o primeiro caractere está em maiúscula e a primeira letra de qualquer palavra concatenada subsequente está em maiúscula.  
  
 Todos os valores de elementos devem seguir as convenções de nomenclatura XML. Para obter mais informações sobre essas convenções, consulte o [XML Textual Content](http://go.microsoft.com/fwlink/?LinkId=7614) na MSDN Library.  
  
 Observe que esta referência não é abrangente. Para obter informações sobre todos os elementos que você pode usar para definir a entrada XML, consulte DTASchema.xds, o esquema XML do Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
## <a name="xml-declaration"></a>Declaração XML  
  
-   [Dados XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
## <a name="dtaxml-root-element"></a>Elemento raiz DTAXML  
  
-   [Elemento DTAXML &#40;DTA&#41;](dtaxml-element-dta.md)  
  
## <a name="dtainput-elements"></a>Elementos DTAInput  
  
-   [Elemento DTAInput &#40;DTA&#41;](dtainput-element-dta.md)  
  
-   [Elemento de servidor &#40;DTA&#41;](server-element-dta.md)  
  
-   [Elemento de carga de trabalho &#40;DTA&#41;](workload-element-dta.md)  
  
-   [Elemento TuningOptions &#40;DTA&#41;](tuningoptions-element-dta.md)  
  
-   [Elemento de configuração &#40;DTA&#41;](configuration-element-dta.md)  
  
## <a name="server-elements"></a>Elementos de servidor   
  
-   [Nome de elemento para o servidor &#40;DTA&#41;](name-element-for-server-dta.md)  
  
-   [Elemento Database para servidor &#40;DTA&#41;](database-element-for-server-dta.md)  
  
## <a name="workload-elements"></a>Elementos de Carga de Trabalho  
  
-   [Elemento de arquivo &#40;DTA&#41;](file-element-dta.md)  
  
-   [Elemento de banco de dados para carga de trabalho &#40;DTA&#41;](database-element-for-workload-dta.md)  
  
-   [Elemento EventString &#40;DTA&#41;](eventstring-element-dta.md)  
  
## <a name="tuning-options-elements"></a>Elementos de opções de ajuste  
  
-   [Elemento TuningTimeInMin &#40;DTA&#41;](tuningtimeinmin-element-dta.md)  
  
-   [Elemento StorageBoundInMB &#40;DTA&#41;](storageboundinmb-element-dta.md)  
  
-   [Elemento TestServer &#40;DTA&#41;](testserver-element-dta.md)  
  
-   [Elemento FeatureSet &#40;DTA&#41;](featureset-element-dta.md)  
  
-   [Elemento de particionamento &#40;DTA&#41;](partitioning-element-dta.md)  
  
-   [Elemento DropOnlyMode &#40;DTA&#41;](droponlymode-element-dta.md)  
  
-   [Elemento KeepExisting &#40;DTA&#41;](keepexisting-element-dta.md)  
  
-   [Elemento OnlineIndexOperation &#40;DTA&#41;](onlineindexoperation-element-dta.md)  
  
-   [Elemento DatabaseToConnect &#40;DTA&#41;](databasetoconnect-element-dta.md)  
  
## <a name="configuration-elements"></a>Elementos de configuração  
  
-   [Elemento Server para a configuração &#40;DTA&#41;](server-element-for-configuration-dta.md)  
  
-   [Elemento de banco de dados para a configuração &#40;DTA&#41;](database-element-for-configuration-dta.md)  
  
-   [Elemento de recomendação &#40;DTA&#41;](recommendation-element-dta.md)  
  
-   [Criar o elemento &#40;DTA&#41;](create-element-dta.md)  
  
-   [Elemento de índice &#40;DTA&#41;](index-element-dta.md)  
  
-   [Nomeie o elemento de índice &#40;DTA&#41;](name-element-for-index-dta.md)  
  
-   [Elemento Column para Index &#40;DTA&#41;](column-element-for-index-dta.md)  
  
-   [Nomeie o elemento para a coluna &#40;DTA&#41;](name-element-for-column-dta.md)  
  
-   [Elemento FileGroup para o índice &#40;DTA&#41;](filegroup-element-for-index-dta.md)  
  
## <a name="database-elements"></a>Elementos de banco de dados  
  
-   [Nome de elemento para o banco de dados &#40;DTA&#41;](name-element-for-database-dta.md)  
  
-   [Elemento de esquema para o banco de dados &#40;DTA&#41;](schema-element-for-database-dta.md)  
  
-   [Nome de elemento para o esquema &#40;DTA&#41;](name-element-for-schema-dta.md)  
  
-   [Elemento de tabela para esquema de &#40;DTA&#41;](table-element-for-schema-dta.md)  
  
-   [Nomeie o elemento para a tabela &#40;DTA&#41;](name-element-for-table-dta.md)  
  
## <a name="see-also"></a>Consulte também  
 [Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  
