---
description: Coleção Parameters (ADO)
title: Coleção Parameters (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::get_Parameters
- Command15::Parameters
- Command15::GetParameters
helpviewer_keywords:
- Parameters collection [ADO]
ms.assetid: 497cae10-3913-422a-9753-dcbb0a639b1b
author: rothja
ms.author: jroth
ms.openlocfilehash: 06020bb66a8fd986d3fbf38bda59b98e29e66386
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773335"
---
# <a name="parameters-collection-ado"></a>Coleção Parameters (ADO)
Contém todos os objetos de [parâmetro](./parameter-object.md) de um objeto de [comando](./command-object-ado.md) .  
  
## <a name="remarks"></a>Comentários  
 Um objeto de **comando** tem uma coleção de **parâmetros** composta de objetos de **parâmetro** .  
  
 O uso do método [Refresh](./refresh-method-ado.md) em uma coleção de **parâmetros** do objeto de **comando** recupera as informações de parâmetro do provedor para o procedimento armazenado ou a consulta parametrizada especificada no objeto **Command** . Alguns provedores não dão suporte a chamadas de procedimento armazenado ou consultas parametrizadas; chamar o método **Refresh** na coleção **Parameters** ao usar um provedor como esse retornará um erro.  
  
 Se você não tiver definido seus próprios objetos de **parâmetro** e acessar a coleção de **parâmetros** antes de chamar o método **Refresh** , o ADO chamará automaticamente o método e preencherá a coleção para você.  
  
 Você pode minimizar as chamadas para o provedor para melhorar o desempenho se souber as propriedades dos parâmetros associados ao procedimento armazenado ou à consulta parametrizada que deseja chamar. Use o método [CreateParameter](./createparameter-method-ado.md) para criar objetos de **parâmetro** com as configurações de propriedade apropriadas e use o método [Append](./append-method-ado.md) para adicioná-los à coleção de **parâmetros** . Isso permite que você defina e retorne valores de parâmetro sem precisar chamar o provedor para as informações de parâmetro. Se você estiver gravando em um provedor que não fornece informações de parâmetro, você deve preencher manualmente a coleção de **parâmetros** usando esse método para poder usar parâmetros. Use o método [delete](./delete-method-ado-parameters-collection.md) para remover objetos de **parâmetro** da coleção **Parameters** , se necessário.  
  
 Os objetos na coleção de **parâmetros** de um **conjunto de registros** saem do escopo (portanto, ficando indisponíveis) quando o **conjunto de registros** é fechado.  
  
 Ao chamar um procedimento armazenado com o **comando**, o parâmetro valor de retorno/saída de um procedimento armazenado é recuperado da seguinte maneira:  
  
1.  Ao chamar um procedimento armazenado que não tem parâmetros, o método **Refresh** na coleção **Parameters** deve ser chamado antes de chamar o método **Execute** no objeto **Command** .  
  
2.  Ao chamar um procedimento armazenado com parâmetros e acrescentar explicitamente um parâmetro à coleção de **parâmetros** com **Append**, o parâmetro de saída/valor de retorno deve ser anexado à coleção de **parâmetros** . O valor de retorno deve primeiro ser acrescentado à coleção de **parâmetros** . Use **Append** para adicionar os outros parâmetros à coleção de **parâmetros** na ordem de definição. Por exemplo, o procedimento armazenado SPWithParam tem dois parâmetros. O primeiro parâmetro, *InParam*, é um parâmetro de entrada definido como adVarChar (20), e o segundo parâmetro, *OutParam*, é um parâmetro de saída definido como adVarChar (20). Você pode recuperar o parâmetro de saída/valor de retorno com o código a seguir.  
  
    ```vb
    ' Open Connection Conn  
    set ccmd = CreateObject("ADODB.Command")  
    ccmd.Activeconnection= Conn  
  
    ccmd.CommandText="SPWithParam"  
    ccmd.commandType = 4 'adCmdStoredProc  
  
    ccmd.parameters.Append ccmd.CreateParameter(, adInteger, adParamReturnValue, , NULL)   ' return value  
    ccmd.parameters.Append ccmd.CreateParameter("InParam", adVarChar, adParamInput, 20, "hello world")   ' input parameter  
    ccmd.parameters.Append ccmd.CreateParameter("OutParam", adVarChar, adParamOutput, 20, NULL)   ' output parameter  
  
    ccmd.execute()  
  
    ' Access ccmd.parameters(0) as return value of this stored procedure  
    ' Access ccmd.parameters("OutParam") as the output parameter of this stored procedure.  
  
    ```  
  
3.  Ao chamar um procedimento armazenado com parâmetros e configurar os parâmetros chamando o método **Item** na coleção **Parameters** , o parâmetro valor de retorno/saída do procedimento armazenado pode ser recuperado da coleção de **parâmetros** . Por exemplo, o procedimento armazenado SPWithParam tem dois parâmetros. O primeiro parâmetro, *InParam*, é um parâmetro de entrada definido como adVarChar (20), e o segundo parâmetro, *OutParam*, é um parâmetro de saída definido como adVarChar (20). Você pode recuperar o parâmetro de saída/valor de retorno com o código a seguir.  
  
    ```vb
    ' Open Connection Conn  
    set ccmd = CreateObject("ADODB.Command")  
    ccmd.Activeconnection= Conn  
  
    ccmd.CommandText="SPWithParam"  
    ccmd.commandType = 4 'adCmdStoredProc  
  
    ccmd.parameters.Item("InParam").value = "hello world" ' input parameter  
    ccmd.execute()  
  
    ' Access ccmd.parameters(0) as return value of stored procedure  
    ' Access ccmd.parameters(2) or ccmd.parameters("OutParam") as the output parameter.  
    ```  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos da coleção Parameters](./parameters-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Método Append (ADO)](./append-method-ado.md)   
 [Método CreateParameter (ADO)](./createparameter-method-ado.md)   
 [Objeto Parameter](./parameter-object.md)