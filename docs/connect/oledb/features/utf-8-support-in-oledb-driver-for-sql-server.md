---
title: Compatibilidade de UTF-8 com OLE DB Driver para SQL Server| Microsoft Docs
description: Suporte ao UTF-8 no OLE DB Driver para SQL Server
ms.custom: ''
ms.date: 04/23/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: v-kaywon
ms.author: v-kaywon
ms.openlocfilehash: fb596365f284a141b5e57bfc8601427fe603d73d
ms.sourcegitcommit: 49f3d12c0a46d98b82513697a77a461340f345e1
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70392014"
---
# <a name="utf-8-support-in-ole-db-driver-for-sql-server"></a>Suporte ao UTF-8 no OLE DB Driver para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

O Microsoft OLE DB Driver para SQL Server (versão 18.2.1) inclui o suporte à codificação UTF-8 do servidor. Para saber mais sobre o suporte à UTF-8 no SQL Server, confira:
- [Suporte a ordenações e a Unicode](../../../relational-databases/collations/collation-and-unicode-support.md)
- [Suporte para UTF-8](#ctp23)

> [!IMPORTANT]
> O Microsoft OLE DB driver for SQL Server usa a função [GetACP](https://docs.microsoft.com/windows/win32/api/winnls/nf-winnls-getacp) para determinar a codificação do buffer de entrada DBTYPE_STR. Os cenários nos quais o GetACP retorna uma codificação UTF-8 não têm suporte. Se o buffer precisar armazenar dados Unicode, o tipo de dados buffer deverá ser definido como DBTYPE_WSTR (UTF-16 encoded).

## <a name="data-insertion-into-a-utf-8-encoded-char-or-varchar-column"></a>Inserção de dados em uma coluna CHAR ou VARCHAR com codificação UTF-8
Ao criar um buffer de parâmetro de entrada para inserção, o buffer é descrito usando uma matriz de [estruturas DBBINDING](https://go.microsoft.com/fwlink/?linkid=2071182). Cada estrutura DBBINDING tem associado um único parâmetro ao buffer do consumidor e contém informações como o comprimento e o tipo dos valores de dados. Para um buffer de parâmetro de entrada do tipo CHAR, o *wType* da estrutura DBBINDING deve ser definido como DBTYPE_STR. Para um buffer de parâmetro de entrada do tipo WCHAR, o *wType* da estrutura DBBINDING deve ser definido como DBTYPE_WSTR.

Ao executar um comando com parâmetros, o driver constrói as informações de tipo de dados do parâmetro. Se o tipo de buffer de entrada e o tipo de dados de parâmetro corresponderem, nenhuma conversão é feita no driver. Caso contrário, o driver converterá o buffer do parâmetro de entrada para o tipo de dados do parâmetro. O tipo de dados do parâmetro pode ser definido explicitamente pelo usuário, chamando [ICommandWithParameters::SetParameterInfo](https://go.microsoft.com/fwlink/?linkid=2071577). Se as informações não forem fornecidas, o driver deriva as informações de tipo de dados do parâmetro (a) recuperando os metadados de coluna do servidor quando a instrução estiver preparada ou (b) tentando uma conversão padrão proveniente do tipo de dados do parâmetro de entrada.

O buffer do parâmetro de entrada pode ser convertido para a ordenação de colunas do servidor pelo driver ou pelo servidor, dependendo do tipo de dados do buffer de entrada e do tipo de dados do parâmetro. Durante a conversão, poderá ocorrer uma perda de dados se a página de código do cliente ou a página de código da ordenação do banco de dados não puder representar todos os caracteres no buffer de entrada. A tabela a seguir descreve o processo de conversão ao inserir dados em uma coluna habilitada para UTF-8:

|Tipo de dados de buffer|Tipo de dados de parâmetro|Conversão|Precaução do usuário|
|---             |---                |---       |---            |
|DBTYPE_STR|DBTYPE_STR|Conversão no servidor da página de código do cliente para a página de código da ordenação de banco de dados; conversão no servidor da página de código da ordenação de banco de dados para a página de código da ordenação de colunas.|Verifique se a página de código do cliente e a página de código da ordenação de banco de dados podem representar todos os caracteres nos dados de entrada. Por exemplo, para inserir um caractere polonês, a página de código do cliente pode ser definida como 1250 (ANSI Europa Central), e a ordenação do banco de dados pode usar o polonês como o designador da ordenação (por exemplo, Polish_100_CI_AS_SC) ou estar habilitado para UTF-8.|
|DBTYPE_STR|DBTYPE_WSTR|Conversão no driver da página de código do cliente para a codificação UTF-16; conversão no servidor da codificação UTF-16 para a página de código da ordenação de colunas.|Verifique se a página de código do cliente pode representar todos os caracteres nos dados de entrada. Por exemplo, para inserir um caractere polonês, a página de código do cliente pode ser definida como 1250 (ANSI Europa Central).|
|DBTYPE_WSTR|DBTYPE_STR|Conversão no servidor da codificação UTF-16 para a página de código da ordenação de banco de dados; conversão no servidor da página de código da ordenação do banco de dados para a página de código da ordenação de colunas.|Verifique se a página de código da ordenação do banco de dados pode representar todos os caracteres nos dados de entrada. Por exemplo, para inserir um caractere polonês, a página de código do agrupamento do banco de dados pode usar o polonês como o designador da ordenação (por exemplo, Polish_100_CI_AS_SC) ou estar habilitada para UTF-8.|
|DBTYPE_WSTR|DBTYPE_WSTR|Conversão no servidor da UTF-16 para a página de código de ordenação de coluna.|Nenhum.|

## <a name="data-retrieval-from-a-utf-8-encoded-char-or-varchar-column"></a>Recuperação de dados de uma coluna CHAR ou VARCHAR com codificação UTF-8
Ao criar um buffer para dados recuperados, esse é descrito usando uma matriz de [estruturas DBBINDING](https://go.microsoft.com/fwlink/?linkid=2071182). Cada estrutura DBBINDING associa uma única coluna na linha recuperada. Para recuperar os dados da coluna como CHAR, defina o *wType* da estrutura DBBINDING como DBTYPE_STR. Para recuperar os dados da coluna como WCHAR, defina o *wType* da estrutura DBBINDING como DBTYPE_WSTR.

Para o indicador DBTYPE_STR de tipo de buffer resultante, o driver converte os dados codificados em UTF-8 para a codificação do cliente. O usuário deverá verificar se a codificação do cliente pode representar os dados da coluna UTF-8, caso contrário, poderá ocorrer uma perda de dados.

Para o indicador DBTYPE_WSTR de tipo de buffer resultante, o driver converte os dados codificados em UTF-8 para a codificação UTF-16.

<a name="ctp23"></a>

### <a name="utf-8-support-sql-server-2019-ctp-23"></a>Suporte a UTF-8 (SQL Server 2019 CTP 2.3)

[!INCLUDE[ss2019](../../../includes/sssqlv15-md.md)] apresenta suporte completo para a amplamente utilizada codificação de caracteres UTF-8 como codificação de importação ou exportação, ou como ordenação em nível de banco de dados ou nível de coluna para dados de texto. A UTF-8 é permitida nos tipos de dados `CHAR` e `VARCHAR` e é habilitada quando você cria ou altera a ordenação de um objeto para uma ordenação com o sufixo `UTF8`.

Por exemplo, `LATIN1_GENERAL_100_CI_AS_SC` para `LATIN1_GENERAL_100_CI_AS_SC_UTF8`. A UTF-8 só está disponível para ordenações do Windows com suporte para caracteres suplementares, conforme introduzida no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]. `NCHAR` e `NVARCHAR` permitem somente a codificação UTF-16 e permanecem inalterados.

Esse recurso pode fornecer economia de armazenamento significativa dependendo do conjunto de caracteres utilizado. Por exemplo, a alteração de um tipo de dados de coluna existente com cadeias de caracteres ASCII (Latinas) de `NCHAR(10)` para `CHAR(10)` usando uma ordenação habilitada para UTF-8 resulta em 50% de redução nos requisitos de armazenamento. Essa redução ocorre porque `NCHAR(10)` exige 20 bytes para armazenamento, enquanto `CHAR(10)` requer 10 bytes para a mesma cadeia de caracteres Unicode.

Para obter mais informações, consulte [Suporte a ordenações e a Unicode](../../../relational-databases/collations/collation-and-unicode-support.md).

O **CTP 2.1** adiciona suporte para selecionar a ordenação de UTF-8 como padrão durante a instalação do [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)].

O **CTP 2.2** adiciona suporte para usar codificação de caracteres UTF-8 com replicação do SQL Server.

O **CTP 2.3** adiciona suporte para usar codificação de caracteres UTF-8 com uma ordenação BIN2 (UTF8_BIN2).

## <a name="see-also"></a>Consulte Também  
[Recursos do Driver do OLE DB para SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md) 

[Suporte ao UTF-16 no Driver do OLE DB para SQL Server](../../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)    
  
  
