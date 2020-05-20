---
title: Propriedade CommandText (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::CommandText
helpviewer_keywords:
- CommandText property [ADO]
ms.assetid: 4dd7e82a-8da5-4a4e-b439-11a29286fa0e
author: rothja
ms.author: jroth
ms.openlocfilehash: 0fea58e679e11ac068189ad622b3dce627fc8a63
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760432"
---
# <a name="commandtext-property-ado"></a>Propriedade CommandText (ADO)
Indica o texto de um comando a ser emitido em relação a um provedor.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Obtém ou define um valor de **cadeia de caracteres** que contém um comando de provedor, como uma instrução SQL, um nome de tabela, uma URL relativa ou uma chamada de procedimento armazenado. O padrão é a cadeia de caracteres vazia ("").  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **CommandText** para definir ou retornar o texto de um comando representado por um objeto [Command](../../../ado/reference/ado-api/command-object-ado.md) . Normalmente, essa será uma instrução SQL, mas também pode ser qualquer outro tipo de instrução de comando reconhecido pelo provedor, como uma chamada de procedimento armazenado. Uma instrução SQL deve ser do dialeto ou da versão específica com suporte do processador de consultas do provedor.  
  
 Se a propriedade [preparada](../../../ado/reference/ado-api/prepared-property-ado.md) do objeto **de comando** for definida como **true** e o objeto de **comando** estiver associado a uma conexão aberta quando você definir a propriedade **CommandText** , o ADO preparará a consulta (ou seja, uma forma compilada da consulta que é armazenada pelo provedor) quando você chamar os métodos [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) ou [Open](../../../ado/reference/ado-api/open-method-ado-connection.md) .  
  
 Dependendo da configuração da propriedade [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) , o ADO pode alterar a propriedade **CommandText** . Você pode ler a propriedade **CommandText** a qualquer momento para ver o texto do comando real que o ADO usará durante a execução.  
  
 Use a propriedade **CommandText** para definir ou retornar uma URL relativa que especifica um recurso, como um arquivo ou diretório. O recurso é relativo a um local especificado explicitamente por uma URL absoluta ou implicitamente por um objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) aberta.  
  
> [!NOTE]
>  As URLs que usam o esquema http invocarão automaticamente o [provedor do Microsoft OLE DB para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [URLs absolutas e relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades ActiveConnection, CommandText, CommandTimeout, CommandType, size e Direction (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [Exemplo das propriedades ActiveConnection, CommandText, CommandTimeout, CommandType, size e Direction (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Método Requery](../../../ado/reference/ado-api/requery-method.md)   
 [Exemplo das propriedades ActiveConnection, CommandText, CommandTimeout, CommandType, size e Direction (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
