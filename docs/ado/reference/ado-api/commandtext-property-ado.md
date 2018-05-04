---
title: A propriedade CommandText (ADO) | Microsoft Docs
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
f1_keywords:
- Command15::CommandText
helpviewer_keywords:
- CommandText property [ADO]
ms.assetid: 4dd7e82a-8da5-4a4e-b439-11a29286fa0e
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aaad9ab5bc4def9975631a875071dc69a44b6028
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="commandtext-property-ado"></a>Propriedade CommandText (ADO)
Indica o texto de um comando a ser emitido em um provedor.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Obtém ou define um **cadeia de caracteres** valor que contém um comando de provedor, como uma instrução SQL, um nome de tabela, uma URL relativa ou uma chamada de procedimento armazenado. O padrão é a cadeia de caracteres vazia ("").  
  
## <a name="remarks"></a>Remarks  
 Use o **CommandText** propriedade para definir ou retornar o texto de um comando representado por um [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto. Geralmente isso será uma instrução SQL, mas também pode ser qualquer outro tipo de instrução de comando reconhecida pelo provedor, como uma chamada de procedimento armazenado. Uma instrução SQL deve ser da versão com suporte pelo processador de consulta do provedor ou dialeto específico.  
  
 Se o [preparado](../../../ado/reference/ado-api/prepared-property-ado.md) propriedade o **comando** objeto é definido como **True** e o **comando** objeto está associado a uma conexão aberta quando você define o **CommandText** propriedade ADO prepara a consulta (ou seja, um formulário compilado da consulta que é armazenado pelo provedor) quando você chama o [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) ou [abrir](../../../ado/reference/ado-api/open-method-ado-connection.md)métodos.  
  
 Dependendo do [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) configuração, da propriedade ADO pode alterar o **CommandText** propriedade. Você pode ler o **CommandText** propriedade a qualquer momento para ver o texto de comando que ADO será usada durante a execução.  
  
 Use o **CommandText** propriedade para definir ou retornar uma URL relativa que especifica um recurso, como um arquivo ou diretório. O recurso está em relação a um local especificado explicitamente por uma URL absoluta, ou implicitamente por um aberto [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
> [!NOTE]
>  URLs usando o esquema http invocará automaticamente o [Microsoft OLE DB Provider para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [Absolute e URLs relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [ActiveConnection CommandText, CommandTimeout, CommandType, tamanho e exemplo de propriedades de direção (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection CommandText, CommandTimeout, CommandType, tamanho e exemplo de propriedades de direção (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Método Requery](../../../ado/reference/ado-api/requery-method.md)   
 [ActiveConnection CommandText, CommandTimeout, CommandType, tamanho e exemplo de propriedades de direção (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
