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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0d697fa5b411d9000c03a700f6b4fe0e4b39aa5e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923517"
---
# <a name="using-pages"></a>Usar páginas
Use o **PageCount** propriedade para determinar quantas páginas de dados estão na **Recordset** objeto. *Páginas* são grupos de registros cujo tamanho é igual a **PageSize** configuração da propriedade. Mesmo se a última página está incompleta porque há menos registros que o **PageSize** valor, ele contará como uma página adicional na **PageCount** valor. Se o **conjunto de registros** objeto não oferece suporte a essa propriedade, **PageCount** será -1 para indicar que o **PageCount** for indeterminável.  
  
 Use o **PageSize** propriedade para determinar quantos registros compõem uma página lógica dos dados. Estabelecer um tamanho de página permite que você use o **AbsolutePage** propriedade para mover para o primeiro registro de uma página específica. Isso é útil em cenários de servidor Web quando você deseja permitir que o usuário à página por meio de dados, exibindo um determinado número de registros por vez.  
  
 Essa propriedade pode ser definida em qualquer momento, e seu valor será usado para calcular a localização do primeiro registro de uma página específica.  
  
 Use o **AbsolutePage** propriedade para identificar o número da página em que o registro atual está localizado. Novamente, o provedor deve oferecer suporte a funcionalidade apropriada para essa propriedade estar disponível.  
  
 **AbsolutePage** é baseado em 1 e é igual a 1 quando o registro atual é o primeiro registro na **conjunto de registros**. Defina essa propriedade para mover para o primeiro registro de uma página específica. Obter o número total de páginas a partir de **PageCount** propriedade.
