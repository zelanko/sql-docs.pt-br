---
title: Importar dados de formato nativo e de caractere de versões anteriores do SQL Server
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- earlier versions [SQL Server], import and export data formats
- -V switch
- data formats [SQL Server], earlier versions
- previous versions [SQL Server], import and export data formats
ms.assetid: e644696f-9017-428e-a5b3-d445d1c630b3
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: ae89c263008c035dc7cd8e0050b50a5cdd9cc705
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "74055994"
---
# <a name="import-native-and-character-format-data-from-earlier-versions-of-sql-server"></a>Importar dados de formato nativo e de caractere de versões anteriores do SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], você pode usar o **bcp** para importar dados de formato de caractere e nativo do [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] usando a opção **-V** . A opção **-V** faz com que o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] use tipos de dados da versão anterior especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e o formato de arquivo de dados é igual ao formato da versão anterior.  
  
 Para especificar uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para um arquivo de dados, use a opção **-V** com os seguintes qualificadores:  
  
|Versão do SQL Server|Qualificador|  
|------------------------|---------------|  
|[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]|**-V80**|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|**-V90**|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|**-V100**|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|**-V 110**|  
  
## <a name="interpretation-of-data-types"></a>Interpretação de tipos de dados  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores oferecem suporte para alguns novos tipos. Para importar um novo tipo de dados para uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o tipo de dados deve ser armazenado em um formato legível pelos clientes **bcp** antigos. A tabela a seguir resume como os novos tipos de dados são convertidos para compatibilidade com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Novos tipos de dados no SQL Server 2005|Tipos de dados compatíveis na versão 6*x*|Tipos de dados compatíveis na versão 70|Tipos de dados compatíveis na versão 80|  
|---------------------------------------|-------------------------------------------|-----------------------------------------|-----------------------------------------|  
|**bigint**|**decimal**|**decimal**|*|  
|**sql_variant**|**text**|**nvarchar(4000)**|*|  
|**varchar(max)**|**text**|**text**|**text**|  
|**nvarchar(max)**|**ntext**|**ntext**|**ntext**|  
|**varbinary(max)**|**imagem**|**imagem**|**imagem**|  
|XML|**ntext**|**ntext**|**ntext**|  
|UDT**|**imagem**|**imagem**|**imagem**|  
  
 *Esse tipo tem suporte nativo.  
  
 **UDT indica um tipo definido pelo usuário.  
  
## <a name="exporting-using--v-80"></a>Exportar usando – V 80  
 Quando você exporta dados em massa usando a opção **-V80**, dados **nvarchar(max)** , **varchar(max)** , **varbinary(max)** , XML e UDT no modo nativo são armazenados com um prefixo de 4 bytes, como dados de **texto**, **imagem** e **ntext**, em vez de com um prefixo de 8 bytes, que é o padrão para o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores.  
  
## <a name="copying-date-values"></a>Copiando valores de dados  
 O**bcp** usa a API de cópia em massa do ODBC. Portanto, para importar valores de data para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o **bcp** usa o formato de data do ODBC (*yyyy-mm-dd hh:mm:ss*[ *.f...* ]).  
  
 O comando **bcp** exporta arquivos de dados de formato de caractere usando o formato padrão ODBC para os valores **datetime** e **smalldatetime** . Por exemplo, uma coluna **datetime** que contém a data `12 Aug 1998` é copiada em massa em um arquivo de dados como a cadeia de caracteres `1998-08-12 00:00:00.000`.  
  
> [!IMPORTANT]  
>  Ao importar dados em um campo **smalldatetime** com o **bcp**, verifique se o valor por segundo é 00.000; caso contrário, a operação falhará. O tipo de dados **smalldatetime** só mantém valores do minuto mais próximo. BULK INSERT e INSERT ... SELECT * FROM OPENROWSET(BULK...) não falharão nesta instância, mas truncarão o valor de segundos.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para usar formatos de dados para importação ou exportação em massa**  
  
-   [Usar o formato de caractere para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato de caractere Unicode para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo Unicode para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Utilitário bcp](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Compatibilidade com versões anteriores do Mecanismo de Banco de Dados do SQL Server](../../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  
