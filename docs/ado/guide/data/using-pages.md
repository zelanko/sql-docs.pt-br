---
title: Usando páginas | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- PageSize property [ADO]
- pages [ADO]
- Recordset object [ADO]
- AbsolutePage property [ADO]
- PageCount property [ADO]
ms.assetid: 442b08c5-ccc7-4192-a1cc-22f250867782
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6afd42480be68c98eafa1d7531a79792620aa255
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35273315"
---
# <a name="using-pages"></a>Usando páginas
Use o **PageCount** propriedade para determinar quantas páginas de dados estão no **registros** objeto. *Páginas* são grupos de registros cujo tamanho é igual a **PageSize** configuração de propriedade. Mesmo que a última página está incompleta porque há menos registros que o **PageSize** valor, ela será considerada como uma página adicional no **PageCount** valor. Se o **registros** objeto não oferece suporte a essa propriedade, **PageCount** será -1 para indicar que o **PageCount** for indeterminável.  
  
 Use o **PageSize** propriedade para determinar quantos registros compõem uma página lógica dos dados. Estabelecer um tamanho de página permite que você use o **AbsolutePage** propriedade para mover para o primeiro registro de uma determinada página. Isso é útil em cenários de servidor Web quando você deseja permitir que o usuário para página de dados, exibindo um determinado número de registros por vez.  
  
 Essa propriedade pode ser definida a qualquer momento, e seu valor será usado para calcular a localização do primeiro registro de uma determinada página.  
  
 Use o **AbsolutePage** propriedade para identificar o número da página em que o registro atual está localizado. Novamente, o provedor deve oferecer suporte a funcionalidade apropriada para essa propriedade disponível.  
  
 **AbsolutePage** é baseado em 1 e é igual a 1 quando o registro atual é o primeiro registro no **registros**. Defina essa propriedade para mover para o primeiro registro de uma determinada página. Obter o número total de páginas a partir de **PageCount** propriedade.
