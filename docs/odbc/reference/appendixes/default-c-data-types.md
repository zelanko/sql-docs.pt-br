---
title: Tipos de dados C padrão | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], about pseudo-type identifiers
- pseudo-type identifiers [ODBC]
ms.assetid: 229140ae-af8f-4ec8-9ccf-1e92360e0bac
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fdb787580e1c79df805f468416ab8993a1d32a26
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307047"
---
# <a name="default-c-data-types"></a>Tipos de dados do C padrão
Se um aplicativo especificar SQL_C_DEFAULT no **SQLBindCol,** **SQLGetData**ou **SQLBindParameter,** o driver assume que o tipo de dados C do buffer de saída ou entrada corresponde ao tipo de dados SQL da coluna ou parâmetro ao qual o buffer está vinculado.  
  
> [!IMPORTANT]  
>  As aplicações interoperáveis não devem usar SQL_C_DEFAULT. Em vez disso, eles devem sempre especificar o tipo C do buffer que eles estão usando. Isso porque os drivers nem sempre podem determinar corretamente o tipo C padrão, pelas seguintes razões:  
  
-   Se o DBMS promover um tipo de dados SQL de uma coluna ou parâmetro, o driver não poderá determinar o tipo de dados SQL original de uma coluna ou parâmetro. Portanto, não pode determinar o tipo de dados C padrão correspondente.  
  
-   Se o driver não puder determinar se uma determinada coluna ou parâmetro está assinado, como é frequentemente o caso quando isso é tratado pelo DBMS, o motorista não pode determinar se o tipo de dados C padrão correspondente deve ser assinado ou não assinado.  
  
     Como SQL_C_DEFAULT é fornecido apenas como uma conveniência de programação, o aplicativo não perde nenhuma funcionalidade quando especifica o tipo de dados C real.  
  
 Uma tabela mostrando o tipo de dados C padrão para cada tipo de dados SQL é incluída na [conversão de dados de SQL para C Tipos de dados,](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)mais tarde neste apêndice.
