---
title: Referência do arquivo (mecanismo de banco de dados do Orientador de otimização) de entrada XML | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: dta
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- Database Engine Tuning Advisor [SQL Server], XML input files
- input file reference [Database Engine Tuning Advisor]
- XML input files [Database Engine Tuning Advisor]
ms.assetid: 05e5e5f0-d6df-4336-b18e-e9bc2835a766
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d507c858f2103af6521e57ffca3385a23c913cd2
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/17/2018
---
# <a name="xml-input-file-reference-database-engine-tuning-advisor"></a>Referência do arquivo de entrada XML (Orientador de Otimização do Mecanismo de Banco de Dados)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)] Orientador de otimização pode usar um arquivo de entrada XML para ajustar um banco de dados. Este arquivo XML define os bancos de dados, tabelas, arquivos ou tabelas da carga de trabalho e as opções a serem usadas na sessão de ajuste. Você também pode usar este arquivo para indicar uma configuração específica de usuário a fim de realizar uma análise hipotética.  
  
 O arquivo de entrada do Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] contém uma hierarquia de elementos XML, cada qual contendo um texto ou outros elementos que especificam os parâmetros da sessão de ajuste. O arquivo de entrada XML do Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve seguir os padrões do XML bem formado para que todos os nomes dos elementos diferenciem letras maiúsculas e minúsculas. Os elementos são especificados usando a caixa Pascal, o que significa que o primeiro caractere está em maiúscula e a primeira letra de qualquer palavra concatenada subsequente está em maiúscula.  
  
 Todos os valores de elementos devem seguir as convenções de nomenclatura XML. Para obter mais informações sobre essas convenções, consulte o [XML Textual Content](http://go.microsoft.com/fwlink/?LinkId=7614) na MSDN Library.  
  
 Observe que esta referência não é abrangente. Para obter informações sobre todos os elementos que você pode usar para definir a entrada XML, consulte DTASchema.xds, o esquema XML do Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
## <a name="xml-declaration"></a>Declaração XML  
  
-   [Dados XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
## <a name="dtaxml-root-element"></a>Elemento raiz DTAXML  
  
-   [Elemento DTAXML &#40; DTA &#41;](../../tools/dta/dtaxml-element-dta.md)  
  
## <a name="dtainput-elements"></a>Elementos DTAInput  
  
-   [Elemento DTAInput &#40; DTA &#41;](../../tools/dta/dtainput-element-dta.md)  
  
-   [Elemento Server &#40; DTA &#41;](../../tools/dta/server-element-dta.md)  
  
-   [Elemento Workload &#40; DTA &#41;](../../tools/dta/workload-element-dta.md)  
  
-   [Elemento TuningOptions &#40; DTA &#41;](../../tools/dta/tuningoptions-element-dta.md)  
  
-   [Elemento Configuration &#40; DTA &#41;](../../tools/dta/configuration-element-dta.md)  
  
## <a name="server-elements"></a>Elementos de servidor  
  
-   [Elemento Name para Server &#40; DTA &#41;](../../tools/dta/name-element-for-server-dta.md)  
  
-   [Elemento Database para Server &#40; DTA &#41;](../../tools/dta/database-element-for-server-dta.md)  
  
## <a name="workload-elements"></a>Elementos de Carga de Trabalho  
  
-   [Elemento File &#40; DTA &#41;](../../tools/dta/file-element-dta.md)  
  
-   [Elemento Database para Workload &#40; DTA &#41;](../../tools/dta/database-element-for-workload-dta.md)  
  
-   [Elemento EventString &#40; DTA &#41;](../../tools/dta/eventstring-element-dta.md)  
  
## <a name="tuning-options-elements"></a>Elementos de opções de ajuste  
  
-   [Elemento TuningTimeInMin &#40; DTA &#41;](../../tools/dta/tuningtimeinmin-element-dta.md)  
  
-   [Elemento StorageBoundInMB &#40; DTA &#41;](../../tools/dta/storageboundinmb-element-dta.md)  
  
-   [Elemento TestServer &#40; DTA &#41;](../../tools/dta/testserver-element-dta.md)  
  
-   [Elemento FeatureSet &#40; DTA &#41;](../../tools/dta/featureset-element-dta.md)  
  
-   [Elemento de particionamento &#40; DTA &#41;](../../tools/dta/partitioning-element-dta.md)  
  
-   [Elemento DropOnlyMode &#40; DTA &#41;](../../tools/dta/droponlymode-element-dta.md)  
  
-   [Elemento KeepExisting &#40; DTA &#41;](../../tools/dta/keepexisting-element-dta.md)  
  
-   [Elemento OnlineIndexOperation &#40; DTA &#41;](../../tools/dta/onlineindexoperation-element-dta.md)  
  
-   [Elemento DatabaseToConnect &#40; DTA &#41;](../../tools/dta/databasetoconnect-element-dta.md)  
  
## <a name="configuration-elements"></a>Elementos de configuração  
  
-   [Elemento Server para Configuration &#40; DTA &#41;](../../tools/dta/server-element-for-configuration-dta.md)  
  
-   [Elemento Database para Configuration &#40; DTA &#41;](../../tools/dta/database-element-for-configuration-dta.md)  
  
-   [Elemento Recommendation &#40; DTA &#41;](../../tools/dta/recommendation-element-dta.md)  
  
-   [Criar elemento &#40; DTA &#41;](../../tools/dta/create-element-dta.md)  
  
-   [Elemento index &#40; DTA &#41;](../../tools/dta/index-element-dta.md)  
  
-   [Elemento Name para Index &#40; DTA &#41;](../../tools/dta/name-element-for-index-dta.md)  
  
-   [Elemento Column para Index &#40; DTA &#41;](../../tools/dta/column-element-for-index-dta.md)  
  
-   [Elemento Name para coluna &#40; DTA &#41;](../../tools/dta/name-element-for-column-dta.md)  
  
-   [Elemento FileGroup para o índice &#40; DTA &#41;](../../tools/dta/filegroup-element-for-index-dta.md)  
  
## <a name="database-elements"></a>Elementos de banco de dados  
  
-   [Elemento de nome de banco de dados &#40; DTA &#41;](../../tools/dta/name-element-for-database-dta.md)  
  
-   [Elemento Schema para Database &#40; DTA &#41;](../../tools/dta/schema-element-for-database-dta.md)  
  
-   [Elemento Name para Schema &#40; DTA &#41;](../../tools/dta/name-element-for-schema-dta.md)  
  
-   [Elemento Table para Schema &#40; DTA &#41;](../../tools/dta/table-element-for-schema-dta.md)  
  
-   [Elemento Name para Table &#40; DTA &#41;](../../tools/dta/name-element-for-table-dta.md)  
  
## <a name="see-also"></a>Consulte também  
 [Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  
