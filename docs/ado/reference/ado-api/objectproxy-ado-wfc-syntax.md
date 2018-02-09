---
title: ObjectProxy (ADO - sintaxe WFC) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- ObjectProxy collection [ADO]
ms.assetid: f68f58bc-ad28-46cc-9fb3-099e1a678397
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 19884e98de3a6ed8070dcd30d3965c7ad9e77a4c
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="objectproxy-ado---wfc-syntax"></a>ObjectProxy (ADO - WFC sintaxe)
Um **ObjectProxy** objeto representa um servidor e é retornado pelo **createObject** método o [DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) objeto. A classe ObjectProxy tem um método, **chamar**, que pode invocar um método no servidor e retornar um objeto resultante dessa invocação.  
  
 **package com.ms.wfc.data**  
  
## <a name="methods"></a>Métodos  
  
### <a name="call-method-adowfc-syntax"></a>Método de chamada (sintaxe de ADO/WFC)  
 Invoca um método no servidor representado pelo ObjectProxy. Opcionalmente, os argumentos de método podem ser passados como uma matriz de objetos.  
  
#### <a name="syntax"></a>Sintaxe  
  
```  
public Object ObjectProxy.( String method )  
public Object ObjectProxy.( String method, Object[] args)  
```  
  
#### <a name="returns"></a>Retorna  
 Objeto  
 Um objeto resultante da invocação do método.  
  
#### <a name="parameters"></a>Parâmetros  
 *ObjectProxy*  
 Um **ObjectProxy** objeto que representa o servidor.  
  
 *método*  
 Uma cadeia de caracteres que contém o nome do método a ser invocado no servidor.  
  
 *args*  
 Opcional. Uma matriz de objetos que são argumentos para o método no servidor. Tipos de dados Java são automaticamente convertidos para tipos de dados adequados para uso no servidor.
