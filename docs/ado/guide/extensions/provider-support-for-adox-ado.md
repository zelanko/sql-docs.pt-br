---
title: Suporte do provedor para ADOX (ADO) | Microsoft Docs
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
helpviewer_keywords:
- ADOX provider support [ADO]
ms.assetid: 64234ce5-dc46-4c8a-a316-61956b6b9abb
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a4a2a8c4f277e7e7fd4abc527e3d01a556a5295f
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
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
