---
title: Método Refresh (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Collection::Refresh
- Parameters::Refresh
- Properties::Refresh
helpviewer_keywords:
- Refresh method [ADO]
ms.assetid: 089b7ca7-684f-4259-8032-5bd1ecc54426
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0fee14a397104f8320fc01ce29f8364384151922
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711719"
---
# <a name="refresh-method-ado"></a>Método Refresh (ADO)
Atualiza os objetos em uma coleção para refletir objetos disponíveis do e específicos ao provedor.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
collection.Refresh  
```  
  
## <a name="remarks"></a>Comentários  
 O **Refresh** método realiza tarefas diferentes, dependendo da coleção da qual você chamá-lo.  
  
### <a name="parameters"></a>Parâmetros  
 Usando o **Refresh** método na [parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) coleção de um [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto recupera informações de parâmetro do lado do provedor para o procedimento armazenado ou consulta parametrizada especificada na **comando** objeto. A coleção estará vazia para provedores que não dão suporte a chamadas de procedimento armazenado ou consultas parametrizadas.  
  
 Você deve definir a [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propriedade da **comando** objeto a ser válido [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto, o [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) propriedade para um comando válido e o [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) propriedade **adCmdStoredProc** antes de chamar o **atualizar** método.  
  
 Se você acessar o **parâmetros** coleção antes de chamar o **atualizar** método, ADO automaticamente chama o método e popular a coleção para você.  
  
> [!NOTE]
>  Se você usar o **Refresh** método para obter informações de parâmetro de provedor e ele retorna um ou mais tipos de dados de comprimento variável [parâmetro](../../../ado/reference/ado-api/parameter-object.md) objetos, o ADO pode alocar memória para os parâmetros com base em seu tamanho potencial máximo, que causará um erro durante a execução. Você deve definir explicitamente o [tamanho](../../../ado/reference/ado-api/size-property-ado-parameter.md) propriedade desses parâmetros antes de chamar o [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) método para evitar erros.  
  
### <a name="fields"></a>Campos  
 Usando o **Refresh** método na [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção não tem nenhum efeito visível. Para recuperar as alterações da estrutura de banco de dados subjacente, você deve usar o [Requery](../../../ado/reference/ado-api/requery-method.md) método ou, se o [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto não oferece suporte a indicadores, o [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)método.  
  
### <a name="properties"></a>Propriedades  
 Usando o **Refresh** método em um **propriedades** coleção de alguns objetos preenche a coleção com as propriedades dinâmicas que o provedor expõe. Essas propriedades fornecem informações sobre a funcionalidade específica ao provedor, além do dá suporte à ADO de propriedades internas.  
  
## <a name="applies-to"></a>Aplica-se a  
  
||||  
|-|-|-|  
|[Coleção Axes](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)|[Coleção de colunas](../../../ado/reference/adox-api/columns-collection-adox.md)|[Coleção CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)|  
|[Coleção de dimensões](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)|[Coleção de erros](../../../ado/reference/ado-api/errors-collection-ado.md)|[Coleção de campos](../../../ado/reference/ado-api/fields-collection-ado.md)|  
|[Coleção de grupos](../../../ado/reference/adox-api/groups-collection-adox.md)|[Coleção hierarquias](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)|[Coleção de índices](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[Coleção de chaves](../../../ado/reference/adox-api/keys-collection-adox.md)|[Coleção de níveis](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)|[Coleção de membros](../../../ado/reference/ado-md-api/members-collection-ado-md.md)|  
|[Coleção de parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md)|[Coleção Positions](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)|[Coleção de procedimentos](../../../ado/reference/adox-api/procedures-collection-adox.md)|  
|[Coleção de propriedades](../../../ado/reference/ado-api/properties-collection-ado.md)|[Coleção de tabelas](../../../ado/reference/adox-api/tables-collection-adox.md)|[Coleção de usuários](../../../ado/reference/adox-api/users-collection-adox.md)|  
|[Coleção Views](../../../ado/reference/adox-api/views-collection-adox.md)|||  
  
## <a name="see-also"></a>Consulte também  
 [Método exemplo Refresh (VB)](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [Atualizar o exemplo do método (VC + +)](../../../ado/reference/ado-api/refresh-method-example-vc.md)   
 [Propriedade Count (ADO)](../../../ado/reference/ado-api/count-property-ado.md)   
 [Método Refresh (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)
