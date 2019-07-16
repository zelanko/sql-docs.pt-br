---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4e062c67f0dedf55d63a076725b46d4405918741
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917703"
---
# <a name="parameters-collection-ado"></a>Coleção Parameters (ADO)
Contém todos os [parâmetro](../../../ado/reference/ado-api/parameter-object.md) objetos de uma [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto.  
  
## <a name="remarks"></a>Comentários  
 Um **comando** objeto tem um **parâmetros** coleção composta por **parâmetro** objetos.  
  
 Usando o [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) método em um **comando** do objeto **parâmetros** coleção recupera informações de parâmetro de provedor para o procedimento armazenado ou uma consulta parametrizada especificado na **comando** objeto. Alguns provedores não têm suporte para chamadas de procedimento armazenado ou consultas parametrizadas; chamar o **Refresh** método na **parâmetros** coleção ao usar esse provedor será retornado um erro.  
  
 Se você não tiver definido sua própria **parâmetro** objetos e você acessar a **parâmetros** coleção antes de chamar o **atualizar** método, ADO chamará automaticamente a método e popular a coleção para você.  
  
 Você pode minimizar as chamadas para o provedor para melhorar o desempenho se você souber as propriedades dos parâmetros associados com o procedimento armazenado ou consulta parametrizada que você deseja chamar. Usar o [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md) método para criar **parâmetro** objetos com as configurações de propriedade apropriada e o uso de [Append](../../../ado/reference/ado-api/append-method-ado.md) método para adicioná-los para o  **Parâmetros** coleção. Isso lhe permite definir e retornar valores de parâmetro sem a necessidade de chamar o provedor para obter as informações de parâmetro. Se você estiver escrevendo um provedor que não fornece informações de parâmetro, você deve preencher manualmente a **parâmetros** coleção usando esse método para ser capaz de usar parâmetros em todos os. Use o [excluir](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md) método para remover **parâmetro** objetos o **parâmetros** coleção, se necessário.  
  
 Os objetos na **parâmetros** coleção de uma **conjunto de registros** vá fora do escopo (portanto, tornando-se indisponível) quando o **Recordset** está fechado.  
  
 Ao chamar um procedimento armazenado com **comando**, o parâmetro de valor de retorno/saída de um procedimento armazenado é recuperado da seguinte maneira:  
  
1.  Ao chamar um procedimento armazenado que não tem parâmetros, o **atualizar** método na **parâmetros** coleção deve ser chamada antes de chamar o **Execute** método no **Comando** objeto.  
  
2.  Ao chamar um procedimento armazenado com parâmetros e acrescentando explicitamente um parâmetro para o **parâmetros** coleção com **Append**, o parâmetro de valor/saída de retorno deve ser acrescentado à **Parâmetros** coleção. O valor de retorno deve ser anexado pela primeira vez para o **parâmetros** coleção. Use **Append** para adicionar os outros parâmetros para o **parâmetros** coleção na ordem de definição. Por exemplo, o procedimento armazenado SPWithParam tem dois parâmetros. O primeiro parâmetro, *InParam*, é um parâmetro de entrada definido como adVarChar (20) e o segundo parâmetro, *OutParam*, é um parâmetro de saída definido como adVarChar (20). Você pode recuperar o parâmetro de valor de retorno/saída com o código a seguir.  
  
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
  
3.  Ao chamar um procedimento armazenado com parâmetros e configuração dos parâmetros ao chamar o **Item** método o **parâmetros** o parâmetro de valor/saída de retorno do procedimento armazenado de coleção, pode ser recuperada do **parâmetros** coleção. Por exemplo, o procedimento armazenado SPWithParam tem dois parâmetros. O primeiro parâmetro, *InParam*, é um parâmetro de entrada definido como adVarChar (20) e o segundo parâmetro, *OutParam*, é um parâmetro de saída definido como adVarChar (20). Você pode recuperar o parâmetro de valor de retorno/saída com o código a seguir.  
  
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
  
-   [Eventos, métodos e propriedades de coleção de parâmetros](../../../ado/reference/ado-api/parameters-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Método append (ADO)](../../../ado/reference/ado-api/append-method-ado.md)   
 [Método CreateParameter (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)
