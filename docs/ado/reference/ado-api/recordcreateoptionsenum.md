---
title: RecordCreateOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordCreateOptionsEnum
helpviewer_keywords:
- RecordCreateOptionsEnum enumeration [ADO]
ms.assetid: 6d746670-0850-4065-9cd4-168dea1d3ea9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 65fe33b73cf77a27fcd69743ffb09cb05e197797
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67917340"
---
# <a name="recordcreateoptionsenum"></a>RecordCreateOptionsEnum
Especifica se um **registro** existente deve ser aberto ou um novo **registro** criado para o método [Open](../../../ado/reference/ado-api/open-method-ado-record.md) do objeto [Record](../../../ado/reference/ado-api/record-object-ado.md) . Os valores podem ser combinados com um operador AND.  
  
|Constante|Valor|DESCRIÇÃO|  
|--------------|-----------|-----------------|  
|**adCreateCollection**|0x2000|Cria um novo **registro** no nó especificado pelo parâmetro de *origem* , em vez de abrir um **registro**existente. Se a origem apontar para um nó existente, ocorrerá um erro em tempo de execução, a menos que **adCreateCollection** seja combinado com **adOpenIfExists** ou **adCreateOverwrite**.|  
|**adCreateNonCollection**|0|Cria um novo **registro** do tipo [adSimpleRecord](../../../ado/reference/ado-api/recordtypeenum.md).|  
|**adCreateOverwrite**|0x4000000|Modifica os sinalizadores de criação **adCreateCollection**, **adCreateNonCollection**e **adCreateStructDoc**. Quando ou é usado com esse valor e um dos valores do sinalizador de criação, se a URL de origem apontar para um nó ou **registro**existente, o **registro** existente será substituído e um novo será criado em seu lugar. Esse valor não pode ser usado junto com **adOpenIfExists**.|  
|**adCreateStructDoc**|0x80000000|Cria um novo **registro** do tipo [adStructDoc](../../../ado/reference/ado-api/recordtypeenum.md), em vez de abrir um **registro**existente.|  
|**adFailIfNotExists**|-1|Padrão. Resultará em um erro de tempo de execução se a *origem* apontar para um nó não existente.|  
|**adOpenIfExists**|0x2000000|Modifica os sinalizadores de criação **adCreateCollection**, **adCreateNonCollection**e **adCreateStructDoc**. Quando ou é usado com esse valor e um dos valores do sinalizador de criação, se a URL de origem apontar para um objeto de **registro** ou nó existente, o provedor deverá abrir o **registro** existente em vez de criar um novo. Esse valor não pode ser usado junto com **adCreateOverwrite**.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Essas constantes não têm equivalentes ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Método Open (Registro do ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)
