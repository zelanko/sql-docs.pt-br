---
title: "Implementação da compactação Unicode | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-data-compression
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Unicode data compression
- compression [SQL Server], Unicode data
ms.assetid: 44e69e60-9b35-43fe-b9c7-8cf34eaea62a
caps.latest.revision: 7
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 27117e609effaa3ded124a33d742ac9a0b374d6f
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="unicode-compression-implementation"></a>Implementação da compactação Unicode
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa uma implementação do algoritmo SCSU (Esquema de Compactação Padrão para Unicode) para compactar valores Unicode que são armazenados em objetos compactados por linha ou página. Para esses objetos compactados, a compactação Unicode é automática para as colunas **nchar(n)** e **nvarchar(n)** . O [!INCLUDE[ssDE](../../includes/ssde-md.md)] armazena dados Unicode como 2 bytes, seja qual for a localidade. Isso é conhecido como codificação UCS-2. Para algumas localidades, a implementação da compactação SCSU no SQL Server pode economizar até 50 por cento em espaço de armazenamento.  
  
## <a name="supported-data-types"></a>Tipos de dados com suporte  
 A compactação Unicode dá suporte aos tipos de dados de comprimento fixo **nchar(n)** e **nvarchar(n)** . Os valores de dados armazenados fora da linha ou em colunas **nvarchar(max)** não são compactados.  
  
> [!NOTE]  
>  A Compactação de Unicode não terá suporte para obter dados **nvarchar(max)** mesmo se forem armazenados em linha. Porém, este tipo de dados ainda pode aproveitar a compactação de página.  
  
## <a name="upgrading-from-earlier-versions-of-sql-server"></a>Atualizando a partir de versões anteriores do SQL Server  
 Quando um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é atualizado para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], as alterações feitas devido à compactação Unicode não são feitas em nenhum objeto do banco de dados, compactado ou não. Depois que o banco de dados é atualizado, os objetos são afetados da seguinte maneira:  
  
-   Se o objeto não for compactado, nenhuma alteração será feita e o objeto continuará funcionando como antes.  
  
-   Objetos compactados por linha ou página continuam funcionando como antes. Dados não compactados permanecerão assim até que seu valor seja atualizado.  
  
-   As novas linhas inseridas em uma tabela compactada por linha ou página usam compactação Unicode.  
  
    > [!NOTE]  
    >  Para aproveitar ao máximo os benefícios da compactação Unicode, o objeto deve ser reconstruído com compactação de página ou linha.  
  
## <a name="how-unicode-compression-affects-data-storage"></a>Como a compactação Unicode afeta o armazenamento de dados  
 Quando um índice é criado ou reconstruído ou quando um valor é alterado em uma tabela que foi compactada por linha ou página, o índice ou valor afetado será armazenado compactado somente se seu tamanho compactado for menor que seu tamanho atual. Isto impede as linhas em uma tabela ou índice de aumentarem de tamanho devido à compactação Unicode.  
  
 O espaço de armazenamento que a compactação economiza depende das características e da localidade dos dados que estão sendo compactados. A tabela a seguir lista a economia de espaço que pode ser obtida para diversas localidades.  
  
|Localidade|Porcentagem de compactação|  
|------------|-------------------------|  
|Inglês|50%|  
|Alemão|50%|  
|Híndi|50%|  
|Turco|48%|  
|Vietnamita|39%|  
|Japonês|15%|  
  
## <a name="see-also"></a>Consulte também  
 [Compactação de dados](../../relational-databases/data-compression/data-compression.md)   
 [sp_estimate_data_compression_savings &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md)   
 [Implementação da compactação de página](../../relational-databases/data-compression/page-compression-implementation.md)   
 [sys.dm_db_persisted_sku_features &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-persisted-sku-features-transact-sql.md)  
  
  
