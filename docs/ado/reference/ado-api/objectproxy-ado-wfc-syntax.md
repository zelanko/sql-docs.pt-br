---
description: ObjectProxy (ADO – Sintaxe WFC)
title: Objectproxy (ADO – sintaxe WFC) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ObjectProxy collection [ADO]
ms.assetid: f68f58bc-ad28-46cc-9fb3-099e1a678397
author: rothja
ms.author: jroth
ms.openlocfilehash: 1c52f9253ced985ed6a53af87c95ff7fe2eee3fa
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990397"
---
# <a name="objectproxy-ado---wfc-syntax"></a>ObjectProxy (ADO – Sintaxe WFC)
Um objeto **objectproxy** representa um servidor e é retornado pelo método **CreateObject** do objeto [DataSpace](../rds-api/dataspace-object-rds.md) . A classe objectproxy tem um método, **Call**, que pode invocar um método no servidor e retornar um objeto resultante dessa invocação.  
  
 **pacote com. ms. wfc. Data**  
  
## <a name="methods"></a>Métodos  
  
### <a name="call-method-adowfc-syntax"></a>Método Call (sintaxe ADO/WFC)  
 Invoca um método no servidor representado pelo objectproxy. Opcionalmente, argumentos de método podem ser passados como uma matriz de objetos.  
  
#### <a name="syntax"></a>Sintaxe  
  
```  
public Object ObjectProxy.( String method )  
public Object ObjectProxy.( String method, Object[] args)  
```  
  
#### <a name="returns"></a>Retornos  
 Objeto  
 Um objeto resultante da invocação do método.  
  
#### <a name="parameters"></a>Parâmetros  
 *ObjectProxy*  
 Um objeto **objectproxy** que representa o servidor.  
  
 *forma*  
 Uma cadeia de caracteres que contém o nome do método a ser invocado no servidor.  
  
 *argumento*  
 Opcional. Uma matriz de objetos que são argumentos para o método no servidor. Os tipos de dados Java são convertidos automaticamente em tipos de dados adequados para uso no servidor.