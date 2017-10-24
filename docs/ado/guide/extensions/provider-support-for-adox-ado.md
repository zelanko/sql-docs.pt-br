---
title: Suporte do provedor para ADOX (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ADOX provider support [ADO]
ms.assetid: 64234ce5-dc46-4c8a-a316-61956b6b9abb
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b15df02c70e2dcdc2efb2ba468b76219a233d65a
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="provider-support-for-adox-ado"></a>Suporte do provedor para ADOX (ADO)
Determinados recursos do ADOX não têm suportados, dependendo do seu provedor de dados OLE DB. ADOX é totalmente compatível com o [OLE DB Provider for Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md). Recursos sem suporte com o [Microsoft OLE DB Provider para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), o [Microsoft OLE DB Provider para ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md), ou o [Microsoft OLE DB Provider for Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md) são listados nas tabelas a seguir. Não há suporte para ADOX por outros provedores de OLE DB do Microsoft.  
  
## <a name="microsoft-ole-db-provider-for-sql-server"></a>Provedor Microsoft OLE DB para SQL Server  
  
|Objeto ou coleção|Restrição de uso|  
|--------------------------|-----------------------|  
|**Tabelas** coleção|Propriedades são somente leitura antes da criação do objeto e somente leitura ao fazer referência a um objeto existente.|  
|**Modos de exibição** coleção|**Modos de exibição** não tem suporte.|  
|**Procedimentos** coleção|O **Append** e **excluir** métodos não são suportados.|  
|**Procedimento** objeto|O **comando** não há suporte para a propriedade.|  
|**Chaves** coleção|O **Append** e **excluir** métodos não são suportados.|  
|**Os usuários** coleção|**Os usuários** não tem suporte.|  
|**Grupos de** coleção|**Grupos de** não tem suporte.|  
  
## <a name="microsoft-ole-db-provider-for-odbc"></a>Microsoft OLE DB Provider para ODBC  
  
|Objeto ou coleção|Restrição de uso|  
|--------------------------|-----------------------|  
|**Catálogo** objeto|O **criar** método não é suportado.|  
|**Tabelas** coleção|O **Append** e **excluir** métodos não são suportados. Propriedades são somente leitura antes da criação do objeto e somente leitura ao fazer referência a um objeto existente.|  
|**Procedimentos** coleção|O **Append** e **excluir** métodos não são suportados.|  
|**Procedimento** objeto|O **comando** não há suporte para a propriedade.|  
|**Índices** coleção|O **Append** e **excluir** métodos não são suportados.|  
|**Chaves** coleção|O **Append** e **excluir** métodos não são suportados.|  
|**Os usuários** coleção|**Os usuários** não tem suporte.|  
|**Grupos de** coleção|**Grupos de** não tem suporte.|  
  
## <a name="microsoft-ole-db-provider-for-oracle"></a>Microsoft OLE DB Provider for Oracle  
  
|Objeto ou coleção|Restrição de uso|  
|--------------------------|-----------------------|  
|**Catálogo** objeto|O **criar** método não é suportado.|  
|**Tabelas** coleção|O **Append** e **excluir** métodos não são suportados. Propriedades são somente leitura antes da criação do objeto e somente leitura ao fazer referência a um objeto existente.|  
|**Modos de exibição** coleção|O **Append** e **excluir** métodos não são suportados.|  
|**Exibição** objeto|O **comando** não há suporte para a propriedade.|  
|**Procedimentos** objeto|O **Append** e **excluir** métodos não são suportados.|  
|**Procedimento** objeto|O **comando** não há suporte para a propriedade.|  
|**Índices** coleção|O **Append** e **excluir** métodos não são suportados.|  
|**Chaves** coleção|O **Append** e **excluir** métodos não são suportados.|  
|**Os usuários** coleção|**Os usuários** não tem suporte.|  
|**Grupos de** coleção|**Grupos de** não tem suporte.|

