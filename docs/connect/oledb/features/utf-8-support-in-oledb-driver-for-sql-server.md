---
title: Compatibilidade de UTF-8 com OLE DB Driver para SQL Server| Microsoft Docs
description: Saiba mais sobre o suporte do Driver do OLE DB para SQL Server à codificação UTF-8 de servidor e de cliente.
ms.custom: ''
ms.date: 05/25/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: reference
ms.reviewer: v-kaywon
ms.author: v-daenge
author: David-Engel
ms.openlocfilehash: b16ba1f6fef9ec82de0e3c4877a52aee344a2b70
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727260"
---
# <a name="utf-8-support-in-ole-db-driver-for-sql-server"></a>Suporte ao UTF-8 no OLE DB Driver para SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

O Microsoft OLE DB Driver para SQL Server (versão 18.2.1) inclui o suporte à codificação UTF-8 do servidor. Para saber mais sobre o suporte à UTF-8 no SQL Server, confira:
- [Suporte a ordenações e a Unicode](../../../relational-databases/collations/collation-and-unicode-support.md)
- [Suporte para UTF-8](../../../relational-databases/collations/collation-and-unicode-support.md#utf8)

A versão 18.4.0 do driver adiciona suporte para a codificação de cliente UTF-8 (habilitada com a caixa de seleção "Usar Unicode UTF-8 para suporte de idioma mundial" nas Configurações de Região no Windows 10).

> [!NOTE]  
> O Driver do Microsoft OLE DB para SQL Server usa a função [GetACP](/windows/win32/api/winnls/nf-winnls-getacp) para determinar a codificação do buffer de entrada DBTYPE_STR.
>
> Os cenários em que GetACP retorna uma codificação UTF-8 (habilitados com a caixa de seleção "Usar Unicode UTF-8 para suporte de idioma mundial" nas Configurações de Região no Windows 10) têm suporte começando com a versão 18.4. Em versões anteriores, se o buffer precisar armazenar dados Unicode, o tipo de dados de buffer deverá ser definido como *DBTYPE_WSTR* (codificado como UTF-16).

## <a name="data-insertion-into-a-utf-8-encoded-char-or-varchar-column"></a>Inserção de dados em uma coluna CHAR ou VARCHAR com codificação UTF-8
Ao criar um buffer de parâmetro de entrada para inserção, o buffer é descrito usando uma matriz de [estruturas DBBINDING](/previous-versions/windows/desktop/ms716845(v=vs.85)). Cada estrutura DBBINDING tem associado um único parâmetro ao buffer do consumidor e contém informações como o comprimento e o tipo dos valores de dados. Para um buffer de parâmetro de entrada do tipo CHAR, o *wType* da estrutura DBBINDING deve ser definido como DBTYPE_STR. Para um buffer de parâmetro de entrada do tipo WCHAR, o *wType* da estrutura DBBINDING deve ser definido como DBTYPE_WSTR.

Ao executar um comando com parâmetros, o driver constrói as informações de tipo de dados do parâmetro. Se o tipo de buffer de entrada e o tipo de dados de parâmetro corresponderem, nenhuma conversão é feita no driver. Caso contrário, o driver converterá o buffer do parâmetro de entrada para o tipo de dados do parâmetro. O tipo de dados do parâmetro pode ser definido explicitamente pelo usuário, chamando [ICommandWithParameters::SetParameterInfo](/previous-versions/windows/desktop/ms725393(v=vs.85)). Se as informações não forem fornecidas, o driver deriva as informações de tipo de dados do parâmetro (a) recuperando os metadados de coluna do servidor quando a instrução estiver preparada ou (b) tentando uma conversão padrão proveniente do tipo de dados do parâmetro de entrada.

O buffer do parâmetro de entrada pode ser convertido para a ordenação de colunas do servidor pelo driver ou pelo servidor, dependendo do tipo de dados do buffer de entrada e do tipo de dados do parâmetro. Durante a conversão, poderá ocorrer uma perda de dados se a página de código do cliente ou a página de código da ordenação do banco de dados não puder representar todos os caracteres no buffer de entrada. A tabela a seguir descreve o processo de conversão ao inserir dados em uma coluna habilitada para UTF-8:

|Tipo de dados de buffer|Tipo de dados de parâmetro|Conversão|Precaução do usuário|
|---             |---                |---       |---            |
|DBTYPE_STR|DBTYPE_STR|Conversão no servidor da página de código do cliente para a página de código da ordenação de banco de dados; conversão no servidor da página de código da ordenação de banco de dados para a página de código da ordenação de colunas.|Verifique se a página de código do cliente e a página de código da ordenação de banco de dados podem representar todos os caracteres nos dados de entrada. Por exemplo, para inserir um caractere polonês, a página de código do cliente pode ser definida como 1250 (ANSI Europa Central), e a ordenação do banco de dados pode usar o polonês como o designador da ordenação (por exemplo, Polish_100_CI_AS_SC) ou estar habilitado para UTF-8.|
|DBTYPE_STR|DBTYPE_WSTR|Conversão no driver da página de código do cliente para a codificação UTF-16; conversão no servidor da codificação UTF-16 para a página de código da ordenação de colunas.|Verifique se a página de código do cliente pode representar todos os caracteres nos dados de entrada. Por exemplo, para inserir um caractere polonês, a página de código do cliente pode ser definida como 1250 (ANSI Europa Central).|
|DBTYPE_WSTR|DBTYPE_STR|Conversão no servidor da codificação UTF-16 para a página de código da ordenação de banco de dados; conversão no servidor da página de código da ordenação do banco de dados para a página de código da ordenação de colunas.|Verifique se a página de código da ordenação do banco de dados pode representar todos os caracteres nos dados de entrada. Por exemplo, para inserir um caractere polonês, a página de código do agrupamento do banco de dados pode usar o polonês como o designador da ordenação (por exemplo, Polish_100_CI_AS_SC) ou estar habilitada para UTF-8.|
|DBTYPE_WSTR|DBTYPE_WSTR|Conversão no servidor da UTF-16 para a página de código de ordenação de coluna.|Nenhum.|

## <a name="data-retrieval-from-a-utf-8-encoded-char-or-varchar-column"></a>Recuperação de dados de uma coluna CHAR ou VARCHAR com codificação UTF-8
Ao criar um buffer para dados recuperados, esse é descrito usando uma matriz de [estruturas DBBINDING](/previous-versions/windows/desktop/ms716845(v=vs.85)). Cada estrutura DBBINDING associa uma única coluna na linha recuperada. Para recuperar os dados da coluna como CHAR, defina o *wType* da estrutura DBBINDING como DBTYPE_STR. Para recuperar os dados da coluna como WCHAR, defina o *wType* da estrutura DBBINDING como DBTYPE_WSTR.

Para o indicador DBTYPE_STR de tipo de buffer resultante, o driver converte os dados codificados em UTF-8 para a codificação do cliente. O usuário deverá verificar se a codificação do cliente pode representar os dados da coluna UTF-8, caso contrário, poderá ocorrer uma perda de dados.

Para o indicador DBTYPE_WSTR de tipo de buffer resultante, o driver converte os dados codificados em UTF-8 para a codificação UTF-16.

## <a name="communication-with-servers-that-dont-support-utf-8"></a>Comunicação com servidores sem suporte para UTF-8
O Driver do Microsoft OLE DB para SQL Server garante que os dados sejam expostos ao servidor de maneira que o servidor possa entender. Ao inserir dados de clientes habilitados para UTF-8, o driver traduz as cadeias de caracteres codificadas em UTF-8 para a página de código de ordenação do banco de dados antes de enviá-las ao servidor.

> [!NOTE]  
> O uso da interface [ISequentialStream](/previous-versions/windows/desktop/ms718035(v=vs.85)) para inserir dados codificados em UTF-8 em uma coluna de texto herdada só é limitado a servidores que dão suporte a UTF-8. Para ver os detalhes, confira [Blobs e Objetos OLE](../ole-db-blobs/blobs-and-ole-objects.md).

## <a name="see-also"></a>Consulte Também  
[Recursos do Driver do OLE DB para SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md) 

[Suporte ao UTF-16 no Driver do OLE DB para SQL Server](../../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)    
  
