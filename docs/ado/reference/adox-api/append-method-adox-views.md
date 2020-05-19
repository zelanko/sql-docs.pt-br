---
title: Método Append (exibições do ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Views::raw_Append
- Views::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 6070fd58-3237-4c77-a966-5b39ce5d57e4
author: rothja
ms.author: jroth
ms.openlocfilehash: 540ff52141139f4748cb2cd4c8979f5f8b55b230
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763997"
---
# <a name="append-method-adox-views"></a>Método Append (Exibições do ADOX)
Cria um novo objeto de [exibição](../../../ado/reference/adox-api/view-object-adox.md) e o anexa à coleção [views](../../../ado/reference/adox-api/views-collection-adox.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Views.Append Name, Command  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Nome*  
 Um valor de **cadeia de caracteres** que especifica o nome da exibição a ser criada.  
  
 *Comando*  
 Um objeto de [comando](../../../ado/reference/ado-api/command-object-ado.md) ADO que representa a exibição a ser criada.  
  
## <a name="remarks"></a>Comentários  
 Cria uma nova exibição na fonte de dados com o nome e os atributos especificados no objeto **Command** .  
  
 Se o texto do comando que o usuário especifica representa um procedimento em vez de uma exibição, o comportamento depende do provedor. **Append** falhará se o provedor não der suporte a comandos persistentes.  
  
> [!NOTE]
>  Ao usar o provedor de OLE DB para o Microsoft Jet, o método de **acréscimo** da coleção **views** permitirá que você especifique um **procedimento** em vez de uma **exibição** no parâmetro *Command* . O **procedimento** será adicionado à fonte de dados e será adicionado à coleção **views** . Após o **acréscimo**, se as coleções de **procedimentos** e **exibições** forem atualizadas, o **procedimento** não estará mais na coleção **views** e aparecerá na coleção **procedures** .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Coleção Views (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método Append views (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Método Append (colunas ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Método Append (grupos ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Método Append (índices ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Método Append (chaves ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Método Append (procedimentos do ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Método Append (tabelas ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Método Append (Usuários do ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)
