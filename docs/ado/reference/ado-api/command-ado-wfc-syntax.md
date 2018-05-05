---
title: Comando (ADO - sintaxe WFC) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Command collection [ADO], ADO/WFC syntax
ms.assetid: 39d0aa06-03ac-4c9a-8400-83947756ef99
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c5e5b50a3e7b05d77c582a3b02c1f9b366dbc066
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="command-ado---wfc-syntax"></a>Comando (ADO - WFC sintaxe)
## <a name="package-commswfcdata"></a>pacote com.ms.wfc.data  
  
### <a name="constructor"></a>Construtor  
  
```  
public Command()  
public Command(String commandtext)  
```  
  
### <a name="methods"></a>Métodos  
  
```  
public void cancel()  
public com.ms.wfc.data.Parameter createParameter(String  
    Name, int Type, int Direction, int Size, Object Value)  
public Recordset execute()  
public Recordset execute(Object[] parameters)  
public Recordset execute(Object[] parameters, int options)  
public int executeUpdate(Object[] parameters)  
public int executeUpdate(Object[] parameters, int options)  
public int executeUpdate()  
```  
  
 O **executeUpdate** método é um método de casos especial que chama o ADO subjacente **executar** método com determinados parâmetros. O **executeUpdate** método não oferece suporte para o retorno de um **registros** objeto, portanto, o **executar** do método *opções* parâmetro é modificado com **AdoEnums.ExecuteOptions.NORECORDS**. Após o **executar** método é concluído, ele é atualizado *RecordsAffected* parâmetro é passado de volta para o **executeUpdate** método, que, por fim, é retornado como um **int**.  
  
### <a name="properties"></a>Propriedades  
  
```  
public com.ms.wfc.data.Connection getActiveConnection()  
public void setActiveConnection(com.ms.wfc.data.Connection con)  
public void setActiveConnection(String conString)  
public String getCommandText()  
public void setCommandText(String command)  
public int getCommandTimeout()  
public void setCommandTimeout(int timeout)  
public int getCommandType()  
public void setCommandType(int type)  
public String getName()  
public void setName(String name)  
public boolean getPrepared()  
public void setPrepared(boolean prepared)  
public int getState()  
public com.ms.wfc.data.Parameter getParameter(int n)  
public com.ms.wfc.data.Parameter getParameter(String n)  
public com.ms.wfc.data.Parameters getParameters()  
public AdoProperties getProperties()  
```  
  
## <a name="see-also"></a>Consulte também  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)
