---
title: Propriedades personalizadas de destino ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 07508c40-6c08-4359-96cd-8ff17671244d
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 093b6da73d55129b1a21e36dfad4fac3c899c296
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="odbc-destination-custom-properties"></a>Propriedades personalizadas de destino ODBC
  A tabela a seguir descreve as propriedades personalizadas do destino ODBC. Todas as propriedades podem ser definidas a partir de expressões de propriedades SSIS.  
  
|Nome da propriedade|Tipo de Dados|Description|  
|-------------------|---------------|-----------------|  
|Conexão|Conexão ODBC|Uma conexão ODBC para acessar o banco de dados de destino.|  
|BatchSize|Integer|O tamanho do lote para carregamento em massa. Esse é o número de linhas carregado como um lote. Isso só será válido se houver suporte para a associação de parâmetro row-wise. Se não houver suporte para a associação de parâmetro row-wise, o tamanho do lote será 1.|  
|BindCharColumnAs|Inteiro (enumeração)|Essa propriedade determina como o destino ODBC associa colunas a tipos de cadeia de caracteres de vários bytes, como SQL_CHAR, SQL_VARCHAR ou SQL_LONGVARCHAR.<br /><br /> Os possíveis valores são Unicode (0), que associa as colunas como SQL_C_WCHAR e ANSI (1), que associa as colunas como SQL_C_CHAR). O valor padrão é Unicode (0).<br /><br /> Unicode é a melhor opção para a maioria dos provedores ODBC 3.x e ODBC 2.x que oferecem suporte para a associação de parâmetros CHAR como cadeias de caracteres amplas. Quando você seleciona Unicode e ExposeCharColumnsAsUnicode como True, o usuário não precisa especificar a página de código utilizada pelo banco de dados de origem.<br /><br /> **Observação:** essa propriedade não está disponível no **Editor de Destinos ODBC**, mas pode ser definida no **Editor Avançado**.|  
|BindNumericAs|Inteiro (enumeração)|Essa propriedade determina como o destino de ODBC associa colunas com dados numéricos a tipos de dados SQL_TYPE_NUMERIC e SQL_TYPE_DECIMAL.<br /><br /> Os valores possíveis são Char (0), que associa as colunas como SQL_C_CHAR e Numeric (1), que associa as colunas como SQL_C_NUMERIC. O valor padrão é Char (0).<br /><br /> **Observação**: essa propriedade não está disponível no **Editor de Destinos ODBC**, mas pode ser definida no **Editor Avançado**.|  
|DefaultCodePage|Integer|A página de código a ser usada para colunas de cadeia de caracteres.<br /><br /> **Observação**: essa propriedade não está disponível no **Editor de Destinos ODBC**, mas pode ser definida no **Editor Avançado**.|  
|InsertMethod|Inteiro (enumeração)|O método usado para inserir os dados. Os valores possíveis são Linha a linha (0) e Lote (1). O valor padrão é Lote (1).<br /><br /> Para obter mais informações sobre essas opções, consulte “Opções de carregamento” em [ODBC Destination](../../integration-services/data-flow/odbc-destination.md).|  
|StatementTimeout|Integer|O número de segundos a aguardar a execução de uma instrução SQL antes de retornar com um erro para o aplicativo. O valor padrão é 120.|  
|TableName|Cadeia de caracteres|O nome da tabela de destino onde os dados estão sendo inseridos.|  
|TransactionSize|Integer|O número de inserções em uma única transação. O valor padrão é 0, que significa que o destino ODBC funciona no modo de confirmação automático.<br /><br /> Como o gerenciador de conexões ODBC não oferece suporte a transações distribuídas, é possível definir essa propriedade com um valor diferente de 0. No entanto, se a propriedade **RetainSameConnection** do gerenciador de conexões for definida como **true** , essa propriedade deverá ser definida como 0.<br /><br /> **Observação**: essa propriedade não está disponível no **Editor de Destinos ODBC**, mas pode ser definida no **Editor Avançado**.|  
|LobChunkSize|Integer|A alocação de tamanho de parte para colunas LOB.|  
  
  
