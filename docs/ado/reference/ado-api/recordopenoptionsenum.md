---
description: RecordOpenOptionsEnum
title: RecordOpenOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordOpenOptionsEnum
helpviewer_keywords:
- RecordOpenOptionsEnum enumeration [ADO]
ms.assetid: 9028aba4-90fc-4dfc-88e4-fa8a7b6fedee
author: rothja
ms.author: jroth
ms.openlocfilehash: 352622f55e82b1941439a242249e067aae090e51
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989777"
---
# <a name="recordopenoptionsenum"></a>RecordOpenOptionsEnum
Especifica as opções para abrir um [registro](./record-object-ado.md). Esses valores podem ser combinados usando o ou o.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adDelayFetchFields**|0x8000|Indica ao provedor que os campos associados ao **registro** não precisam ser recuperados inicialmente, mas podem ser recuperados na primeira tentativa de acessar o campo. O comportamento padrão, indicado pela ausência desse sinalizador, é recuperar todos os campos de objeto de **registro** .|  
|**adDelayFetchStream**|0x4000|Indica ao provedor que o fluxo padrão associado ao **registro** não precisa ser recuperado inicialmente. O comportamento padrão, indicado pela ausência desse sinalizador, é recuperar o fluxo padrão associado ao objeto de **registro** .|  
|**adOpenAsync**|0x1000|Indica que o objeto de **registro** está aberto no modo assíncrono.|  
|**adOpenExecuteCommand**|0x10000|Indica que a cadeia de caracteres de origem contém texto de comando que deve ser executado. Esse valor é equivalente à opção **adCmdText** no **conjunto de registros. Open**.|  
|**adOpenRecordUnspecified**|-1|Padrão. Indica que nenhuma opção foi especificada.|  
|**adOpenOutput**|0x800000|Indica que se a origem aponta para um nó que contém um script executável (como um. Página ASP), o **registro** aberto conterá os resultados do script executado. Esse valor só é válido com registros que não são de coleção.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Essas constantes não têm equivalentes ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Método Open (Registro do ADO)](./open-method-ado-record.md)