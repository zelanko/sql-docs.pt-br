---
title: Executando operações de cópia em massa (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-bulk-copy-operations
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC]
- ODBC, bulk copy operations
- minimally logged operations [SQL Server Native Client]
- bulk copy [ODBC], about bulk copy
ms.assetid: 5c793405-487c-4f52-88b8-0091d529afb3
caps.latest.revision: 38
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5c05849172b018d3fce054727d217fe6a43527f8
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34707144"
---
# <a name="performing-bulk-copy-operations-odbc"></a>Executando operações de cópia em massa (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O padrão ODBC não dá suporte diretamente a operações de cópia em massa do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando conectado a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versão 7.0 ou posterior, o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client dá suporte às funções DB-Library que executam operações de cópia em massa do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta extensão específica do driver fornece um caminho de atualização fácil para aplicativos DB-Library existente que usam funções de cópia em massa. O suporte especializado à cópia em massa se encontra nos seguintes arquivos:  
  
-   sqlncli.h  
  
     Inclui protótipos de função e definições de constantes para funções de cópia em massa. O sqlncli.h deve ser incluído no aplicativo ODBC que executa operações de cópia em massa e deve estar no caminho de inclusão do aplicativo quando ele for compilado.  
  
-   sqlncli11.lib  
  
     Deve estar no caminho da biblioteca do vinculador e ser especificado como um arquivo a ser vinculado. O sqlncli11.lib é distribuído com o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
-   sqlncli11.dll  
  
     Deve estar presente no tempo de execução. O sqlncli11.dll é distribuído com o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
> [!NOTE]  
>  O ODBC **SQLBulkOperations** função não tem relação com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funções de cópia em massa. Os aplicativos devem usar as funções de cópia em massa específicas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para executar operações de cópia em massa.  
  
## <a name="minimally-logging-bulk-copies"></a>Cópias em massa com registro mínimo  
 Com o modelo de Recuperação Completa, todas as operações de inserção de linha executadas pelo carregamento em massa são totalmente registradas no log de transações. Em grandes carregamentos de dados, isso pode preencher o log de transações rapidamente. Em determinadas condições, é possível fazer um registro mínimo. O registro mínimo reduz a possibilidade de uma operação de carregamento em massa preencher o espaço do log, além de ser mais eficiente que o registro completo.  
  
 Para obter informações sobre como usar o log mínimo, consulte [pré-requisitos para log mínimo em importação em massa](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
## <a name="remarks"></a>Remarks  
 Ao usar o bcp.exe no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou posterior, você pode obter erros em situações onde não havia erros antes do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Isto se deve ao fato de, nas versões posteriores, o bcp.exe não executar mais a conversão implícita de tipo de dados. Antes do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], o bcp.exe convertia dados numéricos em um tipo de dados money, se a tabela de destino tivesse um tipo de dados money. Porém, nessa situação, o bcp.exe simplesmente truncava os campos extras. A partir do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], se dados tipos não correspondem entre o arquivo e a tabela de destino, o bcp.exe gera um erro se não houver nenhum dado que teria de ser truncado para caber na tabela de destino. Para resolver este erro, corrija os dados para que correspondam ao tipo de dados de destino. Opcionalmente, use o bcp.exe de uma versão anterior ao [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Usando arquivos de dados e de formato](../../relational-databases/native-client-odbc-bulk-copy-operations/using-data-files-and-format-files.md)  
  
-   [Cópia em massa de variáveis do programa](../../relational-databases/native-client-odbc-bulk-copy-operations/bulk-copying-from-program-variables.md)  
  
-   [Gerenciando tamanhos de lote para cópia em massa](../../relational-databases/native-client-odbc-bulk-copy-operations/managing-bulk-copy-batch-sizes.md)  
  
-   [Copiando em massa dados de texto e imagem](../../relational-databases/native-client-odbc-bulk-copy-operations/bulk-copying-text-and-image-data.md)  
  
-   [Convertendo de cópia em massa DB-Library em ODBC](../../relational-databases/native-client-odbc-bulk-copy-operations/converting-from-db-library-to-odbc-bulk-copy.md)  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [Importação e exportação em massa de dados &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)  
  
  
