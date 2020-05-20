---
title: Usando páginas | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- PageSize property [ADO]
- pages [ADO]
- Recordset object [ADO]
- AbsolutePage property [ADO]
- PageCount property [ADO]
ms.assetid: 442b08c5-ccc7-4192-a1cc-22f250867782
author: rothja
ms.author: jroth
ms.openlocfilehash: 6542cb23deef9f10979e3bdb90c0820d84c0f150
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763027"
---
# <a name="using-pages"></a>Usar páginas
Use a propriedade **PageCount** para determinar quantas páginas de dados estão no objeto **Recordset** . *Páginas* são grupos de registros cujo tamanho é igual à configuração da propriedade **PageSize** . Mesmo que a última página esteja incompleta porque há menos registros do que o valor **PageSize** , ele conta como uma página adicional no valor **PageCount** . Se o objeto **Recordset** não oferecer suporte a essa propriedade, **PageCount** será-1 para indicar que o **PageCount** é interminável.  
  
 Use a propriedade **PageSize** para determinar quantos registros compõem uma página lógica de dados. O estabelecimento de um tamanho de página permite que você use a propriedade **AbsolutePage** para mover para o primeiro registro de uma página específica. Isso é útil em cenários de servidor Web quando você deseja permitir que o usuário percorra dados, exibindo um determinado número de registros por vez.  
  
 Essa propriedade pode ser definida a qualquer momento e seu valor será usado para calcular o local do primeiro registro de uma página específica.  
  
 Use a propriedade **AbsolutePage** para identificar o número de página no qual o registro atual está localizado. Novamente, o provedor deve dar suporte à funcionalidade apropriada para que essa propriedade esteja disponível.  
  
 **AbsolutePage** é baseado em 1 e é igual a 1 quando o registro atual é o primeiro registro no **conjunto de registros**. Defina essa propriedade para mover para o primeiro registro de uma página específica. Obtenha o número total de páginas da propriedade **PageCount** .
