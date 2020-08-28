---
description: Propriedade CommandText (ADO)
title: Propriedade CommandText (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: c0e7f2e9e346a5379051b101236df186b815aa85
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975187"
---
# <a name="commandtext-property-ado"></a>Propriedade CommandText (ADO)
Indica o texto de um comando a ser emitido em relação a um provedor.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Obtém ou define um valor de **cadeia de caracteres** que contém um comando de provedor, como uma instrução SQL, um nome de tabela, uma URL relativa ou uma chamada de procedimento armazenado. O padrão é a cadeia de caracteres vazia ("").  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **CommandText** para definir ou retornar o texto de um comando representado por um objeto [Command](./command-object-ado.md) . Normalmente, essa será uma instrução SQL, mas também pode ser qualquer outro tipo de instrução de comando reconhecido pelo provedor, como uma chamada de procedimento armazenado. Uma instrução SQL deve ser do dialeto ou da versão específica com suporte do processador de consultas do provedor.  
  
 Se a propriedade [preparada](./prepared-property-ado.md) do objeto **de comando** for definida como **true** e o objeto de **comando** estiver associado a uma conexão aberta quando você definir a propriedade **CommandText** , o ADO preparará a consulta (ou seja, uma forma compilada da consulta que é armazenada pelo provedor) quando você chamar os métodos [Execute](./execute-method-ado-command.md) ou [Open](./open-method-ado-connection.md) .  
  
 Dependendo da configuração da propriedade [CommandType](./commandtype-property-ado.md) , o ADO pode alterar a propriedade **CommandText** . Você pode ler a propriedade **CommandText** a qualquer momento para ver o texto do comando real que o ADO usará durante a execução.  
  
 Use a propriedade **CommandText** para definir ou retornar uma URL relativa que especifica um recurso, como um arquivo ou diretório. O recurso é relativo a um local especificado explicitamente por uma URL absoluta ou implicitamente por um objeto de [conexão](./connection-object-ado.md) aberta.  
  
> [!NOTE]
>  As URLs que usam o esquema http invocarão automaticamente o [provedor do Microsoft OLE DB para publicação na Internet](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [URLs absolutas e relativas](../../guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Command (ADO)](./command-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades ActiveConnection, CommandText, CommandTimeout, CommandType, size e Direction (VB)](./activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [Exemplo das propriedades ActiveConnection, CommandText, CommandTimeout, CommandType, size e Direction (VC + +)](./activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Método Requery](./requery-method.md)   
 [Exemplo das propriedades ActiveConnection, CommandText, CommandTimeout, CommandType, size e Direction (JScript)](./activeconnection-commandtext-timeout-type-size-example-jscript.md)