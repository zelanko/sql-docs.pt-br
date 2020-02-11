---
title: Método Append (procedimentos ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Procedures::Append
- Procedures::raw_Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 38e3492c-c1e1-42e3-a71a-befdc90204db
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dd64ba8119db1ecf2d2b621cd202c9f700b53475
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67967286"
---
# <a name="append-method-adox-procedures"></a>Método Append (Procedimentos do ADOX)
Adiciona um novo objeto de [procedimento](../../../ado/reference/adox-api/procedure-object-adox.md) à coleção de [procedimentos](../../../ado/reference/adox-api/procedures-collection-adox.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Procedures.Append Name, Command  
```  
  
#### <a name="parameters"></a>parâmetros  
 *Nome*  
 Um valor de **cadeia de caracteres** que especifica o nome do procedimento a ser criado e acrescentado.  
  
 *Comando*  
 Um objeto de [comando](../../../ado/reference/ado-api/command-object-ado.md) ADO que representa o procedimento para criar e acrescentar.  
  
## <a name="remarks"></a>Comentários  
 Cria um novo procedimento na fonte de dados com o nome e os atributos especificados no objeto **Command** .  
  
 Se o texto do comando que o usuário especifica representa uma exibição em vez de um procedimento, o comportamento depende do provedor que está sendo usado. **Append** falhará se o provedor não der suporte a comandos persistentes.  
  
> [!NOTE]
>  Ao usar o provedor de OLE DB para o Microsoft Jet, o método de **acréscimo** da coleção **procedures** permitirá que você especifique uma **exibição** em vez de um **procedimento** no parâmetro *Command* . O **modo de exibição** será adicionado à fonte de dados e será adicionado à coleção de **procedimentos** . Após o **acréscimo**, se as coleções de **procedimentos** e **exibições** forem atualizadas, a **exibição** não estará mais na coleção de **procedimentos** e aparecerá na coleção **views** .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Coleção Procedures (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método Append Procedures (VB)](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [Método Append (colunas ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Método Append (grupos ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Método Append (índices ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Método Append (chaves ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Método Append (tabelas ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Método Append (usuários do ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Método Append (Exibições do ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
