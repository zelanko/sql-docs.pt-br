---
title: "Atualizar o método (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Collection::Refresh
- Parameters::Refresh
- Properties::Refresh
helpviewer_keywords: Refresh method [ADO]
ms.assetid: 089b7ca7-684f-4259-8032-5bd1ecc54426
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5e7b776b5d861403909b4856406d30109ad7c6b7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="refresh-method-ado"></a>Atualizar o método (ADO)
Atualiza os objetos em uma coleção para refletir os objetos disponíveis do e específico ao provedor.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
collection.Refresh  
```  
  
## <a name="remarks"></a>Comentários  
 O **atualização** método realiza tarefas diferentes, dependendo da coleção na qual você chamá-lo.  
  
### <a name="parameters"></a>Parâmetros  
 Usando o **atualizar** método o [parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) coleção de um [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto recupera informações do provedor do lado do parâmetro para o procedimento armazenado ou consulta parametrizada especificada no **comando** objeto. A coleção estará vazia para provedores que não oferecem suporte a chamadas de procedimento armazenado ou consultas parametrizadas.  
  
 Você deve definir o [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propriedade o **comando** objeto válido [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto, o [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) propriedade para um comando válido e o [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) propriedade **adCmdStoredProc** antes de chamar o **atualização** método.  
  
 Se você acessar o **parâmetros** coleção antes de chamar o **atualização** método, ADO irá chamar o método e preencher a coleção para você automaticamente.  
  
> [!NOTE]
>  Se você usar o **atualizar** método para obter informações de parâmetro de provedor e retorna o tipo de dados de comprimento variável de um ou mais [parâmetro](../../../ado/reference/ado-api/parameter-object.md) objetos, ADO pode alocar memória para os parâmetros com base em seu tamanho potencial máximo, que causará um erro durante a execução. Você deve definir explicitamente o [tamanho](../../../ado/reference/ado-api/size-property-ado-parameter.md) propriedade desses parâmetros antes de chamar o [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) método para evitar erros.  
  
### <a name="fields"></a>Campos  
 Usando o **atualizar** método o [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção não tem nenhum efeito visível. Para recuperar as alterações da estrutura de banco de dados subjacente, você deve usar o [Requery](../../../ado/reference/ado-api/requery-method.md) método ou, se o [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto não oferece suporte a indicadores, o [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)método.  
  
### <a name="properties"></a>Propriedades  
 Usando o **atualizar** método em um **propriedades** coleção de alguns objetos popula a coleção com as propriedades dinâmicas que o provedor expõe. Essas propriedades fornecem informações sobre a funcionalidade específica ao provedor, além de suporte de ADO propriedades internas.  
  
## <a name="applies-to"></a>Aplica-se a  
  
||||  
|-|-|-|  
|[Coleção de eixos](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)|[Coleção de colunas](../../../ado/reference/adox-api/columns-collection-adox.md)|[Coleção CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)|  
|[Coleção de dimensões](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)|[Coleção de erros](../../../ado/reference/ado-api/errors-collection-ado.md)|[Coleção de campos](../../../ado/reference/ado-api/fields-collection-ado.md)|  
|[Coleção de grupos](../../../ado/reference/adox-api/groups-collection-adox.md)|[Coleção hierarquias](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)|[Coleção de índices](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[Coleção de chaves](../../../ado/reference/adox-api/keys-collection-adox.md)|[Coleção de níveis](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)|[Coleção de membros](../../../ado/reference/ado-md-api/members-collection-ado-md.md)|  
|[Coleção de parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md)|[Coleção de posições](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)|[Coleção de procedimentos](../../../ado/reference/adox-api/procedures-collection-adox.md)|  
|[Coleção de propriedades](../../../ado/reference/ado-api/properties-collection-ado.md)|[Coleção de tabelas](../../../ado/reference/adox-api/tables-collection-adox.md)|[Coleção de usuários](../../../ado/reference/adox-api/users-collection-adox.md)|  
|[Coleção de exibições](../../../ado/reference/adox-api/views-collection-adox.md)|||  
  
## <a name="see-also"></a>Consulte também  
 [Atualizar exemplo de método (VB)](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [Atualizar exemplo de método (VC + +)](../../../ado/reference/ado-api/refresh-method-example-vc.md)   
 [Propriedade Count (ADO)](../../../ado/reference/ado-api/count-property-ado.md)   
 [Método Refresh (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)
