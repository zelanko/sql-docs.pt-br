---
title: Compatibilidade de UTF-8 com OLE DB Driver para SQL Server| Microsoft Docs
description: Suporte ao UTF-8 no OLE DB Driver para SQL Server
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: v-kaywon
ms.author: v-kaywon
ms.openlocfilehash: 4a30b233190817faee581106db5c8a18695a00d1
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 04/15/2019
ms.locfileid: "59583009"
---
# <a name="utf-8-support-in-ole-db-driver-for-sql-server"></a>Suporte ao UTF-8 no OLE DB Driver para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

O Microsoft OLE DB Driver para SQL Server (versão 18.2.1) inclui o suporte à codificação UTF-8 do servidor. Para saber mais sobre o suporte à UTF-8 no SQL Server, confira:
- [Suporte a ordenações e a Unicode](../../../relational-databases/collations/collation-and-unicode-support.md)
- [Suporte para UTF-8](../../../sql-server/what-s-new-in-sql-server-ver15.md#utf-8-support-ctp-23)

## <a name="data-insertion-into-a-utf-8-encoded-char-or-varchar-column"></a>Inserção de dados em uma coluna CHAR ou VARCHAR com codificação UTF-8
Ao criar um buffer de parâmetro de entrada para inserção, o buffer é descrito usando uma matriz de [estruturas DBBINDING](https://go.microsoft.com/fwlink/?linkid=2071182). Cada estrutura DBBINDING tem associado um único parâmetro ao buffer do consumidor e contém informações como o comprimento e o tipo dos valores de dados. Para um buffer de parâmetro de entrada do tipo CHAR, o *wType* da estrutura DBBINDING deve ser definido como DBTYPE_STR. Para um buffer de parâmetro de entrada do tipo WCHAR, o *wType* da estrutura DBBINDING deve ser definido como DBTYPE_WSTR.

Ao executar um comando com parâmetros, o driver constrói as informações de tipo de dados do parâmetro. Se o tipo de buffer de entrada e o tipo de dados de parâmetro corresponderem, nenhuma conversão é feita no driver. Caso contrário, o driver converterá o buffer do parâmetro de entrada para o tipo de dados do parâmetro. O tipo de dados do parâmetro pode ser definido explicitamente pelo usuário, chamando [ICommandWithParameters::SetParameterInfo](https://go.microsoft.com/fwlink/?linkid=2071577). Se as informações não forem fornecidas, o driver deriva as informações de tipo de dados do parâmetro (a) recuperando os metadados de coluna do servidor quando a instrução estiver preparada ou (b) tentando uma conversão padrão proveniente do tipo de dados do parâmetro de entrada.

O buffer do parâmetro de entrada pode ser convertido para o agrupamento de colunas do servidor pelo driver ou pelo servidor, dependendo do tipo de dados do buffer de entrada e do tipo de dados do parâmetro. Durante a conversão, poderá ocorrer uma perda de dados se a página de código do cliente ou a página de código do agrupamento do banco de dados não puder representar todos os caracteres no buffer de entrada. A tabela a seguir descreve o processo de conversão ao inserir dados em uma coluna habilitada para UTF-8:

|Tipo de dados de buffer|Tipo de dados de parâmetro|Conversão|Precaução do usuário|
|---             |---                |---       |---            |
|DBTYPE_STR|DBTYPE_STR|Conversão no servidor da página de código do cliente para a página de código do agrupamento de banco de dados; conversão no servidor da página de código do agrupamento de banco de dados para a página de código do agrupamento de colunas.|Verifique se a página de código do cliente e a página de código do agrupamento de banco de dados podem representar todos os caracteres nos dados de entrada. Por exemplo, para inserir um caractere polonês, a página de código do cliente pode ser definida como 1250 (ANSI Europa Central), e a ordenação do banco de dados pode usar o polonês como o designador da ordenação (por exemplo, Polish_100_CI_AS_SC) ou estar habilitado para UTF-8.|
|DBTYPE_STR|DBTYPE_WSTR|Conversão no driver da página de código do cliente para a codificação UTF-16; conversão no servidor da codificação UTF-16 para a página de código do agrupamento de colunas.|Verifique se a página de código do cliente pode representar todos os caracteres nos dados de entrada. Por exemplo, para inserir um caractere polonês, a página de código do cliente pode ser definida como 1250 (ANSI Europa Central).|
|DBTYPE_WSTR|DBTYPE_STR|Conversão no servidor da codificação UTF-16 para a página de código do agrupamento de banco de dados; conversão no servidor da página de código do agrupamento do banco de dados para a página de código do agrupamento de colunas.|Verifique se a página de código do agrupamento do banco de dados pode representar todos os caracteres nos dados de entrada. Por exemplo, para inserir um caractere polonês, a página de código do agrupamento do banco de dados pode usar o polonês como o designador da ordenação (por exemplo, Polish_100_CI_AS_SC) ou estar habilitada para UTF-8.|
|DBTYPE_WSTR|DBTYPE_WSTR|Conversão no servidor da UTF-16 para a página de código de ordenação de coluna.|Nenhum.|

## <a name="data-retrieval-from-a-utf-8-encoded-char-or-varchar-column"></a>Recuperação de dados de uma coluna CHAR ou VARCHAR com codificação UTF-8
Ao criar um buffer para dados recuperados, esse é descrito usando uma matriz de [estruturas DBBINDING](https://go.microsoft.com/fwlink/?linkid=2071182). Cada estrutura DBBINDING associa uma única coluna na linha recuperada. Para recuperar os dados da coluna como CHAR, defina o *wType* da estrutura DBBINDING como DBTYPE_STR. Para recuperar os dados da coluna como WCHAR, defina o *wType* da estrutura DBBINDING como DBTYPE_WSTR.

Para o indicador DBTYPE_STR de tipo de buffer resultante, o driver converte os dados codificados em UTF-8 para a codificação do cliente. O usuário deverá verificar se a codificação do cliente pode representar os dados da coluna UTF-8, caso contrário, poderá ocorrer uma perda de dados.

Para o indicador DBTYPE_WSTR de tipo de buffer resultante, o driver converte os dados codificados em UTF-8 para a codificação UTF-16.
  
## <a name="see-also"></a>Consulte Também  
[Recursos do Driver do OLE DB para SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md) 

[Suporte ao UTF-16 no Driver do OLE DB para SQL Server](../../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)    
  
  
