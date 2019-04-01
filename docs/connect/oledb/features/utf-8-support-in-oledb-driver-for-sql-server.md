---
title: Compatibilidade de UTF-8 com OLE DB Driver para SQL Server| Microsoft Docs
description: Suporte ao UTF-8 no OLE DB Driver para SQL Server
ms.custom: ''
ms.date: 03/27/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: v-kaywon
ms.author: v-kaywon
ms.openlocfilehash: b7f138438d522c9da1b7ef74acbaf963e17d6144
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58492598"
---
# <a name="utf-8-support-in-ole-db-driver-for-sql-server"></a>Suporte ao UTF-8 no OLE DB Driver para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Microsoft Driver do OLE DB para SQL Server (versão 18.2.1) adiciona suporte para a codificação UTF-8 do servidor. Para obter informações sobre o suporte do SQL Server UTF-8, consulte:
- [Suporte a ordenações e a Unicode](../../../relational-databases/collations/collation-and-unicode-support.md)
- [Suporte para UTF-8](../../../sql-server/what-s-new-in-sql-server-ver15.md#utf-8-support-ctp-23)

## <a name="data-insertion-into-a-utf-8-encoded-char-or-varchar-column"></a>Inserção de dados em uma UTF-8 codificados coluna CHAR ou VARCHAR
Ao criar um buffer de parâmetro de entrada para inserção, o buffer é descrito usando uma matriz de [estruturas DBBINDING](https://go.microsoft.com/fwlink/?linkid=2071182). Cada estrutura DBBINDING associa um único parâmetro ao buffer do consumidor e contém informações como o comprimento e tipo do valor de dados. Para um buffer de parâmetro de entrada do tipo CHAR, o *wType* de DBBINDING estrutura deve ser definida como DBTYPE_STR. Para um buffer de parâmetro de entrada do tipo WCHAR, o *wType* de DBBINDING estrutura deve ser definida como DBTYPE_WSTR.

Ao executar um comando com parâmetros, o driver constrói as informações de tipo de dados do parâmetro. Se o tipo de buffer de entrada e os dados de parâmetro de tipo correspondência, nenhuma conversão é feita no driver. Caso contrário, o driver converterá o buffer de parâmetro de entrada para o tipo de dados do parâmetro. O tipo de dados do parâmetro pode ser definido explicitamente pelo usuário chamando [ICommandWithParameters:: SetParameterInfo](https://go.microsoft.com/fwlink/?linkid=2071577). Se as informações não for fornecidas, o driver deriva as informações de tipo de dados do parâmetro (a) ao recuperar metadados de coluna do servidor quando a instrução é preparada ou (b) tentar uma conversão padrão do tipo de dados de parâmetro de entrada.

O buffer de parâmetro de entrada pode ser convertido para o agrupamento de coluna do servidor pelo driver ou pelo servidor, dependendo do tipo de dados do buffer de entrada e o tipo de dados do parâmetro. Durante a conversão, a perda de dados pode ocorrer se a página de código do cliente ou a página de código do agrupamento de banco de dados não pode representar todos os caracteres no buffer de entrada. A tabela a seguir descreve o processo de conversão quando inserindo dados em uma UTF-8 habilitado coluna:

|Tipo de dados do buffer|Tipo de dados de parâmetro|Conversão|Precaução do usuário|
|---             |---                |---       |---            |
|DBTYPE_STR|DBTYPE_STR|Conversão de servidor da página de código do cliente para a página de código do agrupamento de banco de dados; conversão de servidor da página de código do agrupamento de banco de dados para a página de código do agrupamento de coluna.|Verifique se a página de código do cliente e a página de código do agrupamento de banco de dados podem representar todos os caracteres nos dados de entrada. Por exemplo, para inserir um caractere polonês, a página de código do cliente pode ser definida como 1250 (ANSI Europa Central), e o agrupamento de banco de dados poderia usar polonês como o designador de agrupamento (por exemplo, Polish_100_CI_AS_SC) ou ser UTF-8 habilitados.|
|DBTYPE_STR|DBTYPE_WSTR|Conversão de driver de página de código do cliente em codificação UTF-16; conversão de servidor de codificação UTF-16 para a página de código do agrupamento de coluna.|Certifique-se de que a página de código do cliente pode representar todos os caracteres nos dados de entrada. Por exemplo, para inserir um caractere polonês, a página de código do cliente pode ser definida como 1250 (ANSI Europa Central).|
|DBTYPE_WSTR|DBTYPE_STR|Conversão do driver de codificação UTF-16 para a página de código do agrupamento de banco de dados; conversão de servidor da página de código do agrupamento de banco de dados para a página de código do agrupamento de coluna.|Certifique-se de que a página de código do agrupamento de banco de dados pode representar todos os caracteres nos dados de entrada. Por exemplo, para inserir um caractere polonês, a página de código do agrupamento de banco de dados poderia usar polonês como o designador de agrupamento (por exemplo, Polish_100_CI_AS_SC) ou ser UTF-8 habilitados.|
|DBTYPE_WSTR|DBTYPE_WSTR|Conversão de servidor de UTF-16 para a página de código do agrupamento de coluna.|Nenhum.|

## <a name="data-retrieval-from-a-utf-8-encoded-char-or-varchar-column"></a>Recuperação de dados de um UTF-8 codificados coluna CHAR ou VARCHAR
Ao criar um buffer para os dados recuperados, o buffer é descrito usando uma matriz de [estruturas DBBINDING](https://go.microsoft.com/fwlink/?linkid=2071182). Cada estrutura DBBINDING associa uma única coluna na linha recuperada. Para recuperar os dados da coluna como CHAR, defina as *wType* da estrutura DBBINDING como DBTYPE_STR. Para recuperar os dados da coluna como WCHAR, defina as *wType* da estrutura DBBINDING como DBTYPE_WSTR.

Para o resultado buffer indicador de tipo DBTYPE_STR, o driver converte os dados codificados em UTF-8 para o cliente de codificação. O usuário deve verificar se o cliente de codificação pode representar os dados da coluna de UTF-8, caso contrário, pode ocorrer perda de dados.

Para o resultado buffer indicador de tipo DBTYPE_WSTR, o driver converte os dados codificados em UTF-8 para a codificação UTF-16.
  
## <a name="see-also"></a>Consulte Também  
[Recursos do Driver do OLE DB para SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md) 

[Suporte ao UTF-16 no Driver do OLE DB para SQL Server](../../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)    
  
  
