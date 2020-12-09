---
title: ISSDataClassification::GetSensitivityClassification | Microsoft Docs
description: ISSDataClassification::GetSensitivityClassification
ms.custom: ''
ms.date: 09/30/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSDataClassification::GetSensitivityClassification
apitype: COM
helpviewer_keywords:
- GetSensitivityClassification method
author: bazizi
ms.author: v-beaziz
ms.openlocfilehash: 04877e626b57022d0110501b7da6145b2c4997d2
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96506632"
---
# <a name="issdataclassificationgetsensitivityclassification"></a>ISSDataClassification::GetSensitivityClassification
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW](../../../includes/applies-to-version/sql-asdb-asa.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Recupera dados de classificação de confidencialidade para o conjunto de linhas ativo. Para mais informações e um exemplo de código, confira [Usar classificação de dados](../features/using-data-classification.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetSensitivityClassification(
    SENSITIVITYCLASSIFICATION** ppSensitivityClassification);
```  
  
## <a name="arguments"></a>Argumentos  
  *ppSensitivityClassification*[out]  
 Um ponteiro para a estrutura SENSITIVITYCLASSIFICATION. Se o método falhar ou não houver informações de classificação de dados disponíveis, o provedor não alocará nenhuma memória e garantirá que o argumento ppSensitivityClassification seja um ponteiro nulo na saída.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 S_OK  
 O método foi bem-sucedido.    
  
 E_INVALIDARG  
 O argumento *ppSensitivityClassification* era NULL.  
  
 E_OUTOFMEMORY  
 O Driver do OLE DB para SQL Server não conseguiu alocar memória suficiente para concluir a solicitação.  

  
## <a name="remarks"></a>Comentários  
O Driver do OLE DB para SQL Server aloca um bloco de memória para conter a estrutura SENSITIVITYCLASSIFICATION e os dados referenciados por ela. Quando o consumidor não precisar mais de acesso aos dados de classificação, ele deverá desalocar essa memória chamando o método [IMalloc::Free](https://docs.microsoft.com/windows/win32/api/objidl/nf-objidl-imalloc-free).  
  
 A estrutura SENSITIVITYCLASSIFICATION é definida da seguinte maneira:
  
```cpp
typedef struct tagSensitivityClassification
{
    USHORT                     cSensitivityLabels;
    SENSITIVITYLABEL          *rgSensitivityLabels;
    USHORT                     cInformationTypes;
    INFORMATIONTYPE           *rgInformationTypes;
    USHORT                     cColumnSensitivityMetadata;
    COLUMNSENSITIVITYMETADATA *rgColumnSensitivityMetadata;
    SENSITIVITYRANKENUM        eQuerySensitivityRank;
} SENSITIVITYCLASSIFICATION;
```  

|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|*cSensitivityLabels*|O número de estruturas SENSITIVITYLABEL em *rgSensitivityLabels*.|  
|*rgSensitivityLabels*|Uma matriz de estruturas SENSITIVITYLABEL.|  
|*cInformationTypes*|O número de estruturas INFORMATIONTYPE em *rgInformationTypes*.|  
|*rgInformationTypes*|Uma matriz de estruturas INFORMATIONTYPE.|  
|*cColumnSensitivityMetadata*|O número de estruturas COLUMNSENSITIVITYMETADATA em *rgColumnSensitivityMetadata*.|  
|*rgColumnSensitivityMetadata*|Uma matriz de estruturas COLUMNSENSITIVITYMETADATA.|  
|*eQuerySensitivityRank*|Uma classificação relativa da confidencialidade de uma consulta que foi executada para obter o conjunto de linhas.|  

A estrutura SENSITIVITYLABEL é definida da seguinte maneira:
```cpp
typedef struct tagSENSITIVITYLABEL
{
    LPOLESTR pwszName;
    LPOLESTR pwszId;
} SENSITIVITYLABEL;
```

|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|*pwszName*|O nome de um rótulo de confidencialidade.|  
|*pwszId*|O identificador de um rótulo de confidencialidade.|  

A estrutura INFORMATIONTYPE é definida da seguinte maneira:
```cpp
typedef struct tagINFORMATIONTYPE
{
    LPOLESTR pwszName;
    LPOLESTR pwszId;
} INFORMATIONTYPE;
```

|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|*pwszName*|O nome de um tipo de informação.|  
|*pwszId*|O identificador de um tipo de informação.|  

A estrutura COLUMNSENSITIVITYMETADATA é definida da seguinte maneira:
```cpp
typedef struct tagCOLUMNSENSITIVITYMETADATA
{
    SENSITIVITYPROPERTY* rgSensitivityProperties;
    USHORT cSensitivityProperties;
} COLUMNSENSITIVITYMETADATA;
```

|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|*cSensitivityProperties*|O número de estruturas SENSITIVITYPROPERTY em *rgSensitivityProperties*.|  
|*rgSensitivityProperties*|Uma matriz de estruturas de confidencialidade.|  

A enumeração SENSITIVITYRANKENUM é definida da seguinte maneira:
```cpp
typedef enum tagSENSITIVITYRANKENUM
{
    SENSITIVITYRANK_NOT_DEFINED = -1,
    SENSITIVITYRANK_NONE = 0,
    SENSITIVITYRANK_LOW = 10,
    SENSITIVITYRANK_MEDIUM = 20,
    SENSITIVITYRANK_HIGH = 30,
    SENSITIVITYRANK_CRITICAL = 40
} SENSITIVITYRANKENUM;
```

A estrutura SENSITIVITYPROPERTY é definida da seguinte maneira:
```cpp
typedef struct tagSENSITIVITYPROPERTY
{
    SENSITIVITYLABEL* pSensitivityLabel;
    INFORMATIONTYPE* pInformationType;
    SENSITIVITYRANKENUM eSensitivityRank;
} SENSITIVITYPROPERTY;
```

|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|*pSensitivityLabel*|Um ponteiro para uma estrutura SENSITIVITYLABEL.|  
|*pInformationType*|Um ponteiro para uma estrutura INFORMATIONTYPE.|  
|*eSensitivityRank*|Uma classificação relativa da confidencialidade de uma coluna que faz parte de dados por coluna.|  

## <a name="see-also"></a>Consulte Também  
 [ISSDataClassification](../../oledb/ole-db-interfaces/issdataclassification-ole-db.md)  
 [Conjuntos de linhas](../ole-db-rowsets/rowsets.md)  
  
