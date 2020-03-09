---
title: Comparando valores de GUID e uniqueidentifier
description: Demonstra como trabalhar com valores de GUID e uniqueidentifier no SQL Server e .NET.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: aababd75-2335-43e3-ace8-4b7ae84191a8
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 22d27f9a80765aacdfab25c568e8e2635f1779cc
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/07/2020
ms.locfileid: "78897025"
---
# <a name="comparing-guid-and-uniqueidentifier-values"></a>Comparando valores de GUID e uniqueidentifier

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

O tipo de dados GUID (identificador global exclusivo) no SQL Server é representado pelo tipo de dados `uniqueidentifier`, que armazena um valor binário de 16 bytes. Um GUID é um número binário cujo principal uso é como um identificador que deve ser exclusivo em uma rede com vários computadores em muitos sites. Os GUIDs podem ser gerados chamando a função NEWID do Transact-SQL e têm a garantia de serem exclusivos em todo o mundo. Para obter mais informações, confira [uniqueidentifier (Transact-SQL)](../../../t-sql/data-types/uniqueidentifier-transact-sql.md).  
  
## <a name="working-with-sqlguid-values"></a>Como trabalhar com valores de SqlGuid  
Já que os valores de GUIDs são longos e obscuros, eles não são significativos para os usuários. Se GUIDs gerados aleatoriamente forem usados para valores de chave e você inserir muitas linhas, você obterá E/S aleatórias em seus índices, o que poderá afetar negativamente o desempenho. Os GUIDs também são relativamente grandes quando comparados a outros tipos de dados. Em geral, recomendamos o uso de GUIDs apenas em cenários muito restritos, para os quais nenhum outro tipo de dados é adequado.  
  
### <a name="comparing-guid-values"></a>Comparação de valores de GUID  
Operadores de comparação podem ser usados com valores `uniqueidentifier`. Entretanto, a ordenação não é implementada comparando os padrões de bit dos dois valores. As únicas operações que são permitidas em um valor `uniqueidentifier` são as comparações (=, <>, \<, >, \<=, >=) e a verificação de NULL (IS NULL e IS NOT NULL). Nenhum outro operador aritmético é permitido.  
  
Tanto <xref:System.Guid> quanto <xref:System.Data.SqlTypes.SqlGuid> têm um método `CompareTo` para comparar valores GUID diferentes. No entanto, `System.Guid.CompareTo` e `SqlTypes.SqlGuid.CompareTo` são implementados de maneiras diferentes. <xref:System.Data.SqlTypes.SqlGuid> implementa `CompareTo` usando o comportamento do SQL Server, no qual apenas os últimos seis bytes de um valor são mais significativos. <xref:System.Guid> avalia todos os 16 bytes. O exemplo a seguir demonstra essa diferença de comportamento. A primeira seção do código exibe valores de <xref:System.Guid> não classificados e a segunda seção do código mostra os valores de <xref:System.Guid> classificados. A terceira seção mostra os valores de <xref:System.Data.SqlTypes.SqlGuid> classificados. A saída é exibida abaixo da listagem de código.  
  
[!code-csharp[DataWorks SqlGuid#1](~/../sqlclient/doc/samples/SqlGuid.cs#1)]
  
Esse exemplo gera os resultados a seguir.  
  
```console
Unsorted Guids:  
3aaaaaaa-bbbb-cccc-dddd-2eeeeeeeeeee  
2aaaaaaa-bbbb-cccc-dddd-1eeeeeeeeeee  
1aaaaaaa-bbbb-cccc-dddd-3eeeeeeeeeee  
  
Sorted Guids:  
1aaaaaaa-bbbb-cccc-dddd-3eeeeeeeeeee  
2aaaaaaa-bbbb-cccc-dddd-1eeeeeeeeeee  
3aaaaaaa-bbbb-cccc-dddd-2eeeeeeeeeee  
  
Sorted SqlGuids:  
2aaaaaaa-bbbb-cccc-dddd-1eeeeeeeeeee  
3aaaaaaa-bbbb-cccc-dddd-2eeeeeeeeeee  
1aaaaaaa-bbbb-cccc-dddd-3eeeeeeeeeee  
```  
  
## <a name="next-steps"></a>Próximas etapas
- [Tipos de dados do SQL Server e do ADO.NET](sql-server-data-types.md)
