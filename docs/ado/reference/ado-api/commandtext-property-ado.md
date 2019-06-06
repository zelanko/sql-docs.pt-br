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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7ebc6a783aa8520c3ab16465143acdf1a6bf6628
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698944"
---
# <a name="commandtext-property-ado"></a>Propriedade CommandText (ADO)
Indica o texto de um comando ser emitido para um provedor.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Obtém ou define um **cadeia de caracteres** valor que contém um comando de provedor, como uma instrução SQL, um nome de tabela, uma URL relativa ou uma chamada de procedimento armazenado. O padrão é a cadeia de caracteres vazia ("").  
  
## <a name="remarks"></a>Comentários  
 Use o **CommandText** propriedade para definir ou retornar o texto de um comando representado por uma [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto. Normalmente, isso será uma instrução SQL, mas também pode ser qualquer outro tipo de instrução de comando reconhecido pelo provedor, como uma chamada de procedimento armazenado. Uma instrução SQL deve ser da versão com suporte pelo processador de consulta do provedor ou dialeto específico.  
  
 Se o [preparado](../../../ado/reference/ado-api/prepared-property-ado.md) propriedade da **comando** objeto é definido como **verdadeiro** e o **comando** objeto está associado a uma conexão aberta quando você definir o **CommandText** propriedade, o ADO prepara a consulta (ou seja, um formulário compilado da consulta que é armazenado pelo provedor) quando você chama o [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) ou [abrir](../../../ado/reference/ado-api/open-method-ado-connection.md)métodos.  
  
 Dependendo de [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) pode alterar a configuração, da propriedade ADO a **CommandText** propriedade. Você pode ler o **CommandText** propriedade a qualquer momento para ver o texto de comando real que ADO usará durante a execução.  
  
 Use o **CommandText** propriedade para definir ou retornar uma URL relativa que especifica um recurso, como um arquivo ou diretório. O recurso está em relação a um local especificado explicitamente por uma URL absoluta ou implicitamente por uma abertura [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
> [!NOTE]
>  URLs usando o esquema http invocará automaticamente o [Microsoft OLE DB Provider para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [absoluta e relativa URLs](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamanho e exemplo de propriedades de direção (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamanho e exemplo de propriedades de direção (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Método Requery](../../../ado/reference/ado-api/requery-method.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamanho e exemplo de propriedades de direção (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
