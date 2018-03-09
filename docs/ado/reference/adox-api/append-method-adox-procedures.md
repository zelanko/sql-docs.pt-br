---
title: "Método (ADOX procedimentos) append | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Procedures::Append
- Procedures::raw_Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 38e3492c-c1e1-42e3-a71a-befdc90204db
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cdf43784501659e3fd4da883ddeac33439a30719
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="append-method-adox-procedures"></a>Acrescente o método (ADOX procedimentos)
Adiciona um novo [procedimento](../../../ado/reference/adox-api/procedure-object-adox.md) o objeto para o [procedimentos](../../../ado/reference/adox-api/procedures-collection-adox.md) coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Procedures.Append Name, Command  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Nome*  
 Um **cadeia de caracteres** valor que especifica o nome do procedimento para criar e anexar.  
  
 *Comando*  
 ADO [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto que representa o procedimento para criar e anexar.  
  
## <a name="remarks"></a>Remarks  
 Cria um novo procedimento na fonte de dados com o nome e atributos especificados no **comando** objeto.  
  
 Se o texto do comando que especifica o usuário representa uma exibição em vez de um procedimento, o comportamento depende do provedor que está sendo usado. **Acrescentar** falhará se o provedor não oferece suporte a comandos persistentes.  
  
> [!NOTE]
>  Ao usar o provedor OLE DB para Microsoft Jet, o **procedimentos** coleção **Append** método permitirá que você especifique um **exibição** em vez de  **Procedimento** no *comando* parâmetro. O **exibição** será adicionado à fonte de dados e será adicionado para o **procedimentos** coleção. Após o **Append**, se o **procedimentos** e **exibições** coleções são atualizadas, o **exibição** não será o **Procedimentos** coleta e aparecerão no **exibições** coleção.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Coleção Procedures (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos de acrescentar o exemplo de método (VB)](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [Acrescente o método (ADOX colunas)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [(Grupos de ADOX) do método append](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Método (ADOX índices) append](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [(ADOX chaves) do método append](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [(Tabelas ADOX) do método append](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Acrescente o método (ADOX usuários)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Método Append (Exibições do ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
