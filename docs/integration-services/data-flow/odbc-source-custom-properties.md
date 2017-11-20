---
title: Propriedades personalizadas da origem ODBC | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 362bbcd8-b7b0-4bab-8afe-1212b2ad1af9
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 15c78bdb8f093b07ce62a7d710ba583aad96548d
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="odbc-source-custom-properties"></a>Propriedades personalizadas da origem ODBC
  A tabela a seguir descreve as propriedades personalizadas da origem ODBC. Todas as propriedades podem ser definidas a partir de expressões de propriedades SSIS.  
  
|Nome da propriedade|Tipo de Dados|Description|  
|-------------------|---------------|-----------------|  
|Conexão|Conexão ODBC|Uma conexão ODBC para acessar o banco de dados de origem.|  
|AccessMode|Inteiro (enumeração)|O modo usado para acessar o banco de dados. Os valores possíveis são Nome da Tabela (0) e Comando SQL (1).<br /><br /> O padrão é Nome da Tabela (0).|  
|BatchSize|Integer|O tamanho do lote para extração em massa. Esse é o número de registros extraído como uma matriz. Se o provedor ODBC selecionado não oferecer suporte a matrizes, o tamanho de lote será 1.|  
|BindCharColumnAs|Inteiro (enumeração)|Essa propriedade determina como a fonte ODBC associa colunas a tipos de cadeia de caracteres de vários bytes, como SQL_CHAR, SQL_VARCHAR ou SQL_LONGVARCHAR.<br /><br /> Os possíveis valores são Unicode (0), que associa as colunas como SQL_C_WCHAR e ANSI (1), que associa as colunas como SQL_C_CHAR). O valor padrão é Unicode (0).<br /><br /> **Observação**: esta propriedade não está disponível no **Editor de Fonte ODBC**, mas pode ser definida por meio do **Editor Avançado**.|  
|BindNumericAs|Inteiro (enumeração)|Essa propriedade determina como a fonte ODBC associa colunas com dados numéricos a tipos de dados SQL_TYPE_NUMERIC e SQL_TYPE_DECIMAL.<br /><br /> As opções possíveis são Char (0), que associa as colunas como SQL_C_CHAR e Numeric (1), que associa as colunas como SQL_C_NUMERIC. O valor padrão é Char (0).<br /><br /> **Observação**: esta propriedade não está disponível no **Editor de Fonte ODBC**, mas pode ser definida por meio do **Editor Avançado**.|  
|DefaultCodePage|Integer|A página de código a ser usada para colunas de saída de cadeia de caracteres.<br /><br /> **Observação**: esta propriedade não está disponível no **Editor de Fonte ODBC**, mas pode ser definida por meio do **Editor Avançado**.|  
|ExposeCharColumnsAsUnicode|Booliano|Essa propriedade determina como o componente expõe colunas CHAR. O valor padrão é False, que indica as colunas CHAR que são expostas como cadeias de caracteres de vários bytes (DT_STR). Se True, as colunas CHAR são expostas como cadeias de caracteres amplas (DT_WSTR).<br /><br /> **Observação**: esta propriedade não está disponível no **Editor de Fonte ODBC**, mas pode ser definida por meio do **Editor Avançado**.|  
|FetchMethod|Inteiro (enumeração)|O método usado para adquirir os dados. As possíveis opções são Linha a linha (0) e Lote (1). O valor padrão é Lote (1).<br /><br /> Para obter mais informações sobre essas opções, consulte [Fonte ODBC](../../integration-services/data-flow/odbc-source.md).<br /><br /> **Observação**: esta propriedade não está disponível no **Editor de Fonte ODBC**, mas pode ser definida por meio do **Editor Avançado**.|  
|SqlCommand|Cadeia de caracteres|O comando SQL a ser executado quando AccessMode é definido como Comando SQL.|  
|StatementTimeout|Integer|O número de segundos a aguardar a execução de uma instrução SQL antes de retornar com um erro para o aplicativo. O valor padrão é 120. Um valor de 0 indica se o sistema não alcança o tempo limite.|  
|TableName|Cadeia de caracteres|O nome da tabela com os dados que estão sendo usados quando AccessMode é definido como Nome da Tabela.|  
|LobChunckSize|Integer|A alocação de tamanho de parte para colunas LOB.|  
||||  
  
## <a name="see-also"></a>Consulte também  
 [Origem ODBC](../../integration-services/data-flow/odbc-source.md)   
 [Editor de origem ODBC &#40; Página Gerenciador de Conexão &#41;](../../integration-services/data-flow/odbc-source-editor-connection-manager-page.md)  
  
  

